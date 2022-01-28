---
title:  "Using rclone to recover data from Backblaze buckets"
tags:
  - backblaze
  - rclone
---
## ReferencesYou need the `rclone` binary installed, I get mine from my "scoop.sh" package manager. 

> ❗ There are important notes on interacting with Backblaze via Rclone in the [official docs](https://rclone.org/b2/). Read them.

## Configure your remote
Run `rclone config` to open our configuration menu.

1. Press "n" to add a new remote
2. Choose a name for your remote (this name is used later)
3. A large list pops up of known storage solutions, choose "5" for Backblaze B2
4. Enter your Account ID or Application Key ID (these are how you pushed data into B2)
5. Enter your Application Key 
6. You are asked if you want to "hard delete" or "hide files" when they are deleted from this remote. We want to use "false" to prevent stupid accidents.
7. We do not want to edit the advanced config, hit "n"
    > ❗ If you are using encryption that is handled in the next step and does not change the initial remote setup
8. You are presented with the completed config now, you can accept it with "y"
9. Press "q" to end or "n" to make another remote

    > 📝To find where your rclone config is being written to, run `rclone config file`

### Remote with encryption
Setting up an encrypted remote will build upon an existing remote from the step above. You cannot setup an encrypted remote from scratch. To setup our encrypted remote we need to know both the remote name as well as the specific bucket we want. Run `rclone lsd {remote}:` to get the list of available buckets and make not of it.

1. `rclone config` again to setup our encrypted remote.
2. Press "n" to add a new remote
3. Choose a name for this remote ("existingRemote-crypt" is what I use)
4. Press "12" to start the encrypted remote setup
5. 

## Basics
List remotes
```powershell
rclone listremotes
```

List buckets on remote (the colon is required)
```powershell
rclone lsd {remote}:
```

List files in a bucket
```powershell
rclone ls {remote}:{bucket}
```

## Explore the remote
To list your buckets in the remote:
```powershell
> rclone lsd b2:

-1 2022-01-25 13:55:05 -1 backuptest384595
```

To list the contents of a bucket run 
```powershell
> rclone ls b2:backuptest384595

64083579 WindowsTH-KB2693643-x64.msu
```

> 📝 If you list the contents of a remote and see `.bin` extensions on file where you do not expect, this designates the file and encrypted. See how to setup an encrypted rclone mount above.

## Pull from the remote
You should read over the page on [how copy works](https://rclone.org/commands/rclone_copy/) to understand the basics such as `--dry-run` and how rclone appends a trailing `/` automatically. The basics are `rclone copy --progress {remote}:{bucket}\file C:\Dest` when copying data out of Backblaze.
```powershell
> rclone copy --progress  b2:backuptest384595\WindowsTH-KB2693643-x64.msu ./
Transferred:       61.115 MiB / 61.115 MiB, 100%, 4.145 MiB/s, ETA 0s
Transferred:            1 / 1, 100%
Elapsed time:        15.8s
```

> 📝 Transfers
> 
> Backblaze recommends that you do lots of transfers simultaneously for maximum speed. In tests from my SSD equipped laptop the optimum setting is about `--transfers 32` though higher numbers may be used for a slight speed improvement. The optimum number for you may vary depending on your hardware, how big the files are, how much you want to load your computer, etc. The default of `--transfers 4` is definitely too low for Backblaze B2 though.
> 
> Note that uploading big files (bigger than 200 MiB by default) will use a 96 MiB RAM buffer by default. There can be at most `--transfers` of these in use at any moment, so this sets the upper limit on the memory used.