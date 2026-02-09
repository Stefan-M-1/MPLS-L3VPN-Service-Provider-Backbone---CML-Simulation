# MPLS-L3VPN-Service-Provider-Backbone---CML-Simulation
MPLS L3VPN Service Provider Backbone - CML Simulation
Service Provider MPLS L3VPN infrastructure using a 5-node topology in Cisco Modeling Labs (CML). The lab focuses on providing private connectivity between two customer sites over a shared provider core using VRF isolation.

🏗 Topology Overview
The network consists of the following components:

CE1 & CE2 (Customer Edge): Standard routers located at customer sites using OSPF to exchange routes with the provider.

PE1 & PE2 (Provider Edge): The "intelligence" of the network. They handle VRF isolation, MPLS label imposition/disposition, and MP-BGP route exchange.

P (Provider Core): A core router performing pure MPLS Label Switching (LDP). It remains "unaware" of customer IP routes, ensuring scalability.

🛠 Technologies & Protocols
IGP (OSPFv2): Used within the Provider core for internal reachability of Loopback interfaces.

MPLS LDP (Label Distribution Protocol): Used to build the Label Switched Path (LSP) for the transport plane.

MP-BGP (VPNv4): Facilitates the exchange of customer routes between PE routers using Route Distinguishers (RD) and Route Targets (RT).

VRF (Virtual Routing and Forwarding): Enables traffic isolation for CLIENT_A, allowing for overlapping IP address spaces if necessary.

🔍 Key Challenges & Solutions (Lessons Learned)
During the implementation, several critical technical hurdles were addressed:

OSPF Route Redistribution: Identified that the subnets keyword is mandatory when redistributing BGP into OSPF. Without it, OSPF ignores non-classful routes (like /32 Loopbacks), preventing end-to-end reachability.

MPLS MTU Overhead: Addressed packet drops in the virtual environment by increasing the MPLS MTU to 1508 bytes. This accounts for the 8-byte overhead added by the MPLS label stack (Transport + VPN labels).

Control Plane vs. Data Plane: Verified that while BGP can exchange routes (Control Plane), the traffic will fail if the LSP (Data Plane) is not properly established via LDP on all core-facing interfaces.

📊 Verification
The following commands were used to verify the operational status:

show mpls forwarding-table: Confirmed the existence of valid outgoing labels for PE Loopbacks.

show ip bgp vpnv4 all: Verified that VPNv4 prefixes are being exchanged with the correct Route Targets.

show ip route vrf CLIENT_A: Confirmed that customer routes are present in the specific VRF routing table.

Final Test: ping 2.2.2.2 source 1.1.1.1 from CE1 resulted in 100% success.
