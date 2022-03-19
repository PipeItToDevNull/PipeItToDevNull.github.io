---
title:  "DHCP Backups in PowerShell"
tags: 
  - powershell
  - windows_dhcp
  - backups
last_modified_at: '2022-02-08'
---
Backing up a DHCP server is simple using the cmdlets `Backup-DhcpServer` and `Restore-DhcpServer`. There are a couple gotchas and while it is not as directory specific as the [dns backups]() are I chose to use the same directories out of convenience,  

> :pencil: ACLs must be set to give "DHCP Server" full control over the restoration files otherwise the import fails.

> :pencil: The service must be restarted prior to removing the restoration files, otherwise you get errors and no restoration occurs.

## Code
### Backup
<!-- 
https://gist.github.com/PipeItToDevNull/c7725371d0ecc3c62e75243e15ef6b7e
--> 
{% gist c7725371d0ecc3c62e75243e15ef6b7e backup.ps1 %}

> :pencil: This script utilizes my [email script submodule.]({% post_url 2022-01-04-email-script%})

### Recovery
{% gist c7725371d0ecc3c62e75243e15ef6b7e recovery.ps1 %}

### Notes
A DHCP server runs a backup of itself every 60 min by default, using probably `Backup-DHCPServer` cmdlet. This automatic backup is located, always by default in `%SystemRoot%\System32\DHCP\backup`

## References
Official docs
* https://docs.microsoft.com/en-us/powershell/module/dhcpserver/backup-dhcpserver?view=windowsserver2022-ps
* https://docs.microsoft.com/en-us/powershell/module/dhcpserver/restore-dhcpserver?view=windowsserver2022-ps

Backup-DhcpServer vs Export-DhcpServer
* https://www.reddit.com/r/PowerShell/comments/ikb8ok/exportdhcpserver_vs_backupdhcpserver/