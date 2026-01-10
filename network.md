# Network Design
This section gives the detailed network design.

[Assumptions](#assumptions) | [Network Design Diagrams and Justifications](#network-design-diagrams-and-justifications) | [WiFi Design](#wifi-design) | [Address Allocations](#address-allocations) | [Recommended Hardware](#recommended-hardware) | [Plan](./plan.md) | [Cloud Services](./cloud.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

---

## Assumptions

The scenario does not specify all technical details. The following assumptions are made to complete the network design:

1. **Headquarters (HQ) location:**  
   Truelec headquarters is located in **Sydney, Australia**.

2. **Branch locations (minimum 3):**  
   Truelec has branch offices located in:
   - **Melbourne, Australia**
   - **Brisbane, Australia**
   - **Perth, Australia**

3. **Number of staff in HQ:**  
   The HQ has **70 staff members** (within the required 50–75 range).

4. **Number of staff in one branch office (designed branch network):**  
   The Melbourne branch has **25 staff members** (within the required 15–30 range).

5. **Internet/WAN availability:**  
   Each site has an ISP connection capable of supporting business communications and a site-to-site VPN.

6. **Business requirements:**  
   - HQ hosts core business services including booking application servers and file storage.
   - Branch staff require secure access to HQ services via VPN.
   - Guest WiFi must not access internal systems.

---

## Network Design Diagrams and Justifications

The network has been designed for **HQ (Sydney)** and **one Branch office (Melbourne)** using enterprise best practices: perimeter security, segmentation, secure WAN connectivity, and scalable switching.

### Network Diagrams

The diagrams were created using **diagrams.net (draw.io)**.

- **HQ Network diagram (Sydney):**  
  - Draw.io file: `./diagrams/hq_network.drawio`  
  - Image: `./diagrams/hq_network.png`  

  ![HQ Network Diagram](./diagrams/hq_network.png)

- **Branch Network diagram (Melbourne):**  
  - Draw.io file: `./diagrams/branch_network.drawio`  
  - Image: `./diagrams/branch_network.png`  

  ![Branch Network Diagram](./diagrams/branch_network.png)



---

### Key Design Justifications

#### 1) Perimeter Firewall at Each Site
A dedicated firewall is placed at HQ and Branch between the ISP router and internal networks.

**Justification:**
- Enforces security policies for inbound/outbound traffic
- Reduces attack surface
- Supports intrusion filtering, NAT, logging, and VPN functions

---

#### 2) Site-to-Site VPN Between HQ and Branch
A **site-to-site IPsec VPN** tunnel is implemented between HQ and the Melbourne branch.

**Justification:**
- Protects confidentiality and integrity of traffic over the public internet
- Allows branch staff to securely access HQ systems
- Supports secure inter-office communication without leased lines

---

#### 3) Network Segmentation (Separate Security Zones)
The design separates devices into multiple zones such as:
- Staff LAN
- Server zone (HQ)
- CCTV/IoT zone
- Guest WiFi zone
- Network management zone

**Justification:**
- Prevents guest/IoT devices from reaching sensitive systems
- Limits lateral movement if any endpoint is compromised
- Enables clearer access control and easier monitoring

---

#### 4) Use of Managed Switching
Managed switches are recommended for both sites.

**Justification:**
- Improves visibility and control
- Supports monitoring (SNMP), port shutdown, and secure configuration
- Allows future expansion (VLAN-ready switching if needed later)

---

#### 5) Hierarchical Topology (Core + Access)
HQ network uses a structured topology (core switching + access switching).

**Justification:**
- Scales easily as staff grows
- Easier troubleshooting and maintenance
- Supports adding new departments and services with minimal redesign

---

## WiFi Design

WiFi is required at HQ and branch to support staff laptops and mobile devices while keeping guest traffic isolated.

### SSID Configuration

Two SSIDs are configured at each site:

1. **Staff SSID**
   - SSID: `TRUELEC-STAFF`
   - Purpose: Staff corporate devices and authorised users

2. **Guest SSID**
   - SSID: `TRUELEC-GUEST`
   - Purpose: Visitors/guest internet-only access

---

### Security Settings (with values)

| Setting | TRUELEC-STAFF | TRUELEC-GUEST |
|---|---|---|
| Encryption | WPA3-Personal (preferred), fallback WPA2-AES | WPA2-AES |
| Password policy | 12+ characters, changed every semester/term | Separate guest password, changed regularly |
| Client isolation | Optional (OFF for internal services) | ON (required) |
| LAN Access | Allowed (controlled through firewall policies) | Blocked |
| Captive Portal | Not required | Recommended |
| Band steering | Enabled | Enabled |

---

### Frequency Bands and Channel Plan

- **2.4 GHz band:** higher range, lower throughput (compatibility)
- **5 GHz band:** higher speed, less congestion (preferred for staff)

Recommended channel widths:
- 2.4 GHz: **20 MHz**
- 5 GHz: **40/80 MHz** depending on interference and building layout

---

### Access Point Deployment (high level)

- **HQ:** 3–5 access points depending on floor plan, meeting rooms, and staff density
- **Branch:** 1–2 access points depending on office size and walls/interference

Access points should be ceiling-mounted near central work areas where possible.

---

## Address Allocations

### IP Addressing Requirement Compliance

This addressing plan meets the assessment rules:

- Only **/16** and **/24** subnet masks are used
- Private IP ranges are **not used** (no `192.168.x.x`, `10.x.x.x`, `172.16.x.x`)
- The first octet (A in A.B.C.D) must equal the last two digits of a group member student ID  
  - Both group members’ student IDs end in **67**  
  - Therefore, all IP addresses use **67.x.x.x**

---

### Headquarters (Sydney) Address Plan

**HQ supernet:** `67.10.0.0/16`

| HQ Zone | IPv4 Subnet | Default Gateway |
|---|---|---|
| HQ Staff LAN | `67.10.10.0/24` | `67.10.10.1` |
| HQ IT/Admin | `67.10.20.0/24` | `67.10.20.1` |
| HQ Server Zone | `67.10.30.0/24` | `67.10.30.1` |
| HQ CCTV/IoT | `67.10.40.0/24` | `67.10.40.1` |
| HQ Guest WiFi | `67.10.50.0/24` | `67.10.50.1` |
| HQ Network Management | `67.10.60.0/24` | `67.10.60.1` |

Suggested DHCP ranges:
- HQ Staff LAN: `67.10.10.50` – `67.10.10.220`
- HQ Guest WiFi: `67.10.50.50` – `67.10.50.230`

Suggested static IPs in HQ Server Zone:
- App Server 1: `67.10.30.10`
- App Server 2: `67.10.30.11`
- Database Server: `67.10.30.12`
- Backup/File Server: `67.10.30.13`

---

### Branch Office (Melbourne) Address Plan

**Branch supernet:** `67.20.0.0/16`

| Branch Zone | IPv4 Subnet | Default Gateway |
|---|---|---|
| Branch Staff LAN | `67.20.10.0/24` | `67.20.10.1` |
| Branch Local Server | `67.20.20.0/24` | `67.20.20.1` |
| Branch CCTV/IoT | `67.20.30.0/24` | `67.20.30.1` |
| Branch Guest WiFi | `67.20.40.0/24` | `67.20.40.1` |
| Branch Network Management | `67.20.50.0/24` | `67.20.50.1` |

Suggested DHCP ranges:
- Branch Staff LAN: `67.20.10.50` – `67.20.10.200`
- Branch Guest WiFi: `67.20.40.50` – `67.20.40.230`

---

### WAN (HQ to Branch VPN Link)

Dedicated WAN subnet for inter-site connectivity:

| Link | Subnet | HQ Endpoint | Branch Endpoint |
|---|---|---|---|
| HQ ↔ Melbourne WAN | `67.254.1.0/24` | `67.254.1.1` | `67.254.1.2` |

---

## Recommended Hardware

The following equipment is recommended to meet Truelec’s requirements for performance, security, and scalability. Pricing is approximate in AUD and may vary based on suppliers.



---

### Headquarters (Sydney) Hardware

| Component | Recommended Hardware (Example) | Minimum Specifications | Qty | Estimated Price (AUD) |
|---|---|---|---:|---:|---|
| ISP Edge Router | Business-grade router | Gigabit WAN, stable routing | 1 | $250–$800 |
| Firewall Appliance | pfSense appliance / FortiGate 40F | Stateful firewall, NAT, logging, IPsec VPN | 1 | $800–$2,000 |
| Core Managed Switch | 24/48 port managed switch | Gigabit switching, managed features | 1 | $500–$2,500 |
| Access Switches | Managed switches | 24-port Gigabit, reliable throughput | 2 | $250–$900 each |
| Wireless Access Points | Business WiFi AP | Dual-band 2.4/5 GHz, WPA2/WPA3 | 3–5 | $180–$550 each |
| Application Servers | Dell/HPE rack/tower server | 8+ CPU cores, 32GB+ RAM, SSD/RAID | 3 | $2,500–$6,000 each |
| UPS | APC/Equivalent UPS | 1500VA+, surge protection | 2 | $400–$900 each |

---

### Branch Office (Melbourne) Hardware

| Component | Recommended Hardware | Minimum Specifications | Qty | Estimated Price (AUD) |
|---|---|---|---:|---:|---|
| ISP Edge Router | Business-grade router | Gigabit WAN | 1 | $250–$800 |
| Firewall Appliance | pfSense appliance / FortiGate | IPsec VPN support, policy rules, logging | 1 | $800–$2,000 |
| Managed Switch | 24-port managed switch | Gigabit switching | 1 | $250–$1,200 |
| Wireless Access Point | Business WiFi AP | Dual-band, WPA2/WPA3 | 1–2 | $180–$550 each |
| Branch Server | Entry-level server | 4–8 CPU cores, 16–32GB RAM, SSD | 1 | $2,000–$5,000 |
| UPS | UPS | 1000–1500VA | 1 | $300–$700 |

---

### Cabling and Supporting Equipment (Both Sites)

| Item | Minimum Specification | Estimated Price (AUD) | Notes |
|---|---|---:|---|
| Ethernet Cabling | Cat6 certified | $200–$800 | depends on building size |
| Patch Panel | 24/48 port | $90–$250 | structured cabling |
| Network Rack | 12U–24U | $250–$900 | secure mounting |
| Wall ports/keystones | Cat6 compatible | $50–$150 | staff workstation outlets |

---
