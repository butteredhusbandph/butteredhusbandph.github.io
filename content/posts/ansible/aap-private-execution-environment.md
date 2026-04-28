+++
date = '2026-04-17T18:17:45+08:00'
draft = false
title = 'Ansible Automation Platform Execution Environment'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

## Creating custom collection
see [Creating Custom Collection](ansible-automation-platform-contents)  

## Adding Remote Registry
*Automation Hub > Remote Registries*
![Remote Registry](/ansible/rh-remote-registry1.png)
URL: https://registry.redhat.io/ansible-automation-platform-25/

Click `Sync Remote Registry` then `Index execution environments` 
![Remote Registry](/ansible/rh-remote-registry2.png)

Go to *Automation Hub > Execution Environments* it will show Execution Environments from registry.redhat.io

To further check, login to podmn
```console
[chris@mgmt ~]$ podman login gate.lab.local
Authenticating with existing credentials for gate.lab.local
Existing credentials are valid. Already logged in to gate.lab.local
[chris@mgmt ~]$ podman search gate.lab.local/
NAME                                                              DESCRIPTION
gate.lab.local/ansible-automation-platform-24/ee-minimal-rhel8
gate.lab.local/ansible-automation-platform-24/ee-minimal-rhel9
gate.lab.local/ansible-automation-platform-24/ee-supported-rhel8
gate.lab.local/ansible-automation-platform-24/ee-supported-rhel9
gate.lab.local/ansible-automation-platform-25/ee-minimal-rhel8
gate.lab.local/ansible-automation-platform-25/ee-minimal-rhel9
gate.lab.local/ansible-automation-platform-25/ee-supported-rhel8
gate.lab.local/ansible-automation-platform-25/ee-supported-rhel9
gate.lab.local/ansible-automation-platform-26/ee-minimal-rhel9
gate.lab.local/ansible-automation-platform-26/ee-supported-rhel9
gate.lab.local/ansible-automation-platform/ee-minimal-rhel8
gate.lab.local/ansible-automation-platform/ee-minimal-rhel9
gate.lab.local/ansible-builder-rhel8
gate.lab.local/de-minimal-rhel8
gate.lab.local/de-supported-rhel8
gate.lab.local/ee-minimal-rhel8
gate.lab.local/ee-supported-rhel8
gate.lab.local/rhoso-operators/ee-openstack-ansible-ee-rhel9
```

Sync individual Exeuction environment
![Use in Controller](/ansible/rh-aap-execution11.png)

## Uploading Content Collections to Private Automation Hub

In this sample, i want to add my custom collection `lab.webserver` to the execution environment  

~/ansible/ee/execution-environment.yml
```yaml
version: 3

dependencies:
  galaxy: requirements.txt

images:
  base_image:
    name: gate.lab.local/ansible-automation-platform-25/ee-minimal-rhel9:latest

additional_build_files:
  - src: files/ansible.cfg
    dest: configs
  - src: files/ca.crt
    dest: configs

additional_build_steps:
  prepend_base:
    - COPY _build/configs/ansible.cfg /etc/ansible/ansible.cfg
    - COPY _build/configs/ca.crt /etc/pki/ca-trust/source/anchors/
    - RUN update-ca-trust extract
```

requirements.txt
```
---
collections:
  - name: ansible.posix
  - name: community.general
  - name: lab.webserver
```

files/ansible.cfg
```
[galaxy]
server_list = validated, community

[galaxy_server.community]
url=https://gate.lab.local/api/galaxy/content/community/
token=<ansible hub token here>

[galaxy_server.validated]
url=https://gate.lab.local/api/galaxy/content/validated/
token=<ansible hub token here>
```

Login to AAP private automation hub and build the Execution Environment  
```console
[chris@mgmt ee]$ podman login gate.lab.local

[chris@mgmt ee]$ ansible-builder build -t gate.lab.local/lab/ee-minimal-rhel9:latest
Running command:
  podman build -f context/Containerfile -t gate.lab.local/lab/ee-minimal-rhel9:latest context

Complete! The build context can be found at: /home/chris/ansible/ee/context
[chris@mgmt ee]$
[chris@mgmt ee]$ podman images
REPOSITORY                                                      TAG         IMAGE ID      CREATED             SIZE
gate.lab.local/lab/ee-minimal-rhel9                             latest      49eade8d5f49  11 seconds ago      349 MB
<none>                                                          <none>      4a1c5fa1e598  About a minute ago  333 MB
<none>                                                          <none>      a32810498baf  25 hours ago        352 MB
<none>                                                          <none>      3202fc7b1023  25 hours ago        333 MB
gate.lab.local/ansible-automation-platform-25/ee-minimal-rhel9  latest      8db324dbaa70  5 weeks ago         309 MB

[chris@mgmt ee]$ podman push gate.lab.local/lab/ee-minimal-rhel9:latest 
Getting image source signatures
Copying blob 236a7d5e0ec4 done   | 


```

Use the newly created `execution enviroment` in the controller

*Automation Content > Execution Enviroments*
![Redhat Ansible Automation Platform](/ansible/rh-ee-controller.png)

Click `Use in Controller`

![Redhat Ansible Automation Platform](/ansible/rh-aap-execution12.png)

### Optional execution enviroment image check
```console
[chris@mgmt ee]$ podman create --name ansible-container -it gate.lab.local/lab/ee-minimal-rhel9:latest /bin/bash
2bf15e8caca14ec825d5efe76832e0727e178b866641171110792b991a4db8af
[chris@mgmt ee]$ podman ps -a
CONTAINER ID  IMAGE                                       COMMAND     CREATED        STATUS      PORTS       NAMES
2bf15e8caca1  gate.lab.local/lab/ee-minimal-rhel9:latest  /bin/bash   3 seconds ago  Created                 ansible-container
[chris@mgmt ee]$ podman start -ai ansible-container

bash-5.1$ ansible --version
ansible [core 2.16.17]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/runner/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.12/site-packages/ansible

bash-5.1$ ansible-galaxy collection list

# /usr/share/ansible/collections/ansible_collections
Collection        Version
----------------- -------
ansible.posix     2.1.0
community.general 12.6.0
lab.webserver     1.0.0

```
