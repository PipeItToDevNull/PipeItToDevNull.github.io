---
title: "Getting Started with Obsidian and GitHub"
tags:
  - obsidian
  - git
  - github
last_modified_at: '2022-09-04'
---
Using [GitHub](https://github/com) with [Obsidian](https://obsidian.md) is a free way to sync and version control your vault. I have used a personal git server and GitHub to manage/sync my vaults for their entire lifetime.

> 📝 I do not recommend the use of GitHub Desktop

* TOC 
{:toc}

## GitHub repository setup
1. If you do not have an account with GitHub, you can create one [here](https://github.com/signup).
2. After you have created an account and logged in, you can create a new repo from the + sign in the top right.
 
    ![github new repo](/assets/images/2022-09-04-github-obsidian/github-new-repo.png)
3. Choose a repo name, make it Public or Private as you see fit. **Tick Add Readme** 

    ![github repo settings](/assets/images/2022-09-04-github-obsidian/github-repo-settings.png)

4. You should be left with a repo resembling this. If you are presented a "how to" that means you did not include the ReadMe. Delete the repo via the Settings and re-make it.

    ![github bare repo](/assets/images/2022-09-04-github-obsidian/github-bare-repo.png)

## Create a GitHub Personal Access Token (PAT)
These GitHub docs are decent enough: [Creating a personal access token - GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

## Git setup
1. Install git for [Windows](https://git-scm.com/download/win), [MacOS](https://git-scm.com/download/mac), or [Linux](https://git-scm.com/download/linux).
2. Open a PowerShell window or Terminal, this should open in the root of your user directory. 
 
    > 📝 For the purpose of this guide, we will put our repo here, if you want to put it somewhere else `cd` there but we will not be covering it.

3. To pull down the bare repository from GitHub run `git clone <url of the repo>` 

    > 📝 Get the URL for the repo out of your browser.

    > 📝 You will be asked to log into GitHub, or for a password. If you are asked for a plain password use the Personal Access Token (PAT) you generated above.

4. You can now open your File Explorer to find a directory named the same thing as your Repo. It will have a ReadMe file inside that you can remove. 

    > 📝 The repo is located in the root of your User Profile. Such as `C:\Users\User\Obsdidian_Repo` or `~/Obsidian_Repo`

## Vault setup
1. Add any files you want to into the repo. The root of your repository should be treated as the root of your vault. 
2. Once files are added open a new PowerShell and run the following:
    ```powershell
    cd Obsidian_Repo
    git add .
    git commit -a -m 'initial commit'
    git push
    ```

You should now be able to view your files online in your GitHub repo.

## Obsidian git plugin setp
1. From the plugins pane in Obsidian add the "Obsidian Git" plugin.
2. Configure the various timers as you see fit to automatically sync and push your vault. My settings are below:

    ![git backup0](/assets/images/2022-09-04-github-obsidian/git-backup0.png)
 
    ![git backup1](/assets/images/2022-09-04-github-obsidian/git-backup1.png)
3. From now on the auto-magical timers should keep your vault syncing to the cloud without issue!