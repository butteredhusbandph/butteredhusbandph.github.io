+++
date = '2026-04-17T20:56:00+08:00'
draft = false
title = 'Local Lab Docker Squid'
tags = ['squid', 'docker', 'linux']
+++

![Squid Proxy](/squid.png)


My home lab currently runs on a laptop using VirtualBox, with all my VMs configured on a `host‑only` network so I can take the entire environment with me. The downside is that the VMs’ web services are only reachable from the laptop itself. If I want to work from another workstation and connect over SSH, I lose access to anything the VMs expose—HTTP and so on.
One workaround I explored was running a Docker‑based Squid proxy to bridge that gap


*~/Labs/docker/squid/docker-compose.yml*

```
services:
  squid:
    image: ubuntu/squid
    ports:
      - "3128:3128"
    volumes:
      - ./squid.conf:/etc/squid/squid.conf
      - cache:/var/spool/squid
      - logs:/var/log/squid
      - ./whitelist.txt:/etc/squid/whitelist.txt
    extra_hosts:
      - "control.lab.local:192.168.56.111"
      - "hub.lab.local:192.168.56.112"
      - "gate.lab.local:192.168.56.113"
    restart: always
volumes:
  cache:
  logs:

<br>
    
*~/Labs/docker/squid/squid.conf*

```
# Define your local network
acl localnet src 192.168.50.0/24

# Define safe ports (Standard web traffic)
acl Safe_ports port 80          # http
acl Safe_ports port 443         # https
acl CONNECT method CONNECT

dns_nameservers 192.168.50.200 #local Pi-hole dns server
# Recommended minimum Access Control configuration
# Deny requests to certain unsafe ports
http_access deny !Safe_ports

# Deny CONNECT to other than secure SSL ports
#http_access deny CONNECT !SSL_ports

# Allow localnet and localhost access
http_access allow localnet
http_access allow localhost

acl allowed_http_sites dstdomain "/etc/squid/whitelist.txt"
http_access allow localnet allowed_http_sites


# Finally deny all other access to this proxy
http_access deny all

# Squid normally listens to port 3128
http_port 3128

```

<br>

*whitelist.txt*

```
192.168.56.*
192.168.50.*
.lab.local
```


<br>

Bring docker-squid up using `docker compose` command  

```
╭─chris@mint ~/Labs/docker/squid ‹main●›
╰─$ docker compose up -d
[+] up 2/2
 ✔ Network squid_default   Created                                                                                                              0.0s
 ✔ Container squid-squid-1 Started
 ```
