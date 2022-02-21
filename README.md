# Minio Storage Server Setup

## Motivation

If you are like us, you probably have used AWS S3 or Digital Ocean as storage solution. They are cheap and easy, right? In most cases it is true. However, as we offer node snapshot services (up to hundreds of GBs) for the Polkadot and Cosmos ecosystem, we have quickly realized that it is costly to pay for file transfer.

After paying hundreds of dollars each month to AWS and Digital Ocean, we have decided to bite the bullet and implement our own file storage solution. This repo is the Ansible playbook to install Minio.

## Summary

You run one playbook and set up a Minio file server. Boom!

```bash
ansible-playbook -i inventory minio.yml -e "target=MINIO_TARGET"
```

But before you rush with this easy setup, you probably want to read on so you understand the structure of this Ansible program and all the features it offers.

## Some Preparations

First of all, some preparation is in order.

Make sure that you have a production inventory file with your confidential server info. You will start by copying the sample inventory file (included in the repo). The sample file gives you a good idea on how to define the inventory.

```bash
cp inventory.sample inventory
```

Needless to say, you need to update the dummy values in the inventory file. For each Kusama/Polkadot node, you need to update:

1. Server IP: Your server public IP
2. minio_user: Your root Minio user for console access
3. minio_password: Your root Minio password for console access
4. minio_url: Your url to access Minio console (You will need to set up DNS for this)
5. storage_url: Your url to access Minio files (You will need to set up DNS for this)

You will also need to update:

1. ansible_user: The sample file assumes `ansible`, but you might have another username. Make sure that the user has `sudo` privilege.
2. ansible_port: The sample file assumes `22`. But if you are like me, you will have a different ssh port other than `22` to avoid port sniffing.
3. ansible_ssh_private_key_file: The sample file assumes `~/.ssh/id_rsa`, but you might have a different key location.

It is beyond the scope of this guide to help you create a sudo user, alternate ssh port, create a private key, install Ansible on your machine, etc. You can do a quick online search and find the answers. In my experience, Digital Ocean have some quality guides on these topics. Stack Overflow can help you trouble-shoot if you are stuck.

## Main Playbook to Set Up Minio Server

The main setup playbook is:

```bash
ansible-playbook -i inventory minio.yml -e "target=MINIO_TARGET"
```
