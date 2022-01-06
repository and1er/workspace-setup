# Manual Cloud Instance Creation

Create an instance manually in your cloud provider console and set it up almost the same way as [local-manual](../../manual/README.md) setup, but with a few typical changes:

1. OpenSSH server is usuall set up, you need to add your public key to the instance via cloud provider console.
2. Add your own user to the host with sudo and SSH key access.
3. Remove `root` SSH access if it was enabled.

Ubuntu 21.10

```bash
sudo apt update
sudo apt upgrade
```

```bash
sudo apt install zsh
```

```bash
NEW_USERNAME=USERNAME
sudo useradd $NEW_USERNAME --create-home --shell /bin/zsh
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
ssh $NEW_USERNAME@host
```

And from it in `sudo vim /etc/ssh/sshd_config` set `PermitRootLogin no` and

```bash
sudo systemctl restart ssh
```

Then continue with [local-manual](../../manual/README.md).
