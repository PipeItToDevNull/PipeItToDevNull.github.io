---

---
I use FreeNAS (now TrueNAS Core)  as my backup destination for everything in my lab, I push these backups offsite to Backblaze on a schedule using Cloud Sync Tasks. This has worked pretty well for years but it was always annoying when I would check in on my backups and see failures on these tasks. Despite how basic the idea is, TrueNAS has never had a method to send an email on one of these failues. 

I was recently going through and cataloging all of my backups better, documenting where everything goes, when, and ensuring all my boxes are actually being backed up. I decided to give it a google again and it seems that [this feature was added in 11.3](https://www.truenas.com/community/threads/cloud-sync-email-notification.69436/post-574147)

