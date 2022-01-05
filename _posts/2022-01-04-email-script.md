---
title:  "Using an email script in a submodule to simplify your life"
tags:
  - powershell
---
I have gotten tired of constantly writing out or pasting in the same block of code to send email in my environment's powershell scripts. I had the idea to make a single script that accepts basic parameters and is in its own repo to resolve this. The script will be added as a submodule where required then just called with arguments for subject, body, attachments etc. Hopefully, updating accounts and passwords will be much easier if I can just pull down the changes instead of making them in 20 different scripts.

In my script I am setting some vars in the and allowing others to be parameters. Things like the Server and From will always be the same for me but I will change the Subject.

<!--
https://gist.github.com/PipeItToDevNull/39672ada0ac4013ac641902a1fc2a8e0 
-->
{% gist 39672ada0ac4013ac641902a1fc2a8e0 send-mail.ps1 %}

Making a submodule is something you might not be familiar with, I certainly was not until I added [Get-SMART](https://github.com/PipeItToDevNull/Get-Smart) to my [Get-Specs](https://github.com/PipeItToDevNull/Get-Specs) project. From inside your main repository we will run the following where \<repo url\> is your "send-mail" repo. You will need to run a commit and push this up to your origin.

> To pull down submodules into a newly cloned repo, use the "init" and "update" commands.

```bash
git submodule add <repo URL>
git submodule init
git submodule update
```

Once you have the "send-mail" submodule in place you can pull down updates into any main repositories with the following commands.

```bash
git submodule update --recursive --remote
```

Any script in the main repository can source the `send-mail.ps1` and execute the function it contains, that may look like this.

> I include the throw because I sometimes forget to clone the submodule

{% gist 39672ada0ac4013ac641902a1fc2a8e0 load.ps1 %}