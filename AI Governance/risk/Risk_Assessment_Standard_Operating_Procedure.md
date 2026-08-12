# **Risk Assessment SOP — IMAGINARYai**  
**Standard Operating Procedure for Enterprise Risk & Compliance (ISO 27001 / SOC 2 / NIST AI RMF)**  
**Version:** 1.0  
**Effective Date:** _To be assigned_  
**Department:** Governance, Risk & Compliance (GRC)  
**Document Owner:** Security & Compliance Lead  

---

## **Executive Summary**

This SOP defines IMAGINARYai’s standardized methodology for conducting enterprise risk assessments across AI systems, infrastructure, applications, and operational processes. It ensures consistent identification, scoring, documentation, and treatment of risks aligned with ISO 27001, SOC 2, NIST AI RMF, and IMAGINARYai’s internal AI governance requirements.

The process supports audit readiness, responsible AI practices, and risk‑based decision-making across engineering, research, product, and operational teams.

---

## **Purpose**

This SOP establishes a repeatable, structured, and compliant risk assessment methodology for IMAGINARYai. It ensures:

- Standardized risk identification  
- Centralized tracking of risks and remediation  
- Consistent scoring using a 4×4 likelihood/impact model  
- Formal documentation of findings  
- Accountability for remediation  
- Alignment with ISO 27001, SOC 2, and AI governance frameworks  

---

## **Scope**

This SOP applies to all personnel involved in IMAGINARYai’s risk assessment lifecycle:

- GRC Team  
- Engineering & Research Leads  
- Product Owners  
- Security Team  
- AI Safety & Alignment Teams  
- Risk Owners  
- All Employees  

### **Risk Domains Covered**

- Information Security Risks  
- AI Model Risks (bias, hallucination, misuse, safety failures)  
- Application Security Risks  
- Operational Risks  
- Compliance Risks  
- Responsible AI Risks  
- Human Factor Risks  

---

## **Risk Assessment Process Overview**

1. Select or tailor a risk assessment questionnaire.  
2. Collect responses via interviews, workshops, or surveys.  
3. Build a risk register using IMAGINARYai’s standardized template.  
4. Identify, categorize, and score risks using the 4×4 model.  
5. Generate a Risk Assessment Report.  
6. Create a remediation tracker with assigned owners and timelines.  
7. Review findings with Product/Engineering Lead.  
8. Obtain final approval from Security & Compliance Lead.  
9. Monitor risks and remediation actions until closure.  

---

## **Roles & Responsibilities**

| Role | Responsibility | Stakeholders Impacted |
|------|---------------|------------------------|
| **GRC Team** | Designs questionnaires, identifies risks, maintains risk register, drafts reports | Organization-wide |
| **Engineering & Research Leads** | Validate technical risks and model/system context | GRC, Security |
| **Security Team** | Approves risk ratings and validates remediation feasibility | Executive & operational teams |
| **AI Safety & Alignment Teams** | Identify model-specific risks | Product & Research |
| **Risk Owners** | Execute remediation actions and update tracker | Relevant departments |
| **All Employees** | Report risks and follow security/AI governance controls | Organization-wide |

---

## **Inputs & Outputs**

### **Inputs**

- Risk assessment questionnaires  
- Architecture diagrams, model cards, system documentation  
- Threat intelligence and vulnerability data  
- AI model evaluation results  
- Compliance requirements (ISO 27001, SOC 2, NIST AI RMF)  
- Incident records and audit findings  
- Dataset lineage documentation  

### **Outputs**

- Risk Register  
- Risk Assessment Report  
- Remediation Tracker  
- Approved risk documentation  
- Version-controlled records in IMAGINARYai’s Compliance Repository  

---

## **Risk Assessment Methodology**

IMAGINARYai uses a standardized **4×4 Probability × Impact scoring model**.

---

## **Step 1: Risk Identification**

Sources:

- Questionnaire responses  
- Architecture and model evaluations  
- Security reviews and audits  
- Threat modeling  
- AI model safety assessments  
- Dataset governance reviews  

Each risk must include:

- Description  
- Affected asset/model/system  
- Threat & vulnerability context  
- Potential business, safety, or compliance impact  

---

## **Step 2: Risk Analysis**

**Risk Score = Likelihood × Impact**

### **Likelihood Scale**

| Rating | Level | Description |
|--------|--------|-------------|
| 1 | Unlikely | <25% chance |
| 2 | Possible | 26–50% chance |
| 3 | Likely | 51–75% chance |
| 4 | Very Likely | >75% chance |

### **Impact Scale**

| Rating | Level | Description |
|--------|--------|-------------|
| 1 | Low | Minor operational impact |
| 2 | Moderate | Operational disruption or sensitive data exposure |
| 3 | High | Major disruption or regulatory impact |
| 4 | Critical | Severe legal, reputational, or system-wide damage |

---

## **Step 3: Risk Evaluation**

| Score Range | Classification | Required Action |
|-------------|----------------|-----------------|
| 12–16 | Critical | Immediate mitigation |
| 8–11 | High | Prompt mitigation |
| 4–7 | Moderate | Planned mitigation |
| 1–3 | Low | Monitor |

### **Acceptance Criteria**

- Critical/High → must be treated  
- Moderate → justification required  
- Low → acceptable  

---

## **Step 4: Risk Treatment**

Treatment strategies:

- **Mitigate** — Implement controls  
- **Transfer** — Third-party or contractual controls  
- **Avoid** — Remove risk source  
- **Accept** — Formal approval required  

Treatment plans must include:

- Assigned owner  
- Mitigation actions  
- Target dates  
- Expected residual risk  

Residual risk must be rescored using the same 4×4 model.

---

## **Step 5: Documentation & Artifacts**

### **Risk Register Fields**

- Risk ID  
- Asset/Model  
- Description  
- Category  
- Root cause  
- Likelihood & Impact  
- Score & Classification  
- Owner  
- Controls  
- Mitigation plan  
- Residual risk  
- Approval status  
- Acceptance justification  

### **Risk Assessment Report**

Includes:

- Scope  
- Methodology  
- Key findings  
- Model/system risks  
- Control gaps  
- Recommendations  

### **Remediation Tracker**

Tracks:

- Risk ID  
- Owner  
- Actions  
- Priority  
- Status  
- Target dates  
- Evidence  
- Residual risk  
- Exceptions  

---

## **Step 6: Review by Product/Engineering Lead**

Ensures:

- Risks are clearly defined  
- Scoring is consistent  
- Documentation is complete  
- AI model/system context is accurate  

---

## **Step 7: Approval**

Security & Compliance Lead confirms:

- Assessment accuracy  
- Appropriate risk ratings  
- Feasible mitigation plans  
- Alignment with ISO 27001, SOC 2, NIST AI RMF  

---

## **Step 8: Storage & Recordkeeping**

Store approved assessments in:

```
IMAGINARYai Compliance Repository
└── Risk Assessments
    └── Current Year
```

Required metadata:

- Version number  
- Assessment date  
- Last reviewed date  
- Risk owners  
- Treatment plans  
- Version history  

---

## **Step 9: Monitoring & Review**

### **Review Frequency**

| Risk Level | Review Frequency |
|------------|------------------|
| Critical | Quarterly |
| High | Quarterly or Bi-Annual |
| Moderate | Annually |
| Low | Annually or as needed |

### **Triggers for Reassessment**

- Model/system updates  
- New vulnerabilities  
- Incidents  
- Dataset changes  
- Post-mitigation score changes  

---

## **Step 10: Final Review & Approval**

Final approval confirms:

- Accuracy  
- Completeness  
- Correct scoring  
- Effective treatment plans  
- Compliance with ISO 27001, SOC 2, NIST AI RMF  

---

## **KPIs & Metrics**

- % of risks with assigned owners  
- % of Critical/High risks mitigated within SLA  
- Number of overdue remediation actions  
- Average closure time  
- Frequency of risk register updates  
- % of risks reassessed after mitigation  
- % of accepted risks formally approved  

---

## **Risks & Controls**

| Risk | Control |
|------|---------|
| Inconsistent risk identification | Standardized questionnaires |
| AI model misuse or unsafe outputs | Model safety evaluations, red-teaming |
| Incomplete risk tracking | Centralized risk register |
| Delayed remediation | Remediation tracker & ownership model |
| Outdated assessments | Annual & trigger-based reviews |
| Dataset governance gaps | Dataset lineage & approval workflows |

---

## **Related Documents**

- IMAGINARYai AI Governance Policy  
- ISO 27001 Controls  
- SOC 2 Trust Service Criteria  
- NIST AI Risk Management Framework  
- Change Management Policy  
- Model Card Documentation Standards  

---

## **Conclusion**

This SOP establishes a structured, repeatable, and compliant risk assessment process tailored to IMAGINARYai’s environment, including AI model risks, dataset governance, and responsible AI considerations. By standardizing scoring, documentation, and ownership, IMAGINARYai strengthens accountability, audit readiness, and proactive risk management across all teams.


| Field | Value |
| --- | --- |
| **Version** | 1.0 |
| **Status** | Draft / Initial Release |
| **Effective Date** | *To be assigned* |
| **Last Updated** | April 2026 |
| **Author** | Security & Compliance Lead |
| **Contributors** | GRC Team, AI Safety & Alignment Team, Security Engineering |
| **Approved By** | *To be assigned (e.g., CISO / Head of Security)* |

