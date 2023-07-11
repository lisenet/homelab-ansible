# homelab-ansible

Ansible infrastructure for my homelab.

[![version](https://img.shields.io/github/manifest-json/v/lisenet/homelab-ansible?label=Ansible)](https://github.com/lisenet/homelab-ansible/blob/master/VERSIONS.md)
[![license](https://img.shields.io/github/license/lisenet/homelab-ansible)](https://github.com/lisenet/homelab-ansible/blob/master/LICENSE)
[![last commit](https://img.shields.io/github/last-commit/lisenet/homelab-ansible)](https://github.com/lisenet/homelab-ansible/commits/master)
[![commit activity](https://img.shields.io/github/commit-activity/y/lisenet/homelab-ansible)](https://github.com/lisenet/homelab-ansible/commits/master)
[![issues](https://img.shields.io/github/issues/lisenet/homelab-ansible)](https://github.com/lisenet/homelab-ansible/issues)
[![pull_requests_closed](https://img.shields.io/github/issues-pr-closed/lisenet/homelab-ansible)](https://github.com/lisenet/homelab-ansible/pulls)

## Install Ansible

Install `python3` packages. Choose `apt` for Debiad based systems, or `yum` for Red Hat based systems.

```bash
sudo apt install -y python3 python3-pip
sudo yum install -y python3 python3-pip
```

Use `pip` to install the Ansible package of your choice for the current user:

```bash
python3 -m pip install --upgrade --user pip
TMPDIR="${HOME}/tmp" python3 -m pip install --user ansible==4.10
```

Verify:

```bash
python3 -m pip show ansible-core ansible
Name: ansible-core
Version: 2.11.12
Summary: Radically simple IT automation
Home-page: https://ansible.com/
Author: Ansible, Inc.
Author-email: info@ansible.com
License: GPLv3+
Requires: cryptography, jinja2, packaging, PyYAML, resolvelib
Required-by: ansible
---
Name: ansible
Version: 4.10.0
Summary: Radically simple IT automation
Home-page: https://ansible.com/
Author: Ansible, Inc.
Author-email: info@ansible.com
License: GPLv3+
Requires: ansible-core
Required-by:
```

The following collections are required to be installed:

```bash
ansible-galaxy collection install ansible.posix -p ./collections
ansible-galaxy collection install community.general -p ./collections
```

## Passwordless SSH Authentication

Servers built with Kickstart/Packer have root SSH keys pre-configured. If that is not the case, then see below.

Configure passwordless root SSH authentication from the device where Ansible is installed (e.g. your laptop):

```bash
ssh-copy-id -f -i ./roles/hl.users/files/id_rsa_root.pub root@10.11.1.XX
```

## Set Ansible User Password

Create a file `vault.key` to store your Ansible Vault secret (see `ansible.cfg` for vault_password_file). Use Ansible Vault to create an encrypted file `./roles/hl.users/defaults/secure.yml` to store your user password:

```bash
ansible-vault create ./roles/hl.users/defaults/secure.yml
```

The variable for user password is `user_password`.

## Configuration with Ansible

### Configure PXE Hosts

```bash
ansible-playbook ./playbooks/configure-pxe-hosts.yml --extra-vars "download_pxe_boot_media=true download_packer_media=true"
```

### Configure KVM Hosts

```bash
ansible-playbook ./playbooks/configure-kvm-hosts.yml
```

### Configure Admin Hosts

```bash
ansible-playbook ./playbooks/configure-admin-hosts.yml
```

### Configure Kubernetes Hosts

Prepare Kubernetes hosts for cluster deployment:

```bash
ansible-playbook ./playbooks/configure-k8s-hosts.yml
```

Configure Kubernetes cluster for the first time:

```bash
ansible-playbook ./playbooks/configure-k8s-cluster.yml
```

### Configure OpenVAS Hosts

```bash
ansible-playbook ./playbooks/configure-openvas-hosts.yml
```

### Optional: Configure Hosts File

This is optional because of the local DNS server:

```bash
ansible-playbook ./playbooks/configure-hostsfile.yml
```

### Optional: Configure New Relic Agent

```bash
ansible-playbook ./playbooks/configure-newrelic-hosts.yml
```

## Ansible-configured PXE Boot Server

Note that user password for PXE boot Kickstart files is set to `packer`.

![Homelab PXE Boot Menu](./images/homelab-pxe-boot-menu.png)


## Homelab Network Diagram

![Homelab Network Diagram](./images/kubernetes-homelab-diagram.png)
