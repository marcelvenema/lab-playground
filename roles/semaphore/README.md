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


action: **install**<br/>
Installatie van laatste versie van Ansible Semaphore. Basis configuratie.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van Ansible Semaphore.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


***


## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
(geen).<br/>


## Installatie en configuratie
Installatie via action 'install'.<br/>
Voorbeeld voor installatie Semaphore:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: semaphore
      vars:
        action : install

```


## Overige informatie
(geen).<br/>


## Licentie
MIT


## Auteur
Marcel Venema
