# Ansible playbook for configuring a linux laptop

This is an ansible playbook that manages the configuration of a linux laptop. It
manages things like dotfiles (.bash\_profile etc), alternatives, apt repos and
packages, and custom key mappings.

## Initial setup

The playbook should be run on the laptop being configured as it uses a local
connection rather than SSH. On a fresh Linux install you will need to install
the git client and ansible, and then clone this repo:

```bash
sudo apt update
sudo apt install git ansible
mkdir ~/git/personal && cd ~/git/personal
git clone https://github.com/stephengrier/ansible-laptop.git
cd ansible-laptop
```

## Running the playbook

Some tasks require elevated privileges and use `become: true`. You therefore
need to use the `--ask-become-pass` flag when runnng ansible.

```bash
ansible-playbook laptop.yml -K
```

However, if you are using a fingerprint reader for authentication with sudo this
won't work because ansible can't interact with fingerprint readers. In this case
you will need to call sudo first so that the credentials are cached when ansible
is run:

```bash
sudo true
Place your right index finger on the fingerprint reader
...
ansible-playbook laptop.yml
```
