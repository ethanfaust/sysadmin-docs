# Problem
Copy files from kvm guest to kvm host. Guest has no network access.

# Solution 1: Mount guest disk
```
dnf install libguestfs-tools libguestfs
guestmount -a ./disk -i --ro /mnt
```

# Solution 2: Mount within guest
Create container file on host with filesystem. Attach as block device to guest. Mount, copy files, unmount. Mount from host.

## Prepare guest
(on guest, e.g. ```virsh console guest-name```)
```
# determine total size of files to copy, keep for later
ls -alh ...
# list block devices
lsblk
# look for a suitable volume name not yet in use, e.g. vdb, keep for later
```

## Prepare host
(on host)
```
# pick a sensible size container to fit files, in my case 10 MiB
dd if=/dev/zero of=/local/tmp/container.img bs=1M count=10
mkfs.ext4 /local/tmp/container.img
virsh attach-disk guest-name /local/tmp/container.img vdb
```

## Copy from guest
(on guest)
```
lsblk
# validate that vdb shows up, otherwise something went wrong
mount /dev/vdb /mnt
cp target0 /mnt/
...
umount /mnt
# exit guest (e.g. ctrl+])
```

## Copy to host
(on host)
```
virsh detach-disk guest-name vdb
mount -o loop /local/tmp/container.img /mnt
cd /mnt
cp target0 /dst-path/
...
umount /mnt

# clean up
rm /local/tmp/container.img
```

😎
