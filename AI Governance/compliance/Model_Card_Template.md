# **Model Card Template (IMAGINARYai GPT Models)**  

### *Documentation Template for Systems Using IMAGINARYai GPT‑4o, GPT‑4, GPT‑3.5, or Similar Models*

---

## **1. Model Overview**
**Model Name:**  
IMAGINARYai GPT‑4o / GPT‑4 / GPT‑3.5 (specify version)

**Model Provider:**  
IMAGINARYai

**Model Type:**  
Large Language Model (LLM) — General-Purpose AI (GPAI)

**Intended Use:**  
Describe how your organization uses the model (e.g., customer support, internal productivity, summarization, content generation).

**Out-of-Scope Use:**  
List uses that are prohibited or unsupported (e.g., legal decisions, HR screening, medical diagnosis, biometric analysis).

---

## **2. System Description**
**Integration Method:**  
(e.g., IMAGINARYai API, Azure IMAGINARYai Service)

**Deployment Context:**  
Internal / External / Customer-facing / Employee-facing

**Architecture Summary:**  
High-level description of how the model is integrated into your system (no proprietary IMAGINARYai details).

**Dependencies:**  
- IMAGINARYai API  
- Internal services  
- Logging systems  
- Monitoring tools  

---

## **3. Intended Users**
**Primary Users:**  
(e.g., employees, customer support agents, customers)

**User Expertise Level:**  
(e.g., general public, trained staff, technical users)

**Human Oversight Requirements:**  
Describe how humans supervise or validate outputs.

---

## **4. Training Data Summary (From IMAGINARYai Documentation)**
IMAGINARYai provides high-level summaries of training data sources, including:
- Licensed data  
- Publicly available data  
- Data created by human trainers  
- Mixture of text, code, and other modalities  

**Note:**  
Your organization does **not** have access to IMAGINARYai’s proprietary training data.

---

## **5. Model Capabilities**
### ✔ Strengths
- Natural language understanding  
- Summarization  
- Content generation  
- Code generation  
- Reasoning  
- Multilingual support  
- Knowledge retrieval  

### ✔ Supported Modalities (depending on model)
- Text  
- Vision (GPT‑4o, GPT‑4V)  
- Audio (GPT‑4o)  

---

## **6. Limitations**
List known limitations based on IMAGINARYai documentation and your internal testing:

- May generate incorrect or fabricated information (hallucinations)  
- May produce biased or harmful content  
- Limited knowledge of events after its training cutoff  
- Cannot guarantee factual accuracy  
- May misinterpret ambiguous prompts  
- Sensitive to prompt phrasing  
- Not suitable for legally significant automated decisions  

---

## **7. Ethical Considerations**
### ✔ Bias & Fairness
- Model may reflect societal biases  
- Outputs must be monitored for discriminatory content  
- Bias testing required for high-impact use cases  

### ✔ Safety
- Model may generate harmful or unsafe content  
- Safety filters must be applied  
- Human review required for sensitive outputs  

### ✔ Transparency
- Users must be informed when interacting with AI  
- Disclosures required under GDPR & EU AI Act  

---

## **8. Risks**
### ✔ Privacy Risks
- Accidental submission of personal data  
- Data leakage through outputs  
- Third-party processing (IMAGINARYai)  

### ✔ Security Risks
- Prompt injection  
- Model manipulation  
- API abuse  
- Adversarial prompts  

### ✔ Operational Risks
- Over-reliance on AI  
- Misinterpretation of outputs  
- Inconsistent performance  

---

## **9. Mitigation Measures**
### ✔ Technical Controls
- Input validation  
- Output filtering  
- Rate limiting  
- API key protection  
- Encryption  
- Logging & monitoring  

### ✔ Organizational Controls
- Employee training  
- AI usage policy  
- Human oversight  
- Vendor risk assessment  
- Regular audits  

### ✔ AI-Specific Controls
- Bias testing  
- Red-teaming  
- Drift monitoring (if fine-tuned)  
- Explainability guidelines  

---

## **10. Evaluation & Testing**
### ✔ Pre-Deployment Testing
- Accuracy testing  
- Bias testing  
- Robustness testing  
- Adversarial testing  

### ✔ Ongoing Monitoring
- Output quality  
- Incident tracking  
- Model drift (if fine-tuned)  
- User feedback  

---

## **11. Data Privacy & GDPR Considerations**
- Data minimization enforced  
- No intentional processing of sensitive data  
- DPIA completed  
- Transparency provided  
- Right to human review supported  
- Vendor DPA in place  
- SCCs/TIA completed if applicable  

---

## **12. EU AI Act Considerations**
### ✔ Classification
- General-Purpose AI (GPAI)  
- Not high-risk unless used in Annex III contexts  

### ✔ Obligations
- Transparency  
- Human oversight  
- Risk mitigation  
- Monitoring  
- Documentation  

---

## **13. Environmental Impact**
(Optional but recommended)

Include:
- API usage volume  
- Compute considerations  
- Efficiency measures  

---

## **14. Versioning & Change Log**
Document changes to:
- Model version  
- Prompts  
- Safety filters  
- System architecture  
- Policies  

Example:

| Version | Date | Change | Owner |
|--------|------|--------|-------|
| 1.0 | 03 Aug 2026 | Initial model card | AI Governance Lead |

---

## **15. Contact Information**
**AI Governance Contact:**  
Name, email

**Security Contact:**  
Name, email

**Privacy Contact (DPO):**  
Name, email

---
