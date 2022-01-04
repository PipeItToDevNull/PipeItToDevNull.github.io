---
title:  "Using PSWindowsUpdate to Centralize Update Deployment"
tags:
  - powershell
  - homelab
---
For a year or so I have been using ManageEngine PatchEngine hosted on a Windows 10 box in my environment. I am looking to trim down a bit and removed this server. In its place I am looking to use [PSWindowsUpdate](https://www.powershellgallery.com/packages/PSWindowsUpdate/2.0.0.4) in a PowerShell script to manage and deploy my updates instead.

My goal is to make a script that pulls all my hosts from an `.ini` file and first deploys the needed modules and then checks for and applies any updates that are available. I want to get an email report for documentation once this process is complete.

I want this script to schedule random reboots

## Code
```powershell
Install-Module PSWindowsUpdate


```

## References
* http://woshub.com/pswindowsupdate-module/