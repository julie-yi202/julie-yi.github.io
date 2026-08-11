# **AI Threat Modeling Template (IMAGINARYai)**  
*For IMAGINARYai / LLM‑based systems*

---

## **📌 1. System Overview**

### **1.1 System Name**
- Application:  
- Model(s):  
- Owner:  

### **1.2 System Description**
Provide a high‑level overview:
- Purpose  
- Architecture summary  
- Components (LLM, RAG, agents, plugins, APIs)  
- Deployment environment  

### **1.3 Data Flow Summary**
- Inputs → Model → Outputs  
- External integrations  
- Storage locations  
- Network boundaries  

*(Insert diagram or link)*

---

## **📌 2. Threat Modeling Framework**

### **2.1 Methodology**
Select one or more:
- STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege)  
- LLM‑specific threat categories  
- MITRE ATLAS (AI‑focused adversary techniques)  
- Custom enterprise AI threat taxonomy  

### **2.2 Assets to Protect**
- Model integrity  
- Prompts  
- Outputs  
- API keys  
- Training/fine‑tuning data  
- Retrieval sources  
- Logs  
- User data  

---

## **📌 3. AI‑Specific Threat Categories**

### **3.1 Prompt Injection**
**Threat:** User or attacker manipulates model behavior through crafted prompts.  
**Examples:**  
- Jailbreaking  
- Instruction override  
- Hidden malicious instructions  
- Indirect prompt injection (via external data sources)

### **3.2 Model Manipulation**
**Threat:** Attempts to alter model behavior or outputs.  
**Examples:**  
- Adversarial prompts  
- Model poisoning (fine‑tuning attacks)  
- RAG source manipulation  

### **3.3 Data Exfiltration**
**Threat:** Extracting sensitive data through model queries.  
**Examples:**  
- Prompting for internal secrets  
- Leakage via embeddings  
- Retrieval system exploitation  

### **3.4 Unauthorized Access**
**Threat:** Accessing model APIs or internal systems without permission.  
**Examples:**  
- API key theft  
- Token replay  
- Privilege escalation  

### **3.5 Harmful Output Generation**
**Threat:** Model produces unsafe or harmful content.  
**Examples:**  
- Toxicity  
- Bias  
- Disallowed content  
- Hallucinations in critical workflows  

### **3.6 Autonomous Agent Risks**
**Threat:** Agents perform unintended or harmful actions.  
**Examples:**  
- Over‑permissioned tools  
- Infinite loops  
- Unsafe external API calls  

### **3.7 Supply Chain Risks**
**Threat:** External dependencies introduce vulnerabilities.  
**Examples:**  
- Third‑party plugins  
- External APIs  
- Untrusted datasets  

---

## **📌 4. Threat Scenarios & Analysis**

### **4.1 Threat Scenario Table**

| Threat Category | Scenario | Impact | Likelihood | Risk Level | Notes |
|-----------------|----------|--------|------------|------------|-------|
| Prompt Injection | User bypasses safety filters | High | Medium | High | Requires guardrails |
| Data Exfiltration | Attacker extracts PII | High | Low | Medium | Input sanitization needed |
| Model Manipulation | Poisoned RAG source | Medium | Medium | Medium | Validate retrieval sources |
| Unauthorized Access | API key leaked | High | Low | High | Vault storage required |
| Harmful Output | Biased recommendations | Medium | Medium | Medium | Bias testing required |
| Agent Misuse | Agent calls unsafe API | High | Low | Medium | Permission scoping |

---

## **📌 5. Attack Surface Analysis**

### **5.1 Entry Points**
- User prompts  
- API endpoints  
- RAG retrieval queries  
- Fine‑tuning pipelines  
- Agent tool interfaces  

### **5.2 Trust Boundaries**
- Client → API  
- API → Model  
- Model → Plugins  
- Model → Retrieval system  
- Model → Logging system  

### **5.3 External Dependencies**
- Third‑party APIs  
- External datasets  
- Cloud services  
- Plugins  

---

## **📌 6. Mitigation Strategies**

### **6.1 Prompt Injection Mitigations**
- Input validation  
- Prompt isolation  
- Guardrails / moderation  
- System instruction hardening  
- RAG source sanitization  

### **6.2 Model Integrity Mitigations**
- Fine‑tuning approval workflow  
- Dataset validation  
- Version control  
- Red‑team testing  

### **6.3 Data Security Mitigations**
- Sensitive data blocking  
- Encryption  
- Access control  
- Logging restrictions  

### **6.4 API Security Mitigations**
- Key vault storage  
- Key rotation  
- Rate limiting  
- Anomaly detection  

### **6.5 Agent Safety Mitigations**
- Tool permission scoping  
- Action confirmation  
- Execution sandboxing  
- Human‑in‑the‑loop  

### **6.6 Output Safety Mitigations**
- Toxicity filters  
- Bias detection  
- Hallucination detection  
- Human review for critical tasks  

---

## **📌 7. Residual Risk Evaluation**

### **7.1 Remaining Risks**
List risks that cannot be fully mitigated:
- Model limitations  
- Ambiguous prompts  
- Cultural context gaps  
- RAG source unpredictability  

### **7.2 Acceptability Decision**
| Residual Risk | Acceptable? | Justification |
|---------------|-------------|---------------|
| Example | Yes/No | Rationale |

---

## **📌 8. Monitoring & Continuous Improvement**

### **8.1 Monitoring Plan**
- Drift detection  
- Prompt injection alerts  
- API anomaly detection  
- Agent behavior monitoring  

### **8.2 Review Triggers**
- Model updates  
- Fine‑tuning changes  
- New integrations  
- Security incidents  

### **8.3 Feedback Loop**
- Developer feedback  
- User reports  
- Security audits  
- Incident reviews  

---

## **📌 9. Final Approval**

### **9.1 Summary**
Short narrative summarizing threat exposure and readiness for deployment.

### **9.2 Sign‑Off**
- System Owner  
- Security  
- AI Risk Committee  
- Compliance  
- Legal  

---

## **📌 10. Appendices**
- Architecture diagrams  
- Threat trees  
- Red‑team reports  
- Attack simulations  
- Model cards  
- Change logs  



Just tell me which one you want next.
