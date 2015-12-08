# Archivematica playbook

The provided Ansible playbook can be used to install Archivematica on:

  - an ubuntu virtual machine in a host with vagrant/VirtualBox
  - an ubuntu host directly


## Install Archivematica on a VM running on the local host (using Vagrant)

### Requirements

- Vagrant 1.7 or newer
- Ansible 1.9 or newer

### How to use

0. Install ansible, VirtualBox, and vagrant on the host PC, and clone this repositoty. For instructions please refer to:
  - Ansible: http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-apt-ubuntu
  - Vagrant: https://docs.vagrantup.com/v2/installation/index.html
  - VirtualBox: https://help.ubuntu.com/community/VirtualBox/Installation

1. Download the Ansible roles:
  ```
  $ ansible-galaxy install -f -r requirements.yml
  ```

2. Create the virtual machine and provision it:
  ```
  $ vagrant up
  ```

3. To ssh to the VM, run:
  ```
  $ vagrant ssh
  ```

4. If you want to forward your SSH agent too, run:
  ```
  $ vagrant ssh -- -A
  ```

5. To (re-)provision the VM, run:
    * Using vagrant:
        ```
        $ vagrant provision
        ```
    * Using ansible commands directly (this allows you to pass ansible-specific parameters,
      such as tags and the verbose flag; remember to use extra-vars to pass the variables in the Vagrantfile ):
        ```
        $ ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory singlenode.yml \
           -u vagrant \
           --private-key .vagrant/machines/am-local/virtualbox/private_key \
           --extra-vars="archivematica_src_dir=/vagrant/src archivematica_src_environment_type=development" \
           --tags="amsrc-pipeline-instcode" \
           -v
        ```

For more archivematica development information, see: https://wiki.archivematica.org/Getting_started



## Install Archivematica directly on the local host


### Requirements

- An ubuntu host (Trusty 14.04, it may run on other versions but not tested)
- A user account with sudo

### How to use
