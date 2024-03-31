# ubiquiti

## edgemax

configuration: `/config/config.boot `

show available commands: `?`

`show arp`

`show interfaces`

### configure

`show interfaces ethernet eth0 address`

```
delete interfaces ethernet eth0
set interfaces ethernet eth0
commit | save
```

## unifi

ephemeral network configuration: `/etc/udhcpc/udhcpc`

fallback ip is 192.168.1.20/24

routes must be set with commands (`ip route`?)

show status and version: `info`

inform controller: `set-inform http://172.28.16.2:8080/inform`

### telnet

temperatures: swctrl env show
