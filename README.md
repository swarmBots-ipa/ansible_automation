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
ansible-playbook update.yml -i ~/ansible_automation/production/hosts -K
```
- K will ask for the user password to continue as sudo 

To reboot all the devices in the inventory list
```
ansible-playbook reboot.yml -i ~/ansible_automation/production/hosts -K
```
To setup the brinup launch files in all robots
```
ansible-playbook reboot.yml -i ~/ansible_automation/production/hosts -K
```