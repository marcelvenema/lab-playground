# Base_Server_Config

***

<img src="media/icon_management.png" align="left" height="128" width="128" />
Ansible role voor het uitvoeren van diverse lokale management taken tijdens installatie en configuratie van een server.<br/>
<br/>
<br/>
<br/>
<br/>

***

De volgende taken worden uitgevoerd:<br/>
- Aanpassen hostname server, op basis van `{{ admin_hostname }}` parameter. Wordt overgeslagen indien parameter niet is geconfigureerd.</br>
- Aanmaken admin gebruiker, op basis van `{{ admin_username }}` parameter. Indien niet geconfigureerd wordt, 'admin' als standaard waarde gebruikt.<br/>
- Aanmaken wachtwoord gebruiker, op basis van `{{ admin_password }}` parameter. Indien niet geconfigreerd, wordt 'P@ssw0rd!' als standaard waarde gebruikt.<br/>
- Aanmaken SSH key, RSA 4096.<br/>
- Enable automatic software updates.<br/>


# Diensten:

action: **configure**<br/>
Configuratie management van de server.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


***


## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
(geen).<br/>


## Installatie en configuratie
Configuratie via action 'configure'.<br/>
Voorbeeld voor configuratie lab server:
```
---

- hosts: lab_server
  vars:
  roles:
    - role: management
      vars:
        action            : configure
        admin_hostname    : labserver.marcelvenema.com
        admin_username    : ansible
        admin_password    : P@ssw0rd!
```


## Overige informatie

**Globale variabelen**
Onderstaande variabelen kunnen door de base_server_config role worden gebruikt:<br/>
<kbd>admin_hostname</kbd> Hostname van server.<br/>
<kbd>admin_username</kbd> Gebruikersnaam voor admin.<br/>
<kbd>admin_usercomment</kbd> Opmerking bij admin gebruikersnaam.<br/>
<kbd>admin_password</kbd> Wachtwoord voor admin gebruiker.<br/>


## Licentie
MIT


## Auteur
Marcel Venema