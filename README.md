# Lab Playground Development server

***

<img src="media/banner_lab.png" align="left"/>
Ansible playbook to install and configure a development lab playground server. It will automatically install Ansible, Git, Hashicorp Vault, and Nexus Repository OSS. This serves as a foundation for an infrastructure-as-code playground environment.
Use this playground to learn and play with Ansible playbooks and roles. Examine the framework and ultimately develop new Ansible playbooks and roles to become an Ansible master.

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

# Preparations
An example of using the lab-playground is an infrastructure with three virtual machines: an **Ansible Development server**, a **Lab Playground server** and a **Test server**.<br/>
- Ansible Development server: Minimal Linux server to develop and run Ansible playbooks. Mostly used with Visual Studio Code. <br/>
- Lab Playground server: Minnimal Linux server to host LabServer Playground with Vault and Nexus Repository.<br/>
- Test server: Minimal Linux server to test Ansible playbooks.<br/>

## Virtual Machines

**Lab Playground server**<br/>
The Lab Playground server will host the Vault container for secret management and Nexus Repository container to store artifacts. A Linux VM with at least 2 vCPUs and 4GB of memory is recommended. Due to the artifact storage, a disk space of 200GB is recommended.<br/>
- Operating system installation:<br/> The OS can be Ubuntu, RedHat Enterprise Linux, RockyLinux, or another Linux variant. RockyLinux is slightly preferred because the codebase is the same as RedHat Enterprise Linux but without subscriptions.<br>
RockyLinux:<br/>
Create the virtual machine on the hypervisor and boot the RockyLinux Minimal ISO.<br/>
Select desired language for RockyLinux.<br/>
Installation Destination: Automatic partitioning.<br/>
User Creation: Set username to ansible, set password, check 'Make this user administrator'.<br/>
Root Password: Set root password, allow root SSH login with password.<br/>
Network & Hostname: Set network IP address.<br/>
Start installation.<br/>
- Operating system configuration: none, configuration will be done with playbook.<br/>


**Ansible Test server**
The Ansible test server will host the Vault container for secret management and Nexus Repository container to store artifacts. A Linux VM with at least 2 vCPUs and 4GB of memory is recommended. Due to the artifact storage, a disk space of 200GB is recommended.<br/>
- Operating system installation: See instructions for Ansible Development Server.<br/>
- Operating system configuration: none, configuration will be done with playbook.<br/>




**Ansible Development server**<br/>
The Ansible Development server is used to clone and edit the code from Git and start the Ansible playbook. A Linux VM with at least 2 vCPUs and 3GB of memory is recommended. The disk space should be 20GB.<br/>
- Operating system installation: See instructions for Ansible Development Server.<br/>



- Configuration after OS installation:<br/>
Logon with user ansible and install the following packages on the development server: `sudo dnf install epel-release tar nano`.<br/>
epel-release: prerequisite for Ansible, tar: for configuring Visual Studio Code remote SSH, nano: simple editor.<br/>
Install Git and Ansible: `sudo dnf install ansible git`.<br/>
Configure Git: `git config --global user.name "<GitHub username>"` and `git config --global user.email "<GitHub email>"`.<br/>
Create SSH certificate via ssh-keygen: `ssh-keygen -t ed25519 -C "<your_email@example.com>"`<br/>
Copy the public key and add it to GitHub/GitLab settings.<br/>
Test Git connection: `ssh -T git@github.com`<br/>






## Afhankelijkheden
Afhankelijkheden zijn benoemd in het requirements.yml bestand. Gebruik `ansible-galaxy install -r requirements.yml --force` voor installatie.<br/>



# Installatie
Installatie van het playbook kan via onderstaande commandline. De -K parameter vraagt om het BECOME wachtwoord.<br/>
```bash
ansible-playbook install.yml -i inventory.yml -K
```
Clone lab-playground repository: `git clone <address>`.<br/>
Check the IP address of the lab server in the `inventory.yml` file and change it if necessary.<br/>
Check the variables in the `install.yml` file and change them if necessary.<br/>

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
