+++
date = '2026-04-24T17:37:38+08:00'
draft = false
title = 'Ansible Automation Platform Troubleshooting'
+++


https://access.redhat.com/solutions/7127221
https://docs.redhat.com/en/documentation/red_hat_ansible_automation_platform/2.5/html-single/troubleshooting_ansible_automation_platform/index

## Automation Gateway
```console
Usage: automation-gateway-service start|stop|restart|status|enable|disable
```

## Automation Controller
```console
Usage: automation-controller-service start|stop|restart|status|enable|disable
```

## Automation Hub  
Pulp settings  
```
/etc/pulp/settings.py
```

Restarting Automation hub
```console
systemctl stop pulpcore.service pulpcore-api.service pulpcore-content.service pulpcore-worker@1.service pulpcore-worker@2.service nginx.service redis.service

systemctl start pulpcore.service pulpcore-api.service pulpcore-content.service pulpcore-worker@1.service pulpcore-worker@2.service nginx.service redis.service
```
