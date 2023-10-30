# Lab Playground development server

***

<img src="media/logo_lab.png" align="left"/>
Playbook voor installatie en configuratie van een development lab server, als basis voor het ontwikkelen van een moderne infrastructuur. Automatische installatie en configuratie van o.a. Ansible, GitLab, Semaphore, Hashicorp Vault en Nexus Repository OSS.

***


Het playbook installeert de volgende rollen:

- **RedHat Cockpit**<br/>
  Browser-gebaseerde beheeromgeving voor Linux. Toegang via `http://<hostname>:9090`.<br/>
  Gebruikersnaam en wachtwoord zijn gedefinieerd in all.yml group_vars bestand als lab_username en lab_password.<br/>
  Zie ook Ansible role [cockpit](roles/cockpit/README.md)<br/>

- **Podman container infrastructure**<br/>
  Container infrastructuur. Kan worden beheerd via de Cockpit user interface.<br/>
  Zie ook Ansible role [podman](roles/podman/README.md)<br/>

- **Hashicorp Vault**<br/>
  Secret management. Geinstalleerd als container, benaderbaar via `http://<hostname>:8200`.<br/>
  Access token en unseal keys zijn opgeslagen in /data/vault/config folder.<br/>
  Zie ook Ansible role [vault](roles/vault/README.md)<br/>

- **Base-server-config**<br/>
  Basis server configuratie rol met o.a configuratie automation account, configuratie tijdzone, base-server-config in Vault, etc.<br/>
  Zie ook Ansible role [base-server-config](roles/base-server-config/README.md)<br/>

- **MySQL**<br/>
  Installatie en configuratie van MySQL server. UNDER DEVELOPMENT.<br/>
  Zie ook Ansible role [mysql](roles/mysql/README.md)<br/>

- **Ansible Semaphore**<br/>
  Grafische interface voor Ansible. Geinstalleerd als container, benaderbaar via `http://<hostname>:3000`.<br/>
  Zie ook Ansible role [semaphore](roles/semaphore/README.md)<br/>

- **Gogs - Git service**<br/>
  Geinstalleerd als container, benaderbaar via `http://<hostname>:10880`.<br/>
  Zie ook Ansible role [gogs](roles/gogs/README.md)<br/>

- **Sonatype Nexus Repository OSS**<br/>
  Artifact repository. Geinstalleerd als container, benaderbaar via `http://<hostname>:8081`.<br/>
  User name is admin, initial password is opgeslagen in Vault.<br/>
  Zie ook Ansible role [nexus_repository](roles/nexus_repository/README.md)<br/>


***

# Voorbereidingen

# Virtuele Machines

**Ansible Development server**<br/>
De Ansible Development server wordt gebruikt om de code te kopieren (clone) vanuit git en het ansible playbook te starten. Geadviseerd wordt een Linux VM met min. 2 vCPU en 3GB intern geheugen. De diskruimte is 20GB.<br/>

**Lab Playground server**<br/>
De Lab playground omgeving kan via dit playbook geinstalleerd worden op een Linux virtuele machine met 2 vCPU en 4GB geheugen. Geadviseerd wordt een diskruimte van 200Gb ivm mogelijke repository data.<br/>

Development server:<br/>
Installeer volgende packages op development server: `dnf install epel-release tar nano`.<br/>
epel-release: prerequisite voor ansible, tar: voor configuratie visual studio code remote ssh, nano: eenvoudige editor.<br/>
Installeer git en ansible: `dnf install ansible git`.<br/>
configureer git: `git config --global user.name "(github username)` en `git config --global user.email "(github email)`.<br/>
Maak ssh certificaat aan via ssh-keygen: `ssh-keygen -t ed25519 -C "your_email@example.com"`<br/>
kopieer de publieke sleutel en kopieer naar github settings.<br/>
test git connectie: `ssh -T git@github.com`<br/>
<br/>

Clone lab-playground repository: `git clone <adres>`..<br/>
Installeer Ansible Galaxy collections via `sh requirements.sh`.<br/>
Controleer de variabelen in het `inventory/lab/group_vars/all.yml` bestand en wijzig deze indien nodig.<br/>
Controleer de ip-adressen in het `inventory/lab/hosts.ini` bestand en wijzig deze indien nodig.<br/> 


Lab server:<br/>

Installeer volgende packages op development server: `dnf install epel-release tar nano`.<br/>
Installeer git en ansible op development server: `dnf install ansible git`.<br/>
Clone lab-playground repository naar development server.<br/>





# Installatie

```bash
ansible-playbook install.yml -i inventory/lab/hosts.ini -K
```

# Configuratie


## Globale variabelen:

- uninstall: true | false<br/>
  Bij installatie (install) van een role, wordt de role eerst ge-deinstalleerd (uninstall).<br/>


- lab_hostname: labserver.marcelvenema.com<br/>
- lab_username: admin<br/>
- lab_usercomment: "Admin user for Lab environment"<br/>
- lab_password: Password29!<br/>
- lab_email: marcel@marcelvenema.com<br/>

- automation_username: Gedefinieerd in install.yaml<br/>
- automation_password: not present, will be generated.<br/>
- automation_email: "ansible@marcelvenema.com"<br/>

