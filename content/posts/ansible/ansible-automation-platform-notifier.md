+++
date = '2026-04-29T05:52:30+08:00'
draft = false
title = 'Ansible Automation Platform Notifier'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']

+++
*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

## Lab Webhook setup  
docker-compose.yml  
```yaml
services:
  webhook:
    image: almir/webhook
    container_name: webhook
    command: /usr/local/bin/webhook -hooks /etc/webhook/hooks.json -verbose -hotreload
    volumes:
      - ./hooks.json:/etc/webhook/hooks.json
      - ./display_logs.sh:/usr/local/bin/display_logs.sh
    ports:
      - 9000:9000
```

*hooks.json*
```
[
  {
    "id": "show-logs",
    "execute-command": "/usr/local/bin/display_logs.sh",
    "command-working-directory": "/tmp",
    "response-message": "Logs retrieved successfully!"
  }
]
```

*display_logs.sh*
```
#!/bin/sh
/bin/echo "[$(date)] Webhook triggered: ansible playbook triggered" > /proc/1/fd/1 2>&1
```

```console
curl http://192.168.50.217:9000/hooks/show-logs
```

```console
╭─chris@mint ~/Labs/docker/webhook ‹main●›
╰─$ docker logs -f webhook                                                                                                                    127 ↵
[Tue Apr 28 21:49:36 UTC 2026] Webhook triggered: ansible playbook triggered
[Tue Apr 28 21:49:37 UTC 2026] Webhook triggered: ansible playbook triggered
[Tue Apr 28 21:50:04 UTC 2026] Webhook triggered: ansible playbook triggered
```
  
  
## Ansible Automation Platform Webhook Configuration  
 
**Target URL:** http://192.168.50.217:9000/hooks/show-logs  
**HTTP Method:** POST
![Ansible Automation Platform Notifier](/ansible/rh-aap-notifier1.png)

Click the `Bell` icon to test  
![Ansible Automation Platform Notifier](/ansible/rh-aap-notifier2.png)

Add `Notifier` to `Job Template` or `Job Workflow`
![Ansible Automation Platform Notifier](/ansible/rh-aap-notifier3.png)
