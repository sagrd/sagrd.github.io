---
date: 2025-01-20
layout: zettel
category: show
tags:
  - "#github"
title: using multiple github accounts on ya laptop
---
- Generate ssh keys `ssh-keygen -t rsa -b 4096 -C "your-email-address"`
- Enter file in which to save the key (/home/vaati/.ssh/id_rsa): `/home/vaati/.ssh/id_rsa_work|`
- Open and copy the public key `cat .ssh/id_rsa_work.pub`
- Paste new `ssh-keys`  here: https://github.com/settings/keys; type should be `authentication-key` 
- As the key is saved with unique name, we'll need to run this command `ssh-add ~/.ssh/id_rsa_work`
- Create a config file: `nano ~/.ssh/config`
```
#Default GitHub
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

Host github.com-work
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_work
```
- When using git command use `git@github.com-work` instead of `git@github.com`