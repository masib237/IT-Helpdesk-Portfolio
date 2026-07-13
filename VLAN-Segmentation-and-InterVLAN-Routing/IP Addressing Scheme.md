# IP Addressing Scheme

## Network Overview

Each VLAN was assigned its own subnet.

| VLAN | Purpose | Network | Default Gateway |
|---|---|---|---|
| VLAN 10 | HR Department  | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20 | IT Department 2 | 192.168.20.0/24 | 192.168.20.1 |
| VLAN 30 | Finance Department 3 | 192.168.30.0/24 | 192.168.30.1 |

---

# Infrastructure Devices

| Device | IP Address | Purpose |
|---|---|---|
| DHCP Server | 192.168.20.2 | Provides IP addresses |
| Router VLAN 10 Interface | 192.168.10.1 | VLAN 10 Gateway |
| Router VLAN 20 Interface | 192.168.20.1 | VLAN 20 Gateway |
| Router VLAN 30 Interface | 192.168.30.1 | VLAN 30 Gateway |

---

# Client Devices

Client PCs received addresses dynamically through DHCP.
