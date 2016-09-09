====================
Swift Manual Upgrade - On a multi-node Swift cluster (1 Proxy , 3 ACO)
====================

__Upgrade a single storage (ACO) node__
  1.	Stop all background Swift jobs with
        - $ swift-init rest stop
  2.	Shutdown all Swift storage processes with
        - $ swift-init {account|container|object} shutdown --graceful
  3.	Upgrade all system packages and Swift code
    - Update source code
      * $ git tag –l # lists all the tags for the given repo
  	  * $ git checkout <tag_to_update_to>
    - Upgrade the packages
    	* $ sudo pip install –r requirements.txt --upgrade
    	* $ sudo pip install –r test-requirements.txt –upgrade
    	* $ sudo python setup.py develop
  4.	Update Swift configs (in test setup with SAIOs)
      * $ sudo cp $HOME/swift/doc/saio/rsyncd.conf /etc/
      * $ sudo sed –i “s/<your-user-name>/${USER}/” /etc/rsyncd.conf
      * $ sudo cp $HOME/swift/doc/saio/rsyslog.d/10-swift.conf /etc/rsyslog.d/
      * $ sudo cp –r $HOME/swift/doc/saio/swift /etc/swift
      * $ sudo chown –R ${USER}:${USER} /etc/swift
      * $ sudo cp $HOME/swift/test/sample.conf /etc/swift/test.conf
      * $ sudo cp $HOME/swift/doc/saio/bin/* $HOME/bin
      * $ sudo chmod +x $HOME/bin/*
  5.	If needed, reboot server
  6.	Start the storage service with – swift-init {account|container|object} start
  7.	Start background Swift jobs with – swift-init rest start

__Upgrading all of the other storage nodes__
  -	Repeat the above steps for each node

__Upgrading Proxy node__
  - WIP (will update when tested with multiple proxies)

Terms
=====
__ACO__ - Account Container Object

__SAIO__ - Swift All In One

__WIP__ - Work in progress

Reference - https://www.swiftstack.com/blog/2013/12/20/upgrade-openstack-swift-no-downtime/
