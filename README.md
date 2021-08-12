ubuntu-ws
=============

My Ubuntu 20.04 virtual workstation settings.

VM Creation
-----------------

One way is to create VM using Vagrant. But it could be created any other way.

For Vagrant case:

```bash
cd vagrant
vagrant up
vagrant ssh
```

Provisioning
-----------------

Upgrade the distro to the actual state

```bash
sudo apt update && sudo apt upgrade
```

Minimal packages installation to perform further steps

```bash
sudo apt install \
    build-essential \
    dkms \
    git \
    python3 \
    python3-pip \
    python3-venv
```

Generate SSH-keys

```bash
ssh-keygen -t rsa
```

Git Setup

```bash
git config --global user.name "USERNAME"

git config --global user.email "EMAIL"
```

[Generate a GPG-key](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-gpg-key) for GitHub [commit signing](https://docs.github.com/en/github/authenticating-to-github/signing-commits)

```bash
gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
```

[Adding a new GPG key to your GitHub account](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-gpg-key-to-your-github-account)

```bash
gpg --armor --export <KEY-ID>
```

[Telling Git about your signing key](https://docs.github.com/en/github/authenticating-to-github/telling-git-about-your-signing-key)

```bash
git config --global user.signingkey <KEY-ID>
git config --global commit.gpgsign true
```

VS Code installation as a Snap package

```bash
sudo snap install --classic code
```

Then [Setting Sync](https://code.visualstudio.com/docs/editor/settings-sync).

Ansible Installation
------------------------

Ansible is installed to a python virtual environment (venv). In this case it's possible to have multiple Ansible versions in parallel and to get any version.

To create a venv with Ansible 3

```bash
python3 -m venv ~/ansible_venv_3

source ~/ansible_venv_3/bin/activate

(ansible_venv_3) $ pip install wheel 'ansible>=3.0,<4'

(ansible_venv_3) $ $ ansible --version
ansible 2.10.8

  ...

  python version = 3.8.5 (default, Jan 27 2021, 15:41:15) [GCC 9.3.0]

(ansible_venv_3) $ pip list
Package       Version
------------- -------
ansible       3.3.0  
ansible-base  2.10.8 
cffi          1.14.5 
cryptography  3.4.7  
Jinja2        2.11.3 
MarkupSafe    1.1.1  
packaging     20.9   
pip           20.0.2 
pkg-resources 0.0.0  
pycparser     2.20   
pyparsing     2.4.7  
PyYAML        5.4.1  
setuptools    44.0.0 
wheel         0.36.2 

```

If Ansible 2.9 is also needed:

```bash
python3 -m venv ~/ansible_venv_2.9

source ~/ansible_venv_2.9/bin/activate

(ansible_venv_2.9) $ pip install 'ansible<2.10'

(ansible_venv_2.9) $ ansible --version
ansible 2.9.18
  ...
  python version = 3.8.5 (default, Jan 27 2021, 15:41:15) [GCC 9.3.0]

```

Host Self Setup Using Ansible
-----------------------------------

Clone the repository

```bash
git clone https://github.com/and1er/ubuntu-ws.git
cd ubuntu-ws/
```

Activate a venv with Ansible

```bash
source ~/ansible_venv_3/bin/activate
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
