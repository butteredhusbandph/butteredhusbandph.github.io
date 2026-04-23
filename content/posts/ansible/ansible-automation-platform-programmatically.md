+++
date = '2026-04-21T16:27:01+08:00'
draft = false
title = 'Ansible Automation Platform Programmatically'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

## API URL
```
https://gate.lab.local/api/controller/v2/
```

## Commands

```
curl -X GET https://gate.lab.local/api/controller/v2/ | jq
```

### Getting Job Templates
```
curl -X GET https://gate.lab.local/api/controller/v2/job_templates/ --user user1:<password>|jq
```


### Launching a Job 

```
curl -X POST https://gate.lab.local/api/controller/v2/job_templates/13/launch --user user1:<password>|jq

```

### Getting Workflow Job Templates
```
curl -X GET https://gate.lab.local/api/controller/v2/workflow_job_templates/ --user user1:<password> |jq
```

### Launching Workflow Job templates
```
curl -X POST https://gate.lab.local/api/controller/v2/workflow_job_templates/15/launch/ --user user1:<password> |jq
```
