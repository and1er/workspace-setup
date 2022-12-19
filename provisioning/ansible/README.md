# VM Provisioning with Ansible

## Requiements

VM has packages

* `git` to clone the repository;
* Python 3 with `pip3` and `venv` for further local Ansible installation for self-provisioning.

## Ubuntu Packages

Install the packages for further Ansible installation

```bash
sudo apt install \
    git \
    python3 \
    python3-pip \
    python3-venv
```

## Ansible v5 Installation

Ansible is installed to a python virtual environment (venv).
In this case it's possible to have multiple Ansible versions in parallel and to get any version.

Create a venv to install Ansible v5 (requires Python 3.8+) there

```bash
python3 -m venv ~/ansible_venv/v5
```

Activate the venv

```bash
source ~/ansible_venv/v5/bin/activate
```

Upgrade pip

```bash
(v5) $ python -m pip install -U pip
```

Install Ansible with venv activated (see command prompt `v5` prefix)

```bash
(v5) $ pip install wheel 'ansible>=5.0,<6'
```

Ansible version verification.

```bash
(v5) $ ansible --version
ansible [core 2.12.1]
  config file = None
  configured module search path = ['/home/username/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/username/ansible_venv/v5/lib/python3.9/site-packages/ansible
  ansible collection location = /home/username/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/username/ansible_venv/v5/bin/ansible
  python version = 3.9.7 (default, Sep 10 2021, 14:59:43) [GCC 11.2.0]
  jinja version = 3.0.3
  libyaml = True

(v5) $ pip list
Package       Version
------------- -------
ansible       5.1.0
ansible-core  2.12.1
cffi          1.15.0
cryptography  36.0.1
Jinja2        3.0.3
MarkupSafe    2.0.1
packaging     21.3
pip           21.3.1
pkg_resources 0.0.0
pycparser     2.21
pyparsing     3.0.6
PyYAML        6.0
resolvelib    0.5.4
setuptools    44.1.1
wheel         0.37.1
```

## Legacy Ansible 2.9

If Ansible 2.9 is also needed:

```bash
python3 -m venv ~/ansible_venv/v2.9

source ~/ansible_venv/v2.9/bin/activate

(v2.9) $ pip install 'ansible<2.10'

(v2.9) $ ansible --version
ansible 2.9.18
  ...
  python version = 3.8.5 (default, Jan 27 2021, 15:41:15) [GCC 9.3.0]

```

## Host Self Setup Using Ansible

Clone the repository

```bash
git clone https://github.com/and1er/workstation-setup.git
cd workstation-setup/provisioning/ansible/
```

Activate a venv with Ansible

```bash
source ~/ansible_venv/v5/bin/activate
```

Install Ansible role and collection requirements

```bash
ansible-galaxy role install -r requirements.yml
ansible-galaxy collection install -r requirements.yml
```

Run the playbook as `whoami` with `sudo`

```bash
ansible-playbook -i inventory local-ws-setup.yml -K
```
