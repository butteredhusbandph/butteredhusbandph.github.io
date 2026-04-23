+++
date = '2026-04-17T18:17:45+08:00'
draft = false
title = 'Ansible Automation Platform Private Automation Hub'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++

*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own.

## Uploading Content Collections to Private Automation Hub  

~/ansible/ee/execution-environment.yml
```yaml
version: 3

dependencies:
  python_interpreter:
    package_system: "python311"
  ansible_core:
    package_pip: ansible-core
  galaxy:
    collections:
      - name: ansible.posix
  system:
    - libxml2-devel
    - libxslt-devel
    - systemd-devel
    - pkgconf-pkg-config
    - gcc
    - python3.11-devel
    - python3-dnf

build_arg_defaults:
  ANSIBLE_GALAXY_CLI_COLLECTION_OPTS: '-c'

options:
  package_manager_path: /usr/bin/microdnf

images:
  base_image:
   # name: quay.io/ansible/ansible-runner:latest
    name: gate.lab.local/ee-supported-rhel8:latest

additional_build_files:
  - src: files/ansible.cfg
    dest: configs

additional_build_steps:
  prepend_base:
    - COPY _build/configs/ansible.cfg /etc/ansible/ansible.cfg
```


Login to AAP private automation hub and build the Execution Environment  
```
[chris@mgmt ee]$ podman login gate.lab.local

[chris@mgmt ee]$ ansible-builder create
Complete! The build context can be found at: /home/chris/ansible/ee/context

[chris@mgmt ee]$ podman build -f context/Containerfile context/ -t gate.lab.local/lab/ee-lab-rhel8:latest

[chris@mgmt ee]$ podman images
REPOSITORY                             TAG         IMAGE ID      CREATED         SIZE
gate.lab.local/lab/ee-supported-rhel8  latest      b82d0e3de7fe  21 minutes ago  2.8 GB
<none>                                 <none>      5b705cf59ced  24 minutes ago  2.84 GB
<none>                                 <none>      f4088cb2e257  26 minutes ago  2.25 GB
gate.lab.local/ee-supported-rhel8      latest      db463e612f08  18 months ago   2.24 GB

[chris@mgmt ee]$ podman push gate.lab.local/lab/ee-supported-rhel8:latest
Getting image source signatures
Copying blob 4ee656bd17fa done   |
Copying blob 4b636d67cf3a done   |
Copying blob 6f7354abfe11 skipped: already exists

```
