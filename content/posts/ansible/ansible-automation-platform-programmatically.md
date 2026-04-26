+++
date = '2026-04-21T16:27:01+08:00'
draft = false
title = 'Ansible Automation Platform Programmatically'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

## API URL
```
https://gate.lab.local/api/controller/v2/
```

## Commands

```console
curl -X GET https://gate.lab.local/api/controller/v2/ | jq
```

### Getting Job Templates
```console
curl -X GET https://gate.lab.local/api/controller/v2/job_templates/ --user user1:<password>|jq
```


### Launching a Job 

```console
curl -X POST https://gate.lab.local/api/controller/v2/job_templates/13/launch --user user1:<password>|jq

```

### Getting Workflow Job Templates
```console
curl -X GET https://gate.lab.local/api/controller/v2/workflow_job_templates/ --user user1:<password> |jq
```

### Launching Workflow Job templates
```console
curl -X POST https://gate.lab.local/api/controller/v2/workflow_job_templates/15/launch/ --user user1:<password> |jq
```
