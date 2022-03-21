---
title: "Using .deb files on non-debian systems"
tags:
  - linux
last_modified_at: '2022-03-21'
---

## References
While using [Solus](https://getsol.us/home/) I found some apps that were not in the repos like [Obisidian](https://obsidian.md) and [Tabby](https://tabby.sh). I stumbled upon [this post](https://discuss.getsol.us/d/7609-how-to-install-microsoft-edge-on-solus-budgie) on the Solus forums that talked about using `binutils` to run Edge from the official .deb package.

From this post I discovered the same process worked for any .deb package I could find (as long as your dependencies are satisfied).

1. Install the `binutils` package and download the target .deb package.
2. Run `ar xv` against your .deb file

1. Install the `binutils` package and download the target .deb package.

    ```bash
     ar xv ./edge.deb                    
    x - debian-binary
    x - control.tar.xz
    x - data.tar.xz
    x - _gpgorigin
    ```

    > 📝 We only need `data.tar.xz` everything else can be deleted

3. Extract the `data.tar.xz` 
    ```bash
     tar -xvf ./data.tar.xz
    ./
    ./etc/
    ./etc/cron.daily/
    ./opt/
    ./opt/microsoft/
    ./opt/microsoft/msedge-beta/
    ./opt/microsoft/msedge-beta/MEIPreload/
    ...
    ```

    > 📝 You can delete the data tar file now too

4. You are left with a file structure that will look familiar
    ```bash
     ls 
    etc  opt  usr
    ```

For Edge the executable is  `./opt/microsoft/msedge-beta/msedge`, but other packages will vary. In most cases you can execute the binary and be "done" at this point. Place the root of this relative path anywhere you want, I use `~/bin`.

For bonus points take the pre-made `.desktop` file out of `./user/share/applications/` and put it in `~/.local/share/applications` (correct the executable path in this file). You may need to take an icon file from `./user/share/icons/*` and place them in the corresponding `~/.local/share/icons` directory.