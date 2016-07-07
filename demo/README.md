Openstack demo playbook
-----------------------

The following playbook is a demo of openstack management scenario.

The playbook perform the following steps:
# First part - OpenStack configuration:
* Creates a network and a subnet.
* Link the subnet as an interface to the router.
* Creates a security group.
* Assign the following rules to the group - SSH, web(80), ICMP.
* Creates an ssh keypair based on the variable provided by the user.
* Boots an instance. Assign security group to the instance and sets floating ip.
* Build a dynamic inventory based on the instance ip address.

# Second part - Newly created instance configuration:
* Install web server on the instance.
* Create demo page for the web server.


Important notes:

# Demo playbook prerequisites:
* OpenStack environment exists.
* Public network exists and has a name - public.
* Public network has a floating ip that can be allocated to the instance.

# Variables:
Please, review the variables of the demo playbook (roles/openstack_set_demo/vars/main.yml) and edit them to meet your needs.

# Pip requirements:
In order to be able to run the playbook, ansible and shade module should be installed.
pip_ansible_openstack_packages.txt file located at the root directory of the repo and has all the necessary packages. Install it with pip.

# Openstack authentication:
In order to run the ansible against the openstack, we should provide authentication parameters.
We have three ways to authenticate against the openstack:
1. Source the keystonerc_admin file
2. Copy the clouds.yml.sample file as clouds.yml to one of the following directories - ~/.config/openstack/clouds.yml or /etc/openstack/clouds.yml.
3. Provide the authentication parameters within each task.
Current demo playbook, set to use the clouds.yml file located at the ~/.config/openstack/clouds.yml directory.
If you would like to use the keystonerc_admin file instead, you should comment the clouds line within each task.

# Files to edit:
Before running the playbook, the following files should be edited:
Inventory file: hosts
Variable file: roles/openstack_set_demo/vars/main.yml
Environment file: ~/.config/openstack/clouds.yml (Create if does not exists. The sample located at the root of the repo.)
