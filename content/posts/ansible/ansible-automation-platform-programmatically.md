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

### Launching Job with extra vars
```console
curl -X POST -H "Content-Type: application/json" -d '{"extra_vars": {"vm_os":"RHEL", "vm_ram":2, "vm_disk":3}}' https://gate.lab.local/api/controller/v2/job_templates/14/launch/ --user user1:password|jq 
```

## Launching Job with extra vars using Ansible
```yaml
- name: Trigger AAP Job Template with Extra Vars
  hosts: localhost
  gather_facts: false
  vars:
    aap_host: "https://gate.lab.local"
    job_template_id: 14
  tasks:
    - name: Launch job template
      ansible.builtin.uri:
        url: "{{ aap_host }}/api/controller/v2/job_templates/{{ job_template_id }}/launch/"
        user: admin
        password: <password>
        method: POST
        force_basic_auth: yes
        body_format: json
        body:
          extra_vars:
            vm_os: "RHEL"
            vm_ram: 3
            vm_disk: 3
        status_code: 201
        validate_certs: false
```

## API scriplet
```console
#!/bin/bash

echo **************************************
echo **********   Launch Job   ************
echo **************************************

curl -X POST -k -s https://gate.lab.local/api/controller/v2/job_templates/19/launch/ --user <user>:<password>/| jq .

```

```
#!/bin/bash

echo "**************************"
echo "***** Launch Workflow ****"
echo "**************************"

curl -X POST -k -s https://gate.lab.local/api/controller/v2/workflow_job_templates/13/launch/ --user <user>:<password> | jq

```
