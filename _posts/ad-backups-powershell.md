---
title:  "AD Backups in PowerShell"
tags:
  - powershell
  - "active directory"
---
## Overview
The vast majority of sources I checked while trying to re-work our existing backups use the same basic script that invoke `wbadmin.exe` to initiate an image of the server, if it works so well I guess we won't be reinventing the wheel.

## Code
```Powershell
Import-Module ServerManager
$date = $(Get-Date -UFormat %Y-%m-%d)
$path=”\\shares\backups\ad\”

$dir=$path+$date+$env:COMPUTERNAME

$TestTargetUNC= Test-Path -Path $TargetUNC
if (!($TestTargetUNC)){
New-Item -Path $TargetUNC -ItemType directory
}
$WBadmin_cmd = "wbadmin.exe START BACKUP -backupTarget:$TargetUNC -systemState -noverify -vssCopy -quiet"
Invoke-Expression $WBadmin_cmd
```

## References
* http://woshub.com/backup-active-directory-domain-controller/
* https://bobcares.com/blog/backup-active-directory-domain-controller/