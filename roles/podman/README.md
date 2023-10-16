# RedHat Podman

***

<img src="media/icon_podman.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van podman.<br/>
<br/>
<br/>
<br/>
<br/>


***

# Diensten:

## Installatie en configuratie RedHat Podman

action: **install**<br/>
Installatie van laatste versie van RedHat Podman. Basis configuratie.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variablen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van RedHat Podman.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variablen benodigd.<br/>



Voorbeeld voor installatie RedHat Podman:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: podman
      vars:
        action            : install

```



## Overige informatie
