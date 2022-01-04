---
title:  "AD Backups in PowerShell"
tags:
  - powershell
  - active_directory
---
The vast majority of sources I checked while trying to re-work our existing backups use the same basic script that invoke `wbadmin.exe` to initiate an image of the server, if it works so well I guess we won't be reinventing the wheel

## Code
```Powershell
Import-Module ServerManager
$date = $(Get-Date -UFormat %Y-%m-%d)
$path= '\\shares\backups\ad\'

$dir=$path+$date+'-'+$env:COMPUTERNAME

$testPath = Test-Path -Path $dir
if (!($testPath)) {
    New-Item -Path $dir -ItemType directory
}
$WBadmin_cmd = "wbadmin.exe START BACKUP -backupTarget:$dir -systemState -noverify -vssCopy -quiet"
Invoke-Expression $WBadmin_cmd
```

```powershell
Import-Module ServerManager
$date = $(Get-Date -UFormat %Y-%m-%d)
$path= '\\shares\backups\ad\'

$dir=$path+$date+'-'+$env:COMPUTERNAME

$testPath = Test-Path -Path $dir
if (!($testPath)) {
    New-Item -Path $dir -ItemType directory
}
```

## Notes

## References
Backup scripts, ideas, and details
* http://woshub.com/backup-active-directory-domain-controller/
* https://bobcares.com/blog/backup-active-directory-domain-controller/
Docs on WBAdmin
* https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wbadmin
* https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/?view=windowsserver2022-ps