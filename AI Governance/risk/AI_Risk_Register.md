# AI Risk Register for IMAGINARYai

[AI_Risk_Register.xlsx](https://github.com/user-attachments/files/30764855/AI_Risk_Register.xlsx)


# AI Risk Register (IMAGINARYai Systems)

| Risk ID | Risk Name | Description | Model(s) Affected | Likelihood | Impact | Risk Rating | Controls (IDs) | Owner | Status |
|--------|-----------|-------------|-------------------|------------|--------|-------------|----------------|-------|--------|
| **AI-RISK-01** | Hallucination | Model generates incorrect or fabricated information | GPT-4, GPT-4o | Medium | High | High | AI-CTRL-31, AI-CTRL-40 | AI Lead | Open |
| **AI-RISK-02** | Prompt Injection | Malicious prompts manipulate model behavior | All LLMs | High | High | High | AI-CTRL-21, AI-CTRL-20 | Security Team | Open |
| **AI-RISK-03** | Data Leakage | Sensitive data exposed through prompts or outputs | GPT-4, GPT-4o | Low | High | Medium | AI-CTRL-10, AI-CTRL-12 | Privacy Officer | Open |
| **AI-RISK-04** | Bias in Outputs | Model produces biased or discriminatory content | GPT-4, GPT-4o | Medium | High | High | AI-CTRL-30, AI-CTRL-32 | Ethics Lead | Open |
| **AI-RISK-05** | Harmful Content | Model generates unsafe or harmful responses | All LLMs | Medium | High | High | AI-CTRL-32, AI-CTRL-11 | Safety Team | Open |
| **AI-RISK-06** | Model Drift | Model behavior changes over time or after updates | GPT-4, Fine-tuned models | Medium | Medium | Medium | AI-CTRL-70, AI-CTRL-41 | AI Ops | Open |
| **AI-RISK-07** | Cost Overrun | Excessive token usage increases operational cost | All LLMs | Medium | Medium | Medium | AI-CTRL-71, AI-CTRL-40 | Finance | Open |
| **AI-RISK-08** | Misuse / Abuse | Users intentionally misuse AI for harmful purposes | All LLMs | Medium | High | High | AI-CTRL-32, AI-CTRL-60 | Governance | Open |
| **AI-RISK-09** | Regulatory Non-Compliance | AI system violates legal or regulatory requirements | All LLMs | Low | High | Medium | AI-CTRL-50, AI-CTRL-51 | Compliance | Open |
| **AI-RISK-10** | Over-Reliance on AI | Users trust AI outputs without human review | All LLMs | Medium | Medium | Medium | AI-CTRL-61, AI-CTRL-62 | Product Owner | Open |
| **AI-RISK-11** | Security Breach | Unauthorized access to API keys or AI systems | All LLMs | Low | High | Medium | AI-CTRL-20, AI-CTRL-22 | Security Team | Open |
| **AI-RISK-12** | Inaccurate RAG Retrieval | Incorrect retrieval leads to wrong answers | GPT-4 + RAG | Medium | Medium | Medium | AI-CTRL-31, AI-CTRL-70 | AI Lead | Open |
| **AI-RISK-13** | Plugin / Integration Risk | Third-party plugins introduce vulnerabilities | GPT-4 Plugins | Medium | High | High | AI-CTRL-51, AI-CTRL-22 | Security Team | Open |
| **AI-RISK-14** | IP / Copyright Issues | Model generates copyrighted or proprietary content | All LLMs | Medium | Medium | Medium | AI-CTRL-32, AI-CTRL-60 | Legal | Open |
| **AI-RISK-15** | Inconsistent Behavior | Model behaves differently across contexts or prompts | All LLMs | Medium | Medium | Medium | AI-CTRL-70, AI-CTRL-90 | AI Ops | Open |
