+++
date = '2026-04-17T20:56:00+08:00'
draft = false
title = 'Local Lab Docker Squid'

+++


My local lab is currently hosted on a laptop running Virtualbox. I've chose to use `Host-only` network on my VMs so that i can bring my lab with me anywhere. The issue with this is that i can only access the VMs webservers on the laptop itself. Now if i want to use another workstation for my lab and remotely connect via SSH, i wont have access on the VMs hosted services like http, etc. 


One solution that i come with was to install Docker hosted squid
\

~/Labs/docker/squid/docker-compose.yml
\
```
services:
  squid:
    image: ubuntu/squid
    ports:
      - "3128:3128"
    volumes:
      - ./squid.conf:/etc/squid/squid.conf
      - ./cache:/var/spool/squid
      #- ./logs:/var/log/squid
      - /tmp:/var/log/squid
      - ./whitelist.txt:/etc/squid/whitelist.txt
    extra_hosts:
      - "control.lab.local:192.168.56.111"
      - "hub.lab.local:192.168.56.112"
      - "gate.lab.local:192.168.56.113"
    restart: always
```
\
~/Labs/docker/squid/squid.conf
\
```
# Define your local network
acl localnet src 192.168.50.0/24

# Define safe ports (Standard web traffic)
acl Safe_ports port 80          # http
acl Safe_ports port 443         # https
acl CONNECT method CONNECT

dns_nameservers 192.168.50.200
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
\
~/Labs/docker/squid/whitelist.txt  
\
```
192.168.56.*
192.168.50.*
.lab.local
```
\
Bring the docker-squid up using `docker compose` command  
\
```
╭─chris@mint ~/Labs/docker/squid ‹main●›
╰─$ docker compose up -d
[+] up 2/2
 ✔ Network squid_default   Created                                                                                                              0.0s
 ✔ Container squid-squid-1 Started
 ```

\#squid \#linux
