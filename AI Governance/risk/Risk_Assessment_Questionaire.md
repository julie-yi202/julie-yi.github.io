You got it, Julie — creating a **risk assessment questionnaire** is one of those tasks that looks simple on the surface but has a lot of nuance underneath, especially when you’re building it for ISO 27001, SOC 2, and AI‑specific risks.  

Below is a **complete, GitHub‑friendly, production‑ready guide** that shows you *exactly* how to create a risk assessment questionnaire that plugs directly into your SOP and risk register workflow.

I’ll give you:

- The **method** for designing a questionnaire  
- The **structure** every questionnaire should follow  
- A **full template** you can drop into GitHub as `RISK_ASSESSMENT_QUESTIONNAIRE.md`  
- AI‑specific questions (OpenAI‑style)  
- Security, compliance, operational, and human‑factor questions  

Everything is Markdown‑clean and ready for repo use.

---

# **How to Create a Risk Assessment Questionnaire**

## **1. Start with the Scope**
Every questionnaire must begin by defining **what you are assessing**:

- A system  
- An application  
- An AI model  
- A dataset  
- A business process  
- A third‑party vendor  

This scope determines which questions apply.

---

## **2. Align Questions to Risk Domains**
Your SOP defines the domains. Use them as categories:

1. **Information Security**  
2. **Application Security**  
3. **AI Model Risks**  
4. **Operational Risks**  
5. **Compliance Risks**  
6. **Responsible AI Risks**  
7. **Human Factor Risks**

Each domain gets its own section in the questionnaire.

---

## **3. Make Questions Evidence‑Driven**
Every question should:

- Identify a risk  
- Reveal a control gap  
- Produce evidence or documentation  
- Map directly to your risk register fields  

Example:

> “Describe how access to this system is provisioned and deprovisioned. Provide evidence.”

This gives you:

- Process description  
- Control maturity  
- Evidence for audit  
- Potential risk if missing  

---

## **4. Use a Mix of Question Types**
A strong questionnaire includes:

- **Open‑ended questions** (describe, explain, outline)  
- **Yes/No questions** (quick control checks)  
- **Evidence requests** (attach logs, screenshots, configs)  
- **Rating questions** (maturity, frequency, confidence)  

---

## **5. Ensure Questions Map to Risk Register Fields**
Your risk register includes:

- Asset  
- Description  
- Category  
- Root cause  
- Likelihood  
- Impact  
- Controls  
- Mitigation  
- Residual risk  

Your questionnaire should produce answers that fill these fields.

---

# **Risk Assessment Questionnaire Template (GitHub‑Ready)**

Save this as:

```
/docs/risk/RISK_ASSESSMENT_QUESTIONNAIRE.md
```

---

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
