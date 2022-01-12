---
title:  "AD Backups in PowerShell"
tags:
  - powershell
  - active_directory
---
The vast majority of sources I checked while trying to re-work our existing backups use the same basic script that invoke `wbadmin.exe` to initiate an image of the server, but that isn't real powershell and just won't do. I more or less copied my code from the [official docs for Start-WBBackup](https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/start-wbbackup?view=windowsserver2022-ps). 

I added a timer into my script because this tends to take a while and if you see a large variation in the time you may be alerted to other issues you have in your infrastructure which is nice.

## Code 
%% 
https://gist.github.com/PipeItToDevNull/99e6ccccc772684b66175bc6a987ee7a 
%% 

{% gist https://gist.github.com/PipeItToDevNull/99e6ccccc772684b66175bc6a987ee7a backup.ps1 %}

## Recovery
### With Windows install media on a new VM or baremetal
> 📝 You can do this recovery via a network share (easiest) or from files on a disk. If you have various network issues related to drivers or virtualization you will want to try it from files on a disk. 
> 
> To get files onto a VM mount a disk in a working VM to copy files then mount that disk into the recovering VM. You should put the `WindowsImageBackup` directory into the root of the disk you want to use for this.

> ⚠ Error 8007001f
> I had this error when trying to do a network restore on my VMs. I tried VBox, Hyper-V and XCP-NG with the same error. Regardless of path, name vs IP and networking method. I fell back to the CLI method listed here because of it.

Boot up your install media and choose 


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
* https://community.spiceworks.com/topic/2201127-recover-windows-system-image-from-network-error-0x8007001f