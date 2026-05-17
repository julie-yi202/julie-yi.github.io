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
### Configure OSPFv3 on R3. Add the Loopback and the active Gigabit Ethernet interface to Area 1.
<img width="961" height="184" alt="Screenshot 2026-05-16 230657" src="https://github.com/user-attachments/assets/bf72cda2-e2f5-49fe-898d-56e169127c4d" />

### Verify the connectivity on R3. You can ping the preconfigured hostnames, especially R1, which also belongs to Area 1.
<img width="960" height="77" alt="Screenshot 2026-05-16 230908" src="https://github.com/user-attachments/assets/79c6c8ec-ccf2-484e-9015-ac267862b7a5" />
<img width="975" height="247" alt="Screenshot 2026-05-16 230929" src="https://github.com/user-attachments/assets/43d5e5ba-0695-4943-9d78-3b62d125c9f2" />
<img width="965" height="108" alt="Screenshot 2026-05-16 230950" src="https://github.com/user-attachments/assets/97986afc-21c5-4af8-8be8-c46da7cdbddd" />
Although OSPF defines that the backbone area (0) acts as the central area to which all leaf areas are connected, multiple occurrences of the same leaf area ID are possible. Next, you will examine the database for any conflicts related to the duplicate area ID 1. You can perform the verification on any ABR.

### On ABR1, optionally, examine the OSPF database, focusing on the loopback IP of R3. Check if the original area ID is carried in the interarea prefix LSAs.
<img width="968" height="370" alt="Screenshot 2026-05-16 231624" src="https://github.com/user-attachments/assets/48df284b-ce20-4cb1-a419-ac2df9b6d941" />
<img width="963" height="368" alt="Screenshot 2026-05-16 231645" src="https://github.com/user-attachments/assets/8e2def71-c18a-4eef-8b13-ce99ed593a62" />
The interarea prefix LSA occurs twice in the ABR database, in the backbone, and in the leaf database.
<img width="975" height="372" alt="Screenshot 2026-05-16 231710" src="https://github.com/user-attachments/assets/debf7718-1ff6-477e-885a-ec6f831ffc96" />
The network is advertised into Area 0 by ABR2 and into the left Area 1 by ABR1. The double occurrence of the area ID does not cause any conflicts because the originating area ID is not carried in the updates.

### On R2, configure OSPFv3 Area 1 on Gig0/1, attached to R1. Do you expect R2 to become an ABR?
<img width="988" height="121" alt="Screenshot 2026-05-16 232346" src="https://github.com/user-attachments/assets/6eb5e699-af23-409b-9b69-332d6857d5a1" />

### Verify the role of R2. Note that two areas, 1 and 2, are attached to it. Focus on IPv4 only.
<img width="891" height="346" alt="Screenshot 2026-05-16 232727" src="https://github.com/user-attachments/assets/85cfaf41-ebce-4f8a-b83e-a454c04c254b" />
<img width="874" height="370" alt="Screenshot 2026-05-16 232744" src="https://github.com/user-attachments/assets/e9dab716-c085-4edd-bfb6-01d8ec402c0f" />
The two adjacencies are operational.
<img width="908" height="265" alt="Screenshot 2026-05-16 232800" src="https://github.com/user-attachments/assets/86f18391-bf8f-4165-a94b-dfab1280535f" />
One way of verifying that R2 is not an ABR, despite its membership in Area 1 and 2 is to look for advertising routers in the interarea LSAs. R2 is not an advertising router for those LSAs, which means that it is not an ABR. An ABR is a router that has an interface in Area 0 and in at least one leaf area.

Optionally, ping the loopbacks of other routers to check for any loops in the routing table. OSPF prevents the loops by enforcing the fixed hierarchy with the backbone area in the center and the leaf areas attached to the backbone.
## Why an ABR must connect to Area 0
OSPF’s backbone (Area 0) is the central hub for all inter‑area routing.
OSPF requires that:

All non‑backbone areas must have a path to Area 0

All inter‑area LSAs (Type‑3) must be injected into Area 0 first

Only routers connected to Area 0 are allowed to generate Type‑3 LSAs

So a router becomes an ABR only if:

It has interfaces in two or more areas, AND

One of those areas is Area 0

If a router touches multiple non‑backbone areas (like Area 1 and Area 2), it does NOT become an ABR.
## Apply this to your R2
Your R2 has:

Gi0/1 → Area 1

Gi0/0 → Area 2

But no interface in Area 0.

So even though it participates in two areas, it cannot be an ABR.

This is why:

R2 does not set the ABR bit in its Router‑LSA

R2 does not originate any Type‑3 LSAs

Other routers (192.168.0.11 and 192.168.0.12) are doing the ABR work


