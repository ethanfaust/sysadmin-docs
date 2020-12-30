## Create
```
fdisk
t 8e
pvcreate /dev/sda1
vgcreate extm2 /dev/sda1
lvcreate -l 100%FREE -n backup extm2
cryptsetup luksFormat /dev/extm2/backup
cryptsetup open /dev/extm2/backup extm2backup
mkfs.ext4 -m 1 /dev/mapper/extm2backup
mount /dev/mapper/extm2backup /mnt
```

## Close
```
umount /mnt
cryptsetup close /dev/mapper/extm2backup
```

## Extend
```
lvextend -r --size +5G /dev/fedora/root
```
