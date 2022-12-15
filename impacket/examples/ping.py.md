# ping.py

[ping.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/ping.py) allows to do an ICMP ping to an IPv4 address from the specified IPv4 interface. Sufficient rights are needed on the machine to open a raw socket.

## Specificities

This script requires the following positional commands line arguments to work:

* required positional argument 1: `<src ip>`: the IPv4 address of the interface to use to send the ping request.
* required positional argument 2: `<dst ip>`: the IPv4 address of the target machine to ping.

```bash
# Send ping requests from "192.168.10.15" to "192.168.10.16"
sudo ping.py "192.168.10.15" "192.168.10.16"
```
