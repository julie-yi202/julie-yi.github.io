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
Each distribution switch sends BPDUs for each VLAN that it is serving as the root bridge. The BPDUs are sent across the respective VLANs. In this example capture, DS1 is sending a BPDU for VLAN 39, and the BPDU is encapsulated in VLAN 39. This is an expected PVST operation.

### On DS2, re-examine the spanning tree for VLAN 100. Why is Gi0/0 elected as the root port?
<img width="1118" height="510" alt="Screenshot 2026-05-15 130908" src="https://github.com/user-attachments/assets/a495ab7e-28ce-4052-90c4-2be28cea4cdf" />
Two ports are connected to the root bridge, Gi0/0 and Gi0/1. They have identical cost (4) and port priority (128).
The root path cost is the sum of the port costs to the root bridge. It is inversely proportional to the bandwidth of the path. In this case, the cost across the two links is identical (4).
Each port has a Spanning Tree port priority associated with it, with the default value of 128. Spanning Tree Port_ID is formed by adding the 4-bit port priority value (the default value of 128) to the 12-bit interface identifier. The total is 16 bits. If the costs are equal, the Port Priority number is used as the tie-breaker. In this case, the port priorities are equal (128), and the lowest interface ID identifies the best path to the root bridge. The reason G0/0 is elected as root port is that it has lowest interface ID.

## Manipulate Spanning-Tree Topology
Although you can manipulate the Spanning Tree cost and port priority using appropriate interface commands (spanning-tree cost and spanning-tree port-priority in the interface configuration mode), you will now focus on the interface speed and its impact on the spanning tree computation. In Cisco Modeling Labs, an IOSvL2 switch node is equipped with 1-Gbps interfaces. If you want to test the Spanning Tree calculation in a topology with various link speeds, you need to manipulate the interface speed.

The default port costs are defined in the following way:

10 Mbps Ethernet ports have a port cost of 100.

100 Mbps Fast Ethernet ports have a port cost of 19.

1 Gbps Ethernet ports have a port cost of 4.

10 Gbps Ethernet ports have a port cost of 2.

### On DS2, disable autonegotiation on Gi0/0 and lower the interface speed to 100 Mbps. Observe how the STP calculation cycles through the consecutive states:
<img width="1097" height="437" alt="Screenshot 2026-05-15 131939" src="https://github.com/user-attachments/assets/28e242f8-5ede-4168-98f0-6b3f814dd0f2" />
<img width="1118" height="482" alt="Screenshot 2026-05-15 131956" src="https://github.com/user-attachments/assets/19e0008d-37fc-40c5-9f06-22393ded2635" />
<img width="1111" height="452" alt="Screenshot 2026-05-15 132025" src="https://github.com/user-attachments/assets/2a54923e-73a4-4f93-9789-10d256c3f8c0" />
<img width="1102" height="464" alt="Screenshot 2026-05-15 132055" src="https://github.com/user-attachments/assets/35b1a900-7cd7-416c-8b44-2ac394cc3c36" />
<img width="1112" height="448" alt="Screenshot 2026-05-15 132127" src="https://github.com/user-attachments/assets/bcfa5586-53ca-44c6-8593-4a81801b8e6c" />
If you watch carefully, you will see the state cycling through the consecutive states. Gi0/0 has a poorer cost (19) and becomes Blocking. Gig0/1 is immediately elected as the root port and is in the listening state first: Then Gig0/1 changes to Learning: Finally, the topology converges and the port is in the forwarding state:
The first part of each output describes the best path to the root and the total cost. The second part of the output lists the costs and port priorities on each interface. In this case, the total cost and the cost of Gi0/1 are the same, because DS2 is directly connected to the root bridge.

# You have delved into details on how STP eliminates redundant links but your task is to optimize the network. What is the easiest way for using both parallel links between the distribution switches? A port channel.

### On DS1 and DS2, configure a port channel with active LACP across the two parallel links.
<img width="1133" height="227" alt="Screenshot 2026-05-15 133045" src="https://github.com/user-attachments/assets/04861f10-a822-45cf-a481-4dcc8a2b387b" />
<img width="1104" height="233" alt="Screenshot 2026-05-15 133140" src="https://github.com/user-attachments/assets/c784cb1c-267d-4550-ad76-f3518019105f" />

### On DS2, verify the port channel interface speed and the resulting STP cost.
<img width="1101" height="527" alt="Screenshot 2026-05-15 133318" src="https://github.com/user-attachments/assets/095f3af0-6298-447c-bad8-57cace593cba" />
The total speed of the port channel is 2 Mbps.
<img width="1110" height="492" alt="Screenshot 2026-05-15 135248" src="https://github.com/user-attachments/assets/ed02f138-633f-428b-b8e3-bee4f0cf94b4" />

The resulting STP cost of the 2 Mbps link is 3.

### On AS2, verify the current Spanning Tree for VLAN 100.
<img width="1096" height="508" alt="Screenshot 2026-05-15 133433" src="https://github.com/user-attachments/assets/ff286df3-9bc8-4e15-9499-3e65348fbdb0" />

### On AS2, increase the SPT cost on Gi0/0 to 10. Change it for all VLANs.
<img width="1102" height="97" alt="Screenshot 2026-05-15 133625" src="https://github.com/user-attachments/assets/3f72dfb9-35e6-493f-93b0-6caa00443cbd" />

### On AS2, re-examine the current spanning tree for VLAN 100. How is it calculated? The converged state, after the listening and learning state, is shown:
<img width="1106" height="444" alt="Screenshot 2026-05-15 133642" src="https://github.com/user-attachments/assets/f8e8a4eb-bfad-40a2-bf7b-297a984a3e90" />
<img width="1094" height="459" alt="Screenshot 2026-05-15 133746" src="https://github.com/user-attachments/assets/de51600a-319b-43e5-a726-19859394a7f9" />

The root port is Gi0/1, connected to DS2. Its interface cost is 4. The total cost to the root is 7, which includes the cost of the Port Channel DS1-DS2.


## Optimize Spanning-Tree Protocol
In this task, you will optimize the STP operation by disabling BPDUs on the access links where they are not needed. You will validate the effect of this optimization by capturing STP packets.
### Capture STP packets on the PC1 uplink. Can you optimize this behavior?
<img width="1090" height="455" alt="Screenshot 2026-05-15 140628" src="https://github.com/user-attachments/assets/481f48c0-5719-4439-bfe6-f18390fd1005" />
The BPDU is not tagged because it is captured on an access link and not a trunk. The root path cost is 4. All STP timers are shown, including the Hello Time, which indicates that the BPDUs are sent every 2 seconds.

Because it is an access link, you can configure it as portfast-edge. This should be done only on ports that are certain to have only endpoints attached to them.

### On AS1 and AS2 downlinks, use the switchport host command or the spanning-tree portfast edge command to configure the PortFast edge feature.
<img width="1145" height="282" alt="Screenshot 2026-05-15 141038" src="https://github.com/user-attachments/assets/aec91291-81e6-47f9-a468-7aa791fb363a" />
<img width="1107" height="306" alt="Screenshot 2026-05-15 141056" src="https://github.com/user-attachments/assets/ac996314-0cee-490f-96ed-376e83a9c30e" />

### Optionally, verify the PortFast edge feature in the spanning tree for VLAN 100.
<img width="1081" height="513" alt="Screenshot 2026-05-15 141301" src="https://github.com/user-attachments/assets/ea39b372-1549-4989-96cd-5a2320f78985" />
<img width="1106" height="518" alt="Screenshot 2026-05-15 141332" src="https://github.com/user-attachments/assets/aec16ee0-49a0-4545-b13e-3df274a2917c" />

### Go to the STP capture on the AS1 downlink. Do you still see the BPDUs?
<img width="1105" height="626" alt="Screenshot 2026-05-15 141643" src="https://github.com/user-attachments/assets/2783691f-fded-479c-a7e2-99a3352847c0" />
The BPDUs are still being sent. The PortFast edge feature does not disable them. An edge port directly transitions to the forwarding state, and skips the listening and learning stages. However, when a BPDU is received, the interface immediately loses its edge port status and becomes a normal spanning-tree port.

### On the AS1 downlink, enable the BPDU filter.
<img width="1106" height="173" alt="Screenshot 2026-05-15 141818" src="https://github.com/user-attachments/assets/83dd7120-4e1f-40b1-aebe-68f6e5c95bf0" />
<img width="1094" height="631" alt="Screenshot 2026-05-15 142212" src="https://github.com/user-attachments/assets/95ccbc81-0cac-4f71-8f32-98f108951b36" />
Check the STP capture on the AS1 downlink. What are the results?

Answer
No BPDUs are being captured. After enabling the BPDU filter on the interface, the interface does not send any BPDUs, and all incoming BPDUs are ignored. This is the equivalent to disabling the spanning tree.

## Create a Loop
A significant advantage with Cisco Modeling Labs is that you do not need to worry about breaking connectivity in your internal lab network. If connectivity is broken, you can stop the lab. In this task, you will create a loop by connecting the access switches on their access ports. Before doing so, you will test IP connectivity among the switches.

Warning: If you create a loop in a lab connected to the outside world via an external bridged connecter, you might impact the physical topology.
### From DS1, check IP connectivity, via VLAN 100, to DS2 (10.0.100.2).
<img width="1105" height="161" alt="Screenshot 2026-05-15 142525" src="https://github.com/user-attachments/assets/7eba485b-397b-49ff-9d38-991267355ceb" />

### Connect the access switches directly across their G0/3 interfaces.
<img width="1099" height="607" alt="Screenshot 2026-05-15 142659" src="https://github.com/user-attachments/assets/3583b52b-8cb7-49b5-9a04-abeb4553c14a" />

### On both access switches, copy the configuration from their Gi0/2 to Gi0/3.
<img width="1101" height="271" alt="Screenshot 2026-05-15 143111" src="https://github.com/user-attachments/assets/62089acd-481d-4436-834d-c2a577ce543a" />
<img width="1093" height="465" alt="Screenshot 2026-05-15 143134" src="https://github.com/user-attachments/assets/874dcda1-f929-4cd7-9a86-5d7b7598c28e" />
<img width="1133" height="307" alt="Screenshot 2026-05-15 143241" src="https://github.com/user-attachments/assets/33536efc-63a5-4568-a1c2-1307af64c60f" />
<img width="1116" height="352" alt="Screenshot 2026-05-15 143346" src="https://github.com/user-attachments/assets/c7a7eedb-c7e0-49a7-871b-bbb20c2543d3" />

### On both access switches, verify the spanning tree for VLAN 100, focusing on the spanning tree role of Gi0/3. Is a loop created?
<img width="1110" height="464" alt="Screenshot 2026-05-15 143746" src="https://github.com/user-attachments/assets/0365a7fa-b4fc-436a-9df1-cdda23ab5080" />
<img width="1099" height="465" alt="Screenshot 2026-05-15 143822" src="https://github.com/user-attachments/assets/60bfa102-5550-4696-b37c-cec6b7810a50" />
AS1 Gi0/3 has the designated role: AS2 Gi0/3 has also the designated role:

### Generate some traffic. From DS1, you may ping DS2 (10.0.100.2) several times; from PC1, ping PC2 (10.0.100.6).
<img width="1102" height="220" alt="Screenshot 2026-05-15 144254" src="https://github.com/user-attachments/assets/044c53b0-be02-4d09-9a22-1e9d5140d94f" />
