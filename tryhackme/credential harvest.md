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

Database files

Memory

Password managers

Enterprise Vaults

Active Directory

Network Sniffing
