---
title:  "DNS Backups in PowerShell"
tags: 
  - powershell
  - windows_dns
---
DNS backups are a bit complicated, you need to backup and restore each zone individually with files that are in a static location in System32. Most sources I found used `dnscmd` which is too DOS for me, we need to PowerShell it up. I ended up finding that [Add-DnsServerPrimaryZone](https://docs.microsoft.com/en-us/powershell/module/dnsserver/add-dnsserverprimaryzone?view=windowsserver2022-ps) would work for my needs despite what [some sources](https://www.virtualizationhowto.com/2019/07/export-and-import-dns-zone-with-powershell-from-one-server-to-another/) said about there being no PowerShell way to do this.

## Code
### Backup
<!--
https://gist.github.com/PipeItToDevNull/f5668a05f1e19c801f2bd16ba6c89b3b
-->
{% gist f5668a05f1e19c801f2bd16ba6c89b3b backup.ps1 %} 

> :pencil: This script utilizes my [email script submodule](https://blog.dev0.sh/2022/01/04/email-script.html)

### Recovery
{% gist f5668a05f1e19c801f2bd16ba6c89b3b recovery.ps1 %}

## Notes
* The exported files are plaintext
* When exporting you can only specify a file name not location. The files can **only** go to `C:\Windows\System32\dns` and must be moved from there.

## References
Another basic script
* https://thesisadmin.blogspot.com/2016/08/windows-powershell-dns-backup-script.html

An overview on the cmdlets and commands
* https://www.virtualizationhowto.com/2019/07/export-and-import-dns-zone-with-powershell-from-one-server-to-another/

Using PowerShell
* https://rietveld-ict.nl/dns-zone-recovery-using-powershell/
* https://stackoverflow.com/questions/65693302/how-do-you-create-a-new-microsoft-dns-zone-with-powershell-that-loads-from-a-dns

Docs on  DNSServer Module
* https://docs.microsoft.com/en-us/powershell/module/dnsserver/?view=windowsserver2022-ps
    * https://docs.microsoft.com/en-us/powershell/module/dnsserver/export-dnsserverzone?view=windowsserver2022-ps
    * https://docs.microsoft.com/en-us/powershell/module/dnsserver/add-dnsserverprimaryzone?view=windowsserver2022-ps