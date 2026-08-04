# **EU AI Act–Aligned DPIA** 

### *Data Protection Impact Assessment for IMAGINARYai GPT Models Under the EU AI Act & GDPR*

---

## **1. Project Overview**
**Project Name:**  
IMAGINARYai GPT Integration for Productivity & Customer Support

**Department / Owner:**  
Digital Transformation / AI Governance

**Date:**  
03 August 2026

**Version:**  
1.0

**Reviewer(s):**  
DPO, AI Governance Lead, Security Lead

**Summary of the AI System:**  
The organization intends to use IMAGINARYai GPT models (GPT‑4o, GPT‑4, GPT‑3.5) to support employees and customers by generating responses, summarizing content, and providing decision support. The system is not intended to make autonomous decisions with legal or significant effects.

**Business Justification:**  
Improve productivity, reduce response times, and enhance customer experience.

---

# **2. EU AI Act Risk Classification**

### **2.1 AI System Type**
This system qualifies as a **general-purpose AI (GPAI)** under the EU AI Act because:
- It uses a model developed by a third-party provider (IMAGINARYai).  
- It is integrated into internal and customer-facing workflows.  
- It is not fine-tuned for high-risk applications.

### **2.2 Risk Category Determination**
Under the EU AI Act, this system is classified as:

### **➡️ *Non–high-risk GPAI system***  
because:
- It does not perform biometric identification.  
- It does not evaluate individuals for access to essential services.  
- It does not make employment, credit, or legal decisions.  
- It does not fall under Annex III high-risk categories.

### **2.3 High-Risk Check (Annex III)**
The system was evaluated against all high-risk categories:
- Employment/HR screening → **Not applicable**  
- Creditworthiness → **Not applicable**  
- Access to essential services → **Not applicable**  
- Law enforcement → **Not applicable**  
- Border control → **Not applicable**  
- Medical diagnosis → **Not applicable**

**Conclusion:**  
The system is **not high-risk** under the EU AI Act.

---

# **3. EU AI Act Obligations for GPAI Systems**

### **3.1 Provider Obligations (IMAGINARYai)**
IMAGINARYai must provide:
- Model documentation  
- Training data summaries  
- Known limitations  
- System instructions  
- Safety features  
- Cybersecurity measures  
- Model card or equivalent documentation  

### **3.2 Deploying Organization Obligations**
Your organization must:
- Ensure transparency to users  
- Prevent prohibited uses  
- Implement risk mitigation  
- Maintain human oversight  
- Document integration and usage  
- Conduct bias and robustness testing  
- Monitor for misuse  
- Maintain logs  
- Provide user disclosures when AI is used  

---

# **4. Description of Processing**

### **4.1 Nature of Processing**
The system processes:
- User prompts  
- Customer inquiries  
- Internal documents  
- Generated outputs  

Processing includes:
- Text analysis  
- Content generation  
- Summarization  
- Decision support  

### **4.2 Scope**
- **Volume:** High  
- **Subjects:** Employees, customers  
- **Duration:** Real-time  
- **Frequency:** Continuous  
- **Geographic Scope:** Global  

### **4.3 Context**
- Third-party AI provider  
- Potential for bias or hallucinations  
- Users may rely on AI-generated content  

### **4.4 Purposes**
- Customer support  
- Productivity enhancement  
- Internal documentation automation  

---

# **5. Data Categories & Sources**

### **5.1 Personal Data**
- Names  
- Contact details  
- Account information  
- Free-text inputs  
- Inferred data  

### **5.2 Sources**
- Direct user input  
- Internal systems  
- Public knowledge encoded in the model  

### **5.3 Data Quality**
- User-provided data assumed accurate  
- AI outputs may contain inaccuracies  

---

# **6. GDPR Legal Basis**

### **6.1 Lawful Basis**
- **Employees:** Legitimate interests  
- **Customers:** Contractual necessity  

### **6.2 Special Category Data**
Not intentionally processed.

### **6.3 Automated Decision-Making (Article 22)**
No legally significant automated decisions.

---

# **7. EU AI Act Risk Assessment**

### **7.1 AI-Specific Risks**
- Hallucinations  
- Bias  
- Lack of explainability  
- Over-reliance  
- Adversarial prompts  
- Model drift (if fine-tuned)  
- Misuse of GPAI capabilities  

### **7.2 Prohibited Uses Check**
The system does **not** engage in:
- Social scoring  
- Emotion recognition in workplaces  
- Biometric categorization  
- Manipulation of vulnerable groups  
- Predictive policing  

### **7.3 Risk Severity Scoring**

| Risk | Likelihood | Impact | Risk Level | Notes |
|------|------------|--------|------------|-------|
| Hallucinations | Medium | Medium | Medium | Human review required |
| Bias | Medium | High | High | Bias testing required |
| Misuse | Medium | High | High | Access controls required |
| Prompt injection | Medium | High | High | Security controls required |
| Over-reliance | Medium | Medium | Medium | Training required |

---

# **8. Mitigation Measures (EU AI Act + GDPR)**

### **8.1 Technical Controls**
- API key protection  
- Encryption  
- Input validation  
- Output filtering  
- Rate limiting  
- Logging  
- Monitoring for misuse  

### **8.2 Organizational Controls**
- AI usage policy  
- Employee training  
- Governance committee oversight  
- Vendor risk assessment  
- Human-in-the-loop review  

### **8.3 AI-Specific Controls**
- Bias testing  
- Model card documentation  
- Dataset card (if fine-tuned)  
- Red-teaming  
- Explainability guidelines  
- Drift monitoring  

### **8.4 Residual Risk**
Medium due to:
- Bias  
- Hallucinations  
- Third-party infrastructure reliance  

---

# **9. Data Subject Rights**

### **9.1 Rights Supported**
- Access  
- Rectification  
- Erasure  
- Restriction  
- Objection  
- Portability  
- Human review  

### **9.2 Mechanisms**
Handled through existing privacy channels.

---

# **10. Retention & Deletion**

### **10.1 Retention**
- Prompts: Not stored unless logging enabled  
- Logs: 30–90 days  
- Fine-tuning data: Per policy  

### **10.2 Deletion**
- Automated log deletion  
- Manual deletion upon request  
- Anonymization  

---

# **11. Vendor & Third-Party Considerations**

### **11.1 Providers**
- IMAGINARYai  
- Cloud hosting providers  

### **11.2 Safeguards**
- DPA  
- SCCs  
- Vendor risk assessment  
- Security certifications  

---

# **12. Transparency & Communication**

### **12.1 User Notices**
Users informed that:
- AI assists in generating responses  
- Human review is available  
- Data is processed per privacy policy  

### **12.2 Public Documentation**
- Updated privacy notice  
- AI usage disclosure  
- Model card  

---

# **13. Consultation**

### **13.1 DPO Consultation**
Completed.

### **13.2 External Consultation**
Not required.

---

# **14. Final Assessment & Approval**

### **14.1 Summary**
The system is **non-high-risk GPAI** under the EU AI Act.  
Risks are manageable with proper controls.

### **14.2 Decision**
**Proceed with conditions**, including:
- Bias testing  
- Human oversight  
- Employee training  
- Monitoring  

### **14.3 Approvals**

| Role | Name | Signature | Date |
|------|------|-----------|------|
| DPO | — | — | 03 Aug 2026 |
| Legal | — | — | 03 Aug 2026 |
| Security | — | — | 03 Aug 2026 |
| AI Governance Lead | — | — | 03 Aug 2026 |

---

# **Appendices**
- A: EU AI Act Risk Classification Worksheet  
- B: Model Card (IMAGINARYai GPT Integration)  
- C: Dataset Card (if fine-tuned)  
- D: Bias Testing Results  
- E: Monitoring Plan  

---



Just tell me what you want next.
