# linux-ws

My reproducible Linux workstation setup.

I use Visual Studio Code to connect to the VM using Remote SSH feature to work in isolated VM.

## Workflow

### 1. Create a VM

* Goals are:
  1. VM is available for SSH connections (via terminal and VSCode Remote-SSH).
  2. VM has packages
     * `git` to clone the repo;
     * Python 3 with `pip3` and `venv` for further local Ansible installation for self-provisioning.
* VM could be created with any way (I'm gonna try and note different approaches)
  1. a local VM (VirtualBox, Hyper-V, VMWare etc);
     * [manual](./vm-creation/manual/README.md);
     * [Vagrant](./vm-creation/vagrant/README.md);
  2. a cloud instance (AWS, GCP, Digital Ocean etc);
  3. [Windows WSL](./vm-creation/wsl/README.md) (in this case use Windows-WSL integration instead of SSH).
* As OS for now only **Ubuntu 20.04** was taken. But in the future I would try another Linux distributions, maybe
  * Fedora;
  * Manjaro.

### 2. Provision the VM

For now it's [Ansible](./provisioning/ansible/README.md), but maybe I will try Puppet/Chef/Salt in the future.

### 3. Prepare WS to work with GitHub

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

## Issues

### "Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)

To automate this: ["Visual Studio Code is unable to watch for file changes in this large workspace" (error ENOSPC)](https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc)

### Searh `TODO:` in the project

To find small local issues.
