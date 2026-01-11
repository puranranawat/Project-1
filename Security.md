# Security
This section gives a cyber security risk assessment for the company and recommended security controls.

[Risk Assesment](#risk-assessment) | [Security Controls](#security-controls) | [Plan](./plan.md) | [Network Design](./network.md) | [Cloud Services](./cloud.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

---

## Risk Assessment
[View risk assessment spreadsheet](./riskAssessment.xlsx)

### Mini Risk Assessment Summary
A mini cyber security risk assessment was conducted for the proposed Truelec network design (HQ Sydney + Branch Melbourne with site-to-site VPN). The assessment was completed using the unit-provided risk assessment template and process.

This risk assessment meets unit requirements by:
- Considering vulnerabilities across **at least 8 of the 12 information security threats**
- Including assets across **each asset type**
- Including **at least 4 different data assets**

### Key assets included (by asset type)
- **Hardware assets:** firewall, routers, managed switches, wireless access points, servers, end-user PCs/laptops, CCTV cameras.
- **Software assets:** booking application, operating systems, VPN services, authentication systems, monitoring/logging tools.
- **Network/infrastructure assets:** internet connection, VPN tunnel, HQ/branch subnets, WiFi networks.
- **People assets:** staff users, administrators, guests (guest WiFi), third-party support vendors.
- **Data assets (minimum 4):**
  1. Customer booking data (PII)
  2. Payment/transaction records
  3. Employee HR records
  4. Credentials/access logs (VPN keys, admin passwords)
  5. Operational documents (policies/contracts) (additional)

### Threat categories considered (minimum 8)
The following information security threats were considered in the assessment:
1. Unauthorised access / credential compromise  
2. Malware and ransomware  
3. Insider threats (malicious or accidental)  
4. Phishing and social engineering  
5. Data leakage/exfiltration  
6. Network attacks (MITM, VPN compromise, eavesdropping)  
7. Denial of Service (DoS) attacks  
8. Misconfiguration / insecure settings  
9. Physical theft or damage (additional)  
10. Third-party/vendor risk (additional)

### Highest risk area identified
The assessment identified the **Customer Booking Data (database and booking application servers at HQ)** as the highest-risk data asset due to:
- High confidentiality impact (privacy breach)
- High integrity impact (booking manipulation/fraud)
- High availability impact (service downtime affects business operations)

---

## Security Controls

### Selected Data Asset (Highest Risk)
✅ **Customer Booking Data (Booking database and application records)**  
Primary location: **HQ Server Zone (`67.10.30.0/24`)**

This asset must be protected against:
- credential theft and unauthorised access
- ransomware attacks
- leakage of customer personal information
- service disruption

---

### Control 1: Multi-Factor Authentication (MFA) and Strong Identity & Access Management
**Category:** Access Control / Authentication  
**NIST SP 800-53 mapping:** IA-2, AC-2, AC-6

#### How it reduces risk
- Prevents unauthorised access even if passwords are stolen via phishing.
- Reduces likelihood of admin account takeover for servers, VPN, and firewall management.
- Supports least privilege access and reduces insider misuse.

#### Implementation in Truelec network
- Enforce MFA on:
  - VPN authentication accounts (remote/site-to-site administration)
  - Booking system admin portal accounts
  - Firewall and server administrator accounts
- Apply strong password policy:
  - Minimum 12 characters
  - Complexity enabled
  - Account lockout after repeated failed logins
- Apply least privilege:
  - Customer service staff: limited access to bookings only
  - IT admins: admin access only when required

#### Where it applies in the network design
- HQ firewall (VPN access + device management)
- HQ server zone access for booking system administration
- Any remote administration access

#### Disadvantages (user impact)
- Adds an extra login step for staff/admins.
- Requires staff training and MFA reset procedures (lost phone).

---

### Control 2: Network Segmentation + Firewall Policy Enforcement
**Category:** Network security / boundary protection  
**NIST SP 800-53 mapping:** SC-7, AC-4

#### How it reduces risk
- Prevents lateral movement if one device is compromised (e.g., malware on staff PC).
- Blocks guest WiFi users from reaching internal networks.
- Restricts access to booking servers and database to only authorised networks.

#### Implementation in Truelec network
Implement strict firewall policies between zones/subnets:

- **Guest WiFi (`67.10.50.0/24`)**
  - Allowed: internet only (DNS/HTTP/HTTPS)
  - Block: all internal networks
- **CCTV/IoT (`67.10.40.0/24`)**
  - Allowed: CCTV management only (if required)
  - Block: access to server zone and staff LAN
- **Server Zone (`67.10.30.0/24`)**
  - Default deny inbound rules
  - Allow only required ports (e.g., HTTPS for booking app)
- **Branch Staff LAN (`67.20.10.0/24`)**
  - Allow only booking application access through VPN
  - Block access to HQ management subnet

#### Where it applies in network design
- Between the segmented subnets defined in `network.md`
- At HQ firewall (main policy enforcement point)

#### Disadvantages (user impact)
- Incorrect rules can temporarily block legitimate access.
- Increased complexity for troubleshooting and ongoing management.

---

### Control 3: Backup, Recovery, and Anti-Ransomware Protection
**Category:** Data protection / business continuity  
**NIST SP 800-53 mapping:** CP-9, CP-10, SI-3

#### How it reduces risk
- Ensures customer booking data can be recovered after ransomware or accidental deletion.
- Reduces downtime and operational impact.
- Improves availability of the booking service.

#### Implementation in Truelec network
- Apply “3-2-1 backup strategy”:
  - 3 copies of booking database and key server data
  - stored on 2 different media types
  - 1 copy offsite/immutable
- Backup frequency:
  - Daily incremental backups
  - Weekly full backups
- Protect backups:
  - Separate backup credentials from normal admin accounts
  - Use immutable backup storage / write-protected backups
- Install endpoint/server protection:
  - anti-malware tools on endpoints and servers
  - patching schedule for OS and application vulnerabilities

#### Where it applies in the network design
- HQ server zone (`67.10.30.0/24`) hosting:
  - booking application servers
  - database server
  - file/backup server
- Branch endpoints (malware can spread through VPN if not controlled)

#### Disadvantages (user impact)
- Increased storage cost for backups.
- Requires regular testing of restore/recovery procedures.
- Backup operations may cause minor performance impact.

---

### Overall Outcome
The above three controls were selected because they directly reduce the highest risks to Truelec’s most critical data asset (Customer Booking Data). Together they provide:
- Strong authentication and account protection (MFA/IAM)
- Reduced exposure and movement paths for attackers (segmentation/firewall rules)
- Resilience and recovery capability against ransomware/data loss (backup strategy)

---
