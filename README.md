# linux-ws

My reproducible Linux workstation setup.

I use Visual Studio Code to connect to the VM using Remote SSH feature to work in isolated VM.

## VM creation using Vagrant

One way is to create VM using Vagrant. But it could be created any other way.

### Requirements

Tested on following version of Vagrant and VirtualBox

```bash
$ vagrant --version
Vagrant 2.2.16

$ VBoxManage --version
6.1.22r144080
```

### VM up

```bash
cd vagrant
# Create `authorized_keys` file with your public keys (format see in `authorized_keys.example`)
#   e.g. like this:
cat ~/.ssh/id_ed25519.pub > ./authorized_keys

vagrant up
```

VM will be available for direct SSH connection as

```bash
ssh vagrant@192.168.30.30
```

This is needed for VS Code connection.

## Provisioning

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
ssh-keygen -t ed25519
```

and add the public key `~/.ssh/id_ed25519.pub` to [GitHub.com SSH keys](https://github.com/settings/keys).

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

### For GUI usage

VS Code installation as a Snap package

```bash
sudo snap install --classic code
```

Then [Setting Sync](https://code.visualstudio.com/docs/editor/settings-sync).

## Ansible Installation

Ansible is installed to a python virtual environment (venv). In this case it's possible to have multiple Ansible versions in parallel and to get any version.

To create a venv with Ansible 3

```bash
python3 -m venv ~/ansible_venv/v3

source ~/ansible_venv/v3/bin/activate

(v3) $ pip install wheel 'ansible>=3.0,<4'

(v3) $ ansible --version
ansible 2.10.12

  ...

  python version = 3.8.10 (default, Jun  2 2021, 10:49:15) [GCC 9.4.0]

(v3) $ pip list
Package       Version
------------- -------
ansible       3.4.0  
ansible-base  2.10.12
cffi          1.14.6 
cryptography  3.4.7  
Jinja2        3.0.1  
MarkupSafe    2.0.1  
packaging     21.0   
pip           20.0.2 
pkg-resources 0.0.0  
pycparser     2.20   
pyparsing     2.4.7  
PyYAML        5.4.1  
setuptools    44.0.0 
wheel         0.37.0 

```

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
git clone https://github.com/and1er/ubuntu-ws.git
cd ubuntu-ws/
```

Activate a venv with Ansible

```bash
source ~/ansible_venv/v3/bin/activate
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

## Issues

### "Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)

To automate this: ["Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)](https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc)
