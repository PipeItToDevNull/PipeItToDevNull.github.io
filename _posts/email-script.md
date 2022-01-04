---
title:  "Using an email script in a submodule to simplify your life"
tags:
  - powershell
---
I have gotten tired of constantly writing out or pasting in the same block of code to send email in my environments powershell scripts. I had the idea to make a single script that accepts basic parameters and is in its own repo to resolve this. The script will be added as a submodule where required then just called with arguments for subject, body, attachments etc. Hopefully, updating accounts and passwords will be much easier if I can just pull down the changes instead of making them in 20 different scripts.

In my script I am setting some vars in the script and allowing others to be parameters. Things like the Server and From will always be the same for me but I will change the Subject.

## Code
<!--https://gist.github.com/PipeItToDevNull/39672ada0ac4013ac641902a1fc2a8e0 
-->
{% gist 39672ada0ac4013ac641902a1fc2a8e0 send-mail.ps1 %}

## Note
Assuming this is a submodule in the root of a repo alonside the script you are running you can load (and throw if this is missing) with this short block.

{% gist }