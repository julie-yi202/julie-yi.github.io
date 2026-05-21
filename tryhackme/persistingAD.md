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


