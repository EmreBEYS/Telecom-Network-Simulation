# Telecom Network Simulation

> A telecommunications network infrastructure design, simulation, testing, and evaluation project.

## Overview

This repository documents the incremental development of reproducible telecommunications and
enterprise network scenarios using **Cisco Packet Tracer** and related networking tools.

The project begins with requirements, IPv4 addressing, and a basic LAN. Each sprint adds a
verifiable layer such as VLANs, routing, services, security, redundancy, VoIP, QoS, IPv6,
monitoring, troubleshooting, and performance evaluation. The final delivery will combine these
layers into one tested central-office and branch-network scenario.

**Project status:** Sprint 00-00 completed — Sprint 00-01 is next.

## Planned Scope

- Requirements, device inventory, and architecture diagrams
- IPv4/IPv6 addressing and subnetting
- VLANs, trunking, STP, EtherChannel, and inter-VLAN routing
- Static routing and OSPF
- DHCP, DNS, NAT/PAT, and NTP
- ACLs, network segmentation, and secure device management
- Gateway/link redundancy and failure testing
- IP telephony, voice VLANs, and QoS
- Syslog, SNMP, and network visibility
- Branch security and VPN/tunneling scenarios
- Troubleshooting laboratories and performance reports
- Final integrated Packet Tracer topology and technical report

## Tools

- Cisco Packet Tracer
- Wireshark, where packet capture is applicable
- Git and GitHub
- Network diagrams, exported device configurations, and structured test reports

## Sprint Roadmap

The detailed roadmap contains 18 incremental sprints:

| Phase | Sprints | Outcome |
|---|---|---|
| Foundation | 00-00 — 00-03 | Requirements, LAN, addressing, VLANs, Layer 2/3 foundation |
| Routing & services | 00-04 — 00-06 | WAN, OSPF, DHCP, DNS, NAT/PAT, NTP |
| Security & availability | 00-07 — 00-08 | ACL segmentation and gateway/link redundancy |
| Telecom capabilities | 00-09 — 00-11 | VoIP, QoS, IPv6/dual-stack |
| Operations | 00-12 — 00-14 | Hardening, monitoring, secure branch connectivity |
| Validation & delivery | 00-15 — 00-17 | Troubleshooting, performance, final integration |

See [docs/SPRINT_ROADMAP.md](docs/SPRINT_ROADMAP.md) for objectives, tasks, deliverables,
dependencies, completion criteria, and project-wide acceptance tests.

## Repository Convention

Each implementation sprint should provide:

- a versioned Packet Tracer `.pkt` topology;
- an addressing and device inventory update;
- exported router, switch, service, and security configurations;
- at least one positive and one negative/failure test;
- expected-versus-actual results;
- documented Packet Tracer limitations;
- a sprint note linked from the repository.

Proposed structure:

```text
docs/        architecture, addressing, diagrams, and sprint notes
topologies/  versioned Packet Tracer files
configs/     exported device configurations
tests/       connectivity, failure, security, and performance cases
reports/     validation evidence and final reports
```

## Current Progress

**Completed:** Sprint 00-00 — Requirements and Architecture Contract

Sprint 00-00 defines the central site and two-branch planning baseline, capacity assumptions,
VLAN/address plan, logical architecture, device inventory, Packet Tracer 9.0.x authoring policy,
security boundaries, risks, and acceptance evidence.

**Next:** Sprint 00-01 — Basic LAN and IPv4 Addressing

See [docs/sprints/sprint-00-00/README.md](docs/sprints/sprint-00-00/README.md) for the completed
requirements baseline.

## Notes

Simulation results are educational and must not be interpreted as production telecom performance
or security guarantees. Real passwords, keys, customer information, or operator configurations
must not be committed.

## Maintainer

Yunus Emre Kul
