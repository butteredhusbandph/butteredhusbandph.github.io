+++
date = '2026-04-17T17:51:45+08:00'
draft = true
title = 'Certificate Authority Server using EasyRSA'
+++

One of the prerequisite of my Ansible Automation Platform 2.5/2.6 lab environment was to configure a local Certificate Authority.  
I've used my workstation running on LinuxMint to setup my CA server  

Installing EasyRSA  
```
sudo apt update
sudo apt install easy-rsa
mkdir ~/easy-rsa
ln - /usr/share/easy-rsa/* ~/easy-rsa/
```

Initialize  PKI  
```
cd ~/easy-rsa
./easyrsa init-pki
```
