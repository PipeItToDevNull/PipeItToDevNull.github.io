---
title:  "Basic Tools for This Sysadmin"
last_modified_at: '2022-01-23'
---
Every techy you talk to will have their own list of "must-haves" and "best tools" to use, this is mine. You can replace half of these with something that does the job just as well, or maybe better, but for right now these work for me. I put a high value on solutions being cross-platform, I want to maintain one config to do the same task on every computer I interact with. All the solutions noted here are cross platform to Mac, Linux, and Windows except MRemoteNG and Scoop.

## Command Line
I consider the command line critical for any good admin, and even helpdesk. It is more efficient, more powerful and sometimes the only option for certain products or tasks. Even Office365 and Azure lean heavily on PowerShell for many fundamental tasks.

#### PowerShell
While mainly a Windows focused shell, I do use this on Linux as well just to keep my profile the same across all platforms (why use or force two shells to act the same). If you work on Windows or anything in the Microsoft Cloud you must know at least some basic [PowerShell](https://vignette.wikia.nocookie.net/mario/images/b/b0/MKWii_Blue_Shell.png/revision/latest?cb=20171019083814).

#### Scoop
Anyone who has spent time in the Linux realm knows the power of a package manager. [Scoop](https://scoop.sh/) is a Windows package manager. It may not be the first, or the most popular but it is quick, CLI only, and runs as a user without admin just fine. Scoop and all of its applications are put in a single directory making use simple and clean. 

I install my entire environment using this tool and a [messy script](https://git.dev0.sh/piper/scoop_install/src/branch/master/scoop_install.ps1).

#### Git
A very powerful tool, while generally associated with "coding" it serves many uses beyond just holding code. 

I use [Git](https://www.git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F) to store and control all the scripts I use across my environments, I know many people (including myself) have used or continue to use a random network share holding bare files that have no control on them aside from ACLs but why maintain such little control over files that most likely run with relatively high powers across your environment. 

Git allows you to exercise version control and history against any plain text file, you can track any file line by line throughout its life and revert or merge changes to roll back or create an entirely new file. In addition to storing my various PowerShell or other code related projects in Git I also version control: 
* Ansible configurations and files
    * I check in all the files that I handle in my CFM playbooks into Git so I can track each change made for compliance and accountability. This is a great way to control Linux or Network devices to track and correct unauthorized or accidental changes.
* Network maps made using LaTeX and Tikz 
    * For compliance, having version control helps and that is not possible with an image file
* Networking device configurations 
    * Backup and restore templates from a secure and controlled system that maintains history of every change
* Exported policies from ePO
    * Because why not, its a good backup
* Various application configurations
    * I push these out from GPO or other such methods, but I gain that control over changes and tracking for audit purposes.

#### PGP/GPG
We all remember PKI from our IT courses, if you do not then say "Hi" to [Alice and Bob](https://www.ibm.com/blogs/blockchain/wp-content/uploads/2018/06/di-pki.png). I most actively use [GPG](https://gnupg.org/) (GNU implementation of PGP) to sign my Git commits, but I also have this in place on my personal email mostly just for signing. When it comes to simple, cross platform and quick file encryption for storing or sharing though, it does not get much better. There is certainly a learning curve to this but I think learning the basics are worth it.

I store my key on my [YubiKey](#YubiKey), for extra nerd points (and so I use a PIN instead of a passphrase when signing)

#### Oh My Posh
A big helper is a nice prompt in your shell, [Oh My Posh3](https://ohmyposh.dev/) is shell agnostic so you can get the same look and information regardless of your shell with one configuration. 

But why is a fancy shell prompt useful?
* Conditional statements to show a hostname and change colour when in an SSH session
* Visible indications of being Root or having Sudo "active"
* Customized/simplified paths to keep track of where you are easier
* Git status directly in your prompt
* Exit codes from your last commands
* Duration of your last command
* Time stamps to know when each command was ran or started and finished
* Various environmental indicators such as Docker, environment/shell version etc.

#### PSReadLine
This is actually a PowerShell module, but it is critical to my terminal centric life. [PSReadLine](https://docs.microsoft.com/en-us/powershell/module/psreadline/) brings many QOL (quality of life) improvements to PowerShell and gets you some familiar functions from BASH/ZSH/FSH that Linux vets may be missing.

In my PowerShell profile I enable several functions from this module, you can read about them all [here](https://docs.microsoft.com/en-us/powershell/module/psreadline/set-psreadlineoption?view=powershell-7.2) and see what I configure in [my PowerShell profile](https://git.dev0.sh/piper/powershell_profile/src/branch/master/personal_profile.ps1). The highlights of my changes are Vi navigation and tab-completion for modules and total line completion from your `history`.

## GUI
#### Tabby
[Tabby](https://github.com/Eugeny/tabby) is the latest terminal I have settled on, I have also played with [ConEmu](https://conemu.github.io/), [Hyper](https://github.com/vercel/hyper), and likely several others. It of course has tabs like any other proper offering in the last decade but it is also cross platform. Tabby also features some basic plugins that really just give base functionality of any modern terminal.

Tabby can maintain a list of SSH connections with passwords (stored in your credential manger) and when initiated can handle SFTP in a graphical drop down, super handy.

#### MRemoteNG
We use RDP, some of us use RDP all day, some of us RDP to multiple servers at the same time. Putting all these sessions into one tabbed window is a God send, I [MRemoteNG](https://mremoteng.org/) over the Windows 10 Remote Desktop UWP app (I dislike most of UWP).

This can also do SSH, Telnet, VNC, and even HTTPS windows while maintaining all your hosts in a nice tree view.

#### Obsidian
Keeping notes, documenting, and just having a personal knowledge base is something I have struggled with. [Obsidian](https://obsidian.md/) is the latest iteration of that effort. It is markdown based to preserve the independence of your data from the solution as well as to make it easy to interact with in other apps, scripts, or version control systems. 

I use git to sync my "vault" to my server and other devices. I also take advantage of the markdown and git integration to publish this blog directly out of its pages, see my [brief first post]({% post_url 2021-12-29-publishing-pages-obsidian %}) about how I do that.

#### Espanso
Text-Expanders, a concept I didn't know about a year ago but has forever changed my life. Text-Expanders allow you to take a 'trigger' and replace it with some other text. A great example and one I use often is:

> ;;expired <- Trigger turns into the text below
> 
> To change your password choose 'sign in options' and click the 'key' symbol. Enter your current password (the same as sharepoint/email). You will be asked to create a new password. Once set you will be kicked out with 'you must use a smart card to login', this is expected. Choose 'sign in options' again and go back to the card symbol to sign in with your PIN.

 [Espanso](https://espanso.org/) specifically is open source and again, cross-platform.

#### Kate
[Notepad++](https://notepad-plus-plus.org/) or any other real text editor works here, evolve beyond Notepad.exe. [Kate](https://kate-editor.org/) is cross-platform and developed by KDE, it has some basic IDE functions like Git support and of course syntax highlighting.

### Hardware
#### YubiKey
Hardware tokens are a pretty niche utility, but I think having a [YubiKey](https://www.yubico.com/) to at least play around with is a good idea. I have used mine to hole MFA tokens (TOTP Seeds read from an app), SmartCard certificates (for login to workstations/servers), but now I am only using it to hold my GPG keys for signing. Check out the [list of sites that work with Yubi](https://www.yubico.com/works-with-yubikey/catalog/?sort=popular) to know what you can add a Yubi to in order to further secure your logins.