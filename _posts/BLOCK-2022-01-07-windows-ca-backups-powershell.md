---
title:  "Windows CA Backups in Powershell"
tags:
  - powershell
  - windows_ca
---
The CA is an incredibly important piece of infrastructure, especially once you start issuing your own certificates. We are pushing our code signing certs, smart card certs and certs for VPN Authentication. A loss of our CA would be a very bad day. 

Backup and restoration seem simple when first checking out the `Backup-CARoleService` docs but there is no Microsoft documentation saying "This is everything" and that led me down a hole to find that it is indeed not everything. We also care about the "CAPolicy.inf" which controls root cert expiration length and several other critical factors and our Templates to issue. 

I also threw in a registry backup which I read about in [this source](https://dimitri.janczak.net/2016/10/08/backup-of-a-windows-ca-configuration/) but it does contain hostnames and such so I would not restore it on bare principle and check to see if not having the restored registry is an issue.

I will need to run a restoration onto new bare metal to test out this process (as you should be doing anyway). I tested this in my [homelab](https://blog.dev0.sh/homelab/) by removing certs from the store and then conducting a restore, it went off without a hitch.

## Code
### Backup
<!---
https://gist.github.com/PipeItToDevNull/f4c87abda4f86a00aab4a656a76bc264
-->
{% gist f4c87abda4f86a00aab4a656a76bc264 backup.ps1 %}

### Recovery
{% gist f4c87abda4f86a00aab4a656a76bc264 recovery.ps1 %}

## References
Official docs
* https://docs.microsoft.com/en-us/powershell/module/adcsadministration/?view=windowsserver2022-ps
    * https://docs.microsoft.com/en-us/powershell/module/adcsadministration/backup-caroleservice?view=windowsserver2022-ps
    * https://docs.microsoft.com/en-us/powershell/module/adcsadministration/restore-caroleservice?view=windowsserver2022-ps
* https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/component-updates/ca-backup-and-restore-windows-powershell-cmdlets

Backup ideas and tips
* https://blog.ahasayen.com/certification-authority-backup/
* https://dimitri.janczak.net/2016/10/08/backup-of-a-windows-ca-configuration/
* https://redmondmag.com/Articles/2016/03/01/Securing-Windows-Enterprise-CAs.aspx

Cert Templates are stored in AD
* https://social.technet.microsoft.com/wiki/contents/articles/8464.certificate-templates-and-their-storage-within-active-directory.aspx
* https://social.technet.microsoft.com/Forums/windowsserver/en-US/ffcce3ee-1965-4821-bbdb-eb5cfc68083b/backup-up-a-ca-templates-list?forum=winserversecurity