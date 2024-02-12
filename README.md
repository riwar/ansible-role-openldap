Role Name
=========

Install and configure openldap server on Almalinux 9

Requirements
------------

Almalinux9, RedHat (?)

Role Variables (default)
------------------------

Check [defaults/main.yml](defaults/main.yml) for a list of default options and values

Role Variables 
------------------------
### TLS
```yaml
# All of these are optional, to use them create a dir called files/openlapd and put your certs
# in that directory
openldap_tls_cert: tls cert
openldap_tls_key:  tls key
openldap_tls_cacert: cacert
```

### Openldap config
```yaml
openldap_entries:
  - dn: ou=a,dc=dn,dc=to,dc=add
    state: absent | present (default)
    objectClass:
      - list of objectClasses to add
    attributes:
      dict: of attributes

openldap_attributes:
  - dn: ou=a,dc=dn,dc=to,dc=change
    state: 'exact (default) |present|absent'
    attributes:
      dict: of attributes
```
 
Dependencies
------------

Example Playbook
----------------

```
- hosts: servers
  roles:
    - openldap
  vars:
    openldap_schemas:
      - core.ldif
      - cosine.ldif
      - nis.ldif
      - inetorgperson.ldif
      - rfc2739.ldif
    openldap_entries:
      - dn:  'cn=module{0},cn=config'
        objectClass: olcModuleList
        attributes:
          cn: module
          olcModulepath: /usr/lib64/openldap
          olcModuleload: 
            - syncprov.la
    openldap_attributes:
      - dn: 'olcDatabase={0}config,cn=config'
        attributes:
          olcRootDN: 'cn=admin,cn=config'
          olcRootPW: '{Crypt) password'
```

License
-------

BSD

