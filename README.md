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


