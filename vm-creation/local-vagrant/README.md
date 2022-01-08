# Local Vagrant

Create VM locally using Vagrant to avoid manual VM creation.
This approach is applicable for all host systems:

* Windows 10 (via PowerShell, not inside WSL);
* MacOS;
* Linux.

## Requirements

Tested on following version of Vagrant and VirtualBox

```bash
$ vagrant --version
Vagrant 2.2.16

$ VBoxManage --version
6.1.22r144080
```

## VM up

```bash
cd vm-creation/vagrant/
# Create `authorized_keys` file with your public keys (format see in `authorized_keys.example`)
#   e.g. like this:
cat ~/.ssh/id_ed25519.pub > ./authorized_keys

# The key will be copied into VM on provisioning step in Vagrantfile.
vagrant up
```

VM will be available for direct SSH connection as

```bash
# TODO: check connection settings.
ssh vagrant@192.168.30.30
```

In case of problems you could explore connection using `vagrant ssh-config` command

```bash
$ vagrant ssh-config
Host ws
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/USERNAME/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL
```
