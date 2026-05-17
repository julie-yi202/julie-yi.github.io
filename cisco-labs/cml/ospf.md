# Use Cisco Modeling labs to explore OSPF Basics
Cisco Modeling Labs is practical for exploring network technologies and testing new functionalities. Suppose you already used traditional OSPFv2 before but you want to familiarize yourself with OSPFv3 because you are planning to use the same OSPF process for both IPv4 and IPv6. On top of that, you want to test a few features that are related to database exchange and adjacency establishment. You can do all of that in this lab or in a similar lab that you can easily spin up.

## Complete OSPFv3 Configuration for IPv4
In this task, you will examine the configured OSPF topology and complete the configuration on R3. Focus on IPv4 only.

### Make sure that your basic topology is loaded. Start the lab if needed.
<img width="1003" height="580" alt="Screenshot 2026-05-16 224050" src="https://github.com/user-attachments/assets/e6763a67-4bc9-4e34-a979-830fce795837" />

### Open the consoles of all routers and enter the privileged mode. Familiarize yourself with the existing setup. Use OSPFv3 commands to verify the OSPF neighbor relationships, database, and the resulting IPv4 routing tables. Which routing process ID is used in your topology?
Use the following verification commands: show ospfv3 neighbor, show ip route ospfv3, show ospfv3 database.

Your network is configured using OSPFv3, which allows you to exchange both IPv4 and IPv6 address families within a single OSPFv3 process. In this example, only IPv4 is enabled, but you could add IPv6 to the existing process.

The OSPFv3 process ID differs across the routers (ID 10 on the ABRs, ID 1 on R1, and ID 2 on R2). The process ID is a locally significant number and does not have to match between adjacent devices.
