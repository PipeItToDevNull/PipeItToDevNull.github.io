# Using Dislocker to read Bitlocker volumes on Linux
I normally run dual boot on my desktop and encrypt both Linux and Windows, I spend more time on the Linux side of things and sometimes I need to get one or two files off my Windows host that are not stored in my Nextcloud. Dislocker makes this a breeze, it is an application that mounts an NTFS volume encrupted with Bitlocker as a FUSE device. 

Dislocker can be installed from most distros repositories, (I know at least Debian and the AUR).
```bash
sudo apt install dislocker
```

We need to make directories to mount both the FUSE file to and the resulting loop device. 
```bash
sudo mkdir /mnt/windows /mnt/dislocker
```

I use passphrases on my bitlocker disks, to keep things simple and because my desktop lacks a TPM, so my mount command will use the `-u` flag for user password. This will mount the `dislocker-file` FUSE device at `/mnt/dislocker/dislocker-file` which we will then mount again so that our resulting filesystem appears at `/mnt/windows`.

Check the man pages for other mount methods including `--recovery-password` which will interactively request a recovery password segment by segment validating each chunk as it goes. 
```bash
sudo dislocker -v -u -V /dev/sdd4 /mnt/dislocker/
sudo mount /mnt/dislocker/dislocker-file /mnt/windows
```

The documentation mentions that things can go bad should you try to reboot or shutdown with this FUSE system still mounted. To unmount the entire system cleanly run the following (while nothing in these directories are in use).
```bash
sudo umount /mnt/windows
sudo umount /mnt/dislocker
```