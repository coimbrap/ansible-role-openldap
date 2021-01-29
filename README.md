# Role Ansible - OpenLDAP

Ansible role for the openldap setup.

Support RFC 2307bis.

Client cert path : `/opt/ca.crt`

### Example
```yaml
domain: devo.re
org: devo
ldap_backend: "mdb"

ou:
  - name: groups
  - name: people
  - name: system

cn:
  - name: lastGID
    oc: #Object Class
      - device
      - top
    description: last gid of a group
  - name: admins
    base: groups
    description: devo admins
    member: cn=admin,dc=devo,dc=re
  - name: everybody
    base: groups
    description: devo everybody

pen: 99999
schemas:
  - name: mail
    position: 1
    attributes:
      - name: mailquota
        desc: Quota Mail
        equality: caseExactMatch
        options:
          - single-value
      - name: mailactif
        desc: Mail actif
        equality: caseExactMatch
        options:
          - single-value
      - name: mailaliasfrom
        desc: Mail from
        equality: caseExactMatch
        options:
          - single-value
      - name: mailaliasto
        desc: Mail to
        equality: caseExactMatch
    classes:
      - name: mailaccount
        sup: top
        type: auxiliary
        must:
          - mailquota
          - mailactif
```

### License

GPLv3

### Author Information

Pierre Coimbra
