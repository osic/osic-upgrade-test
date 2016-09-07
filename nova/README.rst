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

1. Deployment - Install all nova services at stable/mitaka
  * Controller Nodes:  nova-api nova-scheduler nova-conductor nova-consoleauth nova-novncproxy nova-cert TBD. enable only the compute and metadata APIs enabled_apis
  * Compute Nodes: nova-compute
2. Change the codebase of the repos to current Master Newton
3. DB Expansion
   * Install nova requirements (from requirements.txt) **To Be Confirmed**
   * Run nova-manage db sync
   * Run nova-manage api_db sync
4. Iterate through the controller nodes.
   **TBD Is it iterate through the controllers and restart all services? OR turn off just conductor service on all controllers, then restart conductors then restart the other controller services?**
   * Install nova requirements (from requirements.txt)
   * Run nova-manage db sync
   * Restart all services: nova-conductor, nova-scheduler, nova-api
5. Iterate through the compute nodes:
   * **TBD are requirements and nova-manage required here?
   * Gracefully stop nova-compute service
   .. code:: bash
      $ kill -15 nova-compute
   * Start nova-compute service
6. Other actions? what are they?

