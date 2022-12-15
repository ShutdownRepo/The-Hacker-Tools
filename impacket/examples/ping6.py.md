# ping6.py

[ping6.py](https://github.com/fortra/impacket/blob/master/examples/ping6.py) allows to do an ICMP6 ping to an IPv6 address from the specified IPv6 interface. Sufficient rights are needed on the machine to open a raw socket.

## Specificities

This script requires the following positional commands line arguments to work:

* required positional argument 1: `<src ip>`: the IPv6 address of the interface to use to send the ping request.
* required positional argument 2: `<dst ip>`: the IPv6 address of the target machine to ping.

```bash
# Send ping requests from "2001:861:4001:14f0:d7cd:f2cc:9344:a13a" to "2001:861:4001:14f0::2791:ec35"
sudo ping6.py "2001:861:4001:14f0:d7cd:f2cc:9344:a13a" "2001:861:4001:14f0::2791:ec35"
```
