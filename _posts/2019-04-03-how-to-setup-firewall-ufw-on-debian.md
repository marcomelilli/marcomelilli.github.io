---
layout: post
title: How to setup a firewall with UFW on Debian
gh-repo: marcomelilli
gh-badge:
  - follow
tags:
  - firewall
  - debian
  - security
  - vps
comments: false
published: true
date: '2019-04-03'
---

**Uncomplicated Firewall** (ufw) is a tool for managing firewall designed to be easy to use. It uses a command-line interface and uses **iptables** for configuration.


**Installation**

      apt-get install ufw

**Setup**

- **Allow** main ports and ports you need to expose:

      sudo ufw allow 22
      sudo ufw allow 80
      sudo ufw allow 443

- Deny all other ports and allow outgoing connections:

      sudo ufw default deny incoming
      sudo ufw default allow outgoing
  
- To **delete** a rule you can use: 

      ufw delete allow 80

- Before **enable** the firewall, remember to <b>allow connections from ssh port</b> if you are connecting remotely to your vps:

      sudo ufw enable
    
- To verify the firewall is running you can use the command:

      sudo ufw status
