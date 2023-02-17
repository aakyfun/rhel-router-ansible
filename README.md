<b>Heads up: I am not working on this anymore. There will be an improved spiritual successor in the aakyfun/lab project. Thanks.</b>

# rhel-router-ansible
Simple playbook to provision an IPv4 NAT router with DNS and DHCP on RHEL. Intended for virtual machine labs.  
This is one of my first Ansible playbooks so be warned :)

## Requirements
Requires ansible-core and rhel-system-roles

**Expects *three* network interfaces (including loopback):**  
One that is already being configured to access the internet gateway via DHCP, another one that is connected to a bridge/switch with an unassigned IPv4 address, and the loopback 'lo' interface always being there. The goal is to provide routing, DHCP, and DNS service to hosts connected to the bridge.

## Installation
If you don't care about applying this play to remote hosts then you can use the provided inventory file to run the play against your local system or virtual machine.

    ansible-playbook -i inventory.ini rhel-router.yml
    
## Precautions
**This play messes around with your NetworkManager connections. In fact, it straight up deletes all of them and starts from scratch!**

This was done to ensure a consistent setup with no duplicates. Please keep this in mind if you need to keep your connections or don't want to lose access to a remote system in the event of a failiure.

This is also the reason why this play is designed to run locally - so you can fix your network if the play somehow breaks it!  
As a saving grace, the play is always going to try to create a automatic connection called 'External' to connect to the internet. So under common circumstances, things should be fine.
