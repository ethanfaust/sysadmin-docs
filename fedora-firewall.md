## List existing config
```
firewall-cmd --get-zones
firewall-cmd --info-zone=external

firewall-cmd --direct --get-all-rules
```

## Port Forwarding
```
# add
firewall-cmd --zone=external --add-forward-port=port=8448:proto=tcp:toaddr=192.168.2.2 --permanent

# remove
firewall-cmd --zone=external --remove-forward-port='port=8448:proto=tcp:toport=:toaddr=192.168.2.2' --permanent
```

## Add Service
```
firewall-cmd --zone=internal --add-service=dns --permanent
```

## Direct rules
```
firewall-cmd --permanent --direct --add-rule ipv4 filter FORWARD 0 -m state --state ESTABLISHED,RELATED -i enp4s0f3u2 -o enp2s0 -j ACCEPT
```

## Reload (e.g. to apply changes)
```
firewall-cmd --reload
```
