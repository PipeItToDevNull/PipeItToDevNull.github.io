---
tags:
  - windows_server
  - windows_ca
  - powershell 
---
One of the most ubiquitous actions a sysadmin does is accepting the untrusted certificates we are presented with daily when opening RDP to a server. I believe training this behaviour is a horrible practice that Microsoft should discourage more forcefully. I decided to see what I could do about it in my lab.

There are two solutions available, the first is to trust all of the self-signed certificates from each server at a domain level. If you have 2 or 3 servers that may work but it does not scale well and is not an automated solution. Your second option is to issue certificates from your internal CA through GPO and that is the option we are going to explore.

I found numeruous sources and hit a couple of issues but the docs below should be a solid baseline for anyone else to explore the idea of issuing out signed RDP certificates to all of their servers.

* TOC 
{:toc}

## Default Configuration
Windows server by default uses self signed certificates to secure RDP, this makes sense. The settings that control the issuance are 