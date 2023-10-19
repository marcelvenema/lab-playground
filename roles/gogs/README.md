# Git Gogs

***

<img src="media/icon_gogs.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van Git Gogs.<br/>
<br/>
<br/>
<br/>
<br/>


***

# Diensten:

## Installatie en configuratie Git Gogs

action: **install**<br/>
Installatie van laatste versie van Git Gogs. Basis configuratie.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van Git Gogs.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



Voorbeeld voor installatie Git Gogs:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: podman.gogs
      vars:
        action            : install

```



## Overige informatie
