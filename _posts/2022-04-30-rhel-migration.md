---
title: "RHEL 8 Migration"
tags:
  - RHEL
  - Homelab
last_modified_at: '2022-05-03'
---
My current project is moving off CentOS 7 to RHEL 8. I am doing this partly due to the deprecation of CentOS 8 into Stream but also I want to redo everything properly, using all the things I have learned since first standing up my environment and learning about Ansible, Docker, etc.

I wont expand on things too much here, but plan to make subsequent posts for the major steps and things that I learn along the way.

> 📝 I am using RHEL Developer licensing that I setup in my [RHEL Developer]({% post_url 2022-01-02-rhel-developer%}) post

## Goals
1. Move to RHEL 8 from CentOS 7
2. Utilize Kickstart for initial installs
3. Ansible improvements
    1. Run ansible as its own user
    2. Utilize Ansible for all configurations
4. Leave SELinux on and learn it
5. Move docker into volumes and other best practices
