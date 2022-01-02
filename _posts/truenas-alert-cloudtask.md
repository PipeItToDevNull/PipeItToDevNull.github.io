---
title:  "TrueNAS alert on Cloud Task Failure"
tags:
  - truenas
  - homelab
---
I use FreeNAS (now TrueNAS Core)  as my backup destination for everything in my lab, I push these backups offsite to Backblaze on a schedule using Cloud Sync Tasks. This has worked pretty well for years but it was always annoying when I would check in on my backups and see failures on these tasks. Despite how basic the idea is, TrueNAS has never had a method to send an email on one of these failures. 

I was recently going through and cataloging all of my backups better, documenting where everything goes, when, and ensuring all my boxes were actually being backed up. I decided to give it a google again and it seems that [this feature was added in 11.3](https://www.truenas.com/community/threads/cloud-sync-email-notification.69436/post-574147)

## Setup
To get these emails enabled we need to look in two areas and change one or the other (or both if you want to change more).

The first is the Alert Setting itself, navigate to 
"System>Alert Settings" or `/ui/system/alertsettings`. Scroll down to the last category "Tasks". You will see that "Cloud Sync Task Failed" is already here with the level "ERROR" and frequency "IMMEDIATELY". 

The second area is `/ui/system/alertservice`