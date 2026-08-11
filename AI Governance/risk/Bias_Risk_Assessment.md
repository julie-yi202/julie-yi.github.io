# **Bias Risk Assessment Template (IMAGINARYai)**  
*For IMAGINARYai / LLM‑based systems*

---

## **📌 1. System Overview**

### **1.1 System Name**
- Application:  
- Model(s):  
- Owner:  

### **1.2 Description**
Brief description of the AI system and how it uses model outputs in decision‑making or user‑facing contexts.

### **1.3 Intended Use Cases**
- Approved use cases  
- Expected benefits  

### **1.4 High‑Risk Use Cases**
- Any use involving protected attributes  
- Automated decision‑making  
- Safety‑critical or high‑impact outputs  

---

## **📌 2. Bias Risk Summary**

### **2.1 Overall Bias Risk Rating**
| Rating | Justification |
|--------|---------------|
| Low / Medium / High | Summary of expected bias exposure |

### **2.2 Protected Attributes Considered**
- Race  
- Gender  
- Age  
- Disability  
- Religion  
- Nationality  
- Sexual orientation  
- Socioeconomic status  
- Other context‑specific attributes  

---

## **📌 3. Bias Sources & Exposure Analysis**

### **3.1 Potential Sources of Bias**
- Training data distribution  
- Fine‑tuning datasets  
- RAG / retrieval sources  
- Prompt design  
- System instructions  
- User inputs  
- Model architecture limitations  

### **3.2 Exposure Scenarios**
Describe where bias could manifest:
- Content generation  
- Recommendations  
- Summaries  
- Classifications  
- Scoring / ranking  
- Conversational responses  

### **3.3 Impact Assessment**
| Impact Area | Risk | Notes |
|-------------|------|-------|
| User harm | Low/Med/High | Misleading or offensive content |
| Fairness | Low/Med/High | Unequal treatment across groups |
| Compliance | Low/Med/High | Regulatory exposure |
| Reputation | Low/Med/High | Public trust impact |

---

## **📌 4. Bias Testing & Evaluation**

### **4.1 Testing Methods**
- Synthetic prompt testing  
- Counterfactual evaluation  
- Protected attribute perturbation  
- Benchmark datasets  
- Red‑team bias probes  
- Human review panels  

### **4.2 Test Coverage**
| Category | Coverage | Notes |
|----------|----------|-------|
| Toxicity | % | Tools used |
| Stereotypes | % | Groups tested |
| Disparate treatment | % | Methods |
| Disparate impact | % | Metrics |
| Hallucination‑related bias | % | Scenarios |

### **4.3 Test Results Summary**
Provide a short narrative or attach detailed results.

---

## **📌 5. Bias Mitigation Controls**

### **5.1 Pre‑Processing Controls**
- Input validation  
- Prompt sanitization  
- Removal of sensitive attributes unless required  

### **5.2 In‑Model Controls**
- System instructions  
- Safety tuning  
- Guardrails / moderation endpoints  
- Bias‑aware fine‑tuning  

### **5.3 Post‑Processing Controls**
- Output filtering  
- Re‑ranking  
- Human review for high‑impact outputs  
- Confidence scoring  

### **5.4 Organizational Controls**
- Human‑in‑the‑loop  
- Staff training  
- Escalation paths  
- Documentation transparency  

---

## **📌 6. Residual Bias Risk**

### **6.1 Remaining Risks**
List any bias risks that cannot be fully mitigated:
- Model limitations  
- Ambiguous prompts  
- Edge cases  
- Cultural context gaps  

### **6.2 Acceptability Decision**
| Residual Risk | Acceptable? | Justification |
|---------------|-------------|---------------|
| Example | Yes/No | Rationale |

---

## **📌 7. Monitoring & Continuous Review**

### **7.1 Monitoring Plan**
- Drift detection  
- Bias‑related alerts  
- User feedback channels  
- Periodic re‑testing  

### **7.2 Review Frequency**
- Quarterly  
- Semi‑annual  
- After major model updates  
- After fine‑tuning changes  

### **7.3 Feedback Loop**
- Developer feedback  
- User reports  
- Auditor findings  
- Incident reviews  

---

## **📌 8. Final Approval**

### **8.1 Summary**
Short narrative summarizing bias risk, mitigations, and readiness for deployment.

### **8.2 Sign‑Off**
- System Owner  
- AI Risk Committee  
- Compliance  
- Security  
- Legal  

---

## **📌 9. Appendices**
- Bias test datasets  
- Prompt lists  
- Red‑team reports  
- Evaluation metrics  
- Model cards  
- Change logs  


Just tell me which one you want next, Julie.
