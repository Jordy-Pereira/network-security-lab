# Scope and Rules of Engagement

This document defines what this project touches and what it does not.

## In scope

- **The Packet Tracer lab.** Every device in `packet-tracer/it-ot-lab.pkt` is
  simulated. Attacks are demonstrated only here.
- **The own home network**, for passive traffic capture with Wireshark.
- **The own devices**, for command-line tools and captures.

## Out of scope

- Any network, device or service not owned.
- ISP infrastructure, neighbouring networks, and third-party systems.
- Active attacks against real devices of any kind.

Public DNS lookups and a traceroute to a public resolver were performed as
ordinary client traffic. No other interaction with external systems took place.

## Techniques

| Technique | How it was handled |
|---|---|
| Rogue DHCP | Simulated in Packet Tracer only |
| ARP poisoning | Documented from its signature; never executed |
| Port scanning | Only against the own virtual machine |
| Phishing analysis | Headers of messages received, with third-party data redacted |

## Data handling

- MAC addresses are redacted beyond the OUI.
- SSIDs and public IP addresses are not published.
- Raw capture files (`.pcapng`) are excluded from the repository; only annotated
  and sanitized screenshots are included.
- Credentials and shared secrets are replaced with `<REDACTED>`.
