---
title: "Finding certs that are self-signed or have an untrusted-root"
tags:
  - powershell
last_modified_at: '2022-05-13'
---
I had a need to find all of the self-signed certificates on my machine so I whipped up a tiny function to do it. The largest caveat is the inability to distinguish between a truly self-signed certificate and one that only has an untrusted root cert from someome else.

```powershell
Function Get-UntrustedRoots {
    $badCerts = @()
    $certs = Get-ChildItem -Recurse cert:\ | ? {$_.subject -ne $null} | ? {$_.subject -eq $_.issuer}
    Foreach ($cert in $certs) {
        If (!(Test-Certificate -Cert $cert -WarningVariable reason -ErrorAction SilentlyContinue)) {
            If ($reason -Like "*CERT_TRUST_IS_UNTRUSTED_ROOT") {
                $badCerts += $cert
            }
        }
    }
    Return $badCerts
}
Get-UntrustedRoots | Select Subject,Issuer,EnhancedKeyUsageList,Thumbprint,PSParentPath | fl
```
