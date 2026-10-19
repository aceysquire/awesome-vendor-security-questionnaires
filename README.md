# Awesome Vendor Security Questionnaires & Pre-Filled Answers 🛡️

> **Auditor-approved, open-source pre-filled responses, templates, and architectural specifications for B2B tech startups navigating enterprise procurement.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Compliance: 2026 Ready](https://img.shields.io/badge/Compliance-2026%20Ready-emerald)](https://runbookindex.com)
[![Maintained by: The Runbook Index](https://img.shields.io/badge/Maintained%20by-The%20Runbook%20Index-0f172a)](https://runbookindex.com)

When early-stage SaaS, AI, and developer-tool startups sell to enterprise buyers (Fortune 500, corporate banks, healthcare systems), sales deals inevitably stall at the **Vendor Security Assessment (VSA)** stage. 

Enterprise procurement teams hand founders 150-row Excel spreadsheets with zero guidance. This repository provides open-source, auditor-vetted answer templates and architectural runbooks to help technical founders pass procurement without burning 40 hours of engineering bandwidth.

---

## 📚 Table of Contents

1. [CAIQ v4 (Cloud Security Alliance) Answers](#-caiq-v4-cloud-security-alliance-sample-answers)
2. [SIG Lite 2026 (Shared Assessments) Guide](#-sig-lite-2026-sample-answers)
3. [SOC 2 Type II Bridge / Gap Letter Template](#-soc-2-type-ii-bridge-letter-template)
4. [Enterprise AI & LLM Security Answers](#-enterprise-ai--llm-vendor-security-answers)
5. [Need Done-For-You 72h Completion?](#-need-done-for-you-72h-completion)

---

## 🔒 CAIQ v4 (Cloud Security Alliance) Sample Answers

*Full architectural guide and interactive answer explorer:* [**The Runbook Index — CAIQ v4 Pre-Filled Answers**](https://runbookindex.com/caiq-v4-prefilled-answers.html)

### Sample Control: Identity & Access Management (IAM-01)
> **Question:** Does your organization enforce multi-factor authentication (MFA) and least privilege for administrative access to production systems?

```markdown
Yes. Multi-factor authentication (FIDO2 WebAuthn / hardware security keys preferred, 
TOTP enforced minimum) is mandatory across all production cloud infrastructure (AWS/GCP), 
code repositories (GitHub), and identity providers. Administrative access follows the 
Principle of Least Privilege via role-based access control (RBAC). Production environments 
are completely segregated from staging and corporate networks, requiring ephemeral, 
just-in-time access via SSH bastions/VPN with full session logging.
```

### Sample Control: Encryption at Rest & In Transit (EKM-03)
> **Question:** How is customer data encrypted in transit and at rest across your platform?

```markdown
All customer data in transit is encrypted using TLS 1.3 (with fallback to TLS 1.2 minimum; 
legacy protocols SSLv3, TLS 1.0, and TLS 1.1 are explicitly disabled at load balancers) 
enforcing HSTS and secure cipher suites. All customer data at rest is encrypted using 
AES-256 via platform-managed KMS keys (AWS KMS / GCP Cloud KMS) with automated annual 
key rotation. Database backups and volume snapshots inherit full AES-256 encryption.
```

---

## 📋 SIG Lite 2026 Sample Answers

*Full architectural guide:* [**The Runbook Index — SIG Lite Vendor Assessment Guide**](https://runbookindex.com/sig-lite-vendor-assessment-guide.html)

### Sample Control: Vulnerability & Patch Management (Section T.1)
> **Question:** Describe your organization's automated vulnerability scanning and patch management remediation SLAs.

```markdown
Automated dependency scanning (Snyk/GitHub Dependabot) and container image scanning (Trivy/AWS ECR) 
run automatically on every pull request within our CI/CD pipeline. Production base images are updated 
continuously. Remediation SLAs adhere strictly to CVSS severity: Critical vulnerabilities (CVSS >= 9.0) 
are patched within 48 hours; High vulnerabilities (CVSS 7.0–8.9) within 14 days; Medium vulnerabilities 
within 30 days. External third-party penetration testing is conducted annually.
```

---

## 📝 SOC 2 Type II Bridge Letter Template

*Full template & AICPA guide:* [**The Runbook Index — SOC 2 Bridge Letter Guide**](https://runbookindex.com/soc-2-bridge-letter-guide.html)

When your previous SOC 2 audit ended 3 months ago or your next report has not yet been issued, enterprise buyers will reject your report without a signed executive Bridge Letter confirming no material changes occurred.

* [Download the complete SOC 2 Bridge Letter Template (Markdown)](templates/soc-2-bridge-letter-template.md)

---

## 🤖 Enterprise AI & LLM Vendor Security Answers

*Full guide for AI/LLM founders:* [**The Runbook Index — AI Vendor Security Review Guide**](https://runbookindex.com/ai-vendor-security-review-guide.html)

### Control: Zero Data Retention (ZDR) & Model Training Opt-Out
> **Question:** Are customer prompts or uploaded documents used to train third-party or proprietary AI models?

```markdown
No. Under our institutional terms and upstream enterprise agreements (OpenAI Enterprise, 
Anthropic Commercial Terms, AWS Bedrock), customer prompts, completions, and vector embeddings 
are strictly contractually prohibited from being used for foundation model training or 
fine-tuning. All inference calls operate under verified Zero Data Retention (ZDR) endpoints, 
where payloads are processed strictly in ephemeral memory and discarded upon response completion.
```

### Control: Multi-Tenant Vector Embedding Isolation
> **Question:** How are vector embeddings and RAG document indexes isolated between customer tenants?

```markdown
Multi-tenant vector databases (Pinecone / pgvector) enforce hard tenant-level partitioning. 
Every vector embedding metadata header contains a cryptographically validated Tenant ID. All vector 
similarity searches enforce non-bypassable metadata filters (`filter: { tenant_id: org_id }`) at the 
database query layer. Cross-tenant retrieval is structurally prevented at the data access level.
```

---

## 🚀 Need Done-For-You 72h Completion?

Staring at a 150-row questionnaire right now with an enterprise contract on the line?

The Runbook Index operates an on-demand compliance SWAT team for tech startups:
* **Free 15-Question Pre-Fill under Mutual NDA**: Send over your buyer's blank spreadsheet. We pre-fill the first 15 technical controls for free within 24 hours so you can verify our auditor-grade precision.
* **Full 72-Hour Security Vault**: If you want the full 120+ rows completed alongside your bespoke Incident Response Runbook and cloud policies, we turn around the entire vault in 72 hours for a flat £1,950 fee.
* **14-Day 100% Money-Back Audit Pass Guarantee**.

👉 [**Upload Your Questionnaire Under Mutual NDA (15 Free Rows)**](https://runbookindex.com/nda.html)  
👉 [**Explore The Runbook Index Storefront**](https://runbookindex.com)

---

## 📄 License

This repository and all included markdown templates are open-sourced under the [MIT License](LICENSE).
