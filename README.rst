**********************
osic-upgrade-test
**********************

Repository for artifacts related to test the rolling upgrade of OpenStack.

This repo collects information about the test cases that should run before, during, and after Rolling Upgrade process.

About OSIC QA 3rd Party CI for Rolling Upgrades
################################################

1. CI will run on a daily basis via Jenkins pipelines.
2. CI will deploy OpenStack at N release (Mitaka) on a 22 physical node environment.
3. CI will upgrade environment to N+1 release (Newton). 
4. CI will collect, normalize and present results (success/fail/time rates).
5. CI will run tempest smoke test before upgrading.
6. CI will run upgrade specific test cases during the upgrade <NEED YOUR INFO HERE>
7. CI will run specific test cases after the upgrade  <NEED YOUR INFO HERE>

WE NEED FROM YOU:
#################

1. What tests would your team want executed during an upgrade?
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

   **TO-BE AUTOMATED**

     * Scenario Description: *E.g. Verify nova api endpoints are up and running*
     * Pre-requisites: *E.g. Get nova-api endpoints*
     * Procedure and verification points: *E.g. Run A, Run B, Verify X*
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
