+++
date = '2026-04-20T15:26:26+08:00'
draft = true
title = 'Ansible Automation Platform Mesh'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++

## Why Automation Mesh
- Challenges on automation across different platforms and location
- Ensuring automation executes consistently while managing centrally
- Automate remote areas with limited connectivity

```
[automationcontroller]
control.lab.local

[automationcontroller:vars]
node_type=control
peers=execution_nodes

[execution_nodes]
enode1.lab.local peers=enode2.lab.local
enode2.lab.local

```


Further reads:
https://www.redhat.com/en/blog/whats-new-in-ansible-automation-platform-2.1-automation-mesh
