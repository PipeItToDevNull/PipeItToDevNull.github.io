You need the `rclone` binary installed, I get mine from my "scoop.sh" package manager. 

## Configure your remote
Run `rclone config` to open our configuration menu.

1. Press "n" to add a new remote
2. Choose a name for your remote
3. A large list pops up of known storage solutions, choose "5" for Backblaze B2
4. Enter your Account ID or Application Key ID (these are how you pushed data into B2)
5. Enter your Application Key 
6. You are asked if you want to "hard delete" or "hide files" when they are deleted from this remote. We want to use "false" to prevent stupid accidents.
7. We do not want to edit the advanced config, hit "n"
8. You are presented with the completed config now, you can accept it with "y"
9. Press "q" to end or "n" to make another remote

> 📝To find where your rclone config is being written to, run `rclone config file`

## Explore the remote
To list your buckets in the remote run `rclone lsd <remoteName>:`

To list the contents of a bucket run `rclone lsd <remoteName>:<buketName>

## References
Official docs
* https://rclone.org/b2/