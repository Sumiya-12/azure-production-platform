# ADR 001 - Network Topology

## Decision
Use one Azure Virtual Network with multiple subnets for the initial phase.

## Reason
This provides clear separation between tiers while keeping the first version simple enough to understand and manage.

## Current Subnets
- Web subnet
- App subnet

## Future Expansion
Later phases may introduce:
- management subnet
- data subnet
- peering or hub-spoke topology

## Trade-off
A single VNet is easier for a beginner project, but larger enterprise environments usually require more advanced segmentation and centralized network design.
