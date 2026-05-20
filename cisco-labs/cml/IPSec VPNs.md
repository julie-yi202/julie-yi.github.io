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
<img width="958" height="222" alt="Screenshot 2026-05-20 145228" src="https://github.com/user-attachments/assets/aebfdcc6-fd02-4904-9fc8-430c3e68d706" />

The inbound and outbound Encapsulating Security Payload (ESP) SAs are established. In contrast to the Authentication Header (AH) (not used in this scenario), ESP provides authentication and encryption.
### Verify the IKEv2 and IPsec SAs on the Firewall.
<img width="968" height="241" alt="Screenshot 2026-05-20 145521" src="https://github.com/user-attachments/assets/98d72293-e914-4248-a36e-9ac6deb8365c" />

The IKEv2 SA is established. You can see the protection parameters for the message exchange.
<img width="960" height="465" alt="Screenshot 2026-05-20 145718" src="https://github.com/user-attachments/assets/00fce5bd-978c-4163-a425-2afba499d2f7" />
<img width="958" height="315" alt="Screenshot 2026-05-20 145737" src="https://github.com/user-attachments/assets/544c5015-f32f-471c-a1eb-73ec14e6e7f2" />

The inbound and outbound ESP SAs are established.

## Compare IPsec Configurations on Cisco IOS and ASAv
In this task, you will examine the configuration on both VPN peers. Optionally, you can also verify the settings using various show commands.
### On the Branch-router, examine the IKEv2 proposal.
<img width="962" height="92" alt="Screenshot 2026-05-20 150424" src="https://github.com/user-attachments/assets/84243208-9463-424a-b239-6446a6a28d64" />

An IKEv2 proposal is a collection of transforms used in the negotiation of IKE SAs as part of the IKE_SA_INIT exchange. The transform types used in the negotiation include the encryption algorithm, integrity algorithm, pseudo-random function (PRF) algorithm, and Diffie-Hellman (DH) group. You must configure at least one encryption algorithm, one integrity algorithm, and one DH group for the proposal to be complete. The PRF algorithm is the same as the integrity algorithm, and therefore, it is not configured separately. Multiple transforms can be configured and proposed by the initiator for encryption, integrity, and group, of which one transform is selected by the responder. When multiple transforms are configured for a transform type, the order of priority is from left to right.

Apart from the configured custom proposal, a default IKE2 proposal comes out-of-the-box and can be examined below:
<img width="955" height="212" alt="Screenshot 2026-05-20 150534" src="https://github.com/user-attachments/assets/a9225998-1b19-4735-88fe-2316d3cb23f5" />

<img width="966" height="98" alt="Screenshot 2026-05-20 150637" src="https://github.com/user-attachments/assets/6b9d5538-aa1a-452a-b7eb-cd0ad5f05416" />

An IKEv2 policy contains proposals that are used to negotiate the encryption, integrity, PRF algorithms, and DH group in an SA_INIT exchange. It can have match statements, which are used as selection criteria to select a policy during negotiation.

Apart from the configured policy, the default IKE2 policy is shown below:
<img width="955" height="212" alt="Screenshot 2026-05-20 150723" src="https://github.com/user-attachments/assets/f26bd69f-cb67-4180-9f11-c748e433b096" />
### On the Firewall, examine the IKEv2 policy.
<img width="959" height="169" alt="Screenshot 2026-05-20 151030" src="https://github.com/user-attachments/assets/8df2de6a-c44c-42d8-bf94-81153c5a9241" />

On the ASAv, an IKEv2 policy is equivalent to the IKEv2 proposal and policy on Cisco IOS. You can view it using the following command:
### On the Branch-router, examine the IKEv2 profile.
<img width="981" height="157" alt="Screenshot 2026-05-20 151243" src="https://github.com/user-attachments/assets/ce66f9c4-e16a-4466-ab46-9fed83253792" />

An IKEv2 profile is a repository of the nonnegotiable parameters of the IKE SA, such as local or remote identities and authentication methods and the services that are available to the authenticated peers that match the profile. An IKEv2 profile must be attached to either a crypto map or IPsec profile on both the IKEv2 initiator and responder.

You can examine the IKEv2 profile using the following command:
<img width="948" height="452" alt="Screenshot 2026-05-20 151349" src="https://github.com/user-attachments/assets/1140367b-0b28-4395-b1dc-c90a4fbc750a" />

### On the Firewall, examine the tunnel group.
<img width="968" height="85" alt="Screenshot 2026-05-20 151736" src="https://github.com/user-attachments/assets/6f4052cc-0a1f-470e-b301-9355e19cf92d" />

The configuration commands differ between Cisco IOS routers and ASA, but both platforms support similar IPsec and IKEv2 settings.
### On the Branch-router, examine the IPsec transform-set.
<img width="970" height="87" alt="Screenshot 2026-05-20 151949" src="https://github.com/user-attachments/assets/f5da4f48-2ef4-4c36-a839-d45af46215ee" />

The IPsec transform set defines the protection parameters for Phase 2, to be applied to interesting traffic to be protected. You can view all transform-sets using the following command:
<img width="951" height="156" alt="Screenshot 2026-05-20 152032" src="https://github.com/user-attachments/assets/444433f5-d060-4dd7-ba89-ed3e06c45814" />

A transform-set default is preconfigured for IPsec transport mode.
### On the Firewall, examine the IPsec transform-set.
<img width="966" height="50" alt="Screenshot 2026-05-20 152247" src="https://github.com/user-attachments/assets/da1ff15f-627d-46a0-8a73-7cd1eab81e4a" />

### On the Branch-router, examine the crypto map and the interesting traffic ACL.
<img width="964" height="377" alt="Screenshot 2026-05-20 152531" src="https://github.com/user-attachments/assets/66eeeaaf-0b47-45ed-a924-f69106a571c0" />
<img width="967" height="48" alt="Screenshot 2026-05-20 152552" src="https://github.com/user-attachments/assets/8341159b-212b-422c-b124-e6e947db1172" />

The crypto map gathers the IKEv2 and IPsec parameters and attaches the crypto functionality to an interface.
### Verify the crypto map and the interesting traffic ACL on the Firewall.
<img width="959" height="85" alt="Screenshot 2026-05-20 152857" src="https://github.com/user-attachments/assets/842c412b-dc2c-4d8b-8554-1463fc9062ac" />
<img width="962" height="31" alt="Screenshot 2026-05-20 152806" src="https://github.com/user-attachments/assets/c49c8fd6-47ab-46f3-992c-0e391b6c4127" />

## Troubleshoot IPsec Operation
In this task, you will change the IKEv2 proposal on the Branch-router, to make it different from the Firewall, and debug the IKEv2 exchange.
### On the Branch-router, change the Diffie-Hellman group in the IKEv2 proposal to group 5.
<img width="975" height="84" alt="Screenshot 2026-05-20 153333" src="https://github.com/user-attachments/assets/3696852d-2ecf-4fb8-8b96-d64321bb93f0" />
