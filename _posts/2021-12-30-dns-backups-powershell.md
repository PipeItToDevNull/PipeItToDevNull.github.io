---
title:  "DNS Backups in PowerShell"
tags: 
  - powershell
  - windows_dns
---
DNS backups are a bit complicated, you need to backup each primary zone individually and restore them using a less than sensible command due to the lack of `Import-DnsServerZone` PowerShell cmdlet.

The script we have below is designed to push our backups to a file share with a name based on the date, root zone, and server the backup is from. 

## Code
### Backup
{% comment https://gist.github.com/PipeItToDevNull/02003efef6bfe1f81d13767b734224f1 %}
{% gist eab21304a4e584d1a96d715b5e392329 backup.ps1 %} 

### Recovery
Recovery does not appear to be done easily or simply with powershell but the traditional `dnsdcmd` tool will work fine.
```dos
dnscmd <dns server name> /zoneadd "yourzone.com" /primary /file yourzone.com.dns /load
```

## Notes
* The `.dns` files are plaintext
* When exporting you can only specify a file name not location. The files can **only** go to `C:\Windows\System32\dns` and must be moved from there.

## References
Another basic script
* https://thesisadmin.blogspot.com/2016/08/windows-powershell-dns-backup-script.html

An overview on the cmdlets and commands
* https://www.virtualizationhowto.com/2019/07/export-and-import-dns-zone-with-powershell-from-one-server-to-another/