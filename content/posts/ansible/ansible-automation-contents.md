+++
date = '2026-04-18T06:56:11+08:00'
draft = false
title = 'Ansible Automation Platform Contents'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

## Adding Custom Collection
Create your custom collection
```console
ansible-galaxy collection init lab.webserver
cd lab/webserver/roles
ansible-galaxy role init apache
```
roles/apache/task/main.yml
```yaml
---
---
# tasks file for apache
- ansible.builtin.dnf:
    name:
      - httpd
      - firewalld
    state: present
- ansible.builtin.service:
    name: "{{ item }}"
    state: started
    enabled: yes
  loop:
    - httpd
    - firewalld
- ansible.posix.firewalld:
    service: http
    state: enabled
    permanent: true
    immediate: true
```
lab/webserver/galaxy.yml
```yaml
dependencies:
  community.general: ">=12.6.0"
  ansible.posix: ">=2.1.0"
```

lab/webserver/meta/runtime.yml
```yaml
requires_ansible: '>=2.9.10'
```

Build the collection
```console
[chris@mgmt webserver]$ ansible-galaxy collection build
Created collection for lab.webserver at /home/chris/ansible/cc/lab/webserver/lab-webserver-1.0.0.tar.gz
[chris@mgmt webserver]$
```

Upload custom collection to AAP
*Automation Content > Collections > Upload Collection*
![AAP Custom Collection](/ansible/rh-custom-collection1.png)

Click `Approve and sign collection(thumb up icon)`
![AAP Custom Collection](/ansible/rh-custom-collection2.png)

![AAP Custom Collection](/ansible/rh-custom-collection3.png)

*Automation Hub > Namespaces > lab*
![AAP Custom Collection](/ansible/rh-custom-collection4.png)

## Redhat Repository
In this sample, we will configure Redhat `validated` content from Automation Hub  

First create your token. Login to [console.redhat.com](https://console.redhat.com/ansible/automation-hub/token) and click `Load token`

![Redhat Console Token](/rhub-console-token.png)

Go to `Server URL` and copy `validated URL` and `SSO URL`

![Server URL](/rhub-validated-url.png)

In your AAP Automation Content portal click `Remotes > Create Remote`

**Name:** rh-validated  
**URL:**  `validated URL` from console.redhat.com Automation hub  
**Token:**  `token` from console.redhat.com Automation hub  
**SSO URL:** `SSO URL` from console.redhat.com Automation hub  
  
  
Under Requirements file, i just want to test remote sync and dont want to sync all collections:
```
collections:
  - infra.aap_configuration
```
![AAP Validated](/rh-validated-aap.png)


Go to `Repositories > Create repository`

**Name:** rh-validated-remote  
**Remote:** rh-validated  

![AAP validated remote](/rh-validated-app2.png)

Then `Sync repository`

Check your Collectios under `Automation Content > Collections`

![AAP Collections](/rh-ac-collections.png)

## Ansible Galaxy Remote Repository

*Automation Content > Remotes*
![AAP Ansible Galaxy Remote Repository](/ansible/rh-aap-repo1.png)
