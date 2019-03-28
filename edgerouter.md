# Edgerouter X SSH layer 2 tunneling

Login to Edgerouter

```sh
sudo -H /bin/bash
ssh-keygen -t ed25519
```

1. Collect keys and add them to the VPN server.
1. Copy [tunnel](tunnel) script to `/root/tunnel`
1. `chmod +x /root/tunnel`
1. Add `/root/tunnel &` to /etc/rc.local

