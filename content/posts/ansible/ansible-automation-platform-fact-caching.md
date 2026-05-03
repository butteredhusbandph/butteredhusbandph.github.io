+++
date = '2026-05-03T14:34:52+08:00'
draft = false
title = 'Ansible Automation Platform Fact Caching'
tags = ['ansible', 'ansibleautomationplatform', 'redhat', 'linux']
+++
*Disclaimer:* These notes reflect my personal understanding and working thoughts on Ansible Automation Platform. They are not intended to serve as formal documentation or a step-by-step guide. That said, I hope they offer useful insights, spark ideas, or provide some value as you explore AAP on your own  

*Settings > Job > Per Host Ansible Fact Cache Timeout*  
![Ansible Automation Platform Fact Caching](/ansible/rh-aap-fact-caching1.png)

*Automation Controller > Templates > Job > Enable fact storage*
![Ansible Automation Platform Fact Caching](/ansible/rh-aap-fact-caching2.png)

AAP should now store Facts after Job run
![Ansible Automation Platform Fact Caching](/ansible/rh-aap-fact-caching3.png)
