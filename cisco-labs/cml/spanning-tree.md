# Use Cisco Modeling Lab to Explore Spanning-Tree Protocol

## In this lab, you will explore the operation of the Spanning Tree Protocol. The topology consists of four switches that run the default STP mode. The links are configured for trunking. VLAN range 1-200 is used in the network. You will start by designating the primary and secondary root bridges and then explore the STP root path calculation. Then you will optimize the STP operation by configuring a port channel and configuring the PortFast Edge feature, while verifying the results using packet capture and appropriate switch commands.

## Configure Spanning Tree Root Bridges
In this task, you will configure the primary and secondary root bridges. The initial configuration includes these settings:

All interswitch interfaces are configured as 802.1Q trunk ports.

VLANs 1-200 are used in this pilot but they need to be defined on all switches.

Access interfaces to PC1/PC2 are defined as access ports in VLAN 100.

All devices have IP addresses in VLAN 100 with IP subnet 10.0.100.0/24: DS1 (10.0.100.1/24), DS2 (10.0.100.2/24), AS1 (10.0.100.3/24), AS2 (10.0.100.4/24), PC1 (10.0.100.5/24), PC2 (10.0.100.6/24).

### Initial lab in CML
<img width="1113" height="477" alt="Screenshot 2026-05-15 120852" src="https://github.com/user-attachments/assets/f6074878-739d-47f3-a66a-9c0a3fa4eea6" />

### Define VLAN range 1-200 on DS1, DS2, AS1, AS2
<img width="1185" height="570" alt="Screenshot 2026-05-15 121854" src="https://github.com/user-attachments/assets/65885515-b4cc-4fd7-8679-29a1c3a7a42d" />

### Examine the spanning tree summary information.
<img width="1112" height="558" alt="Screenshot 2026-05-15 122026" src="https://github.com/user-attachments/assets/100c02ea-f6cf-4d22-8a9a-7fdbfe8f522f" />
The default mode is used on the switches: Rapid Per-VLAN STP. The selection of the root bridge is currently based on the MAC addresses because no priorities have been configured. You will configure the root bridge selection priorities.

### On PC1, verify the IP addressing and test connectivity to PC2 (10.0.100.6).
<img width="1100" height="415" alt="Screenshot 2026-05-15 122220" src="https://github.com/user-attachments/assets/f0933555-3d3b-4870-a88c-885e6c792dfa" />
<img width="1099" height="508" alt="Screenshot 2026-05-15 122256" src="https://github.com/user-attachments/assets/acb7a2f1-dcfe-4166-8161-12b894f256d7" />

