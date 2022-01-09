---
title: "Homelab"
permalink: /homelab/
layout: single
author_profile: true
---
## Why I Homelab
I think homelabbing is just a great way to get into IT and a great way to keep skills sharp or develop new ones. I got started with homelabbing like many people do, a Minecraft server running off my own desktop as a kid. From that Minecraft server I moved onto a Raspberry Pi that ran OwnCloud and OpenVPN. 

When I interviewed for my first IT position, a Linux Admin position I was woefully underqualified for, I hit it off with their Security lead who happened to be standing up OpenVPN as a solution and we had a great conversation about the struggles of learning the tool. Needless to say I did not get that job but they did end up calling me back a couple months later for a helpdesk/junior admin position that I accepted. 

Homelabbing is what got me into the field and I encourage anyone who asks me about getting into IT to take a crack at it. You don't need an entire rack of servers, you don't need expensive disk arrays, a Pi is more than enough to get started down the IT road and to learn a couple new things on.

## The Environment
### Hardware

| Hardware      | Purpose     |
| ------------- | ----------- |
| R220          | OPNSense    |
| R320          | Backups NAS |
| R620          | XCP-NG      |
| R510          | Media NAS   |
| Catalyst-4948 |             |

### Service List
* Active Directory
    * For central authentication for all services and GPO
* Windows DNS
* Windows DHCP
* Windows Enterprise CA
    * Testing ideas and the ability to sign local scripts
* Nextcloud
    * Docker
* Gitea
    * Docker
* TheLounge
    * Docker
* HTTPD
    * Basic homepage for https://dev0.sh
    * Docker
* Linx
    * For personal code sharing/file uploads
    * Docker
* Ansible
    * CFM on Linux hosts mostly
* 3CX
    * I run a "work line" over this since we all went WFH and I didn't want to give out my cell
    * voip.ms is my DID provider
* Homebridge
    * My smart home is based around Apple and Siri
* TrueNas
    * I run 2 hosts, one for media and the other for backups/shares (the cost worked out better to have 2 hosts)
* OpenWrt
    * My Cisco WRT series router runs this as my main AP