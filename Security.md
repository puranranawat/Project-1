# Security
This section gives a cyber security risk assessment for the company and recommended security controls.

[Risk Assessment](#risk-assessment) | [Security Controls](#security-controls) | [Return to index](./README.md)

---

## Risk Assessment

### Overview
Truelec operates a headquarters (HQ) office and multiple branch offices connected through a site-to-site VPN. The organisation hosts a special-purpose booking application and stores business-critical and personal information. Since the scenario does not provide full technical details, a **mini cyber security risk assessment** is performed using the unit template and process.

This risk assessment considers vulnerabilities across **at least 8 of the 12 information security threats**, includes assets from **each asset type**, and includes **at least 4 different data assets**.

---

### Scope of assessment
The risk assessment covers:
- Headquarters network (Sydney)
- Branch network (Melbourne)
- Internet edge and firewall security boundary
- Site-to-site VPN between HQ and branch
- Servers and endpoints supporting the booking system
- WiFi networks (Staff + Guest)
- CCTV/IoT devices

---

### Key Assets Identified (by asset type)

#### Hardware assets
- HQ/Branch edge firewall devices
- Managed switches and wireless access points
- Servers (application servers, database server, file/backup server)
- Staff endpoints (PCs/laptops)
- CCTV cameras / IoT devices

#### Software assets
- Booking application platform
- Server operating systems (Linux/Windows)
- Remote access and VPN configuration
- Security monitoring/logging tools

#### Network/infrastructure assets
- ISP connectivity at HQ and branch
- VPN tunnel between sites
- Internal LAN segments (staff, server zone, guest WiFi)
- DNS/DHCP services

#### People assets
- IT administrators
- Staff users
- Guests/visitors using guest WiFi
- Third-party support vendors (if any)

#### Data assets (minimum 4)
1. **Customer booking data** (names, phone, email, booking details)
2. **Payment and transaction records** (invoices, financial data)
3. **Employee HR records** (staff personal details, payroll)
4. **System access credentials and logs** (user accounts, admin credentials, VPN keys)
5. **Operational business documents** (policies, contracts, supplier data)

---

### Threat coverage (minimum 8 threat categories)
The assessment considers vulnerabilities across the following threat categories:

1. Unauthorised access (external attacker)
2. Malware / ransomware
3. Insider threat (malicious or accidental)
4. Phishing / social engineering
5. Data loss / leakage
6. Network attack (MITM, VPN compromise, eavesdropping)
7. Denial of Service (DoS)
8. Misconfiguration / insecure settings
9. Physical security / theft (additional coverage)
10. Third-party/vendor risk (additional coverage)

---

### Summary of High-Level Risks (mini assessment outcome)
The risk assessment identified the following key risks as highest priority:

- Compromise of **customer booking database** through weak access controls or exposed services
- Ransomware affecting server zone and backups
- VPN compromise leading to HQ access from branch side
- Guest WiFi misuse and lateral movement into internal networks (if isolated incorrectly)
- Misconfiguration of firewall rules and access permissions
- Phishing attacks leading to credential theft and unauthorised access

---

### Risk Assessment Evidence
- The completed risk assessment spreadsheet is stored in:
  - `./risk_assessment/risk_assessment.xlsx`
- TVA Matrix evidence screenshots are included in:
  - `./risk_assessment/tva_matrix_screenshot.png`

---

## Security Controls

### Selected highest-risk data asset
From the risk assessment, the data asset rated with the highest risk is:

✅ **Customer Booking Data (stored in the booking database and application systems at HQ)**

This asset has:
- High confidentiality impact (privacy and identity exposure)
- High integrity impact (booking fraud, manipulation)
- High availability impact (service disruption affects business operations)

---

### Recommended Security Control 1: Multi-Factor Authentication (MFA) + Strong IAM
**Control type:** Identity and Access Management  
**Standard mapping (NIST SP 800-53):**
- IA-2 (Identification and Authentication)
- AC-2 (Account Management)
- AC-6 (Least Privilege)

#### How it reduces risk
- Prevents account takeover even if passwords are stolen via phishing
- Reduces risk of unauthorised admin access to servers and cloud dashboards
- Limits insider abuse by enforcing role-based permissions

#### How it will be implemented (specific and practical)
- Enforce MFA for:
  - VPN access accounts
  - Admin accounts on firewalls
  - Server administration accounts (Linux/Windows)
  - Booking system admin portal accounts
- Implement role-based access:
  - Standard staff users: access only booking front-end
  - Customer support staff: read/write limited booking records
  - IT administrators: server and network admin only
- Password policy:
  - Minimum 12 characters
  - Complexity enabled
  - Prevent reuse of recent passwords
  - Account lockout after repeated failures

#### Where it applies in network design
- VPN endpoint at HQ firewall (IPsec/VPN authentication)
- Booking application admin access
- HQ server zone access (`67.10.30.0/24`)

#### Disadvantages (from user perspective)
- Slight inconvenience (extra step on login)
- Requires staff training and MFA app setup
- Risk of support tickets for lost phones / MFA resets

---

### Recommended Security Control 2: Network Segmentation + Firewall Policy Hardening
**Control type:** Network security and access control  
**Standard mapping (NIST SP 800-53):**
- SC-7 (Boundary Protection)
- AC-4 (Information Flow Enforcement)

#### How it reduces risk
- Prevents attackers from moving laterally across the network after compromising one device
- Protects the booking database by limiting which networks can reach server zone
- Separates high-risk networks (Guest WiFi, IoT/CCTV) from business-critical systems

#### How it will be implemented (specific and practical)
- Apply strict firewall rules at HQ firewall:
  - Allow Branch Staff LAN (`67.20.10.0/24`) to access booking app only (specific ports)
  - Block branch access to internal HQ management network
  - Block Guest WiFi zone (`67.10.50.0/24`) from reaching any internal network
  - Allow Staff LAN to server zone only on required ports (e.g., HTTPS, DB access if needed)
- Protect server zone (`67.10.30.0/24`) with default deny policy:
  - Only allow required inbound from Staff/IT networks
  - Deny all unnecessary inbound/outbound connections
- Isolate CCTV/IoT (`67.10.40.0/24`) and allow only:
  - connection to NVR/monitoring system (if used)
  - no access to server zone

#### Where it applies in network design
- Between these zones/subnets in `network.md`:
  - Staff LAN (`67.10.10.0/24`)
  - IT/Admin (`67.10.20.0/24`)
  - Server zone (`67.10.30.0/24`)
  - CCTV/IoT (`67.10.40.0/24`)
  - Guest WiFi (`67.10.50.0/24`)
  - Network management (`67.10.60.0/24`)

#### Disadvantages (from user perspective)
- Misconfigured rules can temporarily block legitimate work
- Requires IT staff time for policy management
- More complex troubleshooting when access is denied

---

### Recommended Security Control 3: Backup Strategy + Anti-Ransomware Protection
**Control type:** Availability and recovery  
**Standard mapping (NIST SP 800-53):**
- CP-9 (System Backup)
- CP-10 (System Recovery and Reconstitution)
- SI-3 (Malicious Code Protection)

#### How it reduces risk
- Ensures customer booking data can be restored after ransomware or accidental deletion
- Minimises downtime for the booking application
- Reduces business impact of malware incidents

#### How it will be implemented (specific and practical)
- Implement “3-2-1 Backup Rule”:
  - 3 copies of data
  - 2 different storage types
  - 1 copy offsite/immutable
- Backups for booking database and servers:
  - Daily incremental backups
  - Weekly full backups
  - Store backups in:
    - local backup server in HQ server zone
    - offsite backup storage/cloud backup repository
- Ensure backups are protected:
  - immutable snapshots / write-once storage
  - backup accounts separated from normal admin accounts
- Deploy endpoint/server protection:
  - anti-malware on servers and endpoints
  - disable macro execution where possible
  - restrict execution of unknown binaries

#### Where it applies in network design
- HQ Server zone (`67.10.30.0/24`) where booking/database servers are located
- Backup/File server (`67.10.30.13`) as backup staging
- Policies extended to branch endpoints (since branch compromise can spread via VPN)

#### Disadvantages (from user perspective)
- Increased storage cost
- Scheduled backups may slightly reduce performance
- Requires periodic recovery testing and staff time

---

## Summary
The mini risk assessment highlighted that **customer booking data** is the most critical asset due to confidentiality, integrity, and availability requirements. The recommended controls (MFA/IAM hardening, segmentation with firewall policy enforcement, and robust backup and malware protection) collectively reduce the risk of the most significant threats, including phishing-led account takeover, ransomware, and unauthorised network access.

---
