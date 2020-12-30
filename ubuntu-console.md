In newer ubuntu releases console is disabled by default

To enable, e.g. for KVM
```
sudo systemctl start serial-getty@ttyS0.service
sudo systemctl enable serial-getty@ttyS0.service
```
