+++
date = '2026-05-01T10:03:10+08:00'
draft = true
title = 'Ansible Automation Platform Git Webhook'
+++

## Gitlab Docker
In my lab, i used gitlab docker.
```yaml
services:
  gitlab:
    image: 'gitlab/gitlab-ce:latest'
    restart: always
    hostname: 'gitlab.lab.local'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.lab.local:8929'
        gitlab_rails['gitlab_shell_ssh_port'] = 2424
        # Add other configurations here
    ports:
      - '8929:8929'
      - '443:443'
      - '2424:22'
    volumes:
      - ./config:/etc/gitlab
      - ./logs:/var/log/gitlab
      - ./data:/var/opt/gitlab
    shm_size: '256m'
```
### Changing root Gitlab password
```console
╭─chris@mint ~/Labs/docker/gitlab ‹main●›
╰─$ docker exec -it gitlab_gitlab_1 /bin/bash

root@gitlab:/etc/gitlab# gitlab-rails console -e production

--------------------------------------------------------------------------------
 Ruby:         ruby 3.3.10 (2025-10-23 revision 343ea05002) [x86_64-linux]
 GitLab:       18.11.2 (7bf35534e4b) FOSS
 GitLab Shell: 14.49.0
 PostgreSQL:   17.8
------------------------------------------------------------[ booted in 32.21s ]
Loading production environment (Rails 7.2.3)
gitlab(prod)>
gitlab(prod)> user = User.where(id: 1).first
=> #<User id:1 @root>
gitlab(prod)> user.password = '********'
=> "secret"
gitlab(prod)> user.password_confirmation = '********'
=> "secret"
gitlab(prod)> user.save!

```

## Allow Outbound Requests in Gitlab
[Allow outbound requests in Gitlab](https://docs.gitlab.com/security/webhooks/#allow-outbound-requests-to-certain-ip-addresses-and-domains)

![AAP Webhook](/ansible/rh-aap-webhook1.png)

## Gitlab Project access tokens
*Gitlab > <project> > Settings > Access Tokens*
![AAP Webhook](/ansible/rh-aap-webhook2.png)
Select scopes  to `api`

## AAP Gitlab Credentials
*Automation Controller > Infrastructure Credentials*  
**Credential Type:** Gitlab Personal Access Token  
Copy Token

## AAP Job Template Webhook  
Under Job Template select `Enable webhook`
![AAP Webhook](/ansible/rh-aap-webhook3.png)

## Register Webhook in Gitlab
Settings > Webhook
**URL** Paste `Webhook URL` from AAP  
**Secret Token:** Paste `Webhook key` from AAP  
**Trigger** Select events(eg Push)  
**SSL Verification** Uncheck
![AAP Webhook](/ansible/rh-aap-webhook4.png)
