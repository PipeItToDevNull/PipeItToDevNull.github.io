---
title:  "AD Backups in PowerShell"
tags:
  - powershell
  - active_directory
---
The vast majority of sources I checked while trying to re-work our existing backups use the same basic script that invoke `wbadmin.exe` to initiate an image of the server, but that isn't real powershell and just won't do.

## Code
 This script is heavily based off the [official docs for Start-WBBackup](https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/start-wbbackup?view=windowsserver2022-ps)

%% 
https://gist.github.com/PipeItToDevNull/99e6ccccc772684b66175bc6a987ee7a 
%% 

{% gist https://gist.github.com/PipeItToDevNull/99e6ccccc772684b66175bc6a987ee7a backup.ps1 %}

> :grey_exclamation: : Restoration of these backups would be done with [Microsoft's documenation](https://docs.microsoft.com/en-us/windows-server-essentials/manage/restore-or-repair-your-server-running-windows-server-essentials#BKMK_Restore_1).

## Recovery onto bare metal
> :pencil: you can do this recovery via a network share (easiest) or from files on a disk. If you have various network issues related to drivers or virtualization you will want to try it from files on a disk. 
> 
> To get files onto a VM mount a disk in a working VM to copy files then mount that disk into the recovering VM.

## References
Backup scripts, ideas, and details
* http://woshub.com/backup-active-directory-domain-controller/
* https://bobcares.com/blog/backup-active-directory-domain-controller/
Docs on WBAdmin.exe
* https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wbadmin
Docs on WindowsServerBackup PowerShell module
* https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/?view=windowsserver2022-ps
Docs on restoration/recovery
* https://askme4tech.com/how-restore-windows-image-backup-different-windows-server