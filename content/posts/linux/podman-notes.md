+++
date = '2026-04-25T21:32:11+08:00'
draft = false
title = 'Podman Notes'
tags = ['linux', 'podman', 'container']
+++


Create the container  
```console
podman create --name my-container -it <image> /bin/bash
```

Verify if exists  
```console
podman ps -a
```

Starting the container  
```console
podman start -ai my-container
```
