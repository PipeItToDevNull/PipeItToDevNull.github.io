---
title:  "Using an email script in a submodule to simplify your life"
tags:
  - powershell
---
I have gotten tired of constantly writing out or pasting in the same block of code to send email in my environments powershell scripts. I had the idea to make a single script that accepts basic parameters and is in its own repo to resolve this. The script will be added as a submodule where required then just called with arguments for subject, 