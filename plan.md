# Project Plan
This section provides the project planning approach, scope, timeline, task allocation, and deliverables for the COIT20246 Networking and Cyber Security Project.

[Project Scope](#project-scope) | [Milestones and Timeline](#milestones-and-timeline) | [Task Allocation](#task-allocation) | [Tools and Collaboration](#tools-and-collaboration) | [Deliverables](#deliverables) | [Return to index](./README.md)

---

## Project Scope

This project is based on the **Truelec** company scenario and aims to design a secure and scalable enterprise network and supporting documentation. The work is divided into two major parts aligned with the unit assessment requirements:

### Part 1 (Network Design)
- Identify key design assumptions
- Create **HQ (Sydney) network design**
- Create **Branch (Melbourne) network design**
- Provide WiFi design details and configuration values
- Provide IPv4 address allocations using the required addressing rule:
  - Only `/16` or `/24`
  - No private addressing (no 10.x.x.x / 172.16.x.x / 192.168.x.x)
  - First octet must start with last two digits of student ID: **67.x.x.x**
- Recommend network hardware with minimum specs, AUD pricing, and references

### Part 2 (Cloud + Security + Ethics + Reflection)
- Compare cloud VM costs for HQ and branch servers (AWS and Azure)
- Estimate total 5-year cloud cost and compare with physical server purchase
- Complete risk assessment using the provided spreadsheet template (TVA Matrix evidence)
- Recommend security controls (3 controls) for the highest-risk data asset
- Address ethical and social issues (privacy, compliance, impacts)
- Provide reflection supported by GitHub commits and team contribution evidence
- Prepare a short presentation (video via Echo360)

---

## Milestones and Timeline

The project is planned over multiple stages to ensure steady progress and frequent GitHub commits.

### Stage 1: Repository Setup and Planning
- Create GitHub repository structure
- Add templates and navigation links in markdown files
- Agree on assumptions and overall design approach
- Establish file naming conventions and diagram naming

### Stage 2: Network Design (Part 1 submission focus)
- Build HQ network diagram in draw.io
- Build branch network diagram in draw.io
- Write key design decisions and network justification
- Design WiFi (SSID, encryption, guest isolation)
- Finalize IPv4 addressing plan and subnet allocations
- Prepare recommended hardware list

### Stage 3: Cloud Services Analysis
- Use AWS Pricing Calculator for VM estimate export
- Use Azure Pricing Calculator for VM estimate export
- Compare providers on price, scalability and fit
- Calculate 5-year cost projection for full server needs

### Stage 4: Security Risk Assessment and Controls
- Identify key assets and threats (minimum 8 of 12 threat categories)
- Complete risk spreadsheet and screenshot TVA matrix
- Select highest-risk data asset
- Recommend 3 security controls (NIST SP800-53 / lecture controls)

### Stage 5: Ethics and Reflection
- Analyse privacy/security risks and compliance requirements
- Write ethical issues section with academic referencing
- Prepare reflection based on team workload and commits
- Collect GitHub commit evidence screenshots

### Stage 6: Final QA and Submission
- Check all rubric requirements are met
- Confirm diagrams included as `.drawio` + `.png`
- Ensure all markdown links work correctly
- Export final PDFs for submission
- Record 5-minute presentation

---

## Task Allocation

Work is distributed to ensure balanced workload and meaningful contributions from both team members.

### Team Members
- **Student 1:** Abhijit Vijesh Chauhan (12318667)
- **Student 2:** Ganga Prashanth Ameti (12317267)

### Task Allocation Table

| Area / Task | Student Responsible | Output File(s) |
|---|---|---|
| GitHub repository setup + folder structure | Student 1 | Repository structure |
| Assumptions and scenario interpretation | Student 1 + Student 2 | `network.md` |
| HQ Network diagram (Sydney) | Student 1 | `./diagrams/hq_network.drawio`, `./diagrams/hq_network.png` |
| Branch Network diagram (Melbourne) | Student 2 | `./diagrams/branch_network.drawio`, `./diagrams/branch_network.png` |
| Network design write-up + key justifications | Student 1 | `network.md` |
| WiFi design (SSID + encryption + guest isolation) | Student 2 | `network.md` |
| IPv4 addressing plan (67.x.x.x rule compliance) | Student 1 | `network.md` |
| Recommended hardware list (min specs + AUD prices + links) | Student 2 | `network.md` |
| AWS cloud VM estimate export | Student 1 | `cloud.md`, `./cloud_estimates/aws_vm_estimate.*` |
| Azure cloud VM estimate export | Student 2 | `cloud.md`, `./cloud_estimates/azure_vm_estimate.*` |
| 5-year cloud vs physical cost comparison | Student 1 + Student 2 | `cloud.md` |
| Risk assessment spreadsheet completion | Student 2 | `./risk_assessment/risk_assessment.xlsx` |
| TVA matrix screenshots for evidence | Student 2 | `security.md`, screenshots |
| Security controls selection (3 controls) | Student 1 | `security.md` |
| Ethical and social issues analysis | Student 2 | `ethics.md` |
| Reflection writing + contribution evidence | Student 1 + Student 2 | `reflection.md` |
| Presentation scripting and recording | Student 1 + Student 2 | Echo360 video |

---

## Tools and Collaboration

### Tools Used
- **Documentation:** GitHub Markdown (`.md`)
- **Diagram Tool:** diagrams.net (draw.io)
- **Cloud Pricing Tools:** AWS Pricing Calculator, Microsoft Azure Pricing Calculator
- **Version Control:** Git and GitHub

### Collaboration Approach
- Work is tracked in GitHub using frequent commits.
- Each team member commits their own work to demonstrate contribution.
- Major work is completed through a simple workflow:
  - Create/edit file locally
  - Commit with meaningful message
  - Push to GitHub repository
  - Peer-review and merge improvements

### Commit and Branching Strategy
- Main branch: `main`
- Suggested commit rules:
  - Commit after each major improvement
  - Use clear commit messages, e.g.:
    - `Add HQ network diagram`
    - `Update addressing allocation for HQ and branch`
    - `Add WiFi configuration section`
    - `Add AWS/Azure VM cost export`
    - `Complete risk assessment spreadsheet`

---

## Deliverables

### Markdown Files (Main Report Sections)
- `README.md`
- `plan.md`
- `network.md`
- `cloud.md`
- `security.md`
- `ethics.md`
- `reflection.md`

### Required Attachments in Repository
- `./diagrams/` folder containing:
  - HQ diagram `.drawio` + `.png`
  - Branch diagram `.drawio` + `.png`
- `./cloud_estimates/` folder containing:
  - AWS estimate export file(s)
  - Azure estimate export file(s)
- `./risk_assessment/` folder containing:
  - Risk assessment spreadsheet `.xlsx`
  - TVA matrix screenshot evidence image(s)

### Submission Outputs
- PDF exports of each markdown file as required by the unit:
  - `README.pdf`
  - `plan.pdf`
  - `network.pdf`
  - `cloud.pdf`
  - `security.pdf`
  - `ethics.pdf`
  - `reflection.pdf`
- Final repository ZIP submission
- Part 2 video submission through Echo360

---
