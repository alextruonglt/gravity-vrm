# Vendor Risk Management Framework
### Gravity Payments, Inc. | June 2026

> A production-grade Third-Party Risk Management (TPRM) framework built for a real-world payment processor context. Covers 15 vendors across 8 service categories with full PCI DSS v4.0, GLBA, SOC 2, and CCPA/CPRA regulatory alignment.

---

<img width="1687" height="760" alt="Screenshot 2026-06-23 at 11 42 15 AM" src="https://github.com/user-attachments/assets/52d561cc-9583-41c3-850d-da729518bcb0" />

---

## What This Is

This project demonstrates applied GRC methodology for a payment processor operating under PCI DSS v4.0. It is not a template or theoretical exercise - every vendor score, tier assignment, and remediation item reflects a genuine risk that a company in Gravity Payments' position would face.

The framework was built to produce audit-ready evidence artifacts that map directly to PCI DSS Requirements 12.8, 12.8.2, 12.8.4, and 11.4.

---

## Deliverables

| File | Description |
|---|---|
| [`gravity_vrm_framework.xlsx`](./gravity_vrm_framework.xlsx) | Six-tab Excel workbook - full risk register, scoring model, heat map, DDQ, and remediation tracker. Also available as a [Google Sheet](https://docs.google.com/spreadsheets/d/11nrl8iISAfhHMlNBZoTznCkTS-X39bYB/edit?usp=sharing&ouid=110260400406162142135&rtpof=true&sd=true). |
| [`gravity_vrm_exec_summary.md`](./gravity_vrm_exec_summary.md) | Executive summary suitable for compliance leadership or audit committee review. Also available as a [PDF via Google Drive](https://drive.google.com/file/d/1GNgCUfZa27zueHOqO6w79p5wsAligYCC/view?usp=sharing). |

---

## Workbook Structure

The Excel workbook contains six tabs:

**1. Cover Sheet** - Document metadata, tier definitions, and regulatory context

**2. Scoring Methodology** - Full explanation of the five-factor composite scoring model with scale definitions for each factor

**3. Vendor Risk Register** - 15 vendors scored with live formulas, conditional formatting by risk tier, assessment status, owner assignments, and key findings

**4. Risk Heat Map** - Portfolio visualization by Data Sensitivity vs. Operational Dependency with summary statistics

**5. Due Diligence Questionnaire (DDQ)** - 35 questions across 7 sections (Company Info, Information Security, Data Handling, PCI DSS, Business Continuity, Incident Response, Contractual/Legal)

**6. Remediation Tracker** - 8 open items with priority, owner, target date, status, and percent complete

---

## Scoring Methodology

The framework uses a five-factor composite model that separates inherent risk from control effectiveness, then multiplies the two scores together. Multiplication - not averaging - is intentional: a high-risk vendor with weak controls receives a non-linear risk escalation that averaging would understate.

**Inherent Risk Score** = Average of three factors scored 1–4

| Factor | 1 (Low) | 4 (Critical) |
|---|---|---|
| Data Sensitivity | No data access | Cardholder data / encryption keys |
| Operational Dependency | Easily replaced | Single point of failure |
| Regulatory Exposure | No regulatory nexus | Directly in PCI CDE scope |

**Control Score** = Average of two factors scored 1–4 (reversed - 1 is strongest)

| Factor | 1 (Strong) | 4 (None) |
|---|---|---|
| Security Posture | SOC 2 Type II + PCI certified | No evidence provided |
| Contract Protections | Full DPA, SLA, audit rights, IR <24h | Click-wrap ToS only |

**Composite Score** = Inherent Risk Score × Control Score (range: 1–16)

| Tier | Threshold |
|---|---|
| Critical | ≥ 10 |
| High | 7 – 9.9 |
| Medium | 4 – 6.9 |
| Low | < 4 |

---

## Portfolio Snapshot

<img width="1107" height="756" alt="Screenshot 2026-06-23 at 11 42 50 AM" src="https://github.com/user-attachments/assets/7da5192b-7243-4321-b2fd-48094e489d27" />


| Metric | Count |
|---|---|
| Total Vendors Assessed | 15 |
| Critical Risk Vendors | 0 |
| High Risk Vendors | 2 |
| Medium Risk Vendors | 7 |
| Low Risk Vendors | 6 |
| Open Remediation Items | 8 |
| P1 Items (Immediate Action) | 2 |

### Tier Breakdown

**HIGH (2 vendors)**
- **Fiserv (8.0)** - Acquiring bank connectivity. IR notification window contractually set at 72h; PCI DSS and card brand rules require 24h. Active contract amendment in progress.
- **Unnamed Pentest Firm (9.0)** - Lapsed SOC 2, privileged CDE access, weak contract protections. RFP in progress for replacement QSA-qualified firm.

**MEDIUM (7 vendors)** - Visa, Mastercard, AWS, Stripe Issuing, Salesforce, Plaid, Experian. High inherent risk offset by strong vendor security posture. Annual assessment cycle with active monitoring.

**LOW (6 vendors)** - Twilio, DocuSign, Zendesk, Okta, Slack, Checkr. Okta illustrates the methodology's intent: maximum operational dependency (OD=4) but best-in-class security posture and contract protections produce a composite of 3.33. The model rewards strong controls.

---

## Open Remediation Items

<img width="1726" height="647" alt="Screenshot 2026-06-23 at 11 43 12 AM" src="https://github.com/user-attachments/assets/55f5abb8-1837-4a8d-a2ef-f5db03783257" />


| ID | Vendor | Priority | Finding | Target |
|---|---|---|---|---|
| REM-001 | Unnamed Pentest Firm | **P1** | SOC 2 lapsed; PCI Req 11.4 violation risk | Sep 2026 |
| REM-002 | Fiserv | **P1** | IR notification window 72h vs. required 24h | Sep 2026 |
| REM-003 | Zendesk | P2 | Partial PANs in support ticket text; CDE scope creep risk | Jul 2026 |
| REM-004 | Slack | P2 | Card numbers shared in internal channels; DLP not deployed | Jul 2026 |
| REM-005 | Salesforce | P2 | Merchant SSNs/EINs in plain-text custom fields | Aug 2026 |
| REM-006 | Okta | P2 | Admin accounts not enrolled in phishing-resistant MFA (WebAuthn) | Aug 2026 |
| REM-007 | Twilio | P3 | SIM-swap risk for high-value merchants not mitigated | Sep 2026 |
| REM-008 | Plaid | P3 | CFPB Section 1033 impact on existing DPA not assessed | Oct 2026 |

---

## Regulatory Alignment

| Framework | Applicability |
|---|---|
| **PCI DSS v4.0** | Requirements 12.8 (third-party risk program), 12.8.2 (written agreements), 12.8.4 (annual monitoring), 11.4 (penetration testing) |
| **GLBA Safeguards Rule** | 16 CFR Part 314 §314.4(f) - service provider oversight via written contracts and monitoring |
| **SOC 2 (AICPA)** | Vendor SOC 2 Type II reports are the primary assurance artifact in the Security Posture scoring factor |
| **CCPA/CPRA** | California merchant personal data (contact info, EINs, SSNs) triggers processor obligations; DDQ Section C enforces DPA requirements at onboarding |
| **CFPB Section 1033** | Emerging open banking rule tracked proactively via REM-008 to prevent non-compliance at effective date |

---

## GRC Skills Demonstrated

- Third-Party Risk Management (TPRM) - vendor tiering, DDQ design, risk register maintenance
- PCI DSS v4.0 application - requirement mapping, CDE scoping, evidence collection methodology
- Risk scoring - inherent vs. residual risk separation, quantitative composite formula design
- Regulatory cross-mapping - PCI DSS, GLBA, SOC 2, state privacy law
- Incident response integration - IR notification SLA requirements, contractual enforcement
- Control assessment - SOC 2 report evaluation, security posture scoring, control gap identification

---

## Notes

All vendor data, scores, and findings are hypothetical assumptions created for portfolio demonstration purposes. Framework Version 1.0.

*Gravity Payments · Information Security and Compliance Team*
