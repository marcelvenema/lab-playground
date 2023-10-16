# Management

***

<img src="media/icon_management.png" align="left" height="128" width="128" />
Ansible role voor het uitvoeren van diverse lokale management taken tijdens installatie en configuratie van een server.<br/>
<br/>
<br/>
<br/>

***

De volgende taken worden uitgevoerd:<br/>
- Aanpassen hostname server, op basis van {{ admin_hostname }} parameter. Wordt overgeslagen indien parameter niet is geconfigureerd.</br>
- Aanmaken admin gebruiker, op basis van {{ admin_username }} parameter. Indien niet geconfigureerd wordt, 'admin' als standaard waarde gebruikt.<br/>
- Aanmaken wachtwoord gebruiker, op basis van {{ admin_password }} parameter. Indien niet geconfigreerd, wordt 'P@ssw0rd!' als standaard waarde gebruikt.<br/>
- Aanmaken SSH key, RSA 4096, passpr

# Diensten:

## Configuratie

action: **configure**<br/>
Configuratie management van de server.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



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



## Globale variabelen
Onderstaande variabelen kunnen door de Management role worden gebruikt:<br/>
<kbd>admin_hostname</kbd> Hostname van server.<br/>
<kbd>admin_username</kbd> Gebruikersnaam voor admin.<br/>
<kbd>admin_usercomment</kbd> Opmerking bij admin gebruikersnaam.<br/>
<kbd>admin_password</kbd> Wachtwoord voor admin gebruiker.<br/>
