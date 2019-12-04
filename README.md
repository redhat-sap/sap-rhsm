# sap-rhsm

This role configures Red Hat Subscriptions for RHEL 8 to enable SAP Solutions to be installed on the target system(s).

## Requirements

A valid Red Hat subscription, either directly with redhat.com or through the use of Red Hat Satellite

## Role Variables

See `Example Inventory` below for more specific details. At a high level, the following variables are accepted:

| variable | info | required? |
|:--------:|:----:|:---------:|
|rhsm_username|Username used to register to access.redhat.com|yes if username/password is used|
|rhsm_password|Password used to register to access.redhat.com|yes if username/password is used|
|rhsm_server_hostname|The Red Hat Satellite hostname/FQDN used for registration|yes if Satellite registration is used|
|rhsm_activationkey|The Red Hat Satellite activation key used for registration|yes if Satellite registration is used|
|rhsm_org_id|The Red Hat Satellite organization ID used for registration|yes if Satellite registration is used|
|rhsm_pool_ids|The subscription pool IDs to consume|no|
|rhsm_repos|A list of repositories to enable|no|
|rhsm_force_register|Set to 'yes' to force a unregister/clean + re-registration|no|
|rhsm_proxy_hostname|Specify a HTTP proxy hostname|no|
|rhsm_proxy_port|Specify a HTTP proxy port|no|
|rhsm_proxy_user|Specify a HTTP proxy user|no|
|rhsm_proxy_password|Specify a HTTP proxy password|no|
|register_insights|Register the system to Red Hat Insights|no (default true)|

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
rhsm_server_hostname: 'sat.example.com'
rhsm_org_id: 'my-org'
rhsm_activationkey: 'my-org-key'
```

When using access.redhat.com:

```yaml
rhsm_username: 'my-username'
rhsm_password: 'my-password'
```

## License

GPLv3

## Author Information

Red Hat SAP Community of Practice
