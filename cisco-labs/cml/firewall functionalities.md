# Use Cisco Modeling Labs to Explore Firewall Functionalities
 This lab centers on a Cisco ASAv firewall. You will first examine the preconfigured inbound access from a branch office to a front-end server, and then you enable outbound internet connectivity across the Cisco ASAv.

 ## Examine Inbound Connectivity
 In this task, you examine the configuration blocks required for inbound access through the Cisco ASAv firewall. The clients are in the Branch office, which is attached to the firewall Branch interface. The front-end server is connected to the firewall Server interface.

 ### Lab Topology
<img width="948" height="426" alt="Screenshot 2026-05-18 000434" src="https://github.com/user-attachments/assets/f4f8b940-1786-413a-92bf-9031ca5cc024" />

 ### Open the console of the Front-end server and log in as cisco/cisco. Activate the ens2 interface and check its preconfigured IP address.
<img width="965" height="286" alt="Screenshot 2026-05-18 000816" src="https://github.com/user-attachments/assets/7c4a7671-6195-4c29-8780-a406e6ee2402" />

### Add a default route via 192.168.1.1, then verify it was applied.
<img width="962" height="77" alt="Screenshot 2026-05-18 000957" src="https://github.com/user-attachments/assets/677559b9-0e13-43ba-8d45-596a04cc17dd" />

### Open the Firewall console and enter the privileged mode using the password cisco. View the routing table and test IP connectivity to the Front-end server (192.168.1.6) and Branch-endpoint 198.51.100.3.
<img width="994" height="281" alt="Screenshot 2026-05-18 001230" src="https://github.com/user-attachments/assets/1034a8cf-89ad-4d59-85f4-8d6ff3f37554" />
<img width="973" height="203" alt="Screenshot 2026-05-18 001318" src="https://github.com/user-attachments/assets/70fbc93e-e791-43cd-8f46-47ee75e44bae" />

### Verify the configured access lists and how they are applied to interfaces.
<img width="975" height="111" alt="Screenshot 2026-05-18 001730" src="https://github.com/user-attachments/assets/af9cc890-de47-4f90-ab0c-1743a73019ea" />

### View the objects used for allowing access to the front-end server via the Branch interface.
<img width="976" height="108" alt="Screenshot 2026-05-18 001956" src="https://github.com/user-attachments/assets/576d5184-1cb5-405c-8890-d81b5fa0cba6" />
The front-end server has two objects associated with it, with the private and the public address:
The object group indicates that only HTTP (port 80) is allowed to the front-end server:

### Open the console of the front-end server and log in cisco/cisco. Use the Netcat utility to open port 80 for listening and thus simulate a running web service and Open the console of the Branch-endpoint and log on as cisco/cisco. Use the Netcat utility to connect to a front-end server public address on port 80. Use the verbosity option to print the scan result.
<img width="975" height="42" alt="Screenshot 2026-05-18 002457" src="https://github.com/user-attachments/assets/0af807ce-9290-4f09-a22f-1416d37e03e3" />
<img width="983" height="310" alt="Screenshot 2026-05-18 002525" src="https://github.com/user-attachments/assets/cdd54929-eb20-4d8c-9b32-97b2c548bc5a" />

### On the Firewall, view the connection and the translation table.
<img width="963" height="142" alt="Screenshot 2026-05-18 002647" src="https://github.com/user-attachments/assets/93948d85-be54-4f1a-8d23-4ac61ef812f5" />
The connection table tracks the state of all connections transiting the firewall. Flag U means that the TCP handshake has completed. The absence of other flags indicates that no additional data is being exchanged:
The translation table displays the address translations used by the traffic:
In this case, the front-end server private address (192.168.1.6, attached to the Servers interface) is presented via the Branch interface using the public address 203.0.113.3.

### Interrupt the Netcat tool on the front-end server. Use the same method to test connectivity on another port, for example 443.
<img width="964" height="44" alt="Screenshot 2026-05-18 003225" src="https://github.com/user-attachments/assets/5d66e83e-e81d-413e-9070-51989e613f45" />
<img width="970" height="55" alt="Screenshot 2026-05-18 003244" src="https://github.com/user-attachments/assets/f4e2d97a-afcd-45a8-9b29-460cd43a961a" />

### On the Firewall, view the access list to examine the hit count for the dropped traffic:
<img width="965" height="103" alt="Screenshot 2026-05-18 003429" src="https://github.com/user-attachments/assets/f4095db2-2cf8-42dd-b90c-759b5c5a4a67" />

## Enable Outbound Connectivity
In this task, you will enable DHCP on the Inside interface to provide IP addressing to the internal clients. You will attach an external connector in NAT mode to provide Internet connectivity. Then, you will configure address translation and test outbound traffic to the Internet.

### Open the console on the Inside-client, log in as cisco/cisco, and view the IP address on the network adapter.
<img width="967" height="150" alt="Screenshot 2026-05-18 003712" src="https://github.com/user-attachments/assets/4d07091b-07ab-46c6-912d-8d094fbf7a48" />
The IP address on the eth0 adapter is missing because the client is configured for DHCP and no offers have been received.

### Optionally, start traffic capture on the firewall inside the interface to see the DHCP exchange that you will enable in the next step.
<img width="974" height="271" alt="Screenshot 2026-05-18 004149" src="https://github.com/user-attachments/assets/1c7ddd60-1c40-4c60-82db-67372be2eeeb" />

### On the Firewall, configure a DHCP server on the Inside interface, with the address range 192.168.0.30-192.168.0.40, DNS server 8.8.8.8, and domain cml.local.
<img width="962" height="146" alt="Screenshot 2026-05-18 004545" src="https://github.com/user-attachments/assets/b45194ed-4b45-47a2-a836-ce7c8f68773e" />

### On the Inside-client, re-check the IP addressing.
<img width="971" height="295" alt="Screenshot 2026-05-18 004627" src="https://github.com/user-attachments/assets/9bcaf01a-19be-4a4e-ac8c-2cdeff30c0b8" />
The inside client should have obtained the IP address from the configured pool:

### On the Inside-client, verify the received DNS server configuration.
<img width="970" height="59" alt="Screenshot 2026-05-18 004902" src="https://github.com/user-attachments/assets/9c1eb7e6-1fdd-4df5-aed0-ec3c5de700f3" />

### In your lab topology, add an external connector and drop it left of the Firewall.
<img width="950" height="449" alt="Screenshot 2026-05-18 005111" src="https://github.com/user-attachments/assets/ce44390d-efa1-4f53-8087-7ac91655f012" />

### Go to the Config tab and make sure that NAT mode is chosen by default.
<img width="959" height="407" alt="Screenshot 2026-05-18 005238" src="https://github.com/user-attachments/assets/0bb5cba7-ad59-4ffd-9d58-91e57b97be8f" />

### On the Firewall, verify the interface IP addresses, focusing on the Outside interface.
<img width="973" height="146" alt="Screenshot 2026-05-18 005516" src="https://github.com/user-attachments/assets/1c1a46b0-993f-4ede-b763-c2699b5304a2" />
The Outside interface is missing.

### On the Firewall, configure the Outside interface to obtain internet connectivity via the external connector and install a default route to the internet. You need to configure the interface name and enable the DHCP client with the setroute option, to install a default route:
<img width="969" height="102" alt="Screenshot 2026-05-18 005810" src="https://github.com/user-attachments/assets/ee358c94-d6d2-43a8-abb6-9ebda5d50095" />
The default security level is set to the lowest, least secure value (0), which is accurate for an Outside interface. There is no need to modify it.

### On the Firewall, verify the IP address on the Outside interface.
<img width="966" height="101" alt="Screenshot 2026-05-18 005947" src="https://github.com/user-attachments/assets/68171200-72bd-4b09-bf73-6d03ff01e154" />

### On the Firewall, verify the routing table and connectivity to the DNS server 8.8.8.8.
<img width="959" height="269" alt="Screenshot 2026-05-18 010126" src="https://github.com/user-attachments/assets/4cf68bdd-b884-4e28-8011-c835665b8209" />
The default route gets installed in the routing table via the Outside interface:
<img width="957" height="85" alt="Screenshot 2026-05-18 010215" src="https://github.com/user-attachments/assets/2a6209ed-c006-4efe-925f-978d058e75d2" />

### On the Inside-client, ping www.cisco.com. Why does it fail? Try to troubleshoot on your own.
<img width="974" height="77" alt="Screenshot 2026-05-18 010431" src="https://github.com/user-attachments/assets/242cc512-2657-4812-9416-7a98fe3fd894" />
Ping fails:
The name resolution also fails. IP connectivity to the firewall and then from the firewall to the Internet has been verified. The two potential reasons for packet drops on the firewall are an ACL and address translation. Traffic from a higher to a lower security level interface is permitted by default, so no explicit ACL is needed. Address translation, however, must be configured. In this case, you need to configure inside PAT using the Outside IP address.
NOTE: This results in traffic using PAT twice; once by the ASAv as traffic passes to the Outside interface, and a second time by the CML server as it passes through the external connector.

### Configure a network object for the Inside-clients and enable dynamic PAT using the Outside interface.
<img width="942" height="84" alt="Screenshot 2026-05-18 010818" src="https://github.com/user-attachments/assets/1135fae9-786a-4067-bf39-23bf4c7643e0" />
NOTE: Now you have a chain of PAT devices: the Firewall and the external connector. Such address translation provides outbound connectivity in Cisco Modeling Labs, as an alternative to attaching the external connector to each device that requires outbound access. You could use this approach with routers, too.

### From the Inside-client, ping the DNS server 8.8.8.8, and test connectivity to Cisco.com.
<img width="958" height="191" alt="Screenshot 2026-05-18 011037" src="https://github.com/user-attachments/assets/687bfc9b-c5cb-48e2-952d-fcbc30cf53da" />

### From the Inside-client, use the Netcat utility to connect to www.cisco.com over port 80.
<img width="967" height="28" alt="Screenshot 2026-05-18 011548" src="https://github.com/user-attachments/assets/0c2fb675-fab4-4a40-b0bd-bfb309a0e37c" />

### On the Firewall, verify the translation and connection table. This validation completes the lab activity.
<img width="958" height="154" alt="Screenshot 2026-05-18 011625" src="https://github.com/user-attachments/assets/af52f615-8225-4d58-9c67-b0414798b923" />
The connection table describes the established session for the stateful firewall purposes.
<img width="960" height="205" alt="Screenshot 2026-05-18 011647" src="https://github.com/user-attachments/assets/e4c8d702-c0bd-482b-b8ed-8af834943371" />
The translation table shows a port translation of the client IP and source port to the firewall outside IP address, preferably using the same port, if available.


