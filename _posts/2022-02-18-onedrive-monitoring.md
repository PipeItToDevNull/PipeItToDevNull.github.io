---
title:  "Proactive OneDrive Monitoring"
tags:
  - onedrive
---
Microsoft is very keen on pushing OneDrive, anyone who has stood up a Windows 10/11 workstation recently knows that. 

OneDrive redirects all of the basic user directories such as "My Documents" and even "Desktop" into itself, this is great for auto-magically enforcing backups of workstations but most users are not aware of/capable of checking that OneDrive is working properly. 

This can be a sad moment for a single user if their machine goes kaput and they lose some files but it can be much worse if a team is using OneDrive to collaborate via [SharePoint sync](https://support.microsoft.com/en-us/office/sync-sharepoint-files-and-folders-87a96948-4dd7-43e4-aca1-53f3e18bea9b). 

I stumbled upon a [comment on Reddit](https://www.reddit.com/r/sysadmin/comments/soewxw/comment/hw8bono/?utm_source=share&utm_medium=web2x&context=3) that mentioned a new admin page from Microsoft, it is of course in Preview™ but I decided to give it a try. A snippet from the [official docs](https://docs.microsoft.com/en-us/onedrive/sync-health):

> From the Sync health dashboard, admins can check the sync status and sync app version of individual devices, monitor Known Folder Move roll out, and track sync errors. The insights range from a high-level executive summary to a drill-down of sync status per device, to be used in various administrative scenarios.
 
## Notes
I do not plan to re-iterate the setup directions here, they are pretty straight forward but a couple notes from the docs and my setup are:

* This is not available to GCC, GCC High, or the DoD Cloud
* The docs say provisioning after step 4 takes 10 minutes, mine took several hours.
* Microsoft suggests rolling this out to no more than 100 devices per day.
* If you generate a new Client Key on the admin panel you need to adjust your deployment method to also use the new Key
* After you enable the SyncAdminReports setting on devices, it takes up to three days for reports to be available. (It took my first machine about a day)

## Client setup
The only thing you need to change on the client side is a registry key. You can change this however you please but there is actually an [Admin Template](https://docs.microsoft.com/en-us/onedrive/use-group-policy#manage-onedrive-using-group-policy) available if you prefer to use GPO.

### GPO
Set `Computer Configuration\Policies\Administrative Templates\OneDrive\Sync Admin Reports` to Enabled and include your "Tenant Association Key" that was generated in step 6 above.

If you do not have the above keys, you need to add the OneDrive AMDX templates from Microsoft. See the next section.

#### Adding Admin Template
Navigate to `%localappdata%\Microsoft\OneDrive\#####\adm` "#####" is a build number, I only have one but you may have more. I would try the latest in that case. Inside `adm` you will find the AMDL and AMDX files we need. If you are non "EN" you can get the AMDL for your language instead from its respective sub directory.

If you don't know how AMDX files work, they are placed into `C:\Windows\SYSVOL\domain\Policies\PolicyDefinitions\` on your DC. AMDL files are placed in `C:\Windows\SYSVOL\domain\Policies\PolicyDefinitions\en-US` or the lang folder that suits your better.

If you did it all correctly you can close then reopen Group Policy Editor on your DC and find the OneDrive polices in `Computer Configuration\Policies\Administrative Templates\OneDrive`

> 📝The SYSVOL replicates between all DCs, you can place these files onto any single DC and they will be available on all others after the next replication cycle.

> 📝 You can put these on any workstation as well, for the policies to appear in local group policy editor by using the directory `C:\Windows\PolicyDefinitions\` and the `en-US` subdir.
 
### Registry
> Edit the registry
> a. Go to HKLM\SOFTWARE\Policies\Microsoft\OneDrive
> b. Right-click > New > String Value.
> c. Name: SyncAdminReports
> d. Type: REG_SZ
> e. Data: Paste your Tenant Association Key.

### CMD
```dos
reg.exe add HKLM\Software\Policies\Microsoft\OneDrive /v SyncAdminReports /t REG_SZ /d <your Tenant Association Key> /f
```

### Check the key on a machine with PowerShell 
This will show you all the keys relating to our OneDrive GPO, the important thing is that `SyncAdminReports` is present and set.
```powershell
Get-ItemProperty 'HKLM:\Software\Policies\Microsoft\OneDrive'
```

## Use
It took a week or more of roll out to get several machines reporting properly for my initial tests, this is certainly not a 1 day roll out task. Machines report well and the information is concise. 

![ODadmin](/assets/images/2022-02-18-onedrive-monitoring/ODadmin.png)