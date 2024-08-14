# ansible-playbook-security

This repository contains a collection of Ansible playbooks and roles to secure a fleet of machines organized as managers and workers.

## Table of contents

Roles:
- config_default_umask
- config_kernel_params
- firewall

Collections used:
- devsec.hardening: OS and SSH hardening

Playbooks:
- apply_hardening

## Usage

Ansible version requires at least Python 3.9

> Take great attention at the version of python and ansible used and follow the installation instructions below.

Please refer to the [Virtual environment documentation](https://virtualenv.pypa.io/en/latest/) for installation best
practices. If not using a virtual environment, please consider passing the
[widely recommended](https://packaging.python.org/tutorials/installing-packages/#installing-to-the-user-site) `'--user' flag`_ when invoking ``pip``.

    $ python3.9 -m venv ansible-venv
    $ source ansible-venv/bin/activate
    (ansible-venv) $ pip install -r requirements.txt

## Requirements

    (ansible-venv) $ ansible-galaxy collection install -r requirements.yml

## Running the playbooks

    ```bash
    (ansible-venv) $ ansible-playbook -i <INVENTORY_FILENAME> <PLAYBOOK_FILENAME>
    ```

## Inventory file format

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
        ansible_ssh_private_key_file: <MANAGER_SSH_KEY_PATH>
    workers:
      hosts:
        member0:
          ansible_host: <MEMBER0_IP>
        member1:
          ansible_host: <MEMBER1_IP>
      vars:
        ansible_user: <MEMBERS_USER>
        ansible_ssh_private_key_file: ~/.ssh/aws_slave.pem
```

## Test with molecule

See [instructions](./molecule/default/install.md)

## devsec.hardening collection

This repository uses the [devsec.hardening](https://galaxy.ansible.com/ui/repo/published/devsec/hardening/) collection to apply security configurations to the fleet. The collection is installed with the `requirements.yml` file.
2 roles are used from the collection:
- devsec.os-hardening: see [documentation](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/os_hardening)
- devsec.ssh-hardening: see [documentation](https://github.com/dev-sec/ansible-collection-hardening/tree/master/roles/ssh_hardening)


