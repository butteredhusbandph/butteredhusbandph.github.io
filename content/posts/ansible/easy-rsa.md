+++
date = '2026-04-17T17:51:45+08:00'
draft = false
title = 'Certificate Authority Server using EasyRSA'
tags = ['ansibleautomationplatform', 'redhat', 'linux']
+++

One of the prerequisite of my Ansible Automation Platform 2.5/2.6 lab environment was to configure a `local` Certificate Authority.  
I've used my workstation running on LinuxMint to configure my Certificate Authority.   

## Installing EasyRSA  
```console
sudo apt update
sudo apt install easy-rsa
mkdir ~/easy-rsa
ln - /usr/share/easy-rsa/* ~/easy-rsa/
cd ~/easy-rsa
./easyrsa init-pki
./easyrsa build-ca
```

## Copy CA certificate to the clients  
RHEL:  
```console
sudo cp /tmp/ca.crt /etc/pki/ca-trust/source/anchors/
sudo update-ca-trust
```

## Creating Signing and Certificate Requests
To be done on the clients  
```console
openssl genrsa -out $(hostname).key
openssl req -new -key $(hostname).key -out $(hostname).req

scp $(hostname).req <user>@ca_server_ip:/tmp

```

## Signing a CSR
To be done on the CA server
```console
cd ~/easy-rsa
./easyrsa import-req /tmp/<client-hostname>.req <client-hostname>
./easyrsa sign-req server <client-hostname>

scp pki/issued/<client-hostname>.crt user@client_ip:/tmp
```



Referrence:
https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-a-certificate-authority-on-ubuntu-22-04
