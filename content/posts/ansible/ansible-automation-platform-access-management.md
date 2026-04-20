+++
date = '2026-04-20T05:36:28+08:00'
draft = true
title = 'Ansible Automation Platform Access Management'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++

[Access Management Documentation](https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.5/html-single/access_management_and_authentication/index)

[Managing Instance Groups](https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.4/html/automation_controller_user_guide/controller-instance-groups)

<br>
    
### Organizations
An organization is a logical collection of users, teams, and resources. It is the highest level object in the Ansible Automation Platform object hierarchy. 
  - **Instance Groups** Collections of nodes (VMs or instances) that can execute jobs.
    - **Purpose**: They allow administrators to assign job templates to specific groups of nodes for dedicated capacity or workload isolation.
    - 

<br>
    
### User Type

- Ansible Automation Platform Administrator
  Has full access to services and can manage other users
  - Automation Execution Administrator
  - Automation Decision Administrator
  - Automation Content Administrator
- Ansible Automation Platform Auditor
  Has view-only permissions on all objects
