# Addressing Plan

Allocated block: **172.16.0.0/22** (172.16.0.0 – 172.16.3.255)
Total usable: 1022 hosts · Required: ~200 · Method: VLSM

| Zone | VLAN | Network | Mask | Gateway | Usable range | Broadcast | Usable | Req |
|---|---|---|---|---|---|---|---|---|
| Corporate | 10 | 172.16.0.0/25 | 255.255.255.128 | 172.16.0.1 | .1 – .126 | 172.16.0.127 | 126 | 100 |
| Wireless | 40 | 172.16.0.128/26 | 255.255.255.192 | 172.16.0.129 | .129 – .190 | 172.16.0.191 | 62 | 50 |
| Servers | 20 | 172.16.0.192/27 | 255.255.255.224 | 172.16.0.193 | .193 – .222 | 172.16.0.223 | 30 | 20 |
| OT | 50 | 172.16.0.224/28 | 255.255.255.240 | 172.16.0.225 | .225 – .238 | 172.16.0.239 | 14 | 14 |
| Management | 99 | 172.16.0.240/28 | 255.255.255.240 | 172.16.0.241 | .241 – .254 | 172.16.0.255 | 14 | 10 |
| DMZ | 30 | 172.16.1.0/29 | 255.255.255.248 | 172.16.1.1 | .1 – .6 | 172.16.1.7 | 6 | 6 |

## Design notes

- Subnets are allocated largest-first with no gaps between blocks.
- **OT and DMZ have zero headroom** — usable capacity equals the requirement.
  This is a deliberate trade-off: both zones are intentionally small and any
  growth should trigger a re-evaluation rather than silent expansion.
- 172.16.1.8 – 172.16.3.255 remains unallocated and is reserved for future zones.
