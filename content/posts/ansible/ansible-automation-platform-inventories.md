+++
date = '2026-04-22T05:27:28+08:00'
draft = false
title = 'Ansible Automation Platform Inventories and Credentials'
+++

This is just my notes on my lab AAP Inventories  

- Inventories
  - User Access
  - Team Access
  - Groups
    - webservers
      - Related Groups
      - Hosts
  - Hosts
  - Sources
    - Vmware Vcenter
    - Amazon EC2
    - Redhat Satellite 6
    - etc
  - Jobs
    - adhoc jobs runs
  - Job Templates


## Create Inventory
*Automation Controller > Inventories > Create Inventory*
![AAP Inventory](/ansible/rh-aap-inventory1.png)

## Add Groups to Inventory
![AAP Inventory](/ansible/rh-aap-inventory2.png)

## Add Host and associate to Host Group
*Automation Controller > Infrastructure > Hosts*
![AAP Inventory](/ansible/rh-aap-inventory3.png)
![AAP Inventory](/ansible/rh-aap-inventory4.png)


## Adding Inventory from Project 
Create `inventory.ini` in your GIT Project and sync your Project
```
[dev]
node1.lab.local

[webserver]
node2.lab.local
```

*Automation Controller > Infrastructure > Inventories*
Select `Sources` tab

![AAP Inventory](/ansible/rh-aap-inventory5.png)
**Source:** Sourced from a Project
**Project** your Project
**Inventory file** inventory.ini

Check `Host` and `Groups` under `Inventories`
