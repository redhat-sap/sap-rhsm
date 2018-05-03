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


Use the following variables to register with your RHN username and password. You should use ansible-vault or tower to encrypt  your credentials.

      reg_pool:
      reg_pool_ids:
      reg_username:
      reg_password:

The following are optional:

    reg_server_insecure: defaults to no
    reg_autosubscribe: defaults to unset
    reg_osrelease: default unset, can set to 7Server, 7.2, 7.3 etc

Set this variable to true if you want to remove/disable all previously existing repositories. The default is false

     repo_reset: true

Use this to define the list of repositories you want to subscribe to

     repositories:
                  - rhel-7-server-rpms
                  - repo2
                  - repo3
The default is set to `rhel-{{ ansible_distribution_major_version }}-server-rpms`which is resolved to e.g. `rhel-7-server-rpms` or `rhel-6-server-rpms`, depending on the RHEL major release.

Example Playbook
----------------

Here is an example playbook that registers a server against Red Hat Network (satellite_server is not defined) with the activationkey `myregistration` and the organization id `123456`. The release is locked down to RHEL 7.4, all previously defined repositories are removed and the system will  `rhel-7-server-e4s-rpms` and `rhel-sap-hana-for-rhel-7-server-e4s-rpms`. (For SAP see also https://access.redhat.com/solutions/3075991)

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
          #reg_autosubscribe: yes
          reg_osrelease: 7.4

          # Set this variable to true if you want to remove/disable all previously existing repositories. The default is false
          repo_reset: true

          repositories:
                  - rhel-7-server-e4s-rpms
                  - rhel-sap-hana-for-rhel-7-server-e4s-rpms

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
