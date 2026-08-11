# **Dataset Documentation Template (IMAGINARYai)**  
*For IMAGINARYai / LLM‑based systems*

---

## **📌 1. Dataset Overview**

### **1.1 Dataset Name**
- Name:  
- Version:  
- Owner / Maintainer:  

### **1.2 Description**
Provide a concise summary:
- What the dataset contains  
- What tasks it supports (training, fine‑tuning, evaluation, RAG)  
- Why it exists / what problem it solves  

### **1.3 Dataset Type**
- Training dataset  
- Fine‑tuning dataset  
- Evaluation dataset  
- RAG corpus  
- Synthetic dataset  
- Human‑labeled dataset  

### **1.4 Intended Use**
- Approved use cases  
- Expected benefits  
- Supported model types  

### **1.5 Out‑of‑Scope Use**
- Disallowed tasks  
- High‑risk applications requiring special approval  

---

## **📌 2. Dataset Composition**

### **2.1 Data Sources**
List all sources:
- Internal data  
- Public datasets  
- Third‑party datasets  
- Synthetic data  
- Human‑generated content  
- Web‑scraped content (if applicable)  

### **2.2 Data Modalities**
- Text  
- Code  
- Images  
- Audio  
- Structured data  
- Documents (PDF, HTML, etc.)  

### **2.3 Data Volume**
| Metric | Value |
|--------|-------|
| Total samples | |
| Total tokens | |
| File count | |
| Storage size | |

### **2.4 Sampling Strategy**
- Random sampling  
- Stratified sampling  
- Domain‑specific sampling  
- Synthetic augmentation  

---

## **📌 3. Data Quality & Validation**

### **3.1 Quality Checks**
- Deduplication  
- Noise removal  
- Format validation  
- Language detection  
- Document parsing checks  

### **3.2 Human Review**
- % of data reviewed  
- Review guidelines  
- Reviewer expertise  

### **3.3 Known Issues**
- Missing metadata  
- Ambiguous labels  
- Noisy text  
- OCR errors  
- Domain imbalance  

---

## **📌 4. Bias & Fairness Considerations**

### **4.1 Protected Attributes**
Dataset may contain references to:
- Race  
- Gender  
- Age  
- Disability  
- Religion  
- Nationality  
- Sexual orientation  
- Socioeconomic status  

### **4.2 Bias Risks**
- Stereotypes  
- Skewed representation  
- Cultural bias  
- Geographic bias  
- Temporal bias  

### **4.3 Mitigation Steps**
- Filtering sensitive content  
- Balancing representation  
- Removing harmful stereotypes  
- Synthetic counterfactuals  
- Human review for sensitive categories  

---

## **📌 5. Privacy & Security**

### **5.1 Sensitive Data Handling**
| Category | Present? | Notes |
|----------|----------|-------|
| PII | Yes/No | |
| PHI | Yes/No | |
| Financial data | Yes/No | |
| Proprietary data | Yes/No | |

### **5.2 Privacy Controls**
- Sensitive data removal  
- Redaction  
- Hashing  
- Differential privacy (if applicable)  

### **5.3 Security Controls**
- Encryption at rest  
- Encryption in transit  
- Access restrictions  
- Audit logging  

---

## **📌 6. Licensing & Legal**

### **6.1 License Type**
- Open source  
- Proprietary  
- Third‑party license  
- Mixed license  

### **6.2 Usage Restrictions**
- Commercial use allowed?  
- Redistribution allowed?  
- Derivative works allowed?  

### **6.3 Compliance Requirements**
- GDPR  
- HIPAA  
- CCPA  
- Copyright considerations  

---

## **📌 7. Dataset Processing Pipeline**

### **7.1 Ingestion**
- Source acquisition  
- Format conversion  
- Initial validation  

### **7.2 Cleaning**
- Deduplication  
- Normalization  
- Tokenization  
- Metadata extraction  

### **7.3 Transformation**
- Labeling  
- Chunking  
- Embedding generation  
- Synthetic augmentation  

### **7.4 Storage**
- Location  
- Format (JSONL, Parquet, CSV, etc.)  
- Versioning  

*(Insert pipeline diagram or link)*

---

## **📌 8. Evaluation & Benchmarking**

### **8.1 Evaluation Tasks**
- Classification  
- Summarization  
- RAG retrieval accuracy  
- Toxicity/bias evaluation  
- Hallucination testing  

### **8.2 Metrics**
| Metric | Description |
|--------|-------------|
| Accuracy | |
| F1 Score | |
| BLEU / ROUGE | |
| Toxicity Score | |
| Bias Indicators | |
| Hallucination Rate | |

### **8.3 Benchmark Results**
Provide summary or attach detailed results.

---

## **📌 9. Dataset Versioning**

### **9.1 Version History**
| Version | Date | Changes |
|---------|------|---------|
| 1.0 | | Initial release |
| 1.1 | | Added new domain data |
| 2.0 | | Major restructuring |

### **9.2 Change Management**
- Approval workflow  
- Testing requirements  
- Documentation updates  

---

## **📌 10. Risks & Mitigations**

### **10.1 Identified Risks**
- Bias  
- Sensitive data exposure  
- Copyright issues  
- Poisoning risk  
- Domain imbalance  

### **10.2 Mitigation Summary**
- Filtering  
- Human review  
- Synthetic balancing  
- Legal review  
- Security controls  

---

## **📌 11. Final Approval**

### **11.1 Reviewers**
- Dataset Owner  
- AI Safety Team  
- Security Team  
- Legal / Compliance  
- AI Risk Committee  

### **11.2 Approval Status**
- Approved  
- Approved with conditions  
- Not approved  

---

## **📌 12. Appendices**
- Schema definitions  
- Labeling guidelines  
- Sampling scripts  
- Data dictionaries  
- Change logs  

---

Julie, if you want, I can also generate:

- **DATASET_DOCUMENTATION_TEMPLATE.yml** (GitHub Issue Template)  
- **A GitHub Wiki version**  
- **A version aligned to NIST AI RMF or ISO 42001**  
- **A version integrated with your AI‑CTRL catalog**  
- **A version tailored for RAG datasets or fine‑tuning datasets**  

Just tell me what you want next.
