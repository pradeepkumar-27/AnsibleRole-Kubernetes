Kubernetes
=========

Ansible role to configure Kubernetes multi node cluster.

Requirements
------------

I have created this role to configure my MapReduce cluster on top of Amazom Web Services (AWS) using Amazon Linux 2 as Operating System. This role will work on any RedHat/Centos systems.

Role Variables

--------------

This role has a default variable "cidr" which represents the cidr of the Flannel CNI.

ansibele.cfg
------------

Ansible configuration file to run this role

    [defaults]
    interpreter_python=auto_silent
    inventory      = ./hosts
    roles_path    = ./yourRolesPath (i.e the path where you have downloaded this role)
    host_key_checking = False
    remote_user = ec2-user
    private_key_file = ./yourKey.pem
    
    [privilege_escalation]
    become=True
    become_method=sudo
    become_user=root
    become_ask_pass=False

hosts
------------

Ansible inventory file where you have to put the IP of the servers.


    [Master]
    master
    
    [Slave]
    slave1
    slave2
    
    [Kubernetes:children]
    Master
    Slave
    

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: Kubernetes
      roles:
         - Kubernetes
           vars:
             cidr: 10.244.0.0/16
