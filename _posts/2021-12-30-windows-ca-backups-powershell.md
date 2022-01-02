---
title:  "Windows CA Backups in Powershell"
tags:
  - powershell
  - windows_ca
---
## Overview
The CA is an incredibly important piece of infrastructure, especially once you start issuing your own certificates. We are pushing our code signing certs, smart card certs and certs for VPN Authentication. A loss of our CA would be a very bad day. 

Backup and restoration appear to be simple, using just one cmdlet each. There is no Microsoft documentation saying "This is everything" so I will need to run a restoration onto new bare metal to test out this process (as you should be doing anyway).

## Code
### Backup
```powershell
$pass = ConvertTo-SecureString 'Password' -AsPlainText -Force
$path = "\\shares\backup\ca\$env:COMPUTERNAME-$date"

Backup-CARoleService -Path $path -Password $pass
```

### Recovery
```powershell
Restore-CARoleService -Path <path>
```

## Notes
* Take a backup of the CAPolicy.inf file if you have created one explicitly during the CA installation.
* When restoring, stop the certsvc service and restart it when done.

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