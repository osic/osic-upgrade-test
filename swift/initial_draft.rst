***********************************************************************
Swift Rolling Upgrade Swift 2.7.0 – Mitaka to current master (2.9.0 +)
***********************************************************************

TEST DURING UPGRADE
###################

- TEMPEST TEST SUITE - tempest.api.object_storage 
   - https://github.com/openstack/tempest/tree/master/tempest/api/object_storage ]
- SWIFT TEST SUIT - swift.test.functional
   - https://github.com/openstack/swift/tree/master/test/functional

TEST AFTER UPGRADE
###################

- TEMPEST TEST SUITE - tempest.api.object_storage 
   - https://github.com/openstack/tempest/tree/master/tempest/api/object_storage ]
- SWIFT TEST SUIT
   - swift.test.functional at https://github.com/openstack/swift/tree/master/test/functional
   - swift.test.probe at https://github.com/openstack/swift/tree/master/test/probe

OTHER TBD
##########

Dataplane
*********

* Erasure Coding (EC storage policy) object download and test
* Replication (Storage policy) object download and test
* Versioned writes (enable middleware) object download and test
* Tempurl (enable middleware) object download and test
* Container , Account create and delete

Generic Object download ,upload: [ http://docs.openstack.org/cli-reference/swift.html ]

$ swift upload <container_name>  <file_or_directory>

container_name -> name of the container to upload the object to

file_or_directory -> object to upload

$ swift download <container_name> <object_name>

How to set the storage policy: Define storage policies in /etc/swift/swift.conf file


