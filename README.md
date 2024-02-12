# Lab Playground development server

***

<img src="media/banner_lab.png" align="left"/>
Playbook voor installatie en configuratie van een development lab server, als basis voor het ontwikkelen van een moderne infrastructuur. Automatische installatie en configuratie van o.a. Ansible, GitLab, Semaphore, Hashicorp Vault en Nexus Repository OSS.

***


Het playbook installeert en configureert de volgende rollen:

- **RedHat Cockpit**<br/>
  Browser-gebaseerde beheeromgeving voor Linux. Toegang via `http://<hostname>:9090`.<br/>
  Gebruikersnaam en wachtwoord worden gedefinieerd tijdens installatie via lab_username en lab_password variabelen.<br/>
  Zie ook role [cockpit](roles/cockpit/README.md)<br/>

- **Podman container infrastructure**<br/>
  Container infrastructuur. Kan worden beheerd via de Cockpit user interface.<br/>
  Zie ook role [podman](roles/podman/README.md)<br/>

- **Hashicorp Vault**<br/>
  Secret management. Geinstalleerd als container, benaderbaar via `http://<hostname>:8200`.<br/>
  Access token en unseal keys zijn opgeslagen in /data/vault/config folder.<br/>
  Zie ook role [vault](roles/vault/README.md)<br/>

- **Server-Config-Linux**<br/>
  Basis server configuratie rol met o.a configuratie automation account, configuratie tijdzone, base-server-config in Vault, etc.<br/>
  Zie ook role [server_config_linux](roles/server_config_linux/README.md)<br/>

- **MySQL**<br/>
  Installatie en configuratie van MySQL server. UNDER DEVELOPMENT.<br/>
  Zie ook role [mysql](roles/mysql/README.md)<br/>

- **Ansible Semaphore**<br/>
  Grafische interface voor Ansible. Geinstalleerd als container, benaderbaar via `http://<hostname>:3000`.<br/>
  Zie ook role [semaphore](roles/semaphore/README.md)<br/>

- **Gogs - Git service**<br/>
  Geinstalleerd als container, benaderbaar via `http://<hostname>:10880`.<br/>
  Zie ook role [gogs](roles/gogs/README.md)<br/>

- **Sonatype Nexus Repository OSS**<br/>
  Artifact repository. Geinstalleerd als container, benaderbaar via `http://<hostname>:8081`.<br/>
  User name is admin, initiele wachtwoord is opgeslagen in Vault.<br/>
  Zie ook role [nexus_repository](roles/nexus_repository/README.md)<br/>
<br/>

Overzicht [ontwerp](docs/DESIGN.md)<br/>

***

# Voorbereidingen
Een voorbeeld om de lab-playground te gebruiken is een infrastructuur met twee virtuele machines: een **Ansible Development server** en een **Lab Playground server**.<br/> 
Het playbook wordt gebruikt om vanaf de Ansible development server een lab server te installeren en configureren met een aantal podman containers als Vault, Nexus Repository, MySQL, Semaphore en Gogs.<br/>

## Virtuele Machines
**Ansible Development server**<br/>
De Ansible Development server wordt gebruikt om de code te kopieren (clone) vanuit git en het ansible playbook te starten. Geadviseerd wordt een Linux VM met min. 2 vCPU en 3GB intern geheugen. De diskruimte is 20GB.<br/>

Voorbereidingen Ansible Development server:<br/>
Installatie besturingssysteem:<br/> Het OS kan Ubuntu, RedHat Enterprise Linux, RockyLinux of een andere Linux variant zijn. RockyLinux heeft een lichte voorkeur omdat de codebase gelijk is aan RedHat zonder subscriptions.<br>
RockyLinux:<br/> 
Installation Destination :Automatic partitioning.<br/>
Software Selection: Minimal Install<br/>
KDump : Disabled<br/>
Root Password : Set root password, allow root SSH login with password<br/>
Network & Hostname : Set network IP address<br/>

Configuratie na OS installatie:<br/>
Installeer volgende packages op development server: `dnf install epel-release tar nano`.<br/>
epel-release: prerequisite voor ansible, tar: voor configuratie visual studio code remote ssh, nano: eenvoudige editor.<br/>
Installeer git en ansible: `dnf install ansible git`.<br/>
Configureer git: `git config --global user.name "<github username>` en `git config --global user.email "<github email>`.<br/>
Maak ssh certificaat aan via ssh-keygen: `ssh-keygen -t ed25519 -C "<your_email@example.com>"`<br/>
kopieer de publieke sleutel en kopieer naar github/gitlab settings.<br/>
Test git connectie: `ssh -T git@github.com`<br/>


Clone lab-playground repository: `git clone <adres>`..<br/>
Controleer het ip-adres van de lab server in het `inventory.yml` bestand en wijzig deze indien nodig.<br/> 
Controleer de variabelen in het `install.yml` bestand en wijzig deze indien nodig.<br/>

**Lab Playground server**<br/>
De Lab playground omgeving kan via dit playbook geinstalleerd worden op een Linux virtuele machine met 2 vCPU en 4GB geheugen. Geadviseerd wordt een diskruimte van 200Gb ivm mogelijke repository data.<br/>
Aanmaken ansible user:<br/>
```
useradd ansible
passwd ansible
usermod -aG wheel ansible

```


## Afhankelijkheden
Afhankelijkheden zijn benoemd in het requirements.yml bestand. Gebruik `ansible-galaxy install -r requirements.yml --force` voor installatie.<br/>



# Installatie
Installatie van het playbook kan via onderstaande commandline. De -K parameter vraagt om het BECOME wachtwoord.<br/>
```bash
ansible-playbook install.yml -i inventory.yml -K
```


# Configuratie


## Globale variabelen:
Onderstaande globale variabelen kunnen worden gebruikt:<br/>

- <kbd>uninstall</kbd>: true | false<br/>
  Bij installatie (install) van een role, wordt de role eerst ge-deinstalleerd (uninstall).<br/>
- <kbd>lab_hostname</kbd>: labserver.marcelvenema.com<br/>
- <kbd>lab_username</kbd>: admin<br/>
- <kbd>lab_usercomment</kbd>: "Admin user for Lab environment"<br/>
- <kbd>lab_password</kbd>: Password29!<br/>
- <kbd>lab_email</kbd>: marcel@marcelvenema.com<br/>

- <kbd>automation_username</kbd>: Gedefinieerd in install.yaml<br/>
- <kbd>automation_password</kbd>: not present, will be generated.<br/>
- <kbd>automation_email</kbd>: "ansible@marcelvenema.com"<br/>


# Licentie
MIT<br/>

# Auteur
Marcel Venema<br/>
