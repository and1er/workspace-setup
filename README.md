ubuntu-ws
=============

My Ubuntu 20.04 virtual workstation settings


Initial Setup
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

Ansible Installation
------------------------

```bash
python3 -m venv ~/ansible_venv

source ~/ansible_venv/bin/activate

(ansible_venv) $ pip install 'ansible<=2.10'

(ansible_venv) $ ansible --version
ansible 2.9.18
  ...
  python version = 3.8.5 (default, Jan 27 2021, 15:41:15) [GCC 9.3.0]

```


Host Self Setup Using Ansible
-----------------------------------

git clone git@github.com:and1er/ubuntu-ws.git
