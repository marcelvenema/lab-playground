# Ansible Semaphore

***

<img src="media/icon_semaphore.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van Ansible Semaphore.<br/>
<br/>
<br/>
<br/>
<br/>


***

# Diensten:

## Installatie en configuratie Ansible Semaphore

action: **install**<br/>
Installatie van laatste versie van Ansible Semaphore. Basis configuratie.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van Ansible Semaphore.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



Voorbeeld voor installatie Ansible Semaphore:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: semaphore
      vars:
        action            : install

```



## Overige informatie
