+++
date = '2026-04-23T15:50:04+08:00'
draft = false
title = 'Ansible Automation Platform Ex467'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++


# EX467 Exam Objectives  

## Manage automation content
  - [Upload a collection to automation hub](/ansible/ansible-automation-contents/#upload-a-collection-to-automation-hub)
  - [Upload an execution environment to automation hub](/ansible/aap-private-execution-environment/#uploading-content-collections-to-private-automation-hub)  

## Manage access to Ansible Automation Platform
  - Create automation controller [users](/ansible/ansible-automation-platform-access-management/#users) and [teams](/ansible/ansible-automation-platform-access-management/#teams)
  - [Associate users with teams associations](/ansible/ansible-automation-platform-access-management/#associate-users-in-teams)
  - [Configure organization roles](/ansible/ansible-automation-platform-access-management/#roles)
  - Configure user types  

## Manage inventories and credentials
  - Create host groups
  - Assign systems to host groups
  - Configure access to inventories
  - Configure inventory variables
  - Create and configure machine credentials to access hosts  
[Lab Referrence](../ansible-automation-platform-inventories)

## Manage controller projects
  - Create projects
  - Create job templates
  - Control user access to job templates
  - Launch jobs  
[Lab Referrence](../ansible-automation-platform-execution)

## Manage controller workflows
  - Create workflow templates
  - Launch workflow jobs
  - Configure workflow jobs for automatic approval  
[Lab Referrence](../ansible-automation-platform-execution)

## Manage jobs
  - [Create a job template survey](/ansible/ansible-automation-platform-execution/#creating-job-template-survey)
  - Schedule jobs and manage [notifications](ansible/ansible-automation-platform-notifier/)  
[Lab Referrence](../ansible-automation-platform-execution)

## Interact with Ansible Automation Platform programmatically
  - Understand how to use an API script to obtain required parameters for launching jobs
  - [Write an API scriptlet to launch a job](/ansible/ansible-automation-platform-programmatically/)
  - Use Ansible Content Collections
  - [Configure a Git webhook](ansible/ansible-automation-platform-git-webhook/)  

## Maintain Ansible Automation Platform
  - Back up an instance of automation controller
  - Back up an instance of Ansible Private Hub
  - Troubleshooting

## [Scale an Ansible Automation Platform deployment](/ansible/ansible-automation-platform-mesh/)
  - Install and configure automation mesh
  - Extend automation mesh
  - Create and manage instance groups
  - Assign default instance groups to controller inventories or templates
  - Run controller job templates in a specific instance group
  - Run a job on segregated network
