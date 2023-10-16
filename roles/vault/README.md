# Hashicorp Vault

***

<img src="media/icon_vault.png" align="left" height="128" width="128" />
Ansible role voor installatie en configuratie van Hashicorp Vault.<br/>
Afhankelijk van de infrastructuur wordt deze als Podman pod (docker container), kubernetes container of direct op het besturingssysteem geinstalleerd.<br/>
Vooralsnog is alleen installatie en configuratie als Podman pod beschikbaar.<br/>
<br/>
<br/>


***

# Diensten:

## Installatie en configuratie Hashicorp Vault


action: **install**<br/>
Installatie van laatste versie van Hashicorp Vault. Basis configuratie.<br/>
variables:<br/>
<kbd>platform (optioneel)</kbd>  : installeer op specifiek platform, bijvoorbeeld podman, kubernetes, linux. Standaard is autodetect.<br/>
<kbd>uninstall (optioneel)</kbd> : true/false. Wanneer, true wordt voor installatie eerst uninstall gestart.<br/>


action: **uninstall**<br/>
De-installatie van Hashicorp Vault.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **update**<br/>
Update Hashicorp Vault naar de laatste versie. (backlog).<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>
<kbd>platform (optioneel)</kbd>  : installeer op specifiek platform, bijvoorbeeld podman, kubernetes, linux. Standaard is autodetect.<br/>


action: **unseal**<br/>
Unseal Vault zodat deze gereed is voor gebruik.<br/>
variables:<br/>
<kbd>vault_unseal_keys</kbd> : Unseal keys.<br/>
<kbd>vault_address</kbd>     : URL naar Vault, bijvoorbeeld `https://192.168.1.0:8200`.<br/>



## Secrets

action: **create_secret_engine**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **destroy_secret_engine**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **get_secret**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **create_secret**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **destroy_secret**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>



## Overige informatie
