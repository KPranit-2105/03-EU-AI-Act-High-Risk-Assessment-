# Operational EU AI Act High-Risk Compliance Assessment (TalentMatch AI)

[![Regulation](https://img.shields.io/badge/Regulation-(EU)_2024%2F1689-blue.svg)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689)
[![Classification](https://img.shields.io/badge/Classification-High--Risk_Annex_III_4(a)-red.svg)](classification/classification-analysis.md)
[![Status](https://img.shields.io/badge/GRC_Decision-GO_WITH_CONDITIONS-orange.svg)](decision/go-no-go.md)
[![Bias Mitigation](https://img.shields.io/badge/Fairness-DIR_%E2%89%A5_0.823_PASSED-green.svg)](testing/fairness-testing.md)

---

> ### 🚨 PORTFOLIO DISCLAIMER
> This repository contains a **simulated EU AI Act High-Risk Compliance Assessment** created for **TalentMatch AI B.V.** It demonstrates practical AI governance engineering, statutory classification, Fairlearn bias testing, human oversight UI design, and regulator challenge readiness under **Regulation (EU) 2024/1689**. **It does not represent a real commercial entity, live regulatory filing, or official certification by an EU Market Surveillance Authority.**

---

## 📌 Executive Summary & Case Study Overview

**TalentMatch AI B.V.** (Amsterdam, Netherlands) develops **TalentMatch AI v2.4**—a B2B SaaS candidate screening and ranking engine used by 150+ enterprise HR departments across the European Union to process over 2.5 million job applicant resumes annually.

This project operationalizes the requirements of **Regulation (EU) 2024/1689 (EU AI Act)**, translating high-level legal articles into technical MLOps pipelines, empirical bias mitigations, structural UI friction controls, and an audit-ready compliance package.

```
┌──────────────────────────────────────────────────────────────────────────────────────┐
│                    TALENTMATCH AI COMPLIANCE SCORECARD                               │
├──────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│   SYSTEM NAME          TalentMatch AI Candidate Screening & Ranking Engine v2.4      │
│   PROVIDER             TalentMatch AI B.V. (Amsterdam, Netherlands)                  │
│   DEPLOYER BASE        150+ Enterprise HR Departments across EU Member States        │
│   CLASSIFICATION       HIGH-RISK AI SYSTEM (Article 6(2) & Annex III, Section 4(a))  │
│   ART. 6(3) EXCEPTION  REJECTED (Statutory bar: Candidate profiling performed)       │
│   ART. 5 PROhibitions  CLEARED (No emotion recognition or biometric categorization)  │
│   DECISION             GO WITH CONDITIONS (6 Mandatory Deployment Gates Required)    │
│                                                                                      │
└──────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🔑 Key Analytical & Technical Highlights

- **Statutory Bar Rejection of Article 6(3) Exemption ([`classification/classification-analysis.md`](file:///c:/Users/ASUS/Documents/03-eu-ai-act-high-risk-assessment/classification/classification-analysis.md)):** 
  The system is classified as High-Risk under Annex III 4(a) (Recruitment). Any attempt to claim an Article 6(3) derogation is **legally barred** because the system performs automated candidate profiling (Article 3(4)), triggering the mandatory statutory bar in the final sub-paragraph of Article 6(3).
- **Empirical Bias Audit & Mitigation ([`testing/fairness-testing.md`](file:///c:/Users/ASUS/Documents/03-eu-ai-act-high-risk-assessment/testing/fairness-testing.md)):**
  Pre-mitigation testing revealed severe indirect discrimination against female applicants (DIR = 0.742), older candidates 45+ (DIR = 0.679), and non-Western EU names (DIR = 0.649). Following Fairlearn demographic parity calibration and proxy feature masking, all subgroup DIR metrics improved to $\ge 0.823$ (passing the 0.80 legal threshold), accepting a slight, legally mandatory accuracy trade-off ($0.78 \rightarrow 0.765$).
- **Anti-Automation Bias Human Oversight ([`human-oversight/human-oversight.md`](file:///c:/Users/ASUS/Documents/03-eu-ai-act-high-risk-assessment/human-oversight/human-oversight.md)):**
  Operationalizes Article 14 by replacing performative 45-second recruiter reviews with structural UI friction: enforcing a mandatory 2-minute review lock, blurring AI scores until recruiters complete a blind initial skill evaluation, and requiring written rationale for score overrides $>25$ points.
- **CV Prompt Injection Cybersecurity Defense ([`cybersecurity/cybersecurity.md`](file:///c:/Users/ASUS/Documents/03-eu-ai-act-high-risk-assessment/cybersecurity/cybersecurity.md)):**
  Neutralizes white-font hidden text instructions in candidate PDF resumes using a multi-stage PyMuPDF text sanitizer pre-parser before NLP tokenization.

---

## 🏗️ Interactive System Architecture & Governance Flow

### 1. AI Pipeline & Governance Boundary
```mermaid
flowchart TB
    subgraph INPUT["Candidate Application Input Layer"]
        PDF["Unstructured Resume (PDF / Word)"]
        JOB["Job Requisition Attributes"]
    end

    subgraph PIPELINE["TalentMatch AI v2.4 Processing Core"]
        SAN["1. PyMuPDF Text Sanitizer (Art 15 Prompt Injection Defense)"]
        BERT["2. Fine-tuned BERT Entity Extractor (Art 10 Data Quality)"]
        MASK["3. Proxy Feature Masking Engine (Strips Grad Year, Name, Photo)"]
        XGB["4. XGBoost Vector Matcher & Ranking Engine (Art 11 Model)"]
    end

    subgraph OVERSIGHT["Recruiter Human Oversight Console (Art 14)"]
        UI_LOCK["Mandatory 2-Minute Review Time Lock"]
        BLIND["Blind Initial Skill Evaluation Interface"]
        OVERRIDE["Score Override Justification Logger (>25 pts)"]
    end

    subgraph AUDIT["Immutable Compliance Storage (Art 12 / 72)"]
        WORM["AWS S3 WORM Audit Log (12-Month Retention)"]
        DATADOG["Datadog Post-Market Embedding Drift Alerting"]
    end

    PDF & JOB --> SAN
    SAN --> BERT
    BERT --> MASK
    MASK --> XGB
    XGB --> UI_LOCK
    UI_LOCK --> BLIND
    BLIND --> OVERRIDE
    OVERRIDE --> WORM & DATADOG

    classDef input fill:#1e293b,stroke:#3b82f6,color:#fff;
    classDef pipe fill:#1e293b,stroke:#f59e0b,color:#fff;
    classDef over fill:#1e293b,stroke:#10b981,color:#fff;
    classDef audit fill:#1e293b,stroke:#8b5cf6,color:#fff;
    class INPUT input;
    class PIPELINE pipe;
    class OVERSIGHT over;
    class AUDIT audit;
```

---

### 2. Legal Classification & Article 6(3) Decision Tree
```mermaid
flowchart TD
    A["Evaluate System Intended Purpose"] --> B{"Falls under Annex III, 4(a)?<br>(Recruitment & Selection)"}
    B -- NO --> C["Not High-Risk under Annex III"]
    B -- YES --> D{"Evaluated against Art 5 Prohibitions?"}
    D -- FAILED --> E["PROHIBITED AI PRACTICE (Art 5 Violation)"]
    D -- CLEARED --> F{"Claim Article 6(3) Derogation?"}
    F -- NO --> G["HIGH-RISK AI SYSTEM (Art 6(2))"]
    F -- YES --> H{"Does System Perform Profiling?<br>(Article 3(4) Evaluation)"}
    H -- YES --> I["STATUTORY BAR TRIGGERED!<br>(Final sub-paragraph of Art 6(3))"]
    I --> G
    H -- NO --> J["Low-Risk Exception Granted"]

    classDef pass fill:#10b981,stroke:#047857,color:#fff;
    classDef fail fill:#ef4444,stroke:#991b1b,color:#fff;
    classDef decision fill:#3b82f6,stroke:#1d4ed8,color:#fff;
    class G,I fail;
    class C,J pass;
    class B,D,F,H decision;
```

---

### 3. End-to-End Compliance Traceability Flow
```mermaid
flowchart LR
    subgraph OBLIGATION["EU AI Act Statutory Obligations"]
        ART10["Art 10: Data & Bias"]
        ART14["Art 14: Oversight"]
        ART15["Art 15: Security"]
    end

    subgraph CONTROL["Internal GRC Controls"]
        CTL2["CTL-AI-03: Fairlearn Tuning"]
        CTL7["CTL-AI-07: 2-Min UI Lock"]
        CTL9["CTL-AI-09: Text Sanitizer"]
    end

    subgraph EVIDENCE["Technical Audit Evidence"]
        EVD2["testing/fairness-testing.md"]
        EVD7["human-oversight/human-oversight.md"]
        EVD9["cybersecurity/cybersecurity.md"]
    end

    ART10 --> CTL2 --> EVD2
    ART14 --> CTL7 --> EVD7
    ART15 --> CTL9 --> EVD9

    classDef ob fill:#3b82f6,stroke:#1d4ed8,color:#fff;
    classDef ct fill:#f59e0b,stroke:#b45309,color:#fff;
    classDef ev fill:#10b981,stroke:#047857,color:#fff;
    class OBLIGATION ob;
    class CONTROL ct;
    class EVIDENCE ev;
```

---

## 🏛️ EU AI Act Implementation Timeline

Anchored strictly in **Regulation (EU) 2024/1689**:

- **August 2024:** Entry into Force.
- **February 2025 (6 Months):** Prohibited AI Practices (Chapter I & II, Art. 5) applicable.
- **August 2025 (12 Months):** General Purpose AI / GPAI Rules (Chapter V) applicable.
- **August 2026 (24 Months):** High-Risk AI Systems under Annex III (Art. 6(2)) applicable.
- **August 2027 (36 Months):** High-Risk AI Systems under Annex I (Art. 6(1)) applicable.

---

## 📋 The 6 Mandatory Deployment Sign-Off Gates

Commercial release to EU enterprise clients is **FROZEN** until all 6 gates receive formal sign-off:

1. **Gate 1 (Bias Calibration):** Disparate Impact Ratio (DIR) $\ge 0.823$ across female, age 45+, and non-Western candidate subgroups.
2. **Gate 2 (Human Oversight UI):** 2-minute UI interaction time lock & blind initial scoring interface deployed in console.
3. **Gate 3 (Cybersecurity Hardening):** PyMuPDF text sanitizer pre-parser deployed to neutralize CV prompt injection payloads.
4. **Gate 4 (Technical Documentation):** Consolidated Annex IV technical documentation binder in QMS repository.
5. **Gate 5 (Deployer Binding Agreements):** EU AI Act Governance Addendums & FRIA Toolkits executed with all 150+ clients.
6. **Gate 6 (Candidate Appeal Mechanism):** Candidate Score Explanation & Re-evaluation Portal launched providing a 14-day human review window.

---

## 📁 Repository Structure & Document Index

This case study is organized into 15 audit-ready AI governance working papers:

```
03-eu-ai-act-high-risk-assessment/
├── README.md                           # Master Overview & Recruiter Dashboard
├── scenario/
│   └── company-profile.md              # Provider (TalentMatch AI B.V.) & Deployer Ecosystem
├── ai-system/
│   ├── system-description.md           # Architecture, NLP Pipeline, ML Models, & Inputs/Outputs
│   ├── intended-purpose.md            # Article 3(12) Intended Purpose & Prohibited Uses
│   └── roles.md                        # Article 16 Provider vs Article 26 Deployer Duties
├── classification/
│   └── classification-analysis.md      # Art 5 Prohibitions, Art 6(2) Annex III 4(a), & Art 6(3) Statutory Bar
├── risk/
│   ├── ai-risk-register.md             # AIR-001..AIR-010 Risk Register & 5x5 Matrix
│   └── risk-treatment-plan.md          # Article 9(4) Treatment Strategies & Board Sign-offs
├── data-governance/
│   └── data-governance.md              # Article 10 Data Quality, Splits, & Proxy Masking
├── human-oversight/
│   └── human-oversight.md              # Article 14 Oversight, 2-Min UI Lock, & Anti-Automation UI
├── model-governance/
│   └── model-governance.md             # Article 11 Technical Documentation, Annex IV, & Model Card
├── testing/
│   ├── performance-testing.md          # Article 15 Accuracy, Robustness, & Trade-Off Analysis
│   └── fairness-testing.md             # Disparate Impact Ratio (DIR) Audit & Fairlearn Tuning
├── cybersecurity/
│   └── cybersecurity.md               # Article 15 Cybersecurity & PyMuPDF Prompt Injection Sanitizer
├── compliance/
│   └── control-matrix.md               # EU AI Act Control Matrix & End-to-End Traceability
├── monitoring/
│   └── post-market-monitoring.md       # Article 72 Post-Market Monitoring & Drift Circuit Breaker
├── incident-management/
│   └── incident-reporting.md           # Article 73 Serious Incident Reporting & 15-Day Playbook
├── decision/
│   └── go-no-go.md                     # Executive GO WITH CONDITIONS Decision & 6 Sign-off Gates
├── audit/
│   └── regulator-questions.md          # 15 EU AI Act Regulator Challenge Scenarios (Strong vs Weak)
└── templates/
    └── ai-assessment-template.md       # Reusable EU AI Act High-Risk Assessment Template
```

---

## 💡 GRC Practitioner Reflection & Takeaways

1. **Defensibility Over Checklist Compliance:** GRC engineering requires grounding decisions in empirical data (Fairlearn DIR metrics) and explicit statutory interpretation (Article 6(3) statutory profiling bar).
2. **Eliminating Performative Oversight:** "Human-in-the-loop" is a legal illusion if recruiters spend 45 seconds per resume. True Article 14 compliance requires cognitive forcing functions (UI locks, blind evaluation).
3. **Accepting Hard Constraints:** Achieving regulatory compliance required accepting a 1.5% drop in model accuracy to protect fundamental rights against age and ethnic discrimination.

---

## 📄 License & Attribution

This case study is published under the **MIT License**. Created as part of the Advanced AI Governance & Regulatory Specialist Portfolio Series.
