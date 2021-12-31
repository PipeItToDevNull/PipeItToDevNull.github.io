---
title:  "DNS Backups in PowerShell"
---
# DNS Backups in PowerShell
## References
Another basic script
* https://thesisadmin.blogspot.com/2016/08/windows-powershell-dns-backup-script.html

An overview on the cmdlets and commands
* https://www.virtualizationhowto.com/2019/07/export-and-import-dns-zone-with-powershell-from-one-server-to-another/

## Overview
DNS backups are a bit complicated, you need to backup each primary zone individually and restore them using a less than sensible command due to the lack of `Import-DnsServerZone` PowerShell cmdlet.

The script we have below is designed to push our backups to a file share with a name based on the date, root zone, and server the backup is from. 

## Script
```powershell
#user vars, change these
$backupLocation = "\\shares\backup\dns\"

#system vars, you likely don't change these
$dnsRoot = 'C:\Windows\System32\dns\'
$primarys = Get-DnsServerZone | Where-Object { $_.ZoneType -eq 'Primary' }

# Do our stuff 
ForEach ($z in $primarys) {
    $zone = $z.ZoneName
    # Edit this to change the name of the backup file
    $file = "$env:COMPUTERNAME-$zone-$(Get-Date -UFormat %Y-%m-%d).dns"
    Export-DnsServerZone -Name $z.ZoneName -FileName $file
    $backupFile = $dnsRoot + $file
    Move-Item -Path $backupFile -Destination $backupLocation
}
```

## Recovery
Recovery does not appear to be done easily or simply with powershell but the traditional `dnsdcmd` tool will work fine.
```dos
dnscmd <dns server name> /zoneadd "yourzone.com" /primary /file yourzone.com.dns /load
```

## Notes
* The `.dns` files are plaintext
* When exporting you can only specify a file name not location. The files can **only** go to `C:\Windows\System32\dns` and must be moved from there.
