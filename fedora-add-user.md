```
useradd efaust
usermod -a -G wheel efaust
sudo visudo
# look for wheel, make sure wheel group is allowed
```

ref: https://docs.fedoraproject.org/en-US/quick-docs/adding_user_to_sudoers_file/
