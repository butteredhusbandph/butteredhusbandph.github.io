+++
date = '2026-04-20T05:36:28+08:00'
draft = false
title = 'Ansible Automation Platform Access Management'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++

*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

[Access Management Documentation](https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.5/html-single/access_management_and_authentication/index)

[Managing Instance Groups](https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.4/html/automation_controller_user_guide/controller-instance-groups)

<br>
    
## Organizations
An organization is a logical collection of users, teams, and resources. It is the highest level object in the Ansible Automation Platform object hierarchy. 
  - **Instance Groups** Collections of nodes (VMs or instances) that can execute jobs.
    - **Purpose**: They allow administrators to assign job templates to specific groups of nodes for dedicated capacity or workload isolation.
### Creating Organization
*Access Management > Organizations*
![Redhat Ansible Automation Platform](/ansible/rh-aap-org1.png)

<br>
    
## Teams
A team is a group of users that can be assigned permissions to resources.
### Creating Organization
*Access Management > Teams > Create Team*
    
## Users
### User Type
- Ansible Automation Platform Administrator
  Has full access to services and can manage other users
  - Automation Execution Administrator
  - Automation Decision Administrator
  - Automation Content Administrator
- Ansible Automation Platform Auditor
  Has view-only permissions on all objects
### Creating Users
*Access Management > Users > Create Users*
![Redhat Ansible Automation Platform](/ansible/rh-aap-org2.png)

## Roles
A role represent set of actions that a team or user may perform on a resource or set of resources
### Adding role
*Access Management > Roles > Create Role*  
Job Template Role
![Redhat Ansible Automation Platform](/ansible/rh-aap-org3.png)
Job Workflow Role
![Redhat Ansible Automation Platform](/ansible/rh-aap-org4.png)

## Assign Roles to a Team
*Access Management > Teams > Roles tab*
![Redhat Ansible Automation Platform](/ansible/rh-aap-org5.png)
