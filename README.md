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
An example of using the lab-playground is an infrastructure with three virtual machines: an **Ansible Development server**, a **Lab Playground server** and an **Lab Core Services server**.<br/>
- Ansible Development server: Minimal Linux server to develop and run Ansible playbooks. Mostly used with Visual Studio Code. <br/>
- Lab Playground server: Minimal Linux server to test and run Ansible playbooks.<br/>
- Lab Core Services server: Minnimal Linux server to host Vault and Nexus Repository containers.<br/>


## Virtual Machines

**Lab Playground server**<br/>
The Lab Playground server will be the server to test and run the Ansible playbooks on. A Linux VM with at least 2 vCPUs and 3GB of memory is recommended. Recommended disk space is 20GB.<br/>
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


**Lab Core Services server**
The Lab Core Services server will host the Vault container for secret management and Nexus Repository container to store artifacts. A Linux VM with at least 2 vCPUs and 4GB of memory is recommended. Due to the artifact storage, a disk space of 200GB is recommended.<br/>
- Operating system installation: See instructions for Lab Playgrouns server.<br/>
- Operating system configuration: none, configuration will be done with playbook.<br/>


**Ansible Development server**<br/>
The Ansible Development server is used to clone and edit the code from Git and start the Ansible playbook. A Linux VM with at least 2 vCPUs and 3GB of memory is recommended. The disk space should be 20GB.<br/>
- Operating system installation: See instructions for Lab Playground server.<br/>
- Configuration after OS installation:<br/>
Logon with user ansible and install the following packages on the development server: `sudo dnf install epel-release tar nano`.<br/>
epel-release: prerequisite for Ansible, tar: for configuring Visual Studio Code remote SSH, nano: simple editor.<br/>
Install Git and Ansible: `sudo dnf install ansible git`.<br/>

Create SSH certificate via ssh-keygen: `ssh-keygen -t ed25519 -C "<your_email@example.com>"`<br/>
Copy the SSH key to the Lab Playground Server and Lab Core Services Server: `ssh-copy-id ansible@<ip address Lab Playground Server>` and `ssh-copy-id ansible@<ip address Lab Core Services Server>`.<br/> 

Configure Git: `git config --global user.name "<GitHub username>"` and `git config --global user.email "<GitHub email>"`.<br/>
Copy the public key from the Ansible Development Server and add it to GitHub/GitLab settings: `nano ~/.ssh/id_ed25519.pub` and copy the key, paste it to Github website User Profile - Settings - SSH and GPG keys. <br/>
Test Git connection: `ssh -T git@github.com`<br/>
It is now a good idea to create a snapshot of all the virtual machines so you can revert to the initial state if something goes wrong or you want to start over or try a new project.<br/>  

Clone lab-playground repository: `git clone git@github.com:marcelvenema/lab-playground.git`.<br/>
Check the IP address of the servers in the `inventory.yml` file and change it if necessary.<br/>


# Dependencies
Dependencies are listed in the requirements.yml file. Use `ansible-galaxy install -r requirements.yml --force` for installation.<br/>


# Installation
Installation of the playbook can be done via the following command line. The -K parameter prompts for the BECOME password.<br/>
```bash
ansible-playbook install_lab_core_services.yml -K
```


# Configuration
Following variables can be configured in the 'install_lab_core_services' playbook:<br/>

<kbd>uninstall</kbd>, true/false, default false. If true, roles will be uninstalled before installation.<br/>
<kbd>automation_username</kbd>, default 'ansible'. username.<br/> 
<kbd>automation_password</kbd>, if not provided, password will be generated and stored in Vault.<br/>
<kbd>automation_email</kbd>, default 'ansible@me.local'. Used during Nexus Repository OSS creation.<br/>
<kbd>vm_name</kbd>, hostname of VM.<br/>
<kbd>vault_repository_url</kbd>, default 'docker.io/hashicorp/vault'. 
<kbd>nexus_repository_url</kbd>, default 'docker.io/sonatype/nexus3'.
<kbd>nexus_repository_vault_id</kbd>, unique id to identify Nexus Repository instance in Vault.<br/>



# License
MIT<br/>


# Author
Marcel Venema<br/>
