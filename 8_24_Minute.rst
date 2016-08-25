************************
Meeting Minute 8_24_2016
************************
Meeting w/ Teams
Wednesday, August 24, 2016
11:09 AM

Joint meeting with Cinder, Swift, Nova and QA teams to talk about Rolling Upgrades.

Agenda:
* QA    - About the rolling upgrade epic
* Teams - Current status of your project
* QA    - CI flow: In scope and Out of scope items
* QA    - What QA needs from you

https://github.com/osic/osic-upgrade-test

Summary:
########

* Cinder – Rolling upgrades working.  Will have list of test to date by end of the week POC: Szymon
* Swift – Rolling upgrades working. see attachment POC: Shashi
* Nova – OSIC team is just digging into this.  Will provide update by the end of the week POC: Maciej & Pushkar
* Keystone – Rolling upgrades done but not stable.  This is not expected in Newton POC: Ron
 
AI - QA - To explore
#####################

* Define stages of upgrade (such as before, stable environment, services down, etc.)
* Need to measure downtime for manual upgrades (but, may also depend on db size)
* When building playbook we need to add hooks in Ansible's playbook for db migration, then record time
 
What we need:

*       re-test to verify functionality
*       Automated test that you run and their location
*       New automations along with credentials and scenario
*       additional test after upgrade to verify upgrade
 
Meeting Notes
#############

Cinder Progress
***************

POC: Szymon

*       Enablement of rolling upgrades
*       They have ovo
*       Multinode test for gates but it is non-voting (what does this test do)
*       Szymon is working on test plan and should be done this week
*       Didn't go Grenade because it is VM and we are on baremetal
 
Swift Progress
***************

POC: Shashi

*       In progress
*       See current plan at swift folder
 
Keystone Progress
*****************

POC: Ron De'Rose

*       Done but not stable
*       Will not be ready for Newton
*       http://docs.openstack.org/developer/keystone/upgrading.html#upgrading-without-downtime
 
Nova Progress
*************

POC: Maciej & Pushkar

*       OSIC team has not started looking into rolling upgrades just yet
*       Maciej and Pushkar agreed to take head
*       Will update by the end of this week
 
Areas of concern for Nova (via John Garbutt):

*   a test to persist throughout the upgrade
*   like something running before and verify it is running throughout to the end
*   John Garbutt prefers steps while running test.  Running specific test at specific points in the upgrade
*   Let them know when the outage pieces may come
*   Does it work A-B, meaning does it start at begin carrying out first steps
*   How long does it take, how long are you out for (These are how all of the projects are doing, here is the down time)
*   How well do each of the bits of the upgrade work (how much performance degradation do you get on the bnd)
*   if you make use of all the products how much is the down time
*   for now just add a hook that occurs right before we do database migrations, or rather right before you turn all of the services off to do database migrations.  A hook before and after.

Summarized:

*   define stages of upgrade, mainly DURING stage
*   down time for manual upgrade
*   down time for rolling upgrade
*   hooks added to distinguish db migration beginning and end
*   measure db migration time

