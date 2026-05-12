# azure-availability-sets-zones
Study notes and concepts covering Azure Availability Sets, Availability Zones, Fault Domains and Update Domains for AZ-104 exam preparation.

# Azure Availability Sets & Availability Zones

## Objective
Understand and document the key concepts of Azure Availability Sets 
and Availability Zones for high availability VM deployments in Azure.

## Key Concepts

### What is High Availability?
High Availability (HA) ensures that applications and services remain 
accessible with minimal downtime, even during planned maintenance or 
unexpected hardware failures.

---

## Availability Sets

### Definition
An Availability Set is a logical grouping of Virtual Machines in Azure 
that ensures VMs are distributed across multiple isolated hardware nodes 
in a cluster. This protects against single points of failure during both 
planned and unplanned downtime.

### When to Use
- When you need to protect VMs within a single datacenter
- When you want basic high availability at no extra cost
- When deploying two or more VMs running the same application

### Fault Domains
- A Fault Domain represents a separate physical rack in the datacenter
- Each rack has its own independent power supply and network switch
- Azure provides 3 Fault Domains (0, 1, 2) by default
- Protects against unplanned hardware failures and power outages
- If one rack loses power, VMs on other racks continue running

### Update Domains
- An Update Domain represents a group of VMs that are updated together
- Azure provides 5 Update Domains (0, 1, 2, 3, 4) by default
- During planned maintenance, Azure updates one Update Domain at a time
- Ensures at least some VMs remain running during Microsoft maintenance
- Protects against planned downtime

### Default Configuration
| Domain Type | Default Count |
|-------------|--------------|
| Fault Domains | 3 |
| Update Domains | 5 |

### SLA
- 99.95% uptime SLA when two or more VMs are in an Availability Set

### Important Rules
- Availability Set must be created at VM creation time
- Cannot add an existing VM to an Availability Set after creation
- All VMs in an Availability Set should perform the same function
- Availability Sets are free - no additional cost

### Example VM Distribution
| VM | Fault Domain | Update Domain |
|----|-------------|---------------|
| VM1 | 0 | 0 |
| VM2 | 1 | 1 |
| VM3 | 2 | 2 |

---

## Availability Zones

### Definition
Availability Zones are physically separate datacenters within the same 
Azure region. Each zone has its own independent power, cooling, and 
networking infrastructure. They protect against complete datacenter failures.

### When to Use
- When you need the highest level of availability
- When running mission critical applications
- When you need protection against full datacenter failure

### Key Characteristics
- Each Azure region has a minimum of 3 Availability Zones
- Each zone is a separate physical datacenter
- Zones are connected via high-speed private fibre networks
- Located within the same Azure region

### SLA
- 99.99% uptime SLA when VMs are deployed across Availability Zones

---

## Availability Sets vs Availability Zones

| Feature | Availability Set | Availability Zone |
|---------|-----------------|-------------------|
| Protects against | Rack failure, planned maintenance | Full datacenter failure |
| Location | Same datacenter | Separate datacenters |
| SLA | 99.95% | 99.99% |
| Cost | Free | Slightly higher |
| Number available | 1 per datacenter | 3 per region |
| Best for | Basic HA | Mission critical apps |
| Created at VM creation | Yes - cannot change later | No - can specify anytime |

---

## Key Exam Concepts

### Common AZ-104 Exam Scenarios

**Scenario 1:**
You need to ensure VMs remain available during planned Azure 
maintenance. What should you configure?
- Answer: Availability Set - Update Domains handle planned maintenance

**Scenario 2:**
You need 99.99% SLA for your mission critical application. 
What should you configure?
- Answer: Availability Zones - higher SLA than Availability Sets

**Scenario 3:**
Can you add an existing VM to an Availability Set?
- Answer: No - must be configured at VM creation time

**Scenario 4:**
How many Fault Domains and Update Domains does Azure create by default?
- Answer: 3 Fault Domains and 5 Update Domains

---

## Important Terms

| Term | Definition |
|------|-----------|
| High Availability | Ensuring services remain accessible with minimal downtime |
| Fault Domain | Separate physical rack with own power and network |
| Update Domain | Group of VMs updated together during maintenance |
| SLA | Service Level Agreement - uptime guarantee from Microsoft |
| Availability Set | Logical grouping of VMs within same datacenter |
| Availability Zone | Separate physical datacenter within same region |
| Region | Geographic area containing one or more datacenters |

---

## References
- [Availability Sets Documentation](https://learn.microsoft.com/en-us/azure/virtual-machines/availability-set-overview)
- [Availability Zones Documentation](https://learn.microsoft.com/en-us/azure/reliability/availability-zones-overview)
- [AZ-104 Study Guide](https://learn.microsoft.com/en-us/certifications/exams/az-104)
