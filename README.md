# OpenWRT config generator

Generates Pikapupu configuration for GL-MT300N-V2 mini
router. Pikapupu is an SSH layer 2 tunneling scheme for ham radio
operations in Jyväskylä region "pupunet" and Kaakon linkkiverkko.

## Flashing the firmware

The most recent firmware at the this time `gl-mt300n-v2-3.012.bin` has
a bug which makes SSH tun/tap not working. So it needs either a
downgrade or a upgrade. We downgraded it to `lede-mt300n-v2-2.271.bin`
which works.

Flash it using web GUI. Do not to keep current configuration. TODO CLI instructions.

## Generating configuration

Give the unit a name such as "pikapupu99", IP address such as 10.100.0.99 and a password:

```sh
./generate-pikapupu-config pikapupu99 10.100.0.99 PASSWORD
```

Upload it using the GUI. TODO CLI instructions.

## After flashing

Installing dependencies and disabling DHCP server

```sh
opkg update
opkg install openssh-client
service dnsmasq disable
service dnsmasq stop
```

## Adding SSH keys to tunnel server

Request the admin to add the given SSH key to the server with proper
security measures. The public key line should look like this:

```
command="pupubridge pikapupu99 kaakko",no-port-forwarding,no-X11-forwarding,no-agent-forwarding,no-pty SSH_PUBLIC_KEY_HERE
```

The server-side script [pupubridge](pupubridge) is located in this repo.
