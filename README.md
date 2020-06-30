# Role Ansible - OpenLDAP

Rôle en cours de développement...

## TDL

- Obtention d'un certificat via notre CA    CHECK
- Installation de slapd    CHECK
- Configuration de l'APT    CHECK
- Activation de STARTTLS    CHECK
- Création des admins
- Overlays
- Structuration de l'arbre
- Sécurisation avec permissions réduite
- Forcer STARTTLS
- Ajout de schéma

### OUs
```yaml
ou:
  - name: group
    orgs:
      - elukerio
      - libmail
  - name: people
    orgs:
      - elukerio
      - libmail
  - name: system
```

### Schema
```yaml
pen: 15586
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
      - name: mailalliasfrom
        desc: Mail from
        equality: caseExactMatch
        options:
          - single-value
      - name: mailalliasto
        desc: Mail to
        equality: caseExactMatch
      - name: mailaliasactif
        desc: Alias actif
        equality: caseExactMatch
        options:
          - single-value
      - name: maildomainactif
        desc: Domaine Actif
        equality: caseExactMatch
        options:
          - single-value
    classes:
      - name: mailaccountlibmail
        sup: top
        type: auxiliary
        must:
          - mailaccountquota
          - mailaccountactif
      - name: mailaliaslibmail
        sup: top
        type: structural
        must:
          - cn
          - mailaliasfrom
          - mailaliasto
          - mailaliasactif
      - name: maildomainlibmail
        sup: top
        type: auxiliary
        must:
          - maildomain
          - maildomainactif
```
