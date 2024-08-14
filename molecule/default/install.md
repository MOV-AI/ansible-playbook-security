# Molecule installation

## Requirements

* Docker Engine
* 20GB of disk space (docker images are stored inside docker volumes)

## Install

Please refer to the [Virtual environment documentation](https://virtualenv.pypa.io/en/latest/) for installation best
practices. If not using a virtual environment, please consider passing the
[widely recommended](https://packaging.python.org/tutorials/installing-packages/#installing-to-the-user-site) `'--user' flag`_ when invoking ``pip``.

    $ python3.9 -m venv molecule-venv
    $ source molecule-venv/bin/activate
    (molecule-venv) $ pip install -r requirements.txt

Verify version:

    $ molecule --version
    molecule 6.0.2 using python 3.9
    ansible:2.15.3
    default:6.0.2 from molecule
    docker:2.1.0 from molecule_docker requiring collections: community.docker>=3.0.2 ansible.posix>=1.4.0
    ec2:0.4 from molecule_ec2
    libvirt:0.0.6 from molecule_libvirt


## Test

    molecule create
    molecule converge

On a VM on HEL:

    molecule converge -- -K -e '{"fleet_extra_hosts": ["172.22.0.106    registry.hel.mov.ai traefik"]}'
