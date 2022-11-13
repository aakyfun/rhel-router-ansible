# rhel-router-ansible
Simple playbook to provision an IPv4 NAT router with DNS and DHCP on RHEL. Intended for virtual machine labs.  
This is one of my first Ansible playbooks so be warned :)

## Requirements
Requires ansible-core and rhel-system-roles

**Expects *three* network interfaces (including loopback):**  
One that is already being used to access the internet gateway and another one that is connected to a bridge/switch with an unassigned IPv4 address. The goal is to provide routing, dhcp, and dns service to hosts connected to the bridge.

## Installation
If you don't care about applying this play to remote hosts then you can use the provided inventory file to run the play against your local system or virtual machine.

    ansible-playbook -i inventory.ini rhel-router.yml
    
## Precautions
**This play messes around with your NetworkManager connections. In fact, it straight up deletes all of them and starts from scratch!**

Please keep this in mind if you need to keep your connections or don't want to lose access to a remote system in the event of a failiure.

This is also the reason why this play is designed to run locally - so you can fix your network if the play somehow breaks it.  
As a saving grace, the play is always going to try to create a automatic connection called 'External'. So under common circumstances, things should be fine.
