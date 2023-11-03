# Oracle MySQL

***

<img src="media/icon_mysql.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van MySQL database server.<br/> 
Afhankelijk van de infrastructuur wordt deze als Podman pod (docker container), kubernetes container of direct op het besturingssysteem geinstalleerd.<br/>

Website leverancier: `https://mysql.com`.<br/>
<br/>


***

# Diensten:


action: **install**<br/>
Installatie van laatste versie van Oracle MySQL. Basis configuratie.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **uninstall**<br/>
De-installatie van Oracle MySQL. Verwijderen configuratie folder.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


***


## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
(geen).<br/>


## Installatie
Installatie via action 'install'.<br/>
Voorbeeld voor installatie Oracle MySQL:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: mysql
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
