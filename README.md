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

Clone the repository

```bash
git clone https://github.com/and1er/ubuntu-ws.git
cd ubuntu-ws/
```

Run the playbook as `whoami` with `sudo`

```bash
ansible-playbook -i inventory local-ws-setup.yml -K
```
