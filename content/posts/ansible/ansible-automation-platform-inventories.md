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
