# BIND
* http://en.wikipedia.org/wiki/BIND

## Config
/var/named/zones/internal.zone 

```
$ORIGIN internal.
$TTL 86400
@   IN    SOA   dns.internal. admin.internal. (
  2014040601
  28800
  3600
  604800
  38400 )
 
    IN    NS    dns.internal.
 
router      IN    A     192.168.1.1
machine0    IN    A     192.168.1.10
machine1    IN    A     192.168.1.11

web         IN    CNAME www
wiki        IN    CNAME w
db          IN    CNAME database
```

/var/named/zones/rev.1.168.192.in-addr.arpa 
```
$ORIGIN 1.168.192.in-addr.arpa.
$TTL 86400
@ IN SOA dns.internal. admin.internal. (
  2014040602;
  28800;
  604800;
  604800;
  86400
  )
            IN    NS    ns1.internal.
1           IN    PTR   router.internal.
10          IN    PTR   machine0.internal.
11          IN    PTR   machine1.internal.
```

/etc/named.conf
```
zone "internal" IN {
  type master;
  file "/var/named/zones/internal.zone";
};
 
zone "1.168.192.in-addr.arpa" {
  type master;
  file "/var/named/zones/rev.1.168.192.in-addr.arpa";
};
```
