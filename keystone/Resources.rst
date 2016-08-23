****************************************
Additional Resources - Keystone Upgrade
****************************************

* Newton Upgrade Procedure: http://docs.openstack.org/developer/keystone/upgrading.html
* Difference with other teams: Keystone uses db-based migration with triggers to allow both old and new code to talk to the db during the process. Once upgrade is completed the triggers are removed.

* Related patches:

    * https://review.openstack.org/#/c/349939/
    * https://review.openstack.org/358723


Test Suggestions
################

* Aug 23
* Run Rally **load (light)** over the entire upgrade process to validate zero downtime.
* Focus area: token creation/validation over the entire process

