# Project Plan
This section presents the initial plan for the project.

[Communication](#communication-plan) | [Schedule](#schedule) | [Network Design](./network.md) | [Cloud Services](./cloud.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

---

## Communication Plan

The group will use the following communication and collaboration strategy to ensure tasks are completed on time and work is evenly distributed.

### Communication Tools
- **WhatsApp**: daily quick updates and coordination
- **Microsoft Teams / Zoom**: weekly meeting for planning and review (screen sharing for diagrams and reports)
- **GitHub**: central repository for all documentation, diagrams, and evidence files

### Meeting Frequency
- **Daily check-in (5–10 minutes)** via WhatsApp
- **Weekly meeting (30–45 minutes)** to review progress, confirm deliverables, and plan the next week’s tasks

### Work Practices
- Each member will:
  - Complete assigned tasks and commit changes to GitHub frequently
  - Use clear commit messages describing work completed
  - Maintain consistent file naming and folder structure
- Both members will review each major file before final submission to ensure quality and correctness.

### Version Control Rules
- Work will be committed regularly to GitHub with meaningful commit messages (examples):
  - `Create HQ network diagram`
  - `Add branch addressing and WiFi design`
  - `Update hardware list with pricing`
  - `Add AWS pricing estimate export`
  - `Complete risk assessment spreadsheet`
- Any conflicts will be resolved together during weekly meetings.

---

## Schedule
The plan of tasks for each group member for the remainder of the project is:

- Week 5: 
  - **Abhijit Vijesh Chauhan**
    - Set up GitHub repository structure
    - Add README navigation links and markdown templates
    - Draft assumptions for HQ and branch offices
  - **Ganga Prashanth Ameti**
    - Review assessment requirements and marking expectations
    - Collect networking design requirements (servers, staff count, branch needs)
    - Research typical enterprise network components for Truelec scenario

- Week 6:
  - **Abhijit Vijesh Chauhan**
    - Create **HQ Network Diagram (Sydney)** using diagrams.net (draw.io)
    - Start writing HQ network justification (perimeter security + segmentation)
  - **Ganga Prashanth Ameti**
    - Create **Branch Network Diagram (Melbourne)** using diagrams.net (draw.io)
    - Document branch connectivity needs (VPN + internet access)

- Week 7:
  - **Abhijit Vijesh Chauhan**
    - Finalize IPv4 addressing plan for HQ and branch
    - Ensure compliance with addressing rule: **67.x.x.x** and only `/16` and `/24`
    - Complete Address Allocation section in `network.md`
  - **Ganga Prashanth Ameti**
    - Finalize WiFi design section:
      - SSIDs, encryption, guest isolation, channel/band planning
    - Review diagrams and update labels (subnets + gateways + VPN)

- Week 8:
  - **Abhijit Vijesh Chauhan**
    - Cloud Services work:
      - AWS VM estimate export (HQ servers + branch server reference)
      - Draft cloud provider comparison notes
  - **Ganga Prashanth Ameti**
    - Cloud Services work:
      - Azure VM estimate export
      - Record cost values and configuration details for reporting

- Week 9:
  - **Abhijit Vijesh Chauhan**
    - Write cloud comparison and 5-year cost analysis in `cloud.md`
    - Summarise advantages/disadvantages of cloud VMs vs physical servers
  - **Ganga Prashanth Ameti**
    - Complete risk assessment spreadsheet (`risk_assessment.xlsx`)
    - Capture TVA matrix screenshot evidence and store in repository

- Week 10:
  - **Abhijit Vijesh Chauhan**
    - Write security controls section:
      - Identify highest-risk data asset
      - Recommend and justify **3 security controls**
  - **Ganga Prashanth Ameti**
    - Write `ethics.md`:
      - ethical/social/privacy issues
      - compliance and stakeholder impacts
    - Add references (Harvard style)

- Week 11: Submit the project
  - **Abhijit Vijesh Chauhan**
    - Write reflection draft and compile GitHub commit screenshots
    - Ensure all diagrams are present as `.drawio` + `.png`
  - **Ganga Prashanth Ameti**
    - Final formatting and proofreading of all markdown files
    - Export markdown reports to PDFs as required for submission
  - **Both Members**
    - Verify all required files are included in repository
    - Record and submit the presentation video via Echo360
    - Submit PDFs + repository ZIP in Moodle

---
