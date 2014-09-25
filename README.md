eucalyptus4-deploy
==================

This playbook uses ansible (tested with 1.6.0 and 1.7 from epel repo) to deploy eucalyptus in almost all possible topologies, using latest packages.

VARIABLES
---------

This playbooks gives differents variables files under the vars/ directory. You will find an example for each mode and topology this playbook has been tested with.


What the user MUST do:
----------------------

- Create a new / edit the "hosts" file in the playbook to fit his environment

- Create a new / edit the "networking.yml" file to fit his network environment (see details in topologies)

What the playbook always do:
----------------------------

- Uses the latest packages to setup your private IaaS cloud

- Allows users to use their private cloud repository | ON YOUR OWN RISKS

- Support distributed deployment

- Creates a ssh key on your Cloud Controller (CLC) authorized on your Front-End components (Walrus,UFS,SC,CC)

- Create s ssh key on your Cluster Controller (CC) authorized on your Node Controllers (NC) - restricted to the partition

- Disable ZEROCONF setting "NOZEROCONF" to "yes" on all interfaces of each hosts

What the playbook doesnt do:
----------------------------

- coffee

Toplogy 1: EDGE without VLANs
------------------------------

Eucalyptus documentation : `<https://www.eucalyptus.com/docs/eucalyptus/4.0/#install-guide/planning_edge.html>`

The playbook will automatically :

- create the bridge interface on your NC

- Allows multi-cluster with different VLAN tags and different subnet

Topology 2: EDGE with VLANs
---------------------------

Eucalyptus documentation : `<https://www.eucalyptus.com/docs/eucalyptus/4.0/#install-guide/planning_edge.html>`

Using a VLAN for your instances backend is an Improvement, not a requirement. This allows you to separate your instances traffic from your servers' traffic.
This also add a security layer.

The playbook will :

- Create the VLAN interface using your VLAN tags defined in the "hosts" file

- Create the BRIDGE interface on-top of the VLAN interface created before for your NC

Topology 3 : MANAGED 
--------------------

`Eucalyptus documentation <https://www.eucalyptus.com/docs/eucalyptus/4.0/#install-guide/planning_managed.html>`

The playbook will automatically :

- Setup Eucalyptus and configure hosts with the defined settings

WARNING
^^^^^^^

To use MANAGED mode, you need to KNOW your networking VLAN allowance

