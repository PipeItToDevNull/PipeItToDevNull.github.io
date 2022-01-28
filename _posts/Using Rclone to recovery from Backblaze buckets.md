You need the `rclone` binary installed, I get mine from my "scoop.sh" package manager. 

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
Setting up an encrypted remote will build upon an existing remote from the step above. You cannot setup an encrypted remote from scratch. We will run `rclone config` again to setup our encrypted remote.

1. Press "n" to add a new remote
2. Choose a name for this remote ("existingRemote-crypt" is what I use)
3. 

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
## References
Official docs
* https://rclone.org/b2/