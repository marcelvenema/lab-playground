
## Role server_config_linux
- Role gebruikt password_hash functie. Ansible geeft deprecation warning, the Python crypt module is deprecated.

## Role cockpit
- TODO Configuratie van banner tekst.
- TODO action: configure - her-configuratie van cockpit. terugzetten cockpit.conf en config opnieuw runnen?

## Role mysql
- Role wordt nu geinstalleerd, verdere configuratie gewenst.


## Role nexus_repository
- Ansible task / powershell / bash script voor import van artifacts in repository. action import_artifacts.
- Ansible task / powershell / bash script voor export van artifacts naar disk. action export_artifacts.
- Ansible task / powershell / bash script voor synchronisatie artifacts tussen repositories. action sync_artifacts.
- Configuratie van update action.
- Configuratie van destroy_user action.
- Configuratie get_repository action.
- Configuratie destroy_repository action.


## Role podman
- Configuratie configure action.



## Role semaphore
- splitsen mysql - semaphore container.
- automatische configuratie semaphore.
- Configuratie import_playbooks action.
- Configuratie export_playbooks action.


## Role gogs
- nader in te vullen.


## Role vault
- Vault service in podman start niet automatisch na reboot. 

- Configuratie van update action.
- Configuratie van destroy_secret action.
- Configuratie van get_policy action.
- Configuratie van destroy_policy action.
- Configuratie van get_approle action.
- Configuratie van destroy_approle action.
- Ansible task / powershell / bash script voor import van secrets naar vault. action import_secrets.
- Ansible task / powershell / bash script voor export van secrets naar disk. action export_secrets.
