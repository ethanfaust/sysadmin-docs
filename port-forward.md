## Make remote port available locally
Make port 3000 on remote machine show up as 3001 on local machine:
```
ssh -NL 3001:localhost:3000 remote.machine
```

## Forward traffic
Create SOCKS proxy on local port through remote machine (you can point your web browser at the port)
```
ssh -ND 9999 remote.machine
```
