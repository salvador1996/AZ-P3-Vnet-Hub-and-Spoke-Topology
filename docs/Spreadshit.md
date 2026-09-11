# Hub-spoke VNet topology — Project 3

## Architecture
Three VNets connected in hub-spoke pattern.
Hub contains shared services. Spokes are isolated workload networks.
Spoke-to-spoke traffic is blocked by design — must route via hub.

## IP address plan

| VNet    | Address space  | Subnet name       | Subnet range   | Purpose          |
|---------|----------------|-------------------|----------------|------------------|
| Hub     | 10.0.0.0/16    | snet-management   | 10.0.1.0/24    | Jump servers     |
| Hub     | 10.0.0.0/16    | snet-shared       | 10.0.2.0/24    | Shared services  |
| Spoke1  | 10.1.0.0/16    | snet-app-spoke1   | 10.1.1.0/24    | Workload A       |
| Spoke2  | 10.2.0.0/16    | snet-app-spoke2   | 10.2.1.0/24    | Workload B       |

## NSG rules (all subnets)
Default deny-all inbound at priority 4096.
Explicit allow rules at lower priority numbers.
No internet-facing inbound rules.

## Peering
Hub ↔ Spoke1: Connected (bidirectional)
Hub ↔ Spoke2: Connected (bidirectional)
Spoke1 ↔ Spoke2: NOT peered (isolated by design)

## Flow logs
NSG flow logs enabled on spoke subnets.
Logs stored in: stflowlogdevweu001
Retention: 7 days

## Compliance
- BSI IT-Grundschutz NET.1.1 (Network architecture)
- CIS Azure Benchmark 6.x (Networking)
- ISO 27001 A.13 (Communications security)