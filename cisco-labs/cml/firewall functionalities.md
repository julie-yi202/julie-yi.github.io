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

### Open the Firewall console and enter the privileged mode using the password cisco. View the routing table and test IP connectivity to the Front-end server (
192.168.1.6) and Branch-endpoint 198.51.100.3.
<img width="994" height="281" alt="Screenshot 2026-05-18 001230" src="https://github.com/user-attachments/assets/1034a8cf-89ad-4d59-85f4-8d6ff3f37554" />
<img width="973" height="203" alt="Screenshot 2026-05-18 001318" src="https://github.com/user-attachments/assets/70fbc93e-e791-43cd-8f46-47ee75e44bae" />
