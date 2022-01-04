---
title:  "Using an email script in a submodule to simplify your life"
tags:
  - powershell
---
I have gotten tired of constantly writing out or pasting in the same block of code to send email in my environments powershell scripts. I had the idea to make a single script that accepts basic parameters and is in its own repo to resolve this. The script will be added as a submodule where required then just called with arguments for subject, body, attachments etc. Hopefully, updating accounts and passwords will be much easier if I can just pull down the changes instead of making them in 20 different scripts.

In my script I am setting some vars in the script and allowing others to be parameters. Things like the server and From will always be the same for me but I will change the Subject.

## Code
```powershell
param (
    [Parameter(Mandatory=$False)]
    [Object]$smtp
)

$smtpServer = ""
$smtpPort = ""
$smtpFrom = ""
$smtpPassword = ConvertTo-SecureString '' -AsPlainText -Force
$smtpCredential = New-Object System.Management.Automation.PSCredential ($smtpFrom, $smtpPassword)
$smtpTo = ""
$messageSubject = ""
$messageBody = ""

Send-MailMessage -From $smtpFrom -To $smtpTo -Subject $messageSubject -Body $messageBody -Credential $smtpCredential -SmtpServer $smtpServer -Port $smtpPort -UseSsl
}
```