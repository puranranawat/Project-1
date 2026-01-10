# Network Design
This section gives the detailed network design.

[Assumptions](#assumptions) | [Network Design Diagrams and Justifications](#network-design-diagrams-and-justifications) | [WiFi Design](#wifi-design) | [Address Allocations](#address-allocations) | [Recommended Hardware](#recommended-hardware) | [Plan](./plan.md) | [Cloud Services](./cloud.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

---

## Assumptions

The scenario does not specify all details. The following assumptions were made to complete the network design:

1. **Headquarters (HQ) location (city):** Brisbane, QLD, Australia  
2. **Branch locations (cities) (minimum 3):**
   - Sydney, NSW
   - Melbourne, VIC
   - Perth, WA
3. **Number of staff in headquarters:** 65 employees  
4. **Number of staff in one branch office (designed branch network):** 25 employees (Sydney branch)

---

## Network Design Diagrams and Justifications

### Network Design Diagrams (draw.io / diagrams.net)

The network design includes one diagram for the headquarters and one for the Sydney branch office. Both diagrams were created using **draw.io / diagrams.net**.

- HQ diagram (drawio): `./diagrams/HQ_Network.drawio`
- Sydney branch diagram (drawio): `./diagrams/Sydney_Branch_Network.drawio`

> Ensure the drawio files are stored in the GitHub repository and images are embedded below.

#### Headquarters Network Diagram
![Headquarters Network Diagram](./diagrams/HQ_Network.png)

#### Sydney Branch Network Diagram
![Sydney Branch Network Diagram](./diagrams/Sydney_Branch_Network.png)

---

### Key Network Design Decisions (Justifications)

#### 1) Use of a Perimeter Firewall (HQ and Branch)
A dedicated perimeter firewall is deployed at both the HQ and the branch edge to:
- enforce security policies (allow/deny rules),
- provide application/traffic filtering,
- support IDS/IPS functions,
- provide VPN services for site-to-site connectivity.

This improves security by reducing the risk of unauthorised access and helping detect malicious traffic.

#### 2) Secure Site-to-Site VPN Connectivity (Sydney ↔ HQ)
A **site-to-site IPsec VPN** connects the Sydney branch to HQ so branch staff can securely access:
- HQ servers (booking services / internal applications),
- file storage,
- authentication services.

This design encrypts traffic across the public internet and reduces the cost compared to a dedicated leased WAN service.

#### 3) Segmentation using separate subnets (simple and justifiable)
To maintain a clear and secure design, the network separates different traffic types into different subnets:
- Corporate staff devices (wired LAN)
- Server subnet
- Staff WiFi subnet
- Guest WiFi subnet
- IoT/CCTV subnet
- Network management subnet

This improves security and reduces the impact of threats, while avoiding advanced designs that are difficult to justify (e.g., complex VLAN implementations).

#### 4) Dedicated Secure Server Subnet at HQ
Servers are grouped into a dedicated **HQ server subnet**. Access is restricted via firewall rules:
- only authorised staff/services can reach servers,
- guest WiFi and IoT networks cannot access servers directly.

This supports confidentiality and integrity of critical systems and data.

#### 5) Guest Network Isolation
The guest WiFi network is isolated so that:
- guests can access internet only,
- guests cannot access internal corporate systems, printers, CCTV or servers.

This reduces risk from unmanaged devices.

---

## WiFi Design

WiFi is required at both HQ and Sydney branch for staff mobility and productivity, and for controlled guest internet access.

### SSIDs
Two SSIDs are configured at both HQ and branch:

- Staff SSID: `TRUELEC-STAFF`
- Guest SSID: `TRUELEC-GUEST`

### WiFi Security Settings (Important settings and values)

| WiFi Setting | TRUELEC-STAFF | TRUELEC-GUEST |
|---|---|---|
| SSID | TRUELEC-STAFF | TRUELEC-GUEST |
| Security Mode | WPA3-Personal (preferred) / WPA2-AES fallback | WPA2-AES |
| Password Policy | Minimum 12 characters, change every 90 days | Rotated regularly (weekly/monthly) |
| Network Access | Internal resources allowed | Internet-only |
| Client Isolation | Not required | Enabled |
| DHCP | Enabled | Enabled |
| DNS | Internal DNS (HQ) | Public DNS |
| Logging/Monitoring | Enabled | Enabled |

### Wireless Performance / Channel Plan
- Dual-band is enabled: **2.4 GHz + 5 GHz**
- 5 GHz is preferred for performance and reduced interference
- 2.4 GHz supports broader coverage and compatibility
- 2.4 GHz channels set to **1 / 6 / 11** to avoid overlap
- Access points are placed to cover:
  - HQ: reception, offices, meeting rooms
  - Sydney branch: open workspace + meeting room

---

## Address Allocations

### IP Addressing Requirements (Assessment Rules)
The addressing plan complies with the assessment rules:
- Only **/16** and **/24** subnet masks are used
- The first octet (A in A.B.C.D) must be the last two digits of a group member student ID
- Group member IDs end in **67**, therefore all IP addresses start with **67.x.x.x**
- Private IP addressing (e.g., 192.168.x.x) is not used anywhere

---

### Headquarters (Brisbane) IPv4 Address Allocation

| Network Purpose | IPv4 Range | Mask |
|---|---|---|
| HQ Wired Staff LAN | 67.10.0.0/16 | /16 |
| HQ Servers (Secure Server Subnet) | 67.20.10.0/24 | /24 |
| HQ Staff WiFi | 67.20.20.0/24 | /24 |
| HQ Guest WiFi | 67.20.30.0/24 | /24 |
| HQ IoT / CCTV / RFID | 67.20.40.0/24 | /24 |
| HQ Network Management (Firewall/Switch/AP Mgmt) | 67.20.50.0/24 | /24 |

---

### Branch (Sydney) IPv4 Address Allocation

| Network Purpose | IPv4 Range | Mask |
|---|---|---|
| Sydney Wired Staff LAN | 67.30.0.0/16 | /16 |
| Sydney Staff WiFi | 67.30.10.0/24 | /24 |
| Sydney Guest WiFi | 67.30.20.0/24 | /24 |
| Sydney IoT / CCTV | 67.30.30.0/24 | /24 |
| Sydney Network Management | 67.30.40.0/24 | /24 |

---

### Site-to-Site VPN Transit Subnet (HQ ↔ Sydney)
A dedicated VPN transit subnet is allocated for VPN tunnel endpoints:

| Network Purpose | IPv4 Range | Mask |
|---|---|---|
| VPN Transit Subnet | 67.99.99.0/24 | /24 |

Example VPN gateway IPs:
- HQ VPN gateway: 67.99.99.1
- Sydney VPN gateway: 67.99.99.2

---

## Recommended Hardware

The following equipment is recommended to support the design. All equipment must be selected with:
- business-grade reliability,
- VPN capability,
- secure firewalling,
- scalable switching,
- WiFi 6 access.

> Note: Insert final product links and AUD prices after selecting products from official vendor websites.

### Headquarters (Brisbane) Recommended Hardware

| Equipment | Minimum Specifications | Qty | Price (AUD) | Link |
|---|---|---:|---:|---|
| Firewall (NGFW) | IPsec VPN, IDS/IPS, 1Gbps+ throughput, logging | 1 | $____ | (insert link) |
| Router / Internet Gateway | Business-grade, dual WAN capable | 1 | $____ | (insert link) |
| Core Switch | 48-port Gigabit Managed Switch, Layer 2 managed features | 1 | $____ | (insert link) |
| Access Switch | 24-port Gigabit Managed Switch | 2 | $____ | (insert link) |
| Wireless Access Point (WiFi 6) | Dual-band WiFi 6, PoE support, business-grade | 4–6 | $____ | (insert link) |
| Server (if hosted on-prem) | 8+ cores CPU, 32GB+ RAM, RAID storage | 1–2 | $____ | (insert link) |
| UPS | 1000VA+ for firewall/switch/servers | 2 | $____ | (insert link) |

---

### Branch (Sydney) Recommended Hardware

| Equipment | Minimum Specifications | Qty | Price (AUD) | Link |
|---|---|---:|---:|---|
| Firewall (NGFW) | IPsec VPN, IDS/IPS, logging | 1 | $____ | (insert link) |
| Router / Internet Gateway | Business-grade routing capability | 1 | $____ | (insert link) |
| Switch | 24-port Gigabit Managed Switch | 1 | $____ | (insert link) |
| Wireless Access Point (WiFi 6) | Dual-band WiFi 6, PoE | 2 | $____ | (insert link) |
| UPS | 650VA+ | 1 | $____ | (insert link) |
