# Manual VM Creation

If you create a VM manually, you could tune it as you wish, but it's necessary to set SSH server up, running and make firewall rules to allow incoming connection to SSH port.

## Ubuntu 21.10 host

Tested on freshly created Ubuntu 21.10 desktop.

Upgrade the distro to the actual state

```bash
sudo apt update && sudo apt upgrade
```

Install OpenSSH server

```bash
sudo apt install openssh-server
```

After that local VM is reachable via SSH with password authentication for your VM username (not `root`).

```bash
ssh username@ip_address
```

Add public SSH key for passwordless authentication

```bash
mkdir -p ~/.ssh
echo "ssh-XXX this is my public key" > ~/.ssh/authorized_keys
```
