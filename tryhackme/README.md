# **TryHackMe Walkthroughs — Credential Harvesting, Active Directory Exploitation & Persistence**

## **Overview**
This repository contains my detailed, educational walkthroughs of various **TryHackMe** rooms focused on:

- **Credential Harvesting**
- **Exploiting Active Directory (AD)**
- **Persisting Access in AD Environments**

Each write‑up explains **how I approached, analyzed, and solved** the rooms — focusing on methodology, reasoning, and defensive understanding.  
All content is strictly for **ethical cybersecurity learning**, aligned with responsible security practices.

---

## **Why These Rooms Matter**
Modern enterprise environments rely heavily on **Active Directory**, making it a prime target for attackers. Understanding AD security is essential for:

- Security engineers  
- GRC and risk professionals  
- Blue team defenders  
- Pentesters  
- Anyone learning offensive security to improve defensive posture  

These rooms teach critical concepts such as:

- Credential harvesting techniques  
- Lateral movement  
- Privilege escalation  
- AD misconfigurations  
- Persistence mechanisms  
- Defensive detection strategies  

---

# **Repository Structure**

## **1. Credential Harvesting**
Walkthroughs covering techniques used to obtain credentials in Windows and AD environments.

- Password spraying  
- Kerberoasting  
- AS‑REP roasting  
- NTLM relay concepts  
- Capturing hashes  
- Credential reuse analysis  

**Files:**

- `credential_harvest.md`  

---

## **2. Exploiting Active Directory**
Step‑by‑step explanations of how AD misconfigurations can be abused.

Topics include:

- Enumeration (LDAP, SMB, RPC, BloodHound)  
- Misconfigured ACLs  
- Privilege escalation paths  
- Exploiting service accounts  
- Token impersonation  
- Domain privilege escalation  

**Files:**

- `exploitingad.md`
  
---

## **3. Persisting in Active Directory**
Persistence techniques used by attackers — and how defenders can detect them.

Covered topics:

- Golden & Silver Tickets (Kerberos)  
- Skeleton key attacks  
- DCSync & DCShadow  
- Malicious GPOs  
- Backdooring service accounts  
- SID history abuse  

**Files:**

- `persistingad.md`  

---

# **Methodology**
Each walkthrough follows a consistent structure:

### **1. Enumeration**
Tools & techniques used to map the environment:

- `ldapsearch`  
- `rpcclient`  
- `crackmapexec`  
- `BloodHound`  
- `Kerbrute`  
- `Impacket` tools  

### **2. Exploitation**
Clear explanation of:

- What vulnerability existed  
- Why it was exploitable  
- How exploitation works conceptually  
- What commands were used (educational context only)

### **3. Persistence**
Analysis of:

- How attackers maintain access  
- What artifacts remain  
- How defenders can detect & mitigate  

### **4. Defensive Perspective**
Every write‑up includes:

- Detection opportunities  
- Logging considerations  
- Hardening recommendations  
- Relevant MITRE ATT&CK mappings  

---

# **Ethical & Educational Purpose**
All content in this repository is:

- For **learning**, **training**, and **defensive security improvement**  
- Based on **TryHackMe rooms**, which are legal training environments  
- Intended to help others understand how attacks work so they can **defend real systems**  

No real‑world systems, organizations, or unauthorized environments are involved.

---

# **About Me**
I work in **Governance, Risk & Compliance (GRC)** with strong technical experience in:

- Windows internals  
- AD security  
- Vulnerability scanning (Nessus, OpenVAS)  
- DPAPI forensics  
- Reverse engineering  
- AI governance & security  
- Risk assessment & remediation workflows  

TryHackMe rooms help me sharpen my offensive skills to better support **defensive and governance work**.

---

# **Future Additions**
Planned expansions include:

- BloodHound path analysis examples  
- DPAPI credential extraction walkthroughs  
- Kerberos attack deep‑dives  
- Detection rules (Sigma)  
- Hardening checklists  
- Mapping each room to MITRE ATT&CK  

---

# **Contact**
If you’d like to collaborate, discuss AD security, or share room recommendations, feel free to reach out through GitHub.

---
