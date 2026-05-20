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
