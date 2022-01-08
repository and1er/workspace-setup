# Virtual Machine Creation

## Requirements

1. VM is available for SSH connections (via terminal and VSCode Remote-SSH).
2. VM has packages
    * `git` to clone the repo;
    * Python 3 with `pip3` and `venv` for further local Ansible installation for self-provisioning.

## OS

As OS for now only **Ubuntu 20.04** was taken. But in the future I would try another Linux distributions, maybe

* Fedora;
* Manjaro.

## VM Providers

VM could be created with any way (I'm gonna try and note different approaches).

1. a local VM (VirtualBox, Hyper-V, VMWare etc);
    * [local-manual](./local-manual/README.md);
    * [Vagrant](./local-vagrant/README.md);
2. a cloud instance (AWS, GCP, Digital Ocean etc);
    * [cloud manual](./cloud-manual/README.md);
    * (TODO someday with instance created by Terraform).
3. [Windows WSL](./local-wsl/README.md) (in this case use Windows-WSL integration instead of SSH).
