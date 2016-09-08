****************************************
Additional Resources - Keystone Upgrade
****************************************

* `Newton Upgrade Procedure
  <http://docs.openstack.org/developer/keystone/upgrading.html#upgrading-without-downtime>`_

* `Step by step example
  <https://gist.github.com/lbragstad/ddfb10f9f9048414d1f781ba006e95d1#file-migration-md>`_,
  focusing on one of keystone's more complicated edge cases (credentials).

* Difference with other teams: Keystone uses trigger-based migrations to allow
  both old and new code to read and write to the database during the entire
  upgrade process. Once the upgrade is completed, the triggers are removed.

  Because neither release of keystone involved in an upgrade is aware of the
  other release's schema, all triggers must be created in the database and the
  data migration process must be complete prior to running any code from the
  next release. This differs from other services where code from the new
  release can be brought online immediately, and is responsible for
  understanding two different database schemas.

* Related patches:

    * https://review.openstack.org/#/c/349939
    * https://review.openstack.org/#/c/358723


Test Suggestions
################

* Aug 23
* Run Rally **load (light)** over the entire upgrade process to validate zero downtime.
* Focus area: token creation/validation over the entire process
  (``tempest.api.identity.v3.test_tokens``)

