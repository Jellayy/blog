---
title: Helpful Linux Commands
date: 2021-03-09
categories: [Helpful Stuff]
tags: [HOMELAB]
media_subpath: /assets/post-assets/2021-03-09-helpful-linux-commands
image:
  path: vm-commands.jpg
---

## Setting Static IPs

Good common practice when running services on VMs is to have everything running on static IP addresses. This can be done through your DHCP server or in your VM itself. The easiest way to do this on Ubuntu Server is through netplan. Use whatever addressing scheme you have setup in your network.

```sh
sudo nano /etc/netplan/01-netcfg.yaml
```
```yml
network:
 version: 2
 renderer: networkd
 ethernets:
  ens5:
   dhcp4: no
   addresses: [192.168.1.6/24]
   gateway4: 192.168.1.1
   nameservers:
    addresses: [192.168.1.1]
```
```sh
sudo netplan apply
```

## Mounting SMB Shares

Often in a VM you will be utilizing external or shared storage on your network. In Ubuntu Server, we can utilize the fstab to mount these on boot.

1. Define Share Mount

    ```sh
sudo apt install cifs-utils
sudo nano /etc/fstab
    ```
    ```
//truenas.jellayy.com/Data /Data cifs credentials=/etc/share-credentials,uid=1000,gid=1000 0 0
    ```

1. Create Credentials File:

    ```sh
sudo nano /etc/share-credentials
    ```
    ```
username=user
password=password
    ```

1. Secure Credentials File:

    ```sh
sudo chown root: /etc/share-credentials
sudo chmod 600 /etc/share-credentials
    ```

1. Mount share:

    ```sh
sudo mount -a
    ```