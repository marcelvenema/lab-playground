# Sonatype Nexus Repository OSS

***

<img src="media/icon_nexus.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van Sonatype Nexus Repository OSS.<br/>
Afhankelijk van de infrastructuur wordt deze als Podman pod (docker container), kubernetes container of direct op het besturingssysteem geinstalleerd.<br/>
Vooralsnog is alleen installatie en configuratie als Podman pod beschikbaar.<br/>
<br/>
<br/>


***

# Diensten:

action: **install**<br/>
Installatie van laatste versie van Sonatype Nexus Repository OSS. Basis configuratie.<br/>
variablen:<br/>
<kbd>repository_url</kbd>        : URL met locatie van container repository. Kan een url zijn of pad naar lokaal bestand.<br/>
<kbd>platform (optioneel)</kbd>  : installeer op specifiek platform, bijvoorbeeld podman, kubernetes, linux. Standaard is autodetect.<br/>
<kbd>uninstall (optioneel)</kbd> : true/false. Wanneer, true wordt voor installatie eerst uninstall gestart.<br/>
<kbd>vault_address</kbd>         : url naar vault adres voor toegang vault, bijvoorbeeld `http://localhost:8081`<br/>
<kbd>vault_token</kbd>           : token voor toegang tot vault.<br/>


action: **update**<br/>
Update naar laatste Sonatype Nexus Repository OSS versie. (backlog).
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **create_repository**<br/>
Aanmaken repository in Nexus.<br/>
variablen:<br/>
<kbd>nexus_repository_name</kbd> : Naam voor repository.<br/>
<kbd>nexus_repository_type</kbd> : Type repository, bijvoorbeeld raw.


action: **destroy_repository**<br/>
Verwijderen repository in Nexus. (backlog).
variablen:<br/>
<kbd>nexus_repository_name</kbd> :  Naam voor repository.<br/>


action: **create_user**<br/>
Aanmaken lokale gebruiker in Nexus Repository.
variablen:<br/>
<kbd>nexus_username</kbd>  : Gebruikersnaam.<br/>
<kbd>nexus_firstname</kbd> : Voornaam van gebruiker.<br/>
<kbd>nexus_lastname</kbd>  : Achternaam van gebruiker.<br/>
<kbd>nexus_email</kbd>     : E-mail adres van gebruiker.<br/>
<kbd>nexus_password</kbd>  : Wachtwoord van gebruiker.<br/>
<kbd>nexus_role</kbd>      : Rol, bijvoorbeeld nx-admin.<br/>


action: **destroy_user**<br/>
Verwijderen gebruiker in Nexus. (backlog).
variablen:<br/>
<kbd>nexus_username</kbd> :  Gebruikersnaam.<br/>


action: **set_password**<br/>
Wijzigen van wachtwoord van een gebruiker in Nexus. (backlog).
variablen:<br/>
<kbd>nexus_username</kbd> :  Gebruikersnaam.<br/>
<kbd>nexus_password</kbd> :  Wachtwoord.<br/>


action: **import_artifacts**<br/>
Importeer artifacts in folderstructuur naar Nexus repository. (backlog).
variablen:<br/>
<kbd>nexus_repository_name</kbd>     :  
<kbd>nexus_repository_folder</kbd>   : 
<kbd>data_folder</kbd>               : 
<kbd>nexus_repository_address</kbd>  : URL van repository, bijvoorbeeld `https://localhost:8081`.
<kbd>nexus_repository_username</kbd> : Gebruikersnaam voor toegang repository.
<kbd>nexus_repository_password</kbd> : Wachtwoord voor toegang repository.


action: **export_artifacts**<br/>
Export artifacts uit repository naar folderstructuur. (backlog).
variablen:<br/>
<kbd>nexus_repository_name</kbd>     :  
<kbd>nexus_repository_folder</kbd>   : 
<kbd>data_folder</kbd>               : 
<kbd>nexus_repository_address</kbd>  : URL van repository, bijvoorbeeld `https://localhost:8081`.
<kbd>nexus_repository_username</kbd> : Gebruikersnaam voor toegang repository. 
<kbd>nexus_repository_password</kbd> : Wachtwoord voor toegang repository.


action: **sync_artifacts**<br/>
Synchroniseer via .json bestand artifacts van extern naar repository. (backlog).
variablen:<br/>
<kbd>config_file</kbd>               : Configuratie file met synchronisatie items. 
<kbd>nexus_repository_address</kbd>  : URL van repository, bijvoorbeeld `https://localhost:8081`.
<kbd>nexus_repository_username</kbd> : Gebruikersnaam voor toegang repository.
<kbd>nexus_repository_password</kbd> : Wachtwoord voor toegang repository.


***

## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
(geen).<br/>


## Installatie
Installatie via action 'install'.<br/>
Voorbeeld voor installatie Nexus Repository OSSL:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: nexus_repository
      vars:
        action        : install
        vault_address : "http://localhost:8200"
        vault_token   : "hvs.9MGoUtPEGZWRgLX3dxZYkqxV"

```


## Configuratie
(geen).<br/>


## Overige informatie

**Globale variabelen**
Onderstaande variabelen kunnen door de nexus_repository role worden gebruikt:<br/>
<kbd>automation_address</kbd> Hostname van server.<br/>
<kbd>automation_username</kbd> Hostname van server.<br/>
<kbd>automation_password</kbd> Hostname van server.<br/>
<kbd>automation_email</kbd> Hostname van server.<br/>


## Licentie
MIT


## Auteur
Marcel Venema
