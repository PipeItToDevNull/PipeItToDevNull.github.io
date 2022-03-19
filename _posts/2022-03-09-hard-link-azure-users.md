---
title: "Making a Hard Link Between On-Prem and Azure-AD Users"
tags:
  - azure
  - O365
last_modified_at: '2022-03-10'
---
When moving from on-prem to 365 you may be left with a `.local` TLD in addition to a proper public `.com` or whatever domain. When making a new user in AD you will be able to choose between these two. 

Having a mixture of the proper and local TLDs will become a headache at one point or another in your scripts. For me the issue arose while using a script to notify my users of expiring smart card certificates. I have a couple users with long hyphenated names that makes their SamAccountName shorter than their UserPrincipalName and therefore their email (which I wanted to send to) as well.

Long story short I changed their domain in AD from `.local` to `.com` and they both became sync issues in O365. I changed them both back to `.local` and resolved a couple attribute issues and they stopped being issues in the O365 admin panel. Later that night though I got notice of a sync issue in Azure, one of the users was still being a pain.

I opened a ticket with Microsoft, the long and short of which is that since a soft match did not work we needed to do a hard match. A hard match requires setting an "ImmutableId" on the Azure and AD objects. 

## Process
1. Check AD for an ID
    1. Open synchronization Service Manage>Metaverse Search>Search using UserPrincipal name and Contains
    2. Double click the User: Under Attributes, there will be SourceAnchor (same as Immutable ID)
    3. Write the above down, you cannot copy it from the table.
2. Check Azure for an ID
```powershell
Get-MsolUser -UserPrincipalName <email> | select ImmutableID
```

#### If you have an ID in AD but not Azure
1. Set the ImmutableID on the Azure user (Replace the QQ00 below)
```powershell
Set-MsolUser -UserPrincipalName <email> -ImmutableId QQ00ApTUDEiiEm5kX==
```
2. Do a Delta Sync on your Connect server
```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```

#### If you have an ID in Azure but not AD
1. We need to get a Hex value for our immutable ID, we cannot use the ID directly. Run the following replacing the QQ00 ID with our own.
```powershell
[system.convert]::FromBase64String("QQ00ApTUDEiiEm5kX==") | %{$a += [System.String]::Format("{0:X}", $_) + " "};$result = $null;$result = $a.trimend();$result
 ```

2. In the AD Attribute editor update `on-premises ms-ds-consistency-guid` value to match Hex we got above
3. Do a Delta Sync on your Connect server 
```powershell
Start-ADSyncSyncCycle -PolicyType Delta
```