# workspace-ws

My reproducible workstation setup.

I use Visual Studio Code to connect to the VM using Remote SSH feature to work in isolated VM.

[![GitHub Super-Linter](https://github.com/and1er/workspace-setup/workflows/Lint%20Code%20Base/badge.svg)](https://github.com/marketplace/actions/super-linter)

## WS initialization

### Linux WS case

1. Create a VM. See [VM Creation](./vm-creation/README.md).
2. Provision the VM. For now it's [Ansible](./provisioning/ansible/README.md), but maybe I will try Puppet/Chef/Salt in the future.

### macOS WS case

A case when working directly on a macOS device without any Linux VM, see [macos-setup/README.md](./macos-setup/README.md).

## Prepare the WS to work with GitHub

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
