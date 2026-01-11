# Cloud Services
This section gives pricing for a cloud setup for the company.

[Cloud VM Provider Comparison](#cloud-vm-provider-comparison) | [Total Cost](#total-cost-of-cloud-vms) | [Plan](./plan.md) | [Network Design](./network.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

---

## Cloud VM Provider Comparison

### Scenario requirement
Truelec is considering shifting servers to the cloud. The special-purpose booking application requires:
- **3 servers in the headquarters**
- **1 server per branch office**

Based on the assumed branch cities in this project (Melbourne, Brisbane, Perth), the required number of cloud servers is:
- HQ: 3 VMs
- Branch offices: 3 VMs (1 VM per branch)
- **Total VMs required = 6**

---

### Cloud providers selected
To meet the assessment requirement, pricing was calculated using official calculators from at least two cloud providers:
- **AWS (Amazon EC2)** using AWS Pricing Calculator
- **Microsoft Azure (Virtual Machines)** using Azure Pricing Calculator

---

### Export files (evidence)
The exported pricing datasets are stored in the repository:

Links to cloud provider export files:
- [AWS](./cloud_estimates/aws_vm_pricing.csv) 
- [Azure](./cloud_estimates/ExportedEstimate.xlsx)

---

### Extracted pricing results (1 VM)

#### AWS pricing (1 VM)
From the exported AWS dataset:
- Usage: **730 hours/month**
- Estimated monthly cost: **3959.52 USD/month**

#### Azure pricing (1 VM)
From the exported Azure dataset:
- Relevant region for Truelec (Australia): **Australia Central**
- VM option listed: **D2 v2 (2 vCPUs, 7 GB RAM)**
- Usage: **730 hours/month**
- Estimated monthly cost: **256.13 USD/month**

> Note: The Azure export file contains another estimate for “East US”; however, the Australia region estimate is used for this project because Truelec operates in Australia and region selection impacts latency and compliance.

---

### Summary comparison table (1 VM)

| Provider | Service | Region | VM type/config | Usage | Monthly cost |
|---|---|---|---|---:|---:|
| AWS | Amazon EC2 | (Pricing export) | (Pricing export) | 730 hrs/month | **3959.52 USD** |
| Azure | Virtual Machines | Australia Central | D2 v2 (2 vCPU, 7 GB RAM) | 730 hrs/month | **256.13 USD** |

---

### Recommended cloud provider
**Recommended provider: Microsoft Azure**

**Reason:**
- Based on the exported calculator values, **Azure’s estimated monthly VM price is significantly lower than AWS** for the estimates produced.
- Azure also provides an Australia-based region (Australia Central) which is suitable for Truelec operations.

---

## Total Cost of Cloud VMs

### Total VM requirement
The booking application requires:
- 3 VMs for HQ
- 1 VM per branch office

Assuming 3 branches (Melbourne, Brisbane, Perth):
- Branch VMs = 3

 Total VMs required:
- **6 VMs**

---

### Total cost calculation over 5 years (Azure recommended)

Azure cost per VM per month:
- **256.13 USD**

#### Total monthly cost (all VMs)
- Total monthly cost = 6 × 256.13
- Total monthly cost = **1536.78 USD/month**

#### Total yearly cost
- Total yearly cost = 1536.78 × 12
- Total yearly cost = **18441.36 USD/year**

#### Total cost for 5 years
- Total 5-year cost = 18441.36 × 5
- **Total 5-year cloud VM cost = 92206.80 USD**

---

### Cloud VMs vs buying new servers (discussion)

#### Advantages of Cloud VMs
- No large upfront capital expense (pay monthly instead of purchasing hardware)
- Scalability: CPU/RAM/storage can be increased as requirements grow
- Faster deployment of servers and environments
- Better disaster recovery options (snapshots, backups)
- Hardware maintenance responsibility is reduced

#### Disadvantages of Cloud VMs
- Continuous operational cost each month
- Dependence on reliable internet connectivity
- Vendor lock-in risk
- Data residency and privacy concerns must be managed carefully

---

### Conclusion
Cloud services provide Truelec with flexibility and scalability, and reduce the burden of managing physical infrastructure. Based on the official exported cost estimates used in this analysis, **Azure is the recommended provider** due to lower estimated VM costs and the availability of an Australia-based region.

---
