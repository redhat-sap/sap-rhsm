# sap-rhsm [![Build Status](https://travis-ci.com/redhat-sap/sap-rhsm.svg?branch=master)](https://travis-ci.com/redhat-sap/sap-rhsm)

This role configures Red Hat Subscriptions for RHEL 8 to enable SAP Solutions to be installed on the target system(s).

## Requirements

A valid Red Hat subscription, either directly with redhat.com or through the use of Red Hat Satellite

## Role Variables

See `Example Inventory` below for more specific details. At a high level, the following variables are accepted:

| variable | info | required? |
|:--------:|:----:|:---------:|
|sap_rhsm_username|Username used to register to access.redhat.com|yes if username/password is used|
|sap_rhsm_password|Password used to register to access.redhat.com|yes if username/password is used|
|sap_rhsm_server_hostname|The Red Hat Satellite hostname/FQDN used for registration|yes if Satellite registration is used|
|sap_rhsm_activationkey|The Red Hat Satellite activation key used for registration|yes if Satellite registration is used|
|sap_rhsm_org_id|The Red Hat Satellite organization ID used for registration|yes if Satellite registration is used|
|sap_rhsm_pool_ids|The subscription pool IDs to consume|no|
|sap_rhsm_repos|A list of repositories to enable|no|
|sap_rhsm_force_register|Set to 'yes' to force a unregister/clean + re-registration|no|
|sap_rhsm_proxy_hostname|Specify a HTTP proxy hostname|no|
|sap_rhsm_proxy_port|Specify a HTTP proxy port|no|
|sap_rhsm_proxy_user|Specify a HTTP proxy user|no|
|sap_rhsm_proxy_password|Specify a HTTP proxy password|no|
|sap_rhsm_register_insights|Register the system to Red Hat Insights|no (default true)|
|sap_rhsm_use_e4s|Whether to use 'e4s' repositories or not|no (default true)|

## Dependencies

None

## Example Playbook

```yaml
    - hosts: servers
      roles:
      - role: sap-rhsm
```

## Example Inventory

When using Satellite:

```yaml
sap_rhsm_server_hostname: 'sat.example.com'
sap_rhsm_org_id: 'my-org'
sap_rhsm_activationkey: 'my-org-key'
```

When using access.redhat.com:

```yaml
sap_rhsm_username: 'my-username'
sap_rhsm_password: 'my-password'
```

## License

GPLv3

## Author Information

Red Hat SAP Community of Practice
