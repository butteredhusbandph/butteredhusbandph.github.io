+++
date = '2026-04-20T15:26:26+08:00'
draft = false
title = 'Ansible Automation Platform Mesh'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++

## Why Automation Mesh
- Challenges on automation across different platforms and location
- Ensuring automation executes consistently while managing centrally
- Automate remote areas with limited connectivity

## Monitooring Autmation Mesh
```console
awx-manage list_instances
```

```console
[root@control ~]# receptorctl --socket /var/run/awx-receptor/receptor.sock status
Node ID: control.lab.local
Version: 1.4.8
System CPU Count: 2
System Memory MiB: 3655

Connection          Cost
execution.lab.local 1

Known Node          Known Connections
control.lab.local   execution.lab.local: 1
execution.lab.local control.lab.local: 1

Route               Via
execution.lab.local execution.lab.local

Node                Service   Type       Last Seen             Tags
control.lab.local   control   StreamTLS  2026-05-09 15:17:35   {'type': 'Control Service'}
execution.lab.local control   StreamTLS  2026-05-09 15:17:13   {'type': 'Control Service'}

Node                Secure Work Types
control.lab.local   local, kubernetes-runtime-auth, kubernetes-incluster-auth
execution.lab.local ansible-runner
[root@control ~]# receptorctl --socket /var/run/awx-receptor/receptor.sock ping
ERROR: Missing parameter: node
[root@control ~]# receptorctl --socket /var/run/awx-receptor/receptor.sock ping execution.lab.local
Reply from execution.lab.local in 689.084µs
Reply from execution.lab.local in 1.526419ms
Reply from execution.lab.local in 2.391137ms
Reply from execution.lab.local in 4.454391ms
```



Further reads:
https://www.redhat.com/en/blog/whats-new-in-ansible-automation-platform-2.1-automation-mesh
