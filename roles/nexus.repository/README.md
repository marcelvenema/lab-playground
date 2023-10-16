# Sonatype Nexus Repository OSS

***

<img src="media/icon_nexus.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van Sonatype Nexus Repository OSS.
Afhankelijk van de infrastructuur wordt deze als Podman pod (docker container), kubernetes container of direct op het besturingssysteem geinstalleerd.
Vooralsnog is alleen installatie en configuratie als Podman pod beschikbaar.

***

# Diensten:

## Installatie en configuratie Nexus Repository OSS

action: **install**<br/>
Installatie van laatste versie van Sonatype Nexus Repository OSS. Basis configuratie.<br/>
variables:<br/>
<kbd>platform (optioneel)</kbd>  : installeer op specifiek platform, bijvoorbeeld podman, kubernetes, linux. Standaard is autodetect.<br/>
<kbd>uninstall (optioneel)</kbd> : true/false. Wanneer, true wordt voor installatie eerst uninstall gestart.<br/>
<kbd>vault_address</kbd>         : url naar vault adres voor toegang vault, bijvoorbeeld `http://localhost:8081`<br/>
<kbd>vault_token</kbd>           : token voor toegang tot vault.<br/>


action: **update**<br/>
Update naar laatste Sonatype Nexus Repository OSS versie. (backlog).
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



## Repositories

action: **create_repository**<br/>
Aanmaken repository in Nexus.<br/>
variables:<br/>
<kbd>nexus_repository_name</kbd> : Naam voor repository.<br/>
<kbd>nexus_repository_type</kbd> : Type repository, bijvoorbeeld raw.


action: **destroy_repository**<br/>
Verwijderen repository in Nexus. (backlog).
variables:<br/>
<kbd>nexus_repository_name</kbd> :  Naam voor repository.<br/>



## Gebruikers en groepen

action: **create_user**<br/>
Aanmaken lokale gebruiker in Nexus.
variables:<br/>
<kbd>nexus_username</kbd>  : Gebruikersnaam.<br/>
<kbd>nexus_firstname</kbd> : Voornaam van gebruiker.<br/>
<kbd>nexus_lastname</kbd>  : Achternaam van gebruiker.<br/>
<kbd>nexus_email</kbd>     : E-mail adres van gebruiker.<br/>
<kbd>nexus_password</kbd>  : Wachtwoord van gebruiker.<br/>
<kbd>nexus_role</kbd>      : Rol, bijvoorbeeld nx-admin.<br/>


action: **destroy_user**<br/>
Verwijderen gebruiker in Nexus. (backlog).
variables:<br/>
<kbd>nexus_username</kbd> :  Gebruikersnaam.<br/>


action: **set_password**<br/>
Wijzigen van wachtwoord van een gebruiker in Nexus. (backlog).
variables:<br/>
<kbd>nexus_username</kbd> :  Gebruikersnaam.<br/>
<kbd>nexus_password</kbd> :  Wachtwoord.<br/>



## Import en Export

action: **import_artifacts**<br/>
Importeer artifacts in folderstructuur naar Nexus repository. (backlog).
variables:<br/>
<kbd>nexus_repository_name</kbd>     :  
<kbd>nexus_repository_folder</kbd>   : 
<kbd>data_folder</kbd>               : 
<kbd>nexus_repository_address</kbd>  : URL van repository, bijvoorbeeld `https://localhost:8081`.
<kbd>nexus_repository_username</kbd> : Gebruikersnaam voor toegang repository.
<kbd>nexus_repository_password</kbd> : Wachtwoord voor toegang repository.


action: **export_artifacts**<br/>
Export artifacts uit repository naar folderstructuur. (backlog).
variables:<br/>
<kbd>nexus_repository_name</kbd>     :  
<kbd>nexus_repository_folder</kbd>   : 
<kbd>data_folder</kbd>               : 
<kbd>nexus_repository_address</kbd>  : URL van repository, bijvoorbeeld `https://localhost:8081`.
<kbd>nexus_repository_username</kbd> : Gebruikersnaam voor toegang repository. 
<kbd>nexus_repository_password</kbd> : Wachtwoord voor toegang repository.


action: **sync_artifacts**<br/>
Synchroniseer via .json bestand artifacts van extern naar repository. (backlog).
variables:<br/>
<kbd>config_file</kbd>               : Configuratie file met synchronisatie items. 
<kbd>nexus_repository_address</kbd>  : URL van repository, bijvoorbeeld `https://localhost:8081`.
<kbd>nexus_repository_username</kbd> : Gebruikersnaam voor toegang repository.
<kbd>nexus_repository_password</kbd> : Wachtwoord voor toegang repository.



## Globale variabelen
Onderstaande variabelen kunnen door de Management role worden gebruikt:<br/>
<kbd>automation_address</kbd> Hostname van server.<br/>
<kbd>automation_username</kbd> Hostname van server.<br/>
<kbd>automation_password</kbd> Hostname van server.<br/>
<kbd>automation_email</kbd> Hostname van server.<br/>

