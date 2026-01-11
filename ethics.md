# Ethical Issues
This section discusses the different ethical issues that arise in the scenario.

[Data Privacy](#data-privacy-and-security-issues) | [Plan](./plan.md) | [Network Design](./network.md) | [Cloud Services](./cloud.md) | [Security](./security.md) | [Reflections](./reflections.md) | [Return to index](./README.md)

---

## Data Privacy and Security Issues

Truelec operates a booking service (similar to a travel agency). This type of organisation collects and stores sensitive personal and business information to provide booking and customer service operations. Therefore, privacy, security, and ethical responsibility are critical for protecting individuals, maintaining trust, and complying with legal obligations.

This section identifies key data privacy and security concerns, types of data involved, relevant regulations, and the impact of possible unauthorised access or data breaches.

---

### 1. Types of Data Collected and Stored

Truelec may collect and store the following types of data:

#### Customer Data (Personally Identifiable Information - PII)
- Full name
- Phone number and email address
- Home address (billing and documentation)
- Booking history and booking details
- Travel-related information (dates, destination, booking reference numbers)

#### Financial and Transaction Data
- Invoices, receipts, refunds
- Transaction history and payment confirmations
- (Card payment information should be processed by secure third-party payment gateways and should not be stored locally unless required)

#### Staff and HR Data
- Employee personal information
- Payroll details
- Contracts and performance records

#### System/Technical Data
- Login records and system access logs
- VPN access logs
- Firewall and network logs
- CCTV recordings (if deployed)

---

### 2. Privacy and Ethical Issues

#### a) Risk of unauthorised access to customer data
Customer booking data is highly sensitive. If attackers access the booking database or servers, this could expose customer PII and lead to identity theft, fraud, and targeted scams.

Ethically, Truelec has a duty of care to protect customer data, especially because customers generally do not fully understand cyber risks but trust the organisation to store their data securely.

---

#### b) Data minimisation (collecting only what is required)
Booking organisations sometimes collect more customer data than is necessary. Over-collection is unethical because:
- it increases breach impact
- it increases long-term privacy risk
- it reduces customer control over personal data

Truelec should only collect information required for bookings, billing, and service delivery.

---

#### c) Data retention and secure deletion
Keeping customer information indefinitely increases privacy harm. If old records remain accessible, the number of affected customers during a breach becomes much larger.

Truelec should define:
- clear retention periods for customer booking records and logs
- secure deletion processes
- restrictions on copying/exporting data by staff

---

#### d) Staff misuse and insider threats
Employees may access booking systems daily. Without least privilege controls and monitoring:
- staff could access customer details without valid purpose
- customer data could be sold, leaked, or misused
- HR data could be exposed internally

Ethically, Truelec must ensure fair access controls and prevent misuse through:
- role-based access control
- logging and audits
- strong disciplinary policy for misuse

---

#### e) Branch office and Guest WiFi security concerns
Truelec uses branch offices connected to HQ. If branch systems are weaker, attackers can exploit them as an entry point into HQ through VPN.

Guest WiFi also increases risk if not isolated correctly. If guest users can reach internal networks, it may result in:
- unauthorised access to business systems
- malware spread
- availability issues

Truelec must ensure strict network separation between:
- Staff networks
- Guest WiFi
- IoT/CCTV systems
- Server zone

---

### 3. Security Vulnerabilities That Increase Ethical Risk

Common vulnerabilities that can cause a breach include:
- weak passwords and lack of MFA
- phishing attacks leading to credential theft
- outdated/unpatched servers
- misconfigured firewall rules
- poor backup practices leading to ransomware impact

These are ethical issues because organisations have a responsibility to implement reasonable controls that prevent avoidable harm.

---

### 4. Relevant Regulations and Compliance Requirements

Truelec operates in Australia, so data privacy and breach response must align with national requirements.

#### a) Privacy Act 1988 (Cth) and Australian Privacy Principles (APPs)
The Privacy Act and APPs require organisations to:
- only collect necessary information
- handle personal information transparently
- store and protect personal information securely
- restrict disclosure and sharing of data

#### b) Notifiable Data Breaches (NDB) scheme
If a breach is likely to cause serious harm, Truelec must:
- notify affected individuals
- notify the Office of the Australian Information Commissioner (OAIC)

This creates both ethical and legal obligations for transparency and timely response.

#### c) International laws (if applicable)
If Truelec serves international customers (e.g., EU customers), GDPR-style obligations may apply such as:
- lawful basis for processing data
- user rights to access/delete data
- strict breach reporting requirements

---

### 5. Potential Impact of a Data Breach

#### Who is impacted?
- Customers (PII exposure, scams, identity theft)
- Employees (HR data exposure)
- Truelec (financial costs, reputation damage)
- Partners (shared booking and payment systems)

#### How significant is the impact?
A breach involving booking information can be extremely serious because customer data may enable:
- targeted phishing and fraud scams
- identity theft
- safety risks (travel schedules and destinations exposed)

For Truelec, impacts include:
- customer loss and reputational damage
- downtime of booking services
- legal penalties and compliance investigations
- costs for incident response, forensic analysis, and recovery

---

### Conclusion

Truelec must treat privacy and security as both ethical responsibilities and compliance requirements. Because the organisation collects and processes sensitive customer booking information, strong access controls, data minimisation, secure retention policies, and breach response planning are essential to reduce harm and protect trust.

---
