*********************
Cinder Rolling Upgrade
*********************

Rolling Upgrade Steps
---------------------

1. Install all cinder services working on stable/mitaka
    * Cinder services: cinder-api, cinder-scheduler, cinder-volume, cinder-backup
2. Change the codebase of the repo used to master (Newton)
3. Upgrading DataBase
    * run cinder-manage db sync
4. Upgrading cinder services
    * Kill and Restart all services
        * cinder-api
        * cinder-scheduler
        * cinder-volume
        * cinder-backup
5. Done upgrading :-)
    - To check cinder services are running
        * pgrep -a cinder-scheduler
        * pgrep -a cinder-api
        * pgrep -a cinder-volume
        * pgrep -a cinder-backup
        
        
##IGNORE THE BELOW TEST :) 
---------------------------

During Upgrade Testing 
---------------------
What are some test that can be executed during rolling upgrade that cross multiple cinder services?

During upgrading of cinder-scheduler 
   * tempest.api.volume.admin.test_volume_quotas.VolumeQuotasAdminV1TestJSON.test_quota_usage
   * tempest.api.volume.test_volume_transfers.VolumesV2TransfersTest.test_create_get_list_accept_volume_transfer
   * tempest.api.volume.admin.test_volume_quotas.VolumeQuotasAdminV1TestJSON.test_quota_usage_after_volume_transfer
   * tempest.api.volume.admin.test_volume_types.VolumeTypesV1Test.test_volume_crud_with_volume_type_and_extra_specs
   * tempest.api.volume.test_volumes_get.VolumesV1GetTest.test_volume_create_get_update_delete
   
During upgrading of cinder-volume 
   * tempest.api.volume.admin.test_backends_capabilities.BackendsCapabilitiesAdminV2TestsJSON.test_get_capabilities_backend
   * tempest.api.volume.admin.test_volume_quotas.VolumeQuotasAdminV1TestJSON.test_quota_usage
   * tempest.api.volume.admin.test_volume_quotas.VolumeQuotasAdminV1TestJSON.test_quota_usage_after_volume_transfer
   * tempest.api.volume.admin.test_volume_quotas.BaseVolumeQuotasAdminV2TestJSON.test_quota_usage
   * tempest.api.volume.admin.test_volume_type_access.VolumeTypesAccessV2Test.test_volume_type_access_add
   * tempest.api.volume.admin.test_volume_types.VolumeTypesV1Test.test_volume_crud_with_volume_type_and_extra_specs
   * tempest.api.volume.admin.test_volume_types.VolumeTypesV2Test.test_volume_crud_with_volume_type_and_extra_specs
   * tempest.api.volume.test_volumes_clone_negative.VolumesCloneTest.test_create_from_volume_decreasing_size
   * tempest.api.volume.test_volumes_clone_negative.VolumesV1CloneTest.test_create_from_volume_decreasing_size
   * tempest.api.volume.test_volumes_extend.VolumesV1ExtendTest.test_volume_extend 
   * tempest.api.volume.test_volumes_extend.VolumesV2ExtendTest.test_volume_extend
   * tempest.api.volume.test_volumes_get.VolumesV1GetTest.test_volume_create_get_update_delete 
   * tempest.api.volume.test_volumes_get.VolumesV1GetTest.test_volume_create_get_update_delete_as_clone
   * tempest.api.volume.test_volume_transfers.VolumesV1TransfersTest.test_create_get_list_accept_volume_transfer 
   * tempest.api.volume.test_volume_transfers.VolumesV1TransfersTest.test_create_list_delete_volume_transfer
   * tempest.api.volume.test_volumes_get.VolumesV1GetTest.test_volume_create_get_update_delete_from_image 
   * tempest.api.volume.test_volume_transfers.VolumesV2TransfersTest.test_create_get_list_accept_volume_transfer
   * tempest.api.volume.test_volumes_get.VolumesV2GetTest.test_volume_create_get_update_delete
   * tempest.api.volume.test_volume_transfers.VolumesV2TransfersTest.test_create_list_delete_volume_transfer
   * tempest.api.volume.test_volumes_get.VolumesV2GetTest.test_volume_create_get_update_delete_as_clone
   * tempest.api.volume.test_volumes_get.VolumesV2GetTest.test_volume_create_get_update_delete_from_image
   * tempest.api.volume.test_volumes_clone.VolumesCloneTest.test_create_from_volume
   * tempest.api.volume.test_volumes_snapshots_negative.VolumesV1SnapshotNegativeTestJSON.test_volume_from_snapshot_decreasing_size
   * tempest.api.volume.test_volumes_snapshots_negative.VolumesV2SnapshotNegativeTestJSON.test_volume_from_snapshot_decreasing_size
