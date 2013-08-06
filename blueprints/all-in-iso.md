enable all-in-one deployment from an ISO without newtork access

Overview
--------

Deploying openstack can be made much easier by things like this [1], but also by having all the code
needed in one handy spot. The ISO produced by this should be self contained so that one may deploy an entire
OpenStack system with just that image.

Motivation
----------

There are a few key motivations:

* Develop while offline
* Deploy for customers who have limited network access for deployment services
* Enable more reliable deployments

Process
-------
1. Capture all of the minimum required modules for an OS deployment including any additional tools needed 
 e.g. puppet, python libraries, packaged puppet, pip packages, etc.
2. create a local mirror (example, extend the CD based install mirror with the added packages needed)
3. create a "live" ISO, and enable it to run as either hypervisor+OS installer, or as a live OS demo


[1]: https://github.com/CiscoSystems/openstack-cosi-blueprints/blob/master/blueprints/ci_system.md
