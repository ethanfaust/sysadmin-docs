```
sudo dnf upgrade --refresh
# suggest reboot if kernel was updated

sudo dnf install dnf-plugin-system-upgrade
sudo dnf system-upgrade download --releasever=33
sudo dnf system-upgrade reboot
```

* [Package Signing Keys](https://getfedora.org/security/)
