# Lab Playground development server

***

<img src="media/logo_lab.png" align="left" height="128" width="128" />
Playbook voor installatie en configuratie van een development lab server, als basis voor het ontwikkelen van een moderne infrastructuur op basis van Ansible, GitLab, Hashicorp Vault en Nexus Repository OSS.

***


Het playbook installeert de volgende rollen:

- RedHat Cockpit<br/>
  Browser-gebaseerde beheeromgeving voor Linux. Toegang via http://<hostname>:9090.<br/>
  Gebruikersnaam en wachtwoord zijn gedefinieerd in all.yml group_vars bestand als lab_username en lab_password.<br/>

- Podman container infrastructure<br/>
  Container infrastructuur. Kan worden beheerd via de Cockpit user interface.<br/>

- Hashicorp Vault<br/>
  Secret management. Geinstalleerd als container, benaderbaar via http://<hostname>:8200.<br/>
  Access token en unseal keys zijn opgeslagen in /data/vault/config folder.<br/>

- Ansible Semaphore<br/>
  Grafische interface voor Ansible. Geinstalleerd als container, benaderbaar via http://<hostname>:3000<br/>

- Gogs - Git service<br/>
  Geinstalleerd als container, benaderbaar via http://<hostname>:10880.<br/>

- Sonatype Nexus Repository OSS<br/>
  Artifact repository. Geinstalleerd als container, banderbaar via http://<hostname>:8081.<br/>
  User name is admin, initial password is opgeslagen in Vault.<br/>


# Pre-requisites

Review en controleer de parameters in inventory/lab/group_vars/all.yml bestand.<br/>

Installeer Ansible Galaxy collections via `sh requirements.sh`<br/>

# Installatie

```bash
ansible-playbook install.yml -i inventory/lab/hosts.ini -K
```

## Globale variabelen:

- uninstall: true | false<br/>
  Bij installatie (install) van een role, wordt de role eerst ge-deinstalleerd (uninstall).<br/>


- lab_hostname: labserver.marcelvenema.com
- lab_username: admin
- lab_usercomment: "Admin user for Lab environment"
- lab_password: Password29!
- lab_email: marcel@marcelvenema.com

- automation_username: Gedefinieerd in group_vars/all.yml
- automation_password: not present, will be generated.
- automation_email: "ansible@marcelvenema.com"



Clean RHEL/RockyLinux installatie:<br/>
Volgende packages dienen te worden geinstalleerd:<br/>
- epel-release : prerequisite voor ansible<br/>
- ansible : voor starten playbooks<br/>
- tar : voor configuratie visual studio code remote ssh<br/>
- nano : makkelijke editor<br/>

git config --global user.name "(github username)"<br/>
git config --global user.email "(github email)"<br/>

maak ssh certificaat aan via ssh-keygen -
`ssh-keygen -t ed25519 -C "your_email@example.com"`
kopieer de publieke sleutel en kopieer naar github settings
test git connectie: 
`ssh -T git@github.com`


vscode extensions:
- ansible
- remote-ssh
