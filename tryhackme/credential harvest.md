# This room discusses the fundamental knowledge for red teamers taking advantage of obtained credentials to perform Lateral Movement and access resources within the AD environment. We will be showing how to obtain, reuse, and impersonate user credentials. 

Credential harvesting consists of techniques for obtaining credentials like login information, account names, and passwords. It is a technique of extracting credential information from a system in various locations such as clear-text files, registry, memory dumping, etc. 

As a red teamer, gaining access to legitimate credentials has benefits:

It can give access to systems (Lateral Movement).
It makes it harder to detect our actions.
It provides the opportunity to create and manage accounts to help achieve the end goals of a red team engagement.

## Credentials Harvesting
Credentials can be found in a variety of different forms, such as:

Accounts details (usernames and passwords)
Hashes that include NTLM hashes, etc.
Authentication Tickets: Tickets Granting Ticket (TGT), Ticket Granting Server (TGS)
Any information that helps login into a system (private keys, etc.)
Generally speaking, there are two types of credential harvesting: external and internal. External credential harvesting most likely involves phishing emails and other techniques to trick a user into entering his username and password. If you want to learn more about phishing emails, we suggest trying the THM Phishing room. Obtaining credentials through the internal network uses different approaches.

In this room, the focus will be on harvesting credentials from an internal perspective where a threat actor has already compromised a system and gained initial acc

## Credential Access
Credentials are stored insecurely in various locations in systems:

Clear-text files

<img width="874" height="932" alt="Screenshot 2026-05-20 213143" src="https://github.com/user-attachments/assets/5550be20-6698-40a4-bc32-b3c04da7a1ae" />
<img width="870" height="509" alt="Screenshot 2026-05-20 213244" src="https://github.com/user-attachments/assets/6fc9826f-255f-4f90-bc27-743d1f8f5c67" />
<img width="905" height="366" alt="Screenshot 2026-05-20 213412" src="https://github.com/user-attachments/assets/74c89d6f-8916-4758-96f9-f927ab820872" />
<img width="714" height="391" alt="Screenshot 2026-05-20 213915" src="https://github.com/user-attachments/assets/e083b51b-cb59-442d-911f-47512df4c370" />

Database files

Memory Dump

Password managers 

                    Built-in password managers (Windows)
                    
                    Third-party: KeePass, 1Password, LastPass

Enterprise Vaults 

                    Clear-text credentials
                  
                    Cached passwords
                  
                    AD Tickets

Active Directory 

                   Users' description: Administrators set a password in the description for new employees and leave it there, which makes the account vulnerable to                          unauthorized access. 

                   Group Policy SYSVOL: Leaked encryption keys let attackers access administrator accounts. Check Task 8 for more information about the vulnerable version                   of SYSVOL.
                   
                   NTDS: Contains AD users' credentials, making it a target for attackers.
                   
                   AD Attacks: Misconfiguration makes AD vulnerable to various attacks, which we will discuss in Task 9.

Network Sniffing

## Local Windows Credentials
In general, Windows operating system provides two types of user accounts: Local and Domain. Local users' details are stored locally within the Windows file system, while domain users' details are stored in the centralized Active Directory. This task discusses credentials for local user accounts and demonstrates how they can be obtained.
### Keystrokes
### Security Account Manager (SAM)
The SAM is a Microsoft Windows database that contains local account information such as usernames and passwords. The SAM database stores these details in an encrypted format to make them harder to be retrieved. Moreover, it can not be read and accessed by any users while the Windows operating system is running. However, there are various ways and attacks to dump the content of the SAM database. 

First, ensure you have deployed the provided VM and then confirm we are not able to copy or read  the c:\Windows\System32\config\sam file:
<img width="715" height="197" alt="Screenshot 2026-05-20 220610" src="https://github.com/user-attachments/assets/5740434d-f3cd-4470-a028-e14411f2dbf8" />

### Metasploit's Hash Dump
The first method is using the built-in Metasploit Framework feature, hashdump, to get a copy of the content of the SAM database. The Metasploit framework uses in-memory code injection to the LSASS.exe process to dump copy hashes.

meterpreter > getuid
Server username: THM\Administrator
meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:98d3b784d80d18385cea5ab3aa2a4261:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:ec44ddf5ae100b898e9edab74811430d:::
CREDS-HARVESTIN$:1008:aad3b435b51404eeaad3b435b51404ee:443e64439a4b7fe780db47fc06a3342d:::

### Volume Shadow Copy Service (VSS)
The other approach uses the Microsoft Volume shadow copy service, which helps perform a volume backup while applications read/write on volumes. 
More specifically, we will be using wmic to create a shadow volume copy. This has to be done through the command prompt with administrator privileges as follows,

1. Run the standard cmd.exe prompt with administrator privileges.
2. Execute the wmic command to create a copy shadow of C: drive
3. Verify the creation from step 2 is available.
4. Copy the SAM database from the volume we created in step 2

Creating a Shadow Copy of Volume C with WMIC
<img width="830" height="205" alt="Screenshot 2026-05-20 221155" src="https://github.com/user-attachments/assets/08073096-dbb5-4bd1-a4b8-7ddfbdafa94e" />

Listing the Available Shadow Volumes
<img width="832" height="285" alt="Screenshot 2026-05-20 221248" src="https://github.com/user-attachments/assets/486d8890-d0dc-49e0-86bf-33d4049d12dd" />

The output shows that we have successfully created a shadow copy volume of (C:) with the following path: \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1. 

As mentioned previously, the SAM database is encrypted either with RC4 (opens in new tab)or AES (opens in new tab)encryption algorithms. In order to decrypt it, we need a decryption key which is also stored in the files system in c:\Windows\System32\Config\system. 

Now let's copy both files (sam and system) from the shadow copy volume we generated to the desktop as follows,
<img width="883" height="208" alt="Screenshot 2026-05-20 221616" src="https://github.com/user-attachments/assets/4f698c80-dc4c-4b5f-8892-955fb7e40cb5" />

Now we have both required files, transfer them to the AttackBox with your favourite method (SCP should work). 
I used smbclient because scp and certutil didn't work due to the unknow Linux box password.
<img width="889" height="75" alt="Screenshot 2026-05-20 222316" src="https://github.com/user-attachments/assets/66bf633e-a174-44d9-a580-2c1b626e5f49" />
<img width="779" height="374" alt="Screenshot 2026-05-20 222335" src="https://github.com/user-attachments/assets/a7e5ab47-85ac-4d7f-a918-54c58e990f36" />

### Registry Hives
Another possible method for dumping the SAM database content is through the Windows Registry. Windows registry also stores a copy of some of the SAM database contents to be used by Windows services. Luckily, we can save the value of the Windows registry using the reg.exe tool. As previously mentioned, we need two files to decrypt the SAM database's content. Ensure you run the command prompt with Administrator privileges.
Save SAM and SYSTEM files from the registry
<img width="889" height="347" alt="Screenshot 2026-05-20 222922" src="https://github.com/user-attachments/assets/31de8e11-9b72-4d14-afd2-d51e165b2ff0" />

Decrypting SAM Database using Impacket SecretsDump Script Locally
<img width="840" height="251" alt="Screenshot 2026-05-20 223420" src="https://github.com/user-attachments/assets/e327ac6b-fbfe-469f-bdf1-97c2a85b2d08" />

Note that we used the SAM and System files that we extracted from Windows Registry. The -sam argument is to specify the path for the dumped sam file from the Windows machine. The -system argument is for a path for the system file. We used the LOCAL argument at the end of the command to decrypt the Local SAM file as this tool handles other types of decryption. 

Note if we compare the output against the NTLM hashes we got from Metasploit's Hashdump, the result is different. The reason is the other accounts belong to Active Directory, and their information is not stored in the System file we have dumped. To Decrypt them, we need to dump the SECURITY file from the Windows file, which contains the required files to decrypt Active Directory accounts.

Once we obtain NTLM hashes, we can try to crack them using Hashcat if they are guessable, or we can use different techniques to impersonate users using the hashes.

## Local Security Authority Subsystem Service (LSASS)
Local Security Authority Server Service (LSASS) is a Windows process that handles the operating system security policy and enforces it on a system. It verifies logged in accounts and ensures passwords, hashes, and Kerberos tickets. Windows system stores credentials in the LSASS process to enable users to access network resources, such as file shares, SharePoint sites, and other network services, without entering credentials every time a user connects.

### Graphic User Interface (GUI)

To dump any running Windows process using the GUI, open the Task Manager, and from the Details tab, find the required process, right-click on it, and select "Create dump file".
<img width="877" height="648" alt="Screenshot 2026-05-20 224612" src="https://github.com/user-attachments/assets/41f56b65-a404-4c70-a14f-c3843ab74d6f" />

Once the dumping process is finished, a pop-up message will show containing the path of the dumped file. Now copy the file and transfer it to the AttackBox to extract NTLM hashes offline.
Copying the LSASS Dumped file
<img width="899" height="129" alt="Screenshot 2026-05-20 224940" src="https://github.com/user-attachments/assets/b8f5d179-1eec-4500-8f52-3ab547474ff4" />

### Sysinternals Suite

An alternative way to dump a process if a GUI is not available to us is by using ProcDump. ProcDump is a Sysinternals process dump utility that runs from the command prompt. 

### MimiKatz

Mimikatz (opens in new tab)is a well-known tool used for extracting passwords, hashes, PINs, and Kerberos tickets from memory using various techniques. Mimikatz is a post-exploitation tool that enables other useful attacks, such as pass-the-hash, pass-the-ticket, or building Golden Kerberos tickets. Mimikatz deals with operating system memory to access information. Thus, it requires administrator and system privileges in order to dump memory and extract credentials.
<img width="889" height="842" alt="Screenshot 2026-05-20 230344" src="https://github.com/user-attachments/assets/b9daf1ff-beb9-4e8d-aad0-5bdb3f97dd9a" />
<img width="871" height="851" alt="Screenshot 2026-05-20 230926" src="https://github.com/user-attachments/assets/b58c1630-5ded-4e61-866e-fc12cbc8cb93" />

This is part of the credentials that harvested from the mimikatz.
