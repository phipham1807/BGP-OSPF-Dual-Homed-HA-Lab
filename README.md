# Enterprise Network Simulation with High Availability (OSPF and eBGP)

## Introduction
This project simulates a large-scale enterprise network architecture using Cisco Packet Tracer. The system integrates Multi-area OSPF for internal routing and eBGP multi-homing with dual independent Internet Service Providers (ISPs) to achieve High Availability (HA) and seamless failover capabilities.

---

## Core Features and Deployed Technologies

### 1. Interior Gateway Protocol (IGP) - Multi-Area OSPF
* **Multi-Area Architecture:** Divides the enterprise network into Area 0 (Backbone) for core/WAN links and Area 10/20 for branch office LAN segments.
* **Default Route Origination:** Configures the edge routers to inject a default route (`0.0.0.0/0`) into the internal OSPF domain, allowing internal hosts to reach external networks.
* **Routing Optimization:** Synchronizes internal routing tables across the Core (`R-CORE`), Edge (`R-EDGE_1`, `R-EDGE_2`), and Branch (`R-BRANCH_A`, `R-BRANCH_B`) routers.

### 2. Exterior Gateway Protocol (EGP) - eBGP Multi-Homing
* **External Peering:** Establishes eBGP sessions between the enterprise AS 65000 and two independent service providers (`ISP-A` as AS 65010 and `ISP-B` as AS 65020).
* **Redundancy and Path Management:** Enables dual connections to the Internet, preventing single points of failure at the network edge.

### 3. Static Routing and Round-Trip Closure
* **Edge Routing:** Implements static default routes pointing from edge routers to respective ISP gateways.
* **Return Path Configuration:** Configures static routes on ISP and Service routers (`R-SERVICE`) to ensure proper round-trip packet flow back into the enterprise network segments (`192.168.x.x` and `10.x.x.x`).

### 4. High Availability and Failover Testing
* **Seamless Failover:** Automatically reroutes traffic through the backup ISP path when the primary ISP link or edge connection fails, ensuring zero permanent interruption for active end-user sessions.

Verification and Testing Guide
1. Open the .pkt topology file using Cisco Packet Tracer software.
2. Access R-CORE and run the command show ip ospf neighbor to verify that all OSPF adjacencies are in the FULL state.
3. From any workstation (e.g., PC-A), execute ping 8.8.8.8 to verify end-to-end connectivity.
4. Test the High Availability feature by shutting down the primary interface facing ISP-A (e.g., interface GigabitEthernet0/0/0 followed by shutdown) and observing the automatic traffic failover to ISP-B.