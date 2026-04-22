+++
date = '2026-04-22T16:41:54+08:00'
draft = false
title = 'Ansible Automation Platform Execution'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

*Disclaimer:* This is just my mental notes for Ansible Automation Platform. It is not intended to be a howto documentation. However, am hoping that will help you in some other ways or give you idea on AAP.

## Configure Credentials
*Automation Controller > Infrastructure > Credentials*
![Redhat Ansible Automation Platform](/ansible/rh-aap-execution10.png)


## Creating a Project using GIT
*Automation Controller > Projects > Create Project*

![Redhat Ansible Automation Platform](/ansible/rh-aap-execution1.png)
Git UrL: https://github.com/penoycentral/ex467-lab

## Creating Job Templates

*Automation Controller > Templates > Create Template > Create Job Template*

ansible.buitin.debug sample job

![Redhat Ansible Automation Platform](/ansible/rh-aap-execution2.png)

ansible.builtin.dnf sample job
![Redhat Ansible Automation Platform](/ansible/rh-aap-execution9.png)
Note: Enable Privilege Escalation

To test, click *Launch template*

![Redhat Ansible Automation Platform](/ansible/rh-aap-execution3.png)

## Creating Workflow Job Template
*Automation Controller > Templates > Create Template > Create Workflow Job Template*
![Redhat Ansible Automation Platform](/ansible/rh-aap-execution4.png)

In the Workflow Visualizer, click `Add step`
![Redhat Ansible Automation Platform](/ansible/rh-aap-execution5.png)

On the added `Step` click `Add step and link`
![Redhat Ansible Automation Platform](/ansible/rh-aap-execution6.png)

![Redhat Ansible Automation Platform](/ansible/rh-aap-execution7.png)

Launch Workflow Job

![Redhat Ansible Automation Platform](/ansible/rh-aap-execution8.png)
