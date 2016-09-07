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

* Persistent resources – verify on recently created resouces (action for a VM):
   * tempest.api.compute.servers.test_server_actions.ServerActionsTestJSON.test_pause_unpause_server
   * tempest.api.compute.servers.test_server_actions.ServerActionsTestJSON.test_suspend_resume_server
   * tempest.api.compute.servers.test_server_actions.ServerActionsTestJSON.test_shelve_unshelve_server
   * tempest.api.compute.servers.test_server_rescue.ServerRescueTestJSON.test_rescue_unrescue_instance
   * tempest.api.compute.servers.test_server_rescue.ServerRescueTestJSON.test_rescued_vm_add_remove_security_group
   * tempest.api.compute.servers.test_server_rescue.ServerRescueTestJSON.test_rescued_vm_associate_dissociate_floating_ip
   * tempest.api.compute.servers.test_server_rescue_negative.ServerRescueNegativeTestJSON.test_rescue_non_existent_server
   * tempest.api.compute.servers.test_server_rescue_negative.ServerRescueNegativeTestJSON.test_rescue_paused_instance
   * tempest.api.compute.servers.test_server_rescue_negative.ServerRescueNegativeTestJSON.test_rescued_vm_attach_volume
   * tempest.api.compute.servers.test_server_rescue_negative.ServerRescueNegativeTestJSON.test_rescued_vm_detach_volume
   * tempest.api.compute.servers.test_server_rescue_negative.ServerRescueNegativeTestJSON.test_rescued_vm_reboot
   * tempest.api.compute.servers.test_server_rescue_negative.ServerRescueNegativeTestJSON.test_rescued_vm_rebuild   
   * tempest.scenario.test_server_multinode.TestServerMultinode.test_schedule_to_all_nodes -- **TBD part of smoke test**
   * tempest.scenario.test_server_basic_ops.TestServerBasicOps.test_server_basic_ops -- **TBD part of smoke test**

* ssh into the VM (tempest hint - set CONF.validation.run_validation to true)
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_create_server_with_scheduler_hint_group
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_host_name_is_same_as_server_name
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_list_servers
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_list_servers_with_detail
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_verify_created_server_vcpus
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_verify_duplicate_network_nics
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_verify_multiple_nics_order
   * tempest.api.compute.servers.test_create_server.ServersTestJSON.test_verify_server_details
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_create_server_with_scheduler_hint_group
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_host_name_is_same_as_server_name
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_list_servers
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_list_servers_with_detail
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_verify_created_server_vcpus
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_verify_duplicate_network_nics
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_verify_multiple_nics_order
   * tempest.api.compute.servers.test_create_server.ServersTestManualDisk.test_verify_server_details
   * tempest.api.compute.servers.test_create_server.ServersWithSpecificFlavorTestJSON.test_verify_created_server_ephemeral_disk

During Upgrade Testing
----------------------

What tests would your team want executed during a rolling upgrade?

* <QA_team_added> nova.servers.list (via python client call)
* TBD – tempest.scenario.test_server_basic_ops.TestServerBasicOps.test_server_basic_ops
* TBD - tempest.scenario.test_server_multinode.TestServerMultinode.test_schedule_to_all_nodes

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

