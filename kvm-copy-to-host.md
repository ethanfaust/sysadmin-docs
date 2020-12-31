## Problem
Copy files from kvm guest to kvm host. Guest has no network access.

## Solution
Create container file on host with filesystem. Attach as block device to guest. Mount, copy files, unmount. Mount from host.

## Steps
```
# host
mkdir /tmp/share

# pick a sensible size, in my case 10 MiB
dd if=/dev/zero of=/tmp/share/container.img bs=1M count=10
mkfs.ext4 /tmp/share/container.img
virsh attach-disk guest-name /tmp/share/container.img vdb
virsh console guest-name

# guest
lsblk
mount /dev/vdb /mnt
cp target0 /mnt/
...
umount /mnt

# host
virsh detach-disk guest-name vdb
mount -o loop /tmp/share/container.img /mnt
cd /mnt
cp target0 /dst-path/
...
umount /mnt
rm /tmp/share/container.img

```
