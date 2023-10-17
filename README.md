# Lab Playground development server

***

<img src="media/logo_lab.png" align="left"/>
Playbook voor installatie en configuratie van een development lab server, als basis voor het ontwikkelen van een moderne infrastructuur op basis van Ansible, GitLab, Hashicorp Vault en Nexus Repository OSS.

***


Het playbook installeert de volgende rollen:

- **RedHat Cockpit**<br/>
  Browser-gebaseerde beheeromgeving voor Linux. Toegang via http://<hostname>:9090.<br/>
  Gebruikersnaam en wachtwoord zijn gedefinieerd in all.yml group_vars bestand als lab_username en lab_password.<br/>
  Zie ook Ansible role [cockpit](roles/cockpit/README.md)<br/>

- **Podman container infrastructure**<br/>
  Container infrastructuur. Kan worden beheerd via de Cockpit user interface.<br/>
  Zie ook Ansible role [podman](roles/podman/README.md)<br/>

- **Hashicorp Vault**<br/>
  Secret management. Geinstalleerd als container, benaderbaar via http://<hostname>:8200.<br/>
  Access token en unseal keys zijn opgeslagen in /data/vault/config folder.<br/>
  Zie ook Ansible role [vault](roles/vault/README.md)<br/>

- **Ansible Semaphore**<br/>
  Grafische interface voor Ansible. Geinstalleerd als container, benaderbaar via http://<hostname>:3000<br/>
  Zie ook Ansible role [podman.semaphore](roles/podman.semaphore/README.md)<br/>

- **Gogs - Git service**<br/>
  Geinstalleerd als container, benaderbaar via http://<hostname>:10880.<br/>
  Zie ook Ansible role [podman.gogs](roles/podman.gogs/README.md)<br/>

- **Sonatype Nexus Repository OSS**<br/>
  Artifact repository. Geinstalleerd als container, banderbaar via http://<hostname>:8081.<br/>
  User name is admin, initial password is opgeslagen in Vault.<br/>
  Zie ook Ansible role [nexus](roles/nexus/README.md)<br/>


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

`git config --global user.name "(github username)`<br/>
`git config --global user.email "(github email)`<br/>

Maak ssh certificaat aan via ssh-keygen: `ssh-keygen -t ed25519 -C "your_email@example.com"`<br/>
kopieer de publieke sleutel en kopieer naar github settings.<br/>
test git connectie: `ssh -T git@github.com`<br/>

vscode extensions:<br/>
- ansible<br/>
- remote-ssh<br/>
