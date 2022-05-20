---
title: "Installing RSAT in 1909+ Online or Offline"
tags:
  - windows
  - powershell
last_modified_at: '2022-05-20'
---
In previous versions of Windows and early versions of Windows 10 [RSAT](https://support.microsoft.com/en-us/topic/e0a3aea3-7bbb-f39c-15db-fd3b51b14cd1) was installed via an update package or `.msu` file. Recent versions of Windows 10/11 have moved past this method to one that is a bit more difficult but more future-proof. This new method is called [Features on Demand](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) (FoD), this unifies how things like Language packs, OpenSSH, Powershell-ISE and other features are added/updated on Windows.  One advantage of this method is RSAT will persist a major version upgrade, such as moving from 20H2 to 21H2.

## Using FoD's
### FoD Online
When doing an online install of a feature you must be able to talk to Windows Update service, FoD's cannot be pulled through WSUS. FoD's are managed via DISM or in PowerShell via DISM wrapper cmdlets such as [Add-WindowsCapability](https://docs.microsoft.com/en-us/powershell/module/dism/add-windowscapability?view=windowsserver2022-ps). 

### FoD Offline
If you are on a gapped network or just want an offline installer to minimize downloads you will need to obtain an FoD ISO, officially you can only obtain these ISOs from the [VLSC](https://www.microsoft.com/licensing/servicecenter/default.aspx). The FoD ISO is over 5GB if you want to reduce the size you can extract it to a file then run the following command to extract only the RSAT parts from it, reducing the size to a couple hundred MB.

<!--
https://gist.github.com/PipeItToDevNull/9bd048c7028b26767fae3c115515ef29
-->
{% gist 9bd048c7028b26767fae3c115515ef29 create-fdo.ps1 %}

## Scripts
My script below can be used for online or offline installs. To install from online sources use `Install-Rsat.ps1 -online`. This will check for WSUS and disable then re-enable it if needed. To install offline use `Install-Rsat.ps1 -offline -source ./fod_repo` where the source path is either your custom repo or the fully extracted ISO. You should be able to point it at a mounted ISO driver letter as well.

<!--
https://gist.github.com/PipeItToDevNull/9bd048c7028b26767fae3c115515ef29
-->
{% gist 9bd048c7028b26767fae3c115515ef29 Install-Rsat.ps1 %}

### Removing RSAT
It is not to attempt the removal of RSAT, in my testing it was often broken and did not remove all components each time. Several reboots and re-running of the following function may be required.

<!--
https://gist.github.com/PipeItToDevNull/9bd048c7028b26767fae3c115515ef29
-->
{% gist 9bd048c7028b26767fae3c115515ef29 Remove-Rsat.ps1 %}
