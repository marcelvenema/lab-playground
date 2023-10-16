# Lab Playground development server
Playbook voor installatie en configuratie van een development lab server, als basis voor het ontwikkelen van een moderne infrastructuur op basis van Ansible, GitLab, Hashicorp Vault en Nexus Repository OSS.
Het playbook installeert de volgende rollen:

- RedHat Cockpit
  Browser-gebaseerde beheeromgeving voor Linux. Toegang via http://<hostname>:9090.
  Gebruikersnaam en wachtwoord zijn gedefinieerd in all.yml group_vars bestand als lab_username en lab_password.

- Podman container infrastructure
  Container infrastructuur. Kan worden beheerd via de Cockpit user interface.

- Hashicorp Vault
  Secret management. Geinstalleerd als container, benaderbaar via http://<hostname>:8200.
  Access token en unseal keys zijn opgeslagen in /data/vault/config folder.

- Ansible Semaphore
  Grafische interface voor Ansible. Geinstalleerd als container, benaderbaar via http://<hostname>:3000

- Gogs - Git service
  Geinstalleerd als container, benaderbaar via http://<hostname>:10880.

- Sonatype Nexus Repository OSS
  Artifact repository. Geinstalleerd als container, banderbaar via http://<hostname>:8081.
  User name is admin, initial password is stored in vault.


# Pre-requisites

Review the parameters in inventory/lab/group_vars/all.yml

Install Ansible Galaxy collections with sh requirements.sh

# Installation

```bash
ansible-playbook install.yml -i inventory/lab/hosts.ini
```

## Globale variabelen:

- uninstall: true | false
  Bij installatie (install) van een role, wordt de role eerst ge-deinstalleerd (uninstall).


- lab_hostname: labserver.marcelvenema.com
- lab_username: admin
- lab_usercomment: "Admin user for Lab environment"
- lab_password: Password29!
- lab_email: marcel@marcelvenema.com

- automation_username: Gedefinieerd in group_vars/all.yml
- automation_password: not present, will be generated.
- automation_email: "ansible@marcelvenema.com"



Clean RHEL/RockyLinux installation:
Volgende packages dienen te worden geinstalleerd:
- epel-release : prerequisite voor ansible
- ansible : voor starten playbooks
- tar : voor configuratie visual studio code remote ssh
- nano : makkelijke editor

git config --global user.name "(github username)"
git config --global user.email "(github email)"

maak ssh certificaat aan via ssh-keygen -
ssh-keygen -t ed25519 -C "your_email@example.com"
kopieer de publieke sleutel en kopieer naar github settings
test git connectie: 
ssh -T git@github.com


vscode extensions:
- ansible
- remote-ssh
