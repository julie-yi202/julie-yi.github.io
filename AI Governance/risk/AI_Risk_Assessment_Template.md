# **AI Risk Assessment Template (IMAGINARYai‑Style)**  
*For IMAGINARYai / LLM‑based systems*

---

## **📌 1. System Overview**

### **1.1 System Name**
- **Application:**  
- **Project Code:**  
- **Business Owner:**  

### **1.2 Description**
Provide a concise description of the AI system, including:
- Purpose  
- Core functionality  
- Architecture summary  
- Deployment environment (prod/staging/on‑prem/cloud)

### **1.3 Intended Users**
- Internal  
- External  
- Automated systems  

### **1.4 Intended Use Cases**
- Approved use cases  
- Expected benefits  

### **1.5 Prohibited / Out‑of‑Scope Use Cases**
- Disallowed tasks  
- High‑risk scenarios requiring special approval  

---

## **📌 2. Risk Classification**

### **2.1 Model Risk Level**
| Risk Level | Justification |
|-----------|---------------|
| Low / Medium / High | Impact, autonomy, data sensitivity, regulatory exposure |

### **2.2 Application Risk Domains**
- Operational  
- Safety  
- Compliance  
- Security  
- Reputational  

### **2.3 Regulatory Mapping**
- GDPR  
- HIPAA  
- NIST AI RMF  
- ISO 42001  
- Industry‑specific regulations  

---

## **📌 3. Data Risk Assessment**

### **3.1 Data Inputs**
- Data types  
- Sensitive data categories  
- Input validation  
- Prompt sanitization  
- Data minimization  

### **3.2 Data Outputs**
- Harmful content risk  
- Bias risk  
- Hallucination risk  
- Output filtering  
- Human review requirements  

### **3.3 Data Storage & Retention**
| Category | Policy |
|----------|--------|
| Prompt Logging | Yes/No + justification |
| Output Logging | Yes/No + justification |
| Encryption | At rest / in transit |
| Retention | Duration + rationale |
| Access Control | Roles + restrictions |

### **3.4 Data Flow Diagram**
*(Insert diagram or link)*

---

## **📌 4. Security Risk Assessment**

### **4.1 API Security**
- Authentication method  
- Key vault storage  
- Key rotation schedule  
- Least‑privilege access  

### **4.2 Threat Vectors**
- Prompt injection  
- Jailbreaking  
- Model manipulation  
- Data exfiltration  
- Agent misuse  

### **4.3 Security Controls**
- Rate limiting  
- Anomaly detection  
- Network segmentation  
- Secure coding standards  
- Monitoring & alerting  

---

## **📌 5. Model Risk Assessment**

### **5.1 Bias & Fairness**
- Bias testing performed  
- Identified risks  
- Mitigation strategies  
- Re‑evaluation schedule  

### **5.2 Hallucination Risk**
- Confidence scoring  
- RAG usage  
- Human‑in‑the‑loop  
- Escalation paths  

### **5.3 Safety & Harm Prevention**
- Disallowed content categories  
- Safety filters  
- Moderation endpoints  
- Red‑team testing results  

### **5.4 Explainability & Transparency**
- Explainability methods  
- User disclosures  
- Documentation  

---

## **📌 6. Operational Risk Assessment**

### **6.1 Monitoring**
- Latency  
- Cost  
- Drift  
- Error rate  
- Alert thresholds  

### **6.2 Change Management**
- Versioning  
- Fine‑tuning history  
- Approval workflow  
- Staging test results  

### **6.3 Incident Response**
- AI‑specific incident categories  
- Response playbooks  
- Escalation contacts  
- Post‑incident review  

---

## **📌 7. Third‑Party & Supply Chain Risk**

### **7.1 Vendor Assessment**
- Security posture  
- Compliance documentation  
- Data handling policies  
- SLA guarantees  

### **7.2 External Plugins / APIs**
- Permissions  
- Data exposure  
- Risk evaluation  

### **7.3 Annual Review**
- Vendor reassessment  
- Contract updates  

---

## **📌 8. Ethical & Responsible AI Assessment**

### **8.1 User Safety**
- Disclaimers  
- Feedback channels  
- Accessibility  

### **8.2 Human Oversight**
- Human‑in‑the‑loop  
- Manual override  
- Staff training  

### **8.3 Societal Impact**
- Potential misuse  
- Community impact  
- Long‑term risks  

---

## **📌 9. Performance & Quality Assessment**

### **9.1 Evaluation Results**
- Accuracy  
- Reliability  
- Relevance  
- Drift detection  

### **9.2 Cost Management**
- Token usage  
- Model selection  
- Caching strategy  

### **9.3 SLA & Reliability**
- Uptime  
- Fallback strategies  
- Redundancy  

---

## **📌 10. Final Risk Summary & Approval**

### **10.1 Overall Risk Rating**
| Rating | Justification |
|--------|---------------|
| Low / Medium / High | Summary of key risks |

### **10.2 Required Mitigations**
- Pre‑launch controls  
- Post‑launch controls  

### **10.3 Approval Signatures**
- System Owner  
- AI Risk Committee  
- Security  
- Compliance  
- Legal  

---

## **📌 11. Appendices**
- Architecture diagrams  
- Model cards  
- DPIA  
- Threat models  
- Red‑team reports  
- Safety evaluation results  

---

If you want, I can also generate:

- A **GitHub Issue Template** version (`.github/ISSUE_TEMPLATE/ai_risk_assessment.yml`)  
- A **GitHub Wiki page** version  
- A **README‑style condensed version**  
- A **table‑only version** for easy diffing in PRs  

Just tell me which one you want next, Julie.
