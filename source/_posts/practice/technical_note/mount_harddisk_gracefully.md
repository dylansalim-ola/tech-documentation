---
title: Mount Harddisk gracefully
index_img: >-
  /images/h5_flutter_web/thumbnail.png
author: Dylan
tags:
  - Hardware
math: true
mermaid: true
date: 2024-10-04 12:27:00
---
Q: My Mac server is running out of disk space. I bought and attached an external hard drive to it. What's the best way to configure it? Desired behaviour: 1. Without changing application configuration, the system offload certain folders, e.g. /Users/ci/go/mod/ to the external hard drive. 2. The system or application shouldn't fail if the external hard drive was unplugged.

A:

Solution 1: Automounting an External Drive to specific folder using `/etc/fstab`

Step 1:  Find UUID of external drive
`diskutil info /Volumes/<Drive to map> | grep 'Volume UUID'`

Step 2: Create a folder to map specific disk
`sudo mkdir -p <Folder to map>`

Step 3: Add the UUID entry and map it to the folder we created earlier 

- Open `/etc/fstab` 
- Add the following UUID entry to the `/etc/fstab` 

`UUID=<UUID from step 1> <Folder to map> hfs rw,auto`




Solution 2:
Step 1: Create a backup folder
`mkdir -p /Users/ci/go/mod_fallback`

Step 2: Create a cron script to check if the Volume is mounted, use Symbolic links to dynamically links the folder

### automount-harddisk.sh
```bash
#!/bin/bash

# Check if the external drive is mounted
if mount | grep -q '/Volumes/ExternalDriveName'; then
    # If the external drive is mounted, ensure the symlink points to it
    if [ ! -L /Users/ci/go/mod ]; then
        sudo rm -rf /Users/ci/go/mod
        sudo ln -s /Volumes/ExternalDriveName/ci_go_mod /Users/ci/go/mod
        echo "External drive mounted. Symlink points to external drive."
    fi
else
    # If the external drive is not mounted, point to fallback
    if [ ! -L /Users/ci/go/mod ]; then
        sudo rm -rf /Users/ci/go/mod
        sudo ln -s /Users/ci/go/mod_fallback /Users/ci/go/mod
        echo "External drive not mounted. Using local fallback."
    fi
fi

```

Run this script periodically
`* * * * * /automount-harddisk.sh`



References: 
disk uuid mapping - https://www.redhat.com/sysadmin/etc-fstab