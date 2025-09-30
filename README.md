# CCNA VLAN,TRUNKING & ROAS LAB (packet tracer)

``
## What I built
I designed a small enterprise-style network and implemented:
- IP subnetting (1 × /24 → 4 × /26) for department isolation  
- VLAN configuration and trunking between switches (802.1Q, native VLAN)  
- Router-on-a-Stick (subinterfaces) for inter-VLAN routing  
- Secure management via SSH from my Ubuntu VM and GitHub for version control

---

## Topology
![Network topology](topology.jpeg)

*(Uploaded from my laptop and included here so reviewers can see the design immediately.)*

---

## Quick highlights
- **Subnetting:** `192.168.1.0/24` split into **4 × /26** subnets (shows IP planning).  
- **VLANs:** Sales / Engineering / HR / Service (separate broadcast domains).  
- **Trunking:** 802.1Q trunk links between switches; native VLAN configured.  
- **Routing:** Router-on-a-Stick with subinterfaces for each VLAN.  
- **Secure management:** SSH from Ubuntu VM to devices; pushed configs to GitHub.  
- **Files included:** Packet Tracer file + per-device configs in `/configurations/`.
```
```
---

## Subnets & VLAN mapping (summary)
| VLAN ID | Name        | Subnet (mask)         | Gateway (router sub-int)   |
|--------:|-------------|------------------------|----------------------------|
| 10      | Sales       | `192.168.1.0/26`       | `192.168.1.62`              |
| 20      | Engineering | `192.168.1.64/26`      | `192.168.1.126`             |
| 30      | HR          | `192.168.1.128/26`     | `192.168.1.190`            |
| 40      | Service     | `192.168.1.192/26`     | `192.168.1.254`            |

```
---

## Small example
**Router (R1) — subinterface example:**
text
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.62 255.255.255.192
!
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.126 255.255.255.192

!
interface GigabitEthernet0/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 1001
!
## Switch (SW1) — VLAN + trunk example:
 interface GigabitEthernet0/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk native vlan 1001
``
