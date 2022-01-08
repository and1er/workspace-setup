# Manual Cloud Instance Creation

Create an instance manually in your cloud provider console and set it up almost the same way as [local-manual](../local-manual/README.md) setup, but with a few typical changes:

1. OpenSSH server is usuall set up, you need to add your public key to the instance via cloud provider console.
2. Add your own user to the host with sudo and SSH key access.
3. Remove `root` SSH access if it was enabled.

## Ubuntu 21.10 host

```bash
sudo apt update && sudo apt upgrade
```

Choose new user name as variable

```bash
NEW_USERNAME=USERNAME
```

And create this user

```bash
sudo useradd $NEW_USERNAME --create-home --shell /bin/bash
sudo adduser $NEW_USERNAME sudo
sudo passwd $NEW_USERNAME
su - $NEW_USERNAME
```

```bash
mkdir -p ~/.ssh
echo "Public SSH key for incoming connections" > ~/.ssh/authorized_keys
exit
exit
```

Check that new user can connect

```bash
ssh USERNAME@host
```

And from it in

```bash
sudo vim /etc/ssh/sshd_config
```

adjust following parameters

```bash
# Check firewall settings before changing the port!
Port NN

PermitRootLogin no
```

Then restart the daemon

```bash
sudo systemctl restart ssh
```
