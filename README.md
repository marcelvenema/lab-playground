# Lab Playground Development server

***

<img src="media/banner_lab.png" align="left"/>
Ansible playbook to install and configure a development lab playground server. It will automatically install Ansible, Git, Hashicorp Vault, and Nexus Repository OSS. This serves as a foundation for an infrastructure-as-code playground environment.
Use this playground to learn and play with Ansible playbooks and roles. Examine the framework and ultimately develop new Ansible roles to become an Ansible master.

***

The play installs and configures the following applications using Ansible roles:

- **RedHat Cockpit**<br/>
  Browser-based management interface for Linux. Access via `http://<hostname>:9090`.<br/>
  Username and password are defined during installation via variables 'lab_username' and 'lab_password'.<br/>
  See also role [cockpit](roles/cockpit/README.md)<br/>

- **Podman container infrastructure**<br/>
  Container infrastructure. Can be managed via the Cockpit user interface.<br/>
  See also role [podman](roles/podman/README.md)<br/>

- **Hashicorp Vault**<br/>
  Secret management. Installed as a container, accessible via `http://<hostname>:8200`.<br/>
  Access token and unseal keys are stored in /data/vault/config folder.<br/>
  See also role [vault](roles/vault/README.md)<br/>

- **Server-Config-Linux**<br/>
  Basic server configuration role including configuration of the automation account, timezone configuration, base-server-config in Vault, etc.<br/>
  See also role [server_config_linux](roles/server_config_linux/README.md)<br/>

- **Sonatype Nexus Repository OSS**<br/>
  Artifact repository. Installed as a container, accessible via `http://<hostname>:8081`.<br/>
  Username is admin, initial password is stored in Vault.<br/>
  See also role [nexus_repository](roles/nexus_repository/README.md)<br/>
<br/>

Overview [design](docs/DESIGN.md)<br/>

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
