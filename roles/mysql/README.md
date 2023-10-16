# Oracle MySQL

***

<img src="media/icon_mysql.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van MySQL database server.<br/> 
Afhankelijk van de infrastructuur wordt deze als Podman pod (docker container), kubernetes container of direct op het besturingssysteem geinstalleerd.<br/>
Website leverancier: `https://project-cockpit.org`<br/>
<br/>
<br/>


***

# Diensten:

## Installatie en configuratie Oracle MySQL

action: **install**<br/>
Installatie van laatste versie van Oracle MySQL. Basis configuratie.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van Oracle MySQL. Verwijderen configuratie folder.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



Voorbeeld voor installatie Oracle MySQL:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: mysql
      vars:
        action            : install

```



## Globale variabelen
Onderstaande variabelen kunnen door de Management role worden gebruikt:<br/>
