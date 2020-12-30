```
# host
virsh blockresize osdev /local/vm/osdev/disk 40G

# guest
dnf install cloud-utils-growpart
growpart /dev/vda 2
lsblk
pvresize /dev/vda2
pvs
df -hT | grep mapper
lvextend -l +100%FREE /dev/mapper/fedora-root

# if xfs
xfs_growfs /

# if ext4
resize2fs /dev/mapper/fedora-root
```
