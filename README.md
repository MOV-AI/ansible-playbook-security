# movai.security

This collection contains a set of roles and playbooks to secure a fleet of machines organized as managers and workers.

## Table of contents

Roles:
- config_default_umask
- config_kernel_params
- firewall

Playbooks:
- apply_hardening

Collections used:
- devsec.hardening: OS and SSH hardening

## Usage

Ansible version requires at least Python 3.9

> Take great attention at the version of python and ansible used and follow the installation instructions below.

### Installing this collection from the GIT repository

You can install the movai.security collection with the Ansible Galaxy CLI:

```sh
ansible-galaxy collection install git+git@github.com:MOV-AI/ansible-collection-security.git
```

You can also include it in a requirements.yml file and install it with `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
collections:
  - name: git@github.com:MOV-AI/ansible-collection-security.git
    type: git
    version: "1.0.0-0"
```

The python module dependencies are not installed by ansible-galaxy. They can be manually installed using pip:

```sh
pip install -r requirements.txt
```

### Using the playbooks

Apply the hardening playbook to secure your machines:

```sh
ansible-playbook -i inventory.yml movai.security.apply_hardening.yml
```

### Using the roles

You can use the roles in your own playbooks:

```yaml
- hosts: all
  roles:
    - role: movai.security.config_default_umask
    - role: movai.security.config_kernel_params
    - role: movai.security.firewall
```

### Inventory file format

Respect the format given in the example below:

```yaml
fleet:
  children:
    managers:
      hosts:
        manager:
          ansible_host: <MANAGER_IP>
      vars:
        ansible_user: <MANAGER_USER>
        ansible_ssh_private_key_file: <MANAGERS_SSH_KEY_PATH>
    workers:
      hosts:
        member0:
          ansible_host: <MEMBER0_IP>
        member1:
          ansible_host: <MEMBER1_IP>
      vars:
        ansible_user: <MEMBERS_USER>
        ansible_ssh_private_key_file: <WORKERS_SSH_KEY_PATH>
```

## Development

### Installing the collection from source

To install the collection from source locally, use the following command:

```sh
ansible-galaxy collection build
ansible-galaxy collection install movai-security-1.0.0.tar.gz
```

### Running the tests

To run the tests, use the following command:

```sh
python3.9 -m venv molecule-venv
source molecule-venv/bin/activate
pip install -r requirements.txt
molecule converge
```
See [detailed instructions](./molecule/default/install.md)

## devsec.hardening collection

This repository uses the [devsec.hardening](https://galaxy.ansible.com/ui/repo/published/devsec/hardening/) collection to apply security configurations to the fleet. The collection is installed with the `requirements.yml` file.
2 roles are used from the collection:
- devsec.os-hardening: see [documentation](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/os_hardening)
- devsec.ssh-hardening: see [documentation](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/ssh_hardening)
```