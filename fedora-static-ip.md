```
nmcli connection show
nmcli connection edit enp1s0
set ipv4.addresses 192.168.1.42/24
set ipv4.dns 192.168.1.1
set ipv4.gateway 192.168.1.1
print
save persistent
 
sudo systemctl restart NetworkManager
```

## Remove
```
remove ipv4.addresses 192.168.1.42/24
```
