# Manual VM creation

If you create a VM manually, you could tune it as you wish, but it's necessary to set SSH server up, running and make firewall rules to allow incoming connection to SSH port.

## Ubuntu

```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl enable sshd
sudo vi /etc/ssh/sshd_config
sudo systemctl restart ssh
sudo ufw allow 22
echo "public key" > ~/.ssh/authorized_keys
```
