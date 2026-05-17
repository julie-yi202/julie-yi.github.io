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
<img width="979" height="357" alt="Screenshot 2026-05-16 224956" src="https://github.com/user-attachments/assets/6c1c53c3-0e2f-4f78-b295-9dc5adf74fc1" />
<img width="974" height="351" alt="Screenshot 2026-05-16 225018" src="https://github.com/user-attachments/assets/3e6c2ad4-5fec-4fde-a783-1d76703af0b2" />
<img width="974" height="333" alt="Screenshot 2026-05-16 225052" src="https://github.com/user-attachments/assets/817dd309-4c03-44d9-8c5a-c1b1e9ef84ff" />
<img width="989" height="276" alt="Screenshot 2026-05-16 225107" src="https://github.com/user-attachments/assets/f1d018c3-943a-4240-82f5-1db5bcf78449" />
<img width="996" height="82" alt="Screenshot 2026-05-16 225245" src="https://github.com/user-attachments/assets/3243bd57-886e-416f-928b-1c6f9348418f" />
<img width="973" height="335" alt="Screenshot 2026-05-16 225302" src="https://github.com/user-attachments/assets/2718b924-c7df-4ad9-9e0a-7255807b1eaa" />
<img width="970" height="311" alt="Screenshot 2026-05-16 225322" src="https://github.com/user-attachments/assets/8154c4b7-cb50-41d8-a1b9-c95e88eaf8a8" />
<img width="973" height="305" alt="Screenshot 2026-05-16 225342" src="https://github.com/user-attachments/assets/24fc903b-24c9-46bb-88c7-fcbbc5f36b72" />
<img width="973" height="339" alt="Screenshot 2026-05-16 225401" src="https://github.com/user-attachments/assets/c108aef7-e064-44cb-98c3-86a3657a3d35" />
<img width="1012" height="296" alt="Screenshot 2026-05-16 225440" src="https://github.com/user-attachments/assets/82611e62-b25d-4b2b-801d-4c178b165efd" />
<img width="969" height="330" alt="Screenshot 2026-05-16 225701" src="https://github.com/user-attachments/assets/a9309334-11c8-4c23-a7dd-f34748d1ec4c" />
<img width="971" height="321" alt="Screenshot 2026-05-16 225720" src="https://github.com/user-attachments/assets/21759132-f07d-4f04-87f1-43539d4a9618" />
<img width="992" height="281" alt="Screenshot 2026-05-16 225737" src="https://github.com/user-attachments/assets/67a64608-1f7b-419d-8618-3a22bdd01b52" />
<img width="1007" height="350" alt="Screenshot 2026-05-16 225759" src="https://github.com/user-attachments/assets/6d4426f2-1206-41f4-892e-f3e4c5212d47" />
<img width="968" height="323" alt="Screenshot 2026-05-16 225816" src="https://github.com/user-attachments/assets/3143c896-833f-41c1-aab8-608e6f517f49" />
<img width="981" height="293" alt="Screenshot 2026-05-16 225831" src="https://github.com/user-attachments/assets/1556561f-efd1-4216-adc7-a6b313c6a50b" />
<img width="990" height="106" alt="Screenshot 2026-05-16 225847" src="https://github.com/user-attachments/assets/240f533b-b414-418a-ba3d-9a5169a04765" />

Imagine that you are requested to configure R3 for OSPFv3 on R3 in Area 1. Is it feasible to have multiple instances of Area 1 in the topology? Note that Area 1 is already used between R1 and ABR1.

The requested R3 settings are:
Router ID set to Loopback 0 IPv4 address
Area 1 configured on Loopback 0 and Gigabit Ethernet 0/0.
