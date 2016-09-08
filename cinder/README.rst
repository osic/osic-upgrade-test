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
