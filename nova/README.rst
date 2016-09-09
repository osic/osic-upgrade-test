*********************
Nova Rolling Upgrade
*********************

Before and After Upgrade Testing
--------------------------------

* Verify Nova services are up and running


.. code-block:: bash

   $ openstack compute service list
   Verify services are up 
      nova-conductor
      nova-scheduler
      nova-consoleauth
      nova-compute

* Persistent resources test suite – verify on a created VM:
   * tempest.api.compute.servers.test_server_actions.ServerActionsTestJSON.test_pause_unpause_server
   * tempest.api.compute.servers.test_server_actions.ServerActionsTestJSON.test_suspend_resume_server
   * tempest.api.compute.servers.test_server_actions.ServerActionsTestJSON.test_shelve_unshelve_server
   * tempest.api.compute.servers.test_server_rescue.ServerRescueTestJSON.test_rescue_unrescue_instance
   * tempest.api.compute.servers.test_server_rescue.ServerRescueTestJSON.test_rescued_vm_add_remove_security_group
   * tempest.scenario.test_server_multinode.TestServerMultinode.test_schedule_to_all_nodes -- **TBD part of smoke test**
   * tempest.scenario.test_server_basic_ops.TestServerBasicOps.test_server_basic_ops -- **TBD part of smoke test**

* ssh into the VM (tempest hint - set CONF.validation.run_validation to true)
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_host_name_is_same_as_server_name
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_verify_created_server_vcpus
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_verify_server_details

During Upgrade Testing
----------------------

What tests would your team want executed during a rolling upgrade?

* <QA_team_added> nova.servers.list (via python client call)
* TBD – basic server operations

Rolling Upgrade Steps
---------------------

TODO: check with OSA on the current and future plans.

1. Deploy previous stable release (i.e. to test Newton, first deploy Mitaka)

  a) Verify the system is working (i.e. tempest smoke test)
  b) Ensure there is sufficient nova-conductor capacity for the extra upgrade
     related load
  c) Read the release notes for the new release, to see if there are any
     release specific tasks that are required for your chosen configuration.

2. Do pre-maintenance window steps, expect zero API downtime

  a) Update venv (i.e. new code and dependencies)
  b) Run DB expansion (nova-manage db sync; nova-manage api_db sync)
     Its possible this may affect performance, but it should not cause
     any operations to fail.

3. Do maintenance window steps, expect API downtime

  a) Stop all services (running the old code), except nova-compute.
     For maximum safety (no failed API operations), drain connections
     to API nodes, then SIG_TERM (i.e. gracefully stop) all the services.
  b) Start all services, with ``[upgrade_pin]compute=auto.``
     It is safest to start nova-conductor first and nova-api last.

4. Do more maintenance window steps, expect some delayed API actions

  a) In small batches gracefully shutdown nova-compute (i.e. SIG_TERM),
     then start the new version of the code with:
     ``[upgrade_pin]compute=auto``
     Note this is done in batches so only a few compute nodes will have
     any delayed API actions, and to ensure there is enough capacity online
     to service any boot requests that happen during this time.
  b) Note there is no upgrade of the hypervisor here, this is just upgrading
     the nova services. Some users choose to live-migrate all instances from
     old nodes to new nodes to do both of these things at the same time.
  c) Once all services are running the new code, double check in the DB
     that there are no old orphaned service records (TODO - provide script)
  d) Now SIG_HUP all services, to reset the min_service_version cache,
     to make new features available.
     (TODO - rollback could be possible before you do this step)

5. Prepare for the next upgrade

  a) Complete all online data migrations by doing:
     ``nova-manage db online_data_migrations --limit <number>``
     Note you can use the limit argument to reduce the load this operation
     will place on the database.
  b) Look for deprecated features and configuration options, and update
     the configuration files to remove them all. All options should be
     supported for one cycle, but should be removed before your next
     upgrade is performed.
