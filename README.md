subscribe-rhn
===============

This playbook configures are RHEL server to receive its updates from RHN or a Satellite 6 server.
It registers against Satellite or RHN with orgid and activationkey or username and password

Requirements
------------

To use this role you need a proper Red Hat subscription. If you are a developer you can obtain your personal free subscription from here https://developers.redhat.com/products/sap/download/ by registering as developer

Role Variables
--------------

You can then set the following variables in the playbook:

    satellite_server: FQDN

Set the following variables if you want to register with activationkey and orgid:

     reg_activation_key: 
     reg_organization_id:


Use the following variables to register with your RHN username and password. Please use ansible-vault or tower for proper encryption of your credentials.

      reg_pool: 
      reg_pool_ids: 
      reg_username: 
      reg_password: 

The following are optional

    reg_server_insecure: defaults to no
    reg_autosubscribe: defaults to yes 
    reg_osrelease: default unset, can set to 7Server, 7.2, 7.3 etc 

Set this variable to true if you want to remove/disable all previously existing repositories. The default is true

     repo_reset: true

Use this to define the list of repositories you want to subscribe to

     repositories:
                  - rhel-7-server-rpms
                  - repo2
                  - repo3

Example Playbook
----------------

Here is an example playbook that adds two disks in volumegroup vg00 and adds another one to the existing root volumegroup

    - hosts: servers
      remote_user: root

      vars:
          # satellite_server: FQDN
          #
          # Option 1
          reg_activation_key: myregistration
          reg_organization_id: 123456

          #
          # Option 2:
          #    reg_pool:
          #    reg_pool_ids:
          #    reg_username:
          #    reg_password:
          #
          # The following are optional
          reg_server_insecure: yes
          reg_autosubscribe: yes
          reg_osrelease: 7.4

          # Set this variable to true if you want to remove/disable all previously existing repositories. The default is false
          repo_reset: true

          repositories:
                  - rhel-7-server-rpms
                  - rhel-sap-hana-for-rhel-7-server-rpms
       
      roles:
         - { role: mk-ansible-roles.subscribe-rhn }

License
-------

Apache License
Version 2.0, January 2004

Author Information
------------------

Markus Koch

Please leave comments in the github repo issue list
