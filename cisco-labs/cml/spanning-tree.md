# Use Cisco Modeling Lab to Explore Spanning-Tree Protocol

# In this lab, you will explore the operation of the Spanning Tree Protocol. The topology consists of four switches that run the default STP mode. The links are configured for trunking. VLAN range 1-200 is used in the network. You will start by designating the primary and secondary root bridges and then explore the STP root path calculation. Then you will optimize the STP operation by configuring a port channel and configuring the PortFast Edge feature, while verifying the results using packet capture and appropriate switch commands.

# Configure Spanning Tree Root Bridges
In this task, you will configure the primary and secondary root bridges. The initial configuration includes these settings:

All interswitch interfaces are configured as 802.1Q trunk ports.

VLANs 1-200 are used in this pilot but they need to be defined on all switches.

Access interfaces to PC1/PC2 are defined as access ports in VLAN 100.

All devices have IP addresses in VLAN 100 with IP subnet 10.0.100.0/24: DS1 (10.0.100.1/24), DS2 (10.0.100.2/24), AS1 (10.0.100.3/24), AS2 (10.0.100.4/24), PC1 (10.0.100.5/24), PC2 (10.0.100.6/24).


