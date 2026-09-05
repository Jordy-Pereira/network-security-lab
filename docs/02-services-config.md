## VLANs and Routing

I created VLAN 10 for corporate and VLAN 20 for servers.

- Switchport VLAN 10 for FE0/1 and FE0/2
- Switchport VLAN 20 for FE0/3

To allow communication between different VLANs, I established a router on a stick with a trunk port, so corporate can reach services in the servers VLAN such as DHCP and, later, DNS.

**Switch — trunk configuration**

```
interface gigabitethernet0/1
 switchport mode trunk
```

**Router — subinterface configuration**

```
enable
configure terminal
interface gigabitethernet0/1
 no shutdown
 exit
interface gigabitethernet0/1.10
 encapsulation dot1q 10
 ip address 172.16.0.1 255.255.255.128
 exit
```

`no shutdown` turns on the physical port. `encapsulation dot1q 10` tells the subinterface to process frames tagged with VLAN 10. The IP address is the default gateway of the corporate VLAN.

## DHCP

I need user pools for the corporate and wireless VLANs.

**Corporate pool**

- Default gateway: 172.16.0.1
- Start IP address: 172.16.0.10 — .2 to .9 left for infrastructure
- Subnet mask: 255.255.255.128
- Maximum number of users: 100

I checked that 100 addresses do not overlap the broadcast address.

**Wireless pool**

- Default gateway: 172.16.0.129
- Start IP address: 172.16.0.139 — .130 to .138 left for infrastructure
- Maximum number of users: 50

Since the DHCP broadcast stops at the router, I configured `ip helper-address` as a DHCP relay so the router forwards the broadcast as a unicast to the DHCP server.

## Issues

**PC-CORP-2 could not reach the server**

PC-CORP-1 already reached the server with ping and PC-CORP-2 did not, so the problem had to be in PC-CORP-2 itself. I opened its configuration, checked the default gateway, and it was not configured.
