## Problem
Copy files from kvm guest to kvm host. Guest has no network access.

## Solution
Create container file on host with filesystem. Attach as block device to guest. Mount, copy files, unmount. Mount from host.

## Steps
```
# host

# pick a sensible size container to fit files, in my case 10 MiB
dd if=/dev/zero of=/local/tmp/container.img bs=1M count=10
mkfs.ext4 /local/tmp/container.img
virsh attach-disk guest-name /local/tmp/container.img vdb
virsh console guest-name

# guest
lsblk
mount /dev/vdb /mnt
cp target0 /mnt/
...
umount /mnt
# exit guest (e.g. ctrl+])

# host
virsh detach-disk guest-name vdb
mount -o loop /tmp/share/container.img /mnt
cd /mnt
cp target0 /dst-path/
...
umount /mnt
rm -rf /tmp/share

```

😎
