## Ansible automation to setup turtlebot4 for SwarmBots

### Installation
1. Install Ansible as desired based on what is specified in [their official documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).
It can be with your OS packet manager, or even through PIP.
2. OpenSSH server is required for every single machine. Therefore make sure to have it,
or install it by running:
```bash
sudo apt install openssh-server
```
3. In the master machine, create for Ansible an ssh key to ensure connection with
the remotes. Give it the desired name, comment, and no passphrase. In this example
the name and comment will be "ansible".
```bash
ssh-keygen -t ed25519 -C "ansible"
```
4. Copy the new generated ssh-key into the remote machines.
```bash
ssh-copy-id -i `username@ip_address`
```
You will no longer require a password to access these remote machines.

### Usage

Update all the devices in the inventory list
```
ansible-playbook update.yaml -i ~/ansible_automation/production/hosts -K
```
**- K will prompt for the user password to continue** 

To setup the environment variables for each robot robots
```
ansible-playbook set_env_variables.yaml -i ~/ansible_automation/production/hosts -K
```

Startup launch files in all robots as systemd service
```
ansible-playbook ros2-deploy.yaml  -e "ansible_user=ipa remove=true" -i production/hosts.yaml -K -v
```
- remove=true for removing the systemd service
- remove=false for starting up systemd service

Startup launch files in all robots
```
ansible-playbook ros2-build-launch.yaml  -e "ansible_user=ipa remove=true" -i production/hosts.yaml -K -v
```

To reboot all the devices in the inventory list
```
ansible-playbook reboot.yaml -i ~/ansible_automation/production/hosts -K
```
