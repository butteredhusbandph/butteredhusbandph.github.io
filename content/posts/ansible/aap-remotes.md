+++
date = '2026-04-18T06:56:11+08:00'
draft = false
title = 'Ansible Automation Platform Remote Contents'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

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
