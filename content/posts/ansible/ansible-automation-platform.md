+++
date = '2026-04-19T21:44:48+08:00'
draft = false
title = 'Ansible Automation Platform Installation in Virtualbox'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++

![Redhat Ansible Automation Platform](/ansible/rh-app.png)

I’ve put together my notes on deploying Ansible Automation Platform (AAP) 2.5(can work on v2.6 too) on VirtualBox. This setup runs entirely on a single host using VirtualBox.

## Lab Prerequisites

- [Squid proxy](../../local-lab-squid)
- [Certificate Authority and client certificates](easy-rsa)
- Register your VMs to RHN

<br>

## Host Computer Spec:
**CPU:**  Intel(R) Core(TM) i7-8665U CPU @ 1.90GHz   
**RAM:**  32 Gb  
**DISK:** 250 Gb  
**OS:** Redhat Enterprise Linux 9.x  
**Network:** Virtualbox Host-Only 192.168.56.0/24

## DNS server
For DNS resolution inside the lab, I’m using my existing Pi‑hole instance as the authoritative local DNS. Under
Pi-hole → Settings → Local DNS Settings, I added:
```
hub.lab.local      192.168.56.112
gate.lab.local     192.168.56.113
control.lab.local  192.168.56.111
```
  
## Virtual Machines Overview
### Ansible Automation Hub 
`hub.lab.local` 
```
vCPU: 2
RAM: 8Gb  
Disk: 40Gb
```

### Ansible Automation Gateway  
`gate.lab.local`
```
vCPU: 2  
RAM: 8Gb  
Disk: 20Gb  
```

### Ansible Automation  Controller and Database server
`control.lab.local`  
```
vCPU: 2  
RAM: 8Gb  
Disk: 20Gb  
```

  
### Downloading AAP 2.5
Create a Red Hat Developer account and download the AAP 2.5 bundle:

 - https://developers.redhat.com/

 - https://developers.redhat.com/content-gateway/file/ansible/Ansible_Automation_Platform_2.5/ansible-automation-platform-setup-bundle-2.5-1-x86_64.tar.gz

Ensure that SSH key‑based authentication and sudo access is already configured between your host and all VMs.  

### Host Ansible Config
`inventory`
```
hub
gate
control
```
  
`ansible.cfg`
```
[defaults]
inventory=./inventory
remote_user=chris
host_key_checking=False
remote_tmp=~/.ansible/tmp

[privilege_escalation]
become=True
become_method=sudo
become_user=root
```
 <br> 
Test your host and VMs connection
```
ansible all -m ping
```

I've created playbook.yml to further configure my VMs

```
playbook.yml here
```

 <br>
Extract the bundle:  
```
tar xvzf ansible-automation-platform-setup-bundle-2.5-1-x86_64.tar.gz
cd ansible-automation-platform-setup-bundle-2.5-1-x86_64
```

## Certificate Authority Setup
[Configure your local Certificate Authority](easy-rsa) so AAP components can trust each other. 

## Inventory Configuration
Edit your inventory file to define the Hub, Controller, and Database hosts:

```
[automationcontroller]
control.lab.local

[automationgateway]
gate.lab.local

[automationhub]
hub.lab.local

[database]
control.lab.local

[all:vars]
admin_password='secret'
redis_mode=standalone
pg_host='control.lab.local'
pg_port=5432
pg_database='awx'
pg_username='awx'
pg_password='******'
pg_sslmode='disable'  # set to 'verify-full' for client-side enforced SSL

# Do not pre-load collections
#automationhub_seed_collections=false

registry_url="hub.lab.local"
registry_username='admin'
registry_password='******'
ee_from_hub_only=True

# Automation Hub Configuration
#
automationhub_admin_password='secret'
automationhub_pg_host='control.lab.local'
automationhub_pg_port='5432'
automationhub_pg_database='automationhub'
automationhub_pg_username='automationhub'
automationhub_pg_password='secret'
automationhub_pg_sslmode='******'

automationgateway_admin_password=secret
automationgateway_pg_host=control.lab.local
automationgateway_pg_port=5432
automationgateway_pg_database=gateway
automationgateway_pg_username=gateway
automationgateway_pg_password='******'
```

## Running the Installer
Execute the setup script:

```
./setup.sh
```

## Configure SSL certificates

Once installation completes, copy ssl key and crt

*hub.lab.local*
```
cp /tmp/hub.lab.local.crt /etc/pulp/certs/pulp_webserver.crt
cp /tmp/hub.lab.local.key /etc/pulp/certs/pulp_webserver.key
reboot
```

*gate.lab.local*
```
cp /tmp/gate.lab.local.crt /etc/ansible-automation-platform/gateway/gateway.cert
cp /tmp/gate.lab.local.key /etc/ansible-automation-platform/gateway/gateway.key
reboot
```



Access the AAP web interface via `gate.lab.local` and register your deployment using your Red Hat Developer account.

![Redhat Ansible Automation Platform](/ansible/rh-app-ui.png)

Referrence:

https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.5/html/rpm_installation/appendix-inventory-files-vars

https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.6/html/rpm_installation/appendix-inventory-files-vars
