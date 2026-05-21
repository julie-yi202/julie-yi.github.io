# Persisting Active Directory
Learn about common Active Directory persistence techniques that can be used post-compromise to ensure the blue team will not be able to kick you out during a red team exercise.
## I used my own kali machine.
<img width="943" height="593" alt="Screenshot 2026-05-14 003118" src="https://github.com/user-attachments/assets/888cdf75-8953-421d-9386-41479b797a40" />

### I ssh into the thmwrk1 ( 10.200.73.248)
<img width="906" height="624" alt="Screenshot 2026-05-14 003223" src="https://github.com/user-attachments/assets/63a597bd-3ff1-4f03-a645-bf1b41b2e9d1" />

Username: Administrator

Password: tryhackmewouldnotguess1@

Domain: ZA
### Persistence Through Credential
DC Sync

It is not sufficient to have a single domain controller per domain in large organisations. These domains are often used in multiple regional locations, and having a single DC would significantly delay any authentication services in AD. As such, these organisations make use of multiple DCs. The question then becomes, how is it possible for you to authenticate using the same credentials in two different offices?

The answer to that question is domain replication. Each domain controller runs a process called the Knowledge Consistency Checker (KCC). The KCC generates a replication topology for the AD forest and automatically connects to other domain controllers through Remote Procedure Calls (RPC) to synchronise information. This includes updated information such as the user's new password and new objects such as when a new user is created. This is why you usually have to wait a couple of minutes before you authenticate after you have changed your password since the DC where the password change occurred could perhaps not be the same one as the one where you are authenticating to.

The process of replication is called DC Synchronisation. It is not just the DCs that can initiate replication. Accounts such as those belonging to the Domain Admins groups can also do it for legitimate purposes such as creating a new domain controller.

A popular attack to perform is a DC Sync attack. If we have access to an account that has domain replication permissions, we can stage a DC Sync attack to harvest credentials from a DC.
Not All Credentials Are Created Equal

Before starting our DC Sync attack, let's first discuss what credentials we could potentially hunt for. While we should always look to dump privileged credentials such as those that are members of the Domain Admins group, these are also the credentials that will be rotated (a blue team term meaning to reset the account's password) first. As such, if we only have privileged credentials, it is safe to say as soon as the blue team discovers us, they will rotate those accounts, and we can potentially lose our access.

The goal then is to persist with near-privileged credentials. We don't always need the full keys to the kingdom; we just need enough keys to ensure we can still achieve goal execution and always make the blue team look over their shoulder. As such, we should attempt to persist through credentials such as the following:

Credentials that have local administrator rights on several machines. Usually, organisations have a group or two with local admin rights on almost all computers. These groups are typically divided into one for workstations and one for servers. By harvesting the credentials of members of these groups, we would still have access to most of the computers in the estate.
Service accounts that have delegation permissions. With these accounts, we would be able to force golden and silver tickets to perform Kerberos delegation attacks.
Accounts used for privileged AD services. If we compromise accounts of privileged services such as Exchange, Windows Server Update Services (WSUS), or System Center Configuration Manager (SCCM), we could leverage AD exploitation to once again gain a privileged foothold.
DCSync All

We will be using Mimikatz to harvest credentials. SSH into THMWRK1 using the DA account and load Mimikatz:
<img width="1224" height="342" alt="Screenshot 2026-05-21 182809" src="https://github.com/user-attachments/assets/08db63d1-be89-47e6-a93a-616f8ab9fc0d" />

you will see quite a bit of output, including the current NTLM hash of your account. You can verify that the NTLM hash is correct by using a website such as this(opens in new tab) to transform your password into an NTLM hash.
<img width="1240" height="755" alt="Screenshot 2026-05-21 182918" src="https://github.com/user-attachments/assets/223ab9bb-6c56-4ae6-a0b9-8d3094d0503e" />

This is great and all, but we want to DC sync every single account. To do this, we will have to enable logging on Mimikatz:
<img width="1244" height="88" alt="Screenshot 2026-05-21 183035" src="https://github.com/user-attachments/assets/d3264d57-75c7-48ee-804d-ffe0fe190672" />

<img width="1248" height="65" alt="Screenshot 2026-05-21 183048" src="https://github.com/user-attachments/assets/ad6b558a-7d7f-48bd-ad5e-dba661301a29" />

### Persistence Through Tickets
Before getting into golden and silver tickets, we first just need to do a quick recap on Kerberos authentication. The diagram below shows the normal flow for Kerberos authentication:
The user makes an AS-REQ to the Key Distribution Centre (KDC) on the DC that includes a timestamp encrypted with the user's NTLM hash. Essentially, this is the request for a Ticket Granting Ticket (TGT). The DC checks the information and sends the TGT to the user. This TGT is signed with the KRBTGT account's password hash that is only stored on the DC. The user can now send this TGT to the DC to request a Ticket Granting Service (TGS) for the resource that the user wants to access. If the TGT checks out, the DC responds to the TGS that is encrypted with the NTLM hash of the service that the user is requesting access for. The user then presents this TGS to the service for access, which can verify the TGS since it knows its own hash and can grant the user access.
<img width="1030" height="574" alt="Screenshot 2026-05-21 183927" src="https://github.com/user-attachments/assets/c79333f3-6842-4241-9fd6-37517d58b7ea" />

Golden Tickets

Golden Tickets are forged TGTs. What this means is we bypass steps 1 and 2 of the diagram above, where we prove to the DC who we are. Having a valid TGT of a privileged account, we can now request a TGS for almost any service we want. In order to forge a golden ticket, we need the KRBTGT account's password hash so that we can sign a TGT for any user account we want. Some interesting notes about Golden Tickets:

By injecting at this stage of the Kerberos process, we don't need the password hash of the account we want to impersonate since we bypass that step. The TGT is only used to prove that the KDC on a DC signed it. Since it was signed by the KRBTGT hash, this verification passes and the TGT is declared valid no matter its contents.
Speaking of contents, the KDC will only validate the user account specified in the TGT if it is older than 20 minutes. This means we can put a disabled, deleted, or non-existent account in the TGT, and it will be valid as long as we ensure the timestamp is not older than 20 minutes.
Since the policies and rules for tickets are set in the TGT itself, we could overwrite the values pushed by the KDC, such as, for example, that tickets should only be valid for 10 hours. We could, for instance, ensure that our TGT is valid for 10 years, granting us persistence.
By default, the KRBTGT account's password never changes, meaning once we have it, unless it is manually rotated, we have persistent access by generating TGTs forever.
The blue team would have to rotate the KRBTGT account's password twice, since the current and previous passwords are kept valid for the account. This is to ensure that accidental rotation of the password does not impact services.
Rotating the KRBTGT account's password is an incredibly painful process for the blue team since it will cause a significant amount of services in the environment to stop working. They think they have a valid TGT, sometimes for the next couple of hours, but that TGT is no longer valid. Not all services are smart enough to release the TGT is no longer valid (since the timestamp is still valid) and thus won't auto-request a new TGT.
Golden tickets would even allow you to bypass smart card authentication, since the smart card is verified by the DC before it creates the TGT.
We can generate a golden ticket on any machine, even one that is not domain-joined (such as our own attack machine), making it harder for the blue team to detect.
Apart from the KRBTGT account's password hash, we only need the domain name, domain SID, and user ID for the person we want to impersonate. If we are in a position where we can recover the KRBTGT account's password hash, we would already be in a position where we can recover the other pieces of the required information.

Silver Tickets

Silver Tickets are forged TGS tickets. So now, we skip all communication (Step 1-4 in the diagram above) we would have had with the KDC on the DC and just interface with the service we want access to directly. Some interesting notes about Silver Tickets:

The generated TGS is signed by the machine account of the host we are targeting.
The main difference between Golden and Silver Tickets is the number of privileges we acquire. If we have the KRBTGT account's password hash, we can get access to everything. With a Silver Ticket, since we only have access to the password hash of the machine account of the server we are attacking, we can only impersonate users on that host itself. The Silver Ticket's scope is limited to whatever service is targeted on the specific server.
Since the TGS is forged, there is no associated TGT, meaning the DC was never contacted. This makes the attack incredibly dangerous since the only available logs would be on the targeted server. So while the scope is more limited, it is significantly harder for the blue team to detect.
Since permissions are determined through SIDs, we can again create a non-existing user for our silver ticket, as long as we ensure the ticket has the relevant SIDs that would place the user in the host's local administrators group.
The machine account's password is usually rotated every 30 days, which would not be good for persistence. However, we could leverage the access our TGS provides to gain access to the host's registry and alter the parameter that is responsible for the password rotation of the machine account. Thereby ensuring the machine account remains static and granting us persistence on the machine.
While only having access to a single host might seem like a significant downgrade, machine accounts can be used as normal AD accounts, allowing you not only administrative access to the host but also the means to continue enumerating and exploiting AD as you would with an AD user account.

Forging Tickets for Fun and Profit

Now that we have explained the basics for Golden and Silver Tickets, let's generate some. You will need the NTLM hash of the KRBTGT account, which you should now have due to the DC Sync performed in the previous task. Furthermore, make a note of the NTLM hash associated with the THMSERVER1 machine account since we will need this one for our silver ticket. You can find this information in the DC dump that you performed. The last piece of information we need is the Domain SID. Using our low-privileged SSH terminal on THMWRK1, we can use the AD-RSAT cmdlet to recover this information:
<img width="946" height="705" alt="Screenshot 2026-05-14 003452" src="https://github.com/user-attachments/assets/54a1cc0d-6b7b-4350-ad22-0798e771fdd2" />

Now that we have all the required information, we can relaunch Mimikatz:
<img width="909" height="687" alt="Screenshot 2026-05-14 003606" src="https://github.com/user-attachments/assets/7d0387a6-f469-4dac-aa2d-afe0e342049e" />

Parameters explained:

/admin - The username we want to impersonate. This does not have to be a valid user.
/domain - The FQDN of the domain we want to generate the ticket for.
/id -The user RID. By default, Mimikatz uses RID 500, which is the default Administrator account RID.
/sid -The SID of the domain we want to generate the ticket for.
/krbtgt -The NTLM hash of the KRBTGT account.
/endin - The ticket lifetime. By default, Mimikatz generates a ticket that is valid for 10 years. The default Kerberos policy of AD is 10 hours (600 minutes)
/renewmax -The maximum ticket lifetime with renewal. By default, Mimikatz generates a ticket that is valid for 10 years. The default Kerberos policy of AD is 7 days (10080 minutes)
/ptt - This flag tells Mimikatz to inject the ticket directly into the session, meaning it is ready to be used.

We can verify that the golden ticket is working by running the dir command against the domain controller:
<img width="901" height="699" alt="Screenshot 2026-05-14 003653" src="https://github.com/user-attachments/assets/53dd7bb6-d464-45a8-9344-ac959b0811ab" />

Even if the golden ticket has an incredibly long time, the blue team can still defend against this by simply rotating the KRBTGT password twice. If we really want to dig in our roots, we want to generate silver tickets, which are less likely to be discovered and significantly harder to defend against since the passwords of every machine account must be rotated. We can use the following Mimikatz command to generate a silver ticket:
<img width="914" height="468" alt="Screenshot 2026-05-14 003735" src="https://github.com/user-attachments/assets/04f1d16f-8cfe-46e9-b9b5-92636818b8e1" />

Parameters explained:

/admin - The username we want to impersonate. This does not have to be a valid user.
/domain - The FQDN of the domain we want to generate the ticket for.
/id -The user RID. By default, Mimikatz uses RID 500, which is the default Administrator account RID.
/sid -The SID of the domain we want to generate the ticket for.
/target - The hostname of our target server. Let's do THMSERVER1.za.tryhackme.loc, but it can be any domain-joined host.
/rc4 - The NTLM hash of the machine account of our target. Look through your DC Sync results for the NTLM hash of THMSERVER1$. The $ indicates that it is a machine account.
/service - The service we are requesting in our TGS. CIFS is a safe bet, since it allows file access.
/ptt - This flag tells Mimikatz to inject the ticket directly into the session, meaning it is ready to be used.
We can verify that the silver ticket is working by running the dir command against THMSERVER1:
<img width="916" height="498" alt="Screenshot 2026-05-14 003921" src="https://github.com/user-attachments/assets/58600455-7e43-4a80-b25e-87c2e88dc49c" />


