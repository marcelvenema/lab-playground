# Lab Playground Development server

***

<img src="media/banner_lab.png" align="left"/>
An Ansible playbook to install and configure a development lab playground server. It will automatically install Ansible, Git, HashiCorp Vault, and Nexus Repository OSS. This serves as a foundation for an infrastructure-as-code playground environment. Use this playground to learn and experiment with Ansible playbooks and roles. Examine the framework and ultimately develop new Ansible playbooks and roles to become proficient in Ansible.

***

The play installs and configures the following applications using Ansible roles:

- **RedHat Cockpit**<br>
  Browser-based management interface for Linux. Access via `http://<hostname>:9090`.<br>
  Username and password are defined during installation via variables 'lab_username' and 'lab_password'.<br>
  See also role [cockpit](roles/cockpit/README.md)<br>

- **Podman container infrastructure**<br>
  Container infrastructure. Can be managed via the Cockpit user interface.<br>
  See also role [podman](roles/podman/README.md)<br>

- **Hashicorp Vault**<br>
  Secret management. Installed as a container, accessible via `http://<hostname>:8200`.<br>
  Access token and unseal keys are stored in /data/vault/config folder.<br>
  See also role [vault](roles/vault/README.md)<br>

- **Server-Config-Linux**<br>
  Basic server configuration role including configuration of the automation account, timezone configuration, base-server-config in Vault, etc.<br>
  See also role [server-config](roles/server-config/README.md)<br>

- **Sonatype Nexus Repository OSS**<br>
  Artifact repository. Installed as a container, accessible via `http://<hostname>:8081`.<br>
  Username is admin, initial password is stored in Vault.<br>
  See also role [nexus-repository](roles/nexus-repository/README.md)<br>
<br>

Overview [design](docs/DESIGN.md)<br>

***

# Preparations
An example of using the lab-playground is an infrastructure with three virtual machines: an **Ansible Development server**, a **Lab Playground server** and an **Lab Core Services server**.<br>
- Ansible Development server: Minimal Linux server to develop and run Ansible playbooks. Mostly used with Visual Studio Code. <br>
- Lab Playground server: Minimal Linux server to test and run Ansible playbooks.<br>
- Lab Core Services server: Minnimal Linux server to host Vault and Nexus Repository containers.<br>


## Virtual Machines

**Lab Playground server**<br>
The Lab Playground server will be the server to test and run the Ansible playbooks on. A Linux VM with at least 2 vCPUs and 3GB of memory is recommended. Recommended disk space is 20GB.<br>
- Operating system installation:<br> The OS can be Ubuntu, RedHat Enterprise Linux, RockyLinux, or another Linux variant. RockyLinux is slightly preferred because the codebase is the same as RedHat Enterprise Linux but without subscriptions.<br>
RockyLinux:<br>
Create the virtual machine on the hypervisor and boot the RockyLinux Minimal ISO.<br>
Select desired language for RockyLinux.<br>
Installation Destination: Automatic partitioning.<br>
User Creation: Set username to ansible, set password, check 'Make this user administrator'.<br>
Root Password: Set root password, allow root SSH login with password.<br>
Network & Hostname: Set network IP address.<br>
Start installation.<br>
- Operating system configuration: 
Create ansible user with `useradd ansible`, set password `passwd ansible` and grant ansible user access to sudo with `usermod -aG wheel ansible`.<br>
Update OS with `sudo dnf upgrade --all`.<br>


**Lab Core Services server**
The Lab Core Services server will host the Vault container for secret management and Nexus Repository container to store artifacts. A Linux VM with at least 2 vCPUs and 4GB of memory is recommended. Due to the artifact storage, a disk space of 200GB is recommended.<br>
- Operating system installation: See instructions for Lab Playground server.<br>
- Operating system configuration: See instructions for Lab Playground server.<br>


**Ansible Development server**<br>
The Ansible Development server is used to clone and edit the code from Git and start the Ansible playbook. A Linux VM with at least 2 vCPUs and 3GB of memory is recommended. The disk space should be 20GB.<br>
- Operating system installation: See instructions for Lab Playground server.<br>
- Configuration after OS installation:<br>
See instructions for Lab Playground server.<br>
Logon with user ansible and install the following packages on the development server: `sudo dnf install epel-release tar nano git python3.12 python3.12-pip`.<br>
tar: for configuring Visual Studio Code remote SSH; nano: simple editor; git: version control system; epel-release, python3.12 and python3.12-pip: prerequisites for Ansible.<br>
Install Ansible: `python3.12 -m pip install ansible`.<br>

Create SSH certificate via ssh-keygen: `ssh-keygen -t ed25519 -C "<your_email@example.com>"`<br>
Copy the SSH key to the Lab Playground Server and Lab Core Services Server: `ssh-copy-id ansible@<ip address Lab Playground Server>` and `ssh-copy-id ansible@<ip address Lab Core Services Server>`.<br> 

Configure Git: `git config --global user.name "<GitHub username>"` and `git config --global user.email "<GitHub email>"`.<br>
Test Git connection: `ssh -T git@github.com`<br>
It is now a good idea to create a snapshot of all the virtual machines so you can revert to the initial state if something goes wrong or you want to start over or try a new project.<br>  

Clone lab-playground repository: `git clone git@github.com:marcelvenema/lab-playground.git`.<br>
Check the IP address of the servers in the `hosts.ini` file and change it if necessary.<br>


# Dependencies
Dependencies are listed in the requirements.yml file. Use `ansible-galaxy install -r requirements.yml --force` for installation.<br>


# Installation
Installation of the playbook can be done via the following command line. The -K parameter prompts for the BECOME password.<br>
```bash
ansible-playbook install_lab_core_services.yml -K
```


# Configuration
Following variables can be configured in the `install_lab_core_services` playbook:

- **uninstall**: `true`/`false`, default is `false`. If `true`, roles will be uninstalled before installation.
- **automation_username**: Default is `ansible`. The username for the automation account.
- **automation_password**: If not provided, a password will be generated and stored in Vault.
- **automation_email**: Default is `ansible@me.local`. Used during Nexus Repository OSS creation.
- **vm_name**: Hostname of the VM.
- **vault_repository_url**: Default is `docker.io/hashicorp/vault`.
- **nexus_repository_url**: Default is `docker.io/sonatype/nexus3`.
- **nexus_repository_vault_id**: Unique ID to identify the Nexus Repository instance in Vault.

# License
MIT<br>


# Author
Marcel Venema<br>
