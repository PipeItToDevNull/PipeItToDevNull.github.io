---
title:  "DHCP Backups in PowerShell"
---
# DHCP Backups in PowerShell
## Overview
Backing up a DHCP server is simple using the cmdlets `Backup-DhcpServer` and `Restore-DhcpServer`. Make a directory based on the date and then read/write from/to it in the 2 commands. Add archiving if you want to be fancy.

## Code
```powershell
$date = $(Get-Date -UFormat %Y-%m-%d)
$path = "\\shares\backup\dhcp\$env:COMPUTERNAME-$date"

Backup-DhcpServer -Path $path
```

```powershell
Restore-DhcpServer -Path <directory>
```

## Backup vs Export
* There is minimal difference between the cmdlets `Export-DhcpServer` and `Backup-DhcpServer` so I just stick with Backup

## Notes
> A DHCP server runs a backup of itself every 60 min by default, using probably `Backup-DHCPServer` cmdlet. This automatic backup is located, always by default in `%SystemRoot%\System32\DHCP\backup`

## References
Official docs
* https://docs.microsoft.com/en-us/powershell/module/dhcpserver/backup-dhcpserver?view=windowsserver2022-ps
* https://docs.microsoft.com/en-us/powershell/module/dhcpserver/restore-dhcpserver?view=windowsserver2022-ps

Backup-DhcpServer vs Export-DhcpServer
* https://www.reddit.com/r/PowerShell/comments/ikb8ok/exportdhcpserver_vs_backupdhcpserver/
