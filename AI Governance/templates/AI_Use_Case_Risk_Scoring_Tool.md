| Impact Area | Score (1–5) | Notes |
| --- | --- | --- |
| Safety Impact |  |  |
| Bias Impact |  |  |
| Privacy Impact |  |  |
| Security Impact |  |  |
| Regulatory Impact |  |  |
| Reputational Impact |  |  |


| Likelihood Factor | Score (1–5) | Notes |
| --- | --- | --- |
| User misuse likelihood |  |  |
| Jailbreak likelihood |  |  |
| Sensitive data exposure likelihood |  |  |
| Model failure likelihood |  |  |


| Total Score | Risk Level |
| --- | --- |
| 0–25 | Low |
| 26–50 | Medium |
| 51–100 | High |




| Use Case Category | Specific Use Case | Description | Risk Level (Initial) | Data Sensitivity | Owner | Status |
| --- | --- | --- | --- | --- | --- | --- |
| Conversational AI | Customer Support Chatbot | Answers customer questions | Medium | Medium |  |  |
| Conversational AI | Internal Helpdesk Assistant | IT/HR support | Low | Low |  |  |
| Conversational AI | Executive Assistant | Summaries, scheduling | Medium | Medium |  |  |
| RAG Systems | Enterprise Knowledge Search | Retrieves internal documents | Medium | High |  |  |
| RAG Systems | Policy Retrieval Assistant | Compliance/policy lookup | Medium | High |  |  |
| RAG Systems | Technical Documentation Search | Engineering knowledge | Low | Medium |  |  |
| Autonomous Agents | Workflow Automation Agent | Executes tasks via tools | High | High |  |  |
| Autonomous Agents | Financial Operations Agent | Performs financial actions | Very High | High |  |  |
| Autonomous Agents | Security Operations Agent | SOC automation | High | High |  |  |
| Classification | Document Classification | Categorizes documents | Medium | Medium |  |  |
| Classification | Email Triage | Sorts incoming emails | Low | Low |  |  |
| Classification | Risk Classification | Flags risky content | High | High |  |  |
| Summarization | Legal Document Summaries | Summaries of contracts | High | High |  |  |
| Summarization | Meeting Summaries | Internal meeting notes | Low | Medium |  |  |
| Summarization | Medical Summaries | Clinical notes | Very High | High |  |  |
| Generation | Marketing Content Generation | Ads, blogs | Low | Low |  |  |
| Generation | Code Generation | Developer assistance | Medium | Medium |  |  |
| Generation | Report Generation | Business reports | Medium | Medium |  |  |
| Decision Support | Fraud Detection | Flags suspicious activity | High | High |  |  |
| Decision Support | HR Screening | Candidate evaluation | Very High | High |  |  |
| Decision Support | Medical Decision Support | Clinical recommendations | Very High | High |  |  |
| Analytics | Data Insights | Trend analysis | Medium | Medium |  |  |
| Analytics | Forecasting | Predictive analytics | High | High |  |  |
| Analytics | KPI Monitoring | Business dashboards | Low | Medium |  |  |
| Safety | Content Moderation | Detects harmful content | High | Medium |  |  |
| Safety | Bias Detection | Flags biased outputs | High | Medium |  |  |
| Safety | Hallucination Detection | Flags unsupported claims | High | Medium |  |  |



| Process Category | Specific Process | Description | Risk Level | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| Data Pipeline | Data Ingestion | Collecting raw data | Medium |  |  |
| Data Pipeline | Data Cleaning | Deduplication, normalization | Medium |  |  |
| Data Pipeline | Data Labeling | Human or synthetic labeling | High |  |  |
| Data Pipeline | Data Transformation | Chunking, tokenization | Medium |  |  |
| Data Pipeline | Data Storage | Storing datasets | High |  |  |
| Model Pipeline | Prompt Processing | Input validation, sanitization | High |  |  |
| Model Pipeline | Model Invocation | Calling GPT‑4/GPT‑4o | Medium |  |  |
| Model Pipeline | Output Filtering | Safety, bias, hallucination filters | High |  |  |
| Model Pipeline | Logging | Prompt/output logging | High |  |  |
| Model Pipeline | Monitoring | Safety, security, performance | High |  |  |
| RAG Pipeline | Document Ingestion | Adding docs to RAG index | High |  |  |
| RAG Pipeline | Embedding Generation | Creating vector embeddings | Medium |  |  |
| RAG Pipeline | Indexing | Building FAISS/Elastic index | Medium |  |  |
| RAG Pipeline | Retrieval | Querying index | Medium |  |  |
| RAG Pipeline | Grounding | Combining retrieval + model | High |  |  |
| Agent Pipeline | Tool Invocation | Agent calling tools/APIs | Very High |  |  |
| Agent Pipeline | Action Validation | Confirming agent actions | High |  |  |
| Agent Pipeline | Execution Sandbox | Safe execution environment | High |  |  |
| Agent Pipeline | Loop Detection | Prevent runaway agents | High |  |  |
| Security | API Security | Key vault, rotation | High |  |  |
| Security | Prompt Injection Defense | Detecting malicious prompts | Very High |  |  |
| Security | Anomaly Detection | Monitoring unusual activity | High |  |  |
| Security | Access Control | RBAC, least privilege | High |  |  |
| Governance | Change Management | Model updates, approvals | Medium |  |  |
| Governance | Risk Assessment | Use case scoring | High |  |  |
| Governance | Incident Response | AI‑specific incidents | High |  |  |
| Governance | Audit & Compliance | Regulatory alignment | High |  |  |



[AI Use Case & Process Inventory.xlsx](https://github.com/user-attachments/files/30948210/AI.Use.Case.Process.Inventory.xlsx)
