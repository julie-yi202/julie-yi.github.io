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
PC1 (10.0.100.5) and PC2 (10.0.100.6) have been assigned to VLAN 100 and can communicate with one another.

### Next, you will divide the VLANs into two ranges: 1-100 and 101-200. For the first range, DS1 should be the primary root bridge and DS2 the secondary root bridge. Reverse the roles for the second range. You do not need to modify the priorities on the access switches.
<img width="1102" height="142" alt="Screenshot 2026-05-15 123911" src="https://github.com/user-attachments/assets/5bb5883a-2de8-4366-8b82-bd1736530cdf" />
<img width="1106" height="142" alt="Screenshot 2026-05-15 123930" src="https://github.com/user-attachments/assets/70ab99f8-7699-4c07-b93d-62c7db9d0cf5" />

### Verify the spanning tree information for a VLAN in the first range, such as 100. Examine the topology on all four switches.
<img width="1098" height="432" alt="Screenshot 2026-05-15 124359" src="https://github.com/user-attachments/assets/b58fd402-7ac7-41cf-98f4-b8d03ef77df5" />
<img width="1093" height="484" alt="Screenshot 2026-05-15 124451" src="https://github.com/user-attachments/assets/51e8e27e-ca2b-4e16-8b2b-3012dd37ac92" />
<img width="1097" height="502" alt="Screenshot 2026-05-15 124538" src="https://github.com/user-attachments/assets/7a32e732-3d91-4ba8-bd01-1d529267e0cc" />
<img width="1122" height="502" alt="Screenshot 2026-05-15 124609" src="https://github.com/user-attachments/assets/7570c0fd-bd2b-4510-8aa2-f592c2ab7639" />
In the Spanning Tree for VLAN 100, DS1 has a better priority (24676) than DS2 (28772) and is, therefore, elected as the root bridge.
The access switches have the default priority 32868.
On access switches, the interface connected to DS1 (Gi0/0) is the root port. The interface toward DS2 (Gi0/1) is the alternate port in a blocking state.

### Verify the spanning tree information for a VLAN in the second range, such as 101.
<img width="1118" height="523" alt="Screenshot 2026-05-15 125357" src="https://github.com/user-attachments/assets/8513322d-796d-47ca-9914-2706336c7cfa" />
<img width="1111" height="510" alt="Screenshot 2026-05-15 125442" src="https://github.com/user-attachments/assets/ba7b2cfa-410f-4ead-b01d-8a542320024c" />
<img width="1130" height="563" alt="Screenshot 2026-05-15 125511" src="https://github.com/user-attachments/assets/b838b9c1-44c9-47b3-9e50-5e96996c15ec" />
<img width="1108" height="491" alt="Screenshot 2026-05-15 125539" src="https://github.com/user-attachments/assets/d2f13c4e-4c2b-4e91-9ef9-e8cfc74e082f" />
In the Spanning Tree for VLAN 101, the roles of the distribution switches are reversed.
As in VLAN 100, the access switches have the default priority 32868 in the SPT for VLAN 101.
On access switches, the interface connected to DS2 (Gi0/1) is the root port. The interface toward DS1 (Gi0/0) is the alternate port in a blocking state.

### Configure packet capture on the first DS1-DS2 link (Gi0/0-Gi0/0). Examine the STP BPDUs.
<img width="1093" height="502" alt="Screenshot 2026-05-15 130231" src="https://github.com/user-attachments/assets/ca58ec6a-2276-4a95-8a41-f9cca92d2a5a" />
<img width="1101" height="479" alt="Screenshot 2026-05-15 130331" src="https://github.com/user-attachments/assets/16a3679d-e67c-4e37-8526-979e39b7bb7b" />
