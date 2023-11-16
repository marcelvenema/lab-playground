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

action: **install**<br/>
Installatie van laatste versie van Git Gogs. Basis configuratie.<br/>
variables:<br/>
<kbd>repository_url</kbd> : URL met locatie van container repository. Kan een url zijn of path.<br/>


action: **uninstall**<br/>
De-installatie van Git Gogs.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


***


## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
Gogs maakt gebruik van een MySQL database.<br/>


## Installatie
Installatie via action 'install'.<br/>
Voorbeeld voor installatie Gogs Git service:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: podman.gogs
      vars:
        action : install

```


## Configuratie
(geen).<br/>


## Overige informatie
(geen).<br/>


## Licentie
MIT


## Auteur
Marcel Venema
