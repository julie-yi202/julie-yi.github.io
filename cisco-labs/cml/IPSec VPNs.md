# Explore IPsec VPNs
In this lab, you explore IPsec VPNs on Cisco IOS routers and ASAv. A site-to-site is already preconfigured and you will examine the similarities and differences across the two platforms.
## Test IKEv2 IPsec Tunnel Between Cisco Router and ASAv
In this task, you can complete several verification steps that are helpful for troubleshooting IPsec tunnels. Then you will send some interesting traffic and, therefore, establish the tunnel.

<img width="968" height="544" alt="Screenshot 2026-05-20 134754" src="https://github.com/user-attachments/assets/eeefac31-1927-40c2-96b4-60c7fa1d3ab4" />

### Open the consoles of the VPN devices, Branch-router, Firewall, and Internet-router. Go to the privileged mode.
### On the Branch-router, examine the crypto map.
<img width="961" height="383" alt="Screenshot 2026-05-20 135413" src="https://github.com/user-attachments/assets/6116afdd-0106-49cb-991c-274666dd20cb" />

The most important settings in a crypto map include:

The peer, which identifies the remote tunnel headend. In this case, it is the Firewall's outside interface IP address.

IKEv2 profile, which defines the local and remote identities and IKEv2 authentication method.

Interesting traffic, which is defined with an extended ACL. In this case, all traffic from the Branch network 172.16.0.0/24 to the remote subnet 192.168.0.0/24 will be encrypted.

Tunnel negotiation parameters, such as perfect forward secrecy (PFS) and Diffie-Hellman (DH) group.

IPsec transform set, which defines the encryption and authentication protocols applied to the protected traffic.

The interface to which the crypto map is applied. When traffic goes out toward the Internet-router, the access-list is matched to identify which packets must be protected.

### On the Branch-router, examine the routing table and ping the VPN peer (the firewall outside the interface):
<img width="959" height="464" alt="Screenshot 2026-05-20 140132" src="https://github.com/user-attachments/assets/1ce22c4c-1bce-4257-9657-cad0cdff4a2c" />

The routing table must provide reachability information for the VPN peer address and also for the remote site subnet, in this case 192.168.0.0/24. In this scenario, the default route provides both.

### Examine the crypto map and routing configuration on the Firewall.
<img width="962" height="452" alt="Screenshot 2026-05-20 140508" src="https://github.com/user-attachments/assets/4935460b-70ff-4c5e-8efe-9c1edf19dbdf" />

The configuration in the crypto map on the Firewall mirrors the crypto map on the Branch-router, although the configuration syntax is different.
The default route provides the reachability information to the VPN peer and remote subnet.

### view the routing table on the Internet-router.
<img width="959" height="382" alt="Screenshot 2026-05-20 140853" src="https://github.com/user-attachments/assets/cd614e82-121a-4613-98a5-7d4f6cbb0a80" />

The Internet-router knows only its directly connected routes, providing connectivity between the VPN peers. The remote subnets, 172.16.0.0/24 and 192.168.0.0/24, are missing. Packets destined to these subnets would be dropped. You will see the traffic flowing through the VPN tunnel because the interesting traffic is encapsulated in an ESP header. The outer IP addresses of the tunneled traffic will be set to the VPN peer IP addresses.

### On the Branch-router, check the IKEv2 security associations (SAs) before sending traffic through the tunnel.
<img width="962" height="122" alt="Screenshot 2026-05-20 141100" src="https://github.com/user-attachments/assets/cdb8d251-79bc-4862-a24c-e416b10b143d" />

There are no IKEv2 SAs because no interesting traffic has been exchanged and the IKEv2 negotiation has not been triggered. The Internet Key Exchange (IKE) is used to set up a secure and authenticated communication channel between two VPN peers. This is known as Phase 1. The main role of IKE is to negotiate IPsec security associations, allowing the traffic to be protected. The negotiation of the IPsec SAs is known as Phase 2.

### On the Branch-router, check the IPsec security associations before sending traffic through the tunnel.
<img width="465" height="365" alt="Screenshot 2026-05-20 142754" src="https://github.com/user-attachments/assets/70e241c6-7bf7-44ed-b070-6a40e4d97d10" />

You can see the interesting traffic definition but the packet counters should be "0." There are no outbound or inbound SAs. The IPsec SAs have not yet been negotiated but Cisco IOS routers display the interesting traffic description as it is already known. One set of counters describes the outgoing traffic: encapsulated with the tunnel header, encrypted, and authenticated (computed digest message). The next set of counters describes the incoming traffic (decapsulated, decrypted, and with verified message digest). The remaining counters refer to the compression.

### Check the IKEv2 and IPsec SAs on the Firewall.
<img width="972" height="113" alt="Screenshot 2026-05-20 143135" src="https://github.com/user-attachments/assets/fd8a792e-6675-455b-b603-0ceb763c15a4" />

The Firewall does not display any IPsec security associations.

### Open the consoles of Branch-endpoint and Inside-endpoint. Log in as cisco/cisco. On the Branch-endpoint, check the IP addressing and routing information and ping the remote endpoint 192.168.0.1. Keep the ping running to monitor the packet counters on the IPsec SAs.
<img width="969" height="201" alt="Screenshot 2026-05-20 143711" src="https://github.com/user-attachments/assets/0d159bff-a46f-411a-8e76-992203fce106" />

<img width="953" height="114" alt="Screenshot 2026-05-20 143742" src="https://github.com/user-attachments/assets/a6466683-f7e1-42e3-9a09-df6a118e160d" />

The default gateway, 172.16.0.254, is the Branch-router.
<img width="953" height="192" alt="Screenshot 2026-05-20 143856" src="https://github.com/user-attachments/assets/97c39201-77ed-4870-8f28-476ae8803121" />

The traffic is flowing through the tunnel, otherwise it would be dropped by the Internet-router, which does not know the remote networks.

### Verify the IKEv2 SAs on the Branch-router.
<img width="965" height="201" alt="Screenshot 2026-05-20 144334" src="https://github.com/user-attachments/assets/488f0ef6-4582-47ca-9a41-52d1f39852b5" />

The IKEv2 SA is established. You can think of it as a secure channel to negotiate the IPsec SAs (Phase 2).
### Verify the IPsec SAs on the Branch-router.
<img width="973" height="483" alt="Screenshot 2026-05-20 145059" src="https://github.com/user-attachments/assets/1ea07cf4-4ef4-4433-b148-2227d45060a9" />

The inbound and outbound Encapsulating Security Payload (ESP) SAs are established. In contrast to the Authentication Header (AH) (not used in this scenario), ESP provides authentication and encryption.
