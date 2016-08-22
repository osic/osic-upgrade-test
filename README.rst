**********************
osic-upgrade-test
**********************

Repository for artifacts related to test the rolling upgrade of OpenStack.

This repo collects information about the test cases that should run before, during, and after Rolling Upgrade process.

About OSIC QA 3rd Party CI for Rolling Upgrades
################################################

* CI will run on a daily basis via Jenkins pipelines.
* CI will deploy OpenStack at N release (Mitaka) on a 22 physical node environment.
* CI will upgrade environment to N+1 release (Newton: master branch). 
* CI will collect, normalize and present results (success/fail/time rates).
* CI will run tempest smoke test before upgrading.
* CI will run upgrade specific test cases during the upgrade <NEED YOUR INFO HERE>
* CI will run specific test cases after the upgrade  <NEED YOUR INFO HERE>

WE NEED FROM YOU:
#################

1. What tests would your team want executed during an upgrade?
***********************************************************

   **ALREADY AUTOMATED**
   
   What gets executed is not necessarily a Tempest test but we need to know what it is...

     * TEMPEST

       *E.g.*
        *tempest.api.compute.servers.test_servers.*

        *tempest.api.compute.servers.test_servers.*

     * OTHER

       *[tempest_plugin| private_repo| rally|etc]*
       
       *How is test suite executed?*

       *<URL1>*
       *<URL2>*
       *...*

   **NOT SURE IF AUTOMATED**
   
   **OR**

   **TO-BE AUTOMATED**

     * Scenario Description: *E.g. Verify attached volume remains attached during and after the upgrade.*
     * Pre-requisites: *E.g. Create a server, Create a volume, Attach volume to the server.*
     * Procedure and verification points: *E.g. Save file to the volume, measure downtime during upgrade process.*
     * Additional Resources/ Notes: *E.g. Any additional information you consider relevant*


2. What tests would your team wanted executed after an upgrade?
***********************************************************

   **ALREADY AUTOMATED**

     * TEMPEST

       *E.g.*
        *tempest.api.compute.servers.test_servers.*

        *tempest.api.compute.servers.test_servers.*

     * OTHER
   
       *[tempest_plugin| private_repo| rally|etc]*

       *How it is executed*

       *<URL1>*
       *<URL2>*
       *...*
