# **Risk Assessment Questionnaire**

## **1. System / Model Information**

| Field | Response |
|-------|----------|
| System / Model Name |  |
| Owner / Team |  |
| Description |  |
| Business Purpose |  |
| Data Sensitivity Level |  |
| External Exposure (Yes/No) |  |
| Third‑Party Dependencies |  |

---

## **2. Information Security**

### **Access Control**
- Describe how access is provisioned and deprovisioned.  
- Who approves access?  
- Are privileged roles separated?  
- Is MFA enforced?  
- Provide evidence (screenshots, logs, policy).

### **Data Protection**
- What data does the system store or process?  
- Is data encrypted at rest?  
- Is data encrypted in transit?  
- Are encryption keys centrally managed?  
- Provide evidence.

### **Logging & Monitoring**
- What logs are collected?  
- Who reviews logs?  
- Are alerts configured?  
- Provide evidence.

---

## **3. Application Security**

### **Secure Development**
- Are secure coding practices followed?  
- Are dependencies scanned for vulnerabilities?  
- Are code reviews required?  
- Provide evidence.

### **Vulnerability Management**
- When was the last security scan?  
- Are critical vulnerabilities remediated within SLA?  
- Provide reports.

### **API Security**
- Are APIs authenticated?  
- Are rate limits enforced?  
- Are error messages sanitized?  
- Provide API documentation.

---

## **4. AI Model Risks (OpenAI‑specific)**

### **Model Behavior**
- What model is used (GPT‑4, GPT‑5, custom)?  
- What tasks does the model perform?  
- What safety evaluations have been conducted?  
- Provide model card or evaluation report.

### **Hallucination Risk**
- Does the model generate factual outputs?  
- What safeguards exist to prevent hallucinations?  
- How is output validated?

### **Bias & Fairness**
- Has the model been tested for bias?  
- What demographic or contextual risks exist?  
- Provide evaluation results.

### **Misuse Potential**
- Could the model be used maliciously?  
- What safeguards prevent harmful outputs?  
- Provide red‑team results.

### **Prompt Injection / Jailbreak Risks**
- Are prompts sanitized?  
- Are user inputs filtered?  
- Provide examples of mitigations.

---

## **5. Operational Risks**

### **Process Maturity**
- Are processes documented?  
- Are roles clearly defined?  
- Are changes reviewed before deployment?

### **Change Management**
- How are changes approved?  
- Is rollback capability available?  
- Provide change logs.

### **Business Continuity**
- Are backups configured?  
- Is disaster recovery tested?  
- Provide evidence.

---

## **6. Compliance Risks**

### **Regulatory Alignment**
- Does the system handle regulated data (GDPR, HIPAA, AI Act)?  
- Are data subject rights supported?  
- Provide compliance documentation.

### **Policy Alignment**
- Does the system follow internal policies?  
- Are exceptions documented?  
- Provide policy references.

---

## **7. Responsible AI Risks**

### **Transparency**
- Is the model’s behavior documented?  
- Are limitations disclosed?

### **Explainability**
- Can the model’s outputs be explained?  
- Provide documentation.

### **Human Oversight**
- Is human review required?  
- Provide workflow diagrams.

---

## **8. Human Factor Risks**

### **Training**
- Are users trained on system risks?  
- Provide training materials.

### **Insider Threat**
- Are access logs reviewed?  
- Are privileged users monitored?

---

## **9. Additional Notes / Observations**

Free‑form section for anything not covered above.

---

## **10. Evidence Attachments**

List all attached evidence:

- Logs  
- Screenshots  
- Config files  
- Policies  
- Architecture diagrams  
- Model cards  
- Evaluation reports  

---
