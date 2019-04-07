# Edgerouter X SSH layer 2 tunneling

Login to Edgerouter

```
configure
delete interfaces ethernet eth3 address
commit
set interfaces bridge br0 address 10.101.5.6/16
set interfaces ethernet eth3 bridge-group bridge br0
commit

```sh
sudo -H /bin/bash
ssh-keygen -t ed25519
```

1. Collect keys and add them to the VPN server.
1. Copy [tunnel](tunnel) script to `/root/tunnel`
1. `chmod +x /root/tunnel`
1. Add `/root/tunnel &` to /etc/rc.local

## Example with oikopupu feature

rc.local or @reboot target in crontab:

```
/root/tunnel &
iptables -t nat -N PUPU_DNAT
iptables -N PUPU_FILTER     
iptables -t nat -A PREROUTING -i switch0 -j PUPU_DNAT
```

And in crontab add the following script (Edgerouter doesn't have systemd):

```
#!/bin/sh -eu
curl -Ss https://net.pupu.li/oikopupu?format=iptables | /sbin/iptables-restore --noflush
```
