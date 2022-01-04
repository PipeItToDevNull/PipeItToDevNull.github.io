---
title:  "AD Backups in PowerShell"
tags:
  - powershell
  - active_directory
---
The vast majority of sources I checked while trying to re-work our existing backups use the same basic script that invoke `wbadmin.exe` to initiate an image of the server, but that isn't real powershell and just won't do.

## Code
 This script is heavily based off the [official docs for Start-WBBackup](https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/start-wbbackup?view=windowsserver2022-ps)

```powershell
#Requires -RunAsAdministrator

# user vars
$path= '\\shares\backups\ad\'

# create our backup policy
$policy = New-WBPolicy
Add-WBSystemState $policy
Add-WBBareMetalRecovery $Policy
Set-WBVssBackupOptions -Policy $policy -VssCopyBackup
$backupDir = New-WBBackupTarget -NetworkPath $path
Add-WBBackupTarget -Policy $Policy -Target $backupDir

# run it
Start-WBBackup -Policy $policy

# Validate a success
$summary = Get-WBSummary
$lastSuccess = $summary.LastSuccessfulBackupTime
```

## Notes

## References
Backup scripts, ideas, and details
* http://woshub.com/backup-active-directory-domain-controller/
* https://bobcares.com/blog/backup-active-directory-domain-controller/
Docs on WBAdmin.exe
* https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wbadmin
Docs on WindowsServerBackup PowerShell module
* https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/?view=windowsserver2022-ps