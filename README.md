# NIST-HIPAA-GOOGLEDOCS-COMPLIANCE
# Mapping Google Docs YARA Files to a NIST / HIPAA Compliant Framework
## Google Workspace & Google SecOps: HIPAA Compliance Automation Kit

This repository contains production-ready detection rules, templates, and configurations designed to harden Google Workspace environments and integrate logs natively into Google Security Operations (formerly Chronicle SIEM) for healthcare providers under HIPAA compliance frameworks.



## 📌 Overview

Managing Electronic Protected Health Information (ePHI) requires continuous monitoring and strict administrative safeguards. The configurations provided in this repository map directly to **NIST CSF 2.0 (Respond Function)** and the **HIPAA Security Rule (45 CFR § 164.308)**.

These artifacts are designed to give enterprise IT Administrators and Security Operations Center (SOC) teams "copy-paste-deploy" utilities to detect and mitigate compliance violations in real-time.

---

## 📂 Repository Structure

* [`yara-l-rules/`](https://github.com/tcharboneau/NIST-HIPAA-GOOGLEDOCS-COMPLIANCE/tree/main/yara-l-rules)) — Specialized detection logic for Google Security Operations (Chronicle SIEM).
* [`dlp-policies/`](/dlp_policies) — Data Loss Prevention regex templates for the Google Workspace Admin Console.
* 
* ### 🛡️ Core Detection Rules (YARA-L)
Configure these rules within Google Security Operations (Chronicle) to monitor your HIPAA scope:

* [Detect USB Exfiltration](https://github.com/tcharboneau/NIST-HIPAA-GOOGLEDOCS-COMPLIANCE/blob/main/yara-l-rules/Detect_%20USB_%20Exfiltration) — Tracks local file movement to external media.
* [Detect Cloud Data Loss](yara-l-rules/data_loss.yaral) — Monitors high-volume sensitive document downloads.
* [Google SIEM Base Detection](yara-l-rules/google_siem_base.yaral) — Core endpoint and environment security baseline.
* [MFA / 2SV Disabled Alarm](yara-l-rules/mfa_disabled.yaral) — Alerts immediately if a user disables multi-factor authentication.

---
Google Workspace Hardening for HIPAA ComplianceThis repository contains configuration templates and detection rules to help secure Google Workspace (specifically Google Docs and Drive) for HIPAA compliance.It provides tools for both real-time prevention (Google Workspace DLP) and post-event alerting (YARA-L for SIEM log analysis).

📂 Repository Structuredlp-policies/ - Contains raw Regular Expression (Regex) patterns to copy-paste directly into your Google Workspace Admin Console to block data leaks before they happen.

yara-l-rules/ - Contains YARA-L rule files to deploy in your Security Operations platform (like Google Chronicle) to alert security teams if Protected Health Information (PHI) is shared improperly.

🛠️ Setup Instructions1. Real-Time Prevention: Google Workspace DLP SetupTo proactively block users from typing or sharing PHI inside Google Docs:Log into your Google Workspace Admin Console.Navigate to Security > Access and data control > Data protection.Click Manage Detectors, then select Create Custom Detector.Choose Regular Expression (Regex).Open any file inside the dlp-policies/ folder of this repository, copy the pattern, and paste it into Google's regex field.Create a DLP Rule using your new detector to define an action (e.g., Block external sharing or Warn user).

2. Post-Event Alerting: YARA-L Rules SetupTo monitor Google Workspace audit logs for compliance violations after they occur:Open your SIEM / Log Analytics platform (such as Google Chronicle).Navigate to the Rules Editor.Create a new rule and copy-paste the contents of the .yaral files found in the yara-l-rules/ folder of this repository.Save and activate the rules to begin receiving security alerts.
3.
4. ⚖️ DisclaimerThis repository is intended for security hardening reference only. Deploying these rules does not automatically guarantee legal HIPAA 
compliance. Consult with your organization's legal and compliance officers to verify full compliance requirements.

## 🛡️ Featured Detections & Policies

### 1. Unauthorized External File Sharing
* **Code File:** [`workspace_hipaa_external_share.yaral`](yara-l-rules/workspace_hipaa_external_share.yaral)
* **Framework Mapping:** HIPAA Security Incident Procedures (§ 164.308(a)(6)(i)) | NIST CSF 2.0 RS.MA
* **Purpose:** Triggers a HIGH severity alert the moment an internal user shares a Google Doc, Sheet, or Drive file with an unapproved personal email domain (e.g., `@gmail.com`, `@yahoo.com`).

### 2. Multi-Factor Authentication Deactivation
* **Code File:** [`workspace_mfa_disabled.yaral`](yara-l-rules/workspace_mfa_disabled.yaral)
* **Framework Mapping:** HIPAA Access Control (§ 164.312(a)(1)) | NIST CSF 2.0 PR.AA
* **Purpose:** Triggers a CRITICAL severity alert if an administrative action or user setting disables 2-Step Verification (2SV), creating an immediate identity gap.

### 3. DLP Policy Tampering Detection
* **Code File:** [`workspace_dlp_policy_tampering.yaral`](yara-l-rules/workspace_dlp_policy_tampering.yaral)
* **Framework Mapping:** HIPAA Security Management Process (§ 164.308(a)(1))
* **Purpose:** Alerts security teams instantly if an administrator or compromised account modifies, disables, or deletes an active Data Loss Prevention safeguard.

### 4. Healthcare DLP Regex Identifiers
* **Configuration File:** [`healthcare_dlp_regex_templates.json`](dlp-policies/healthcare_dlp_regex_templates.json)
* **Framework Mapping:** HIPAA Protected Health Information Identifiers (§ 164.514)
* **Purpose:** Custom regular expressions designed for the Google Admin Console to scan Google Docs for National Provider Identifiers (NPI), ICD-10 medical codes, and Medical Record Numbers (MRN).

---

## 🚀 Quick Start Guide

### Prerequisites
* Paid subscription to **Google Workspace Enterprise Standard/Plus** or **Education Standard/Plus** (required for direct Native Ingestion pipelines).
* A signed **Google Workspace Business Associate Agreement (BAA)**.
* Active tenant access to **Google Security Operations** (Chronicle SIEM).

### How to Deploy YARA-L Rules
1. Log in to your **Google Security Operations** console.
2. Navigate to **SIEM Settings** > **Rules Studio**.
3. Click **New Rule**.
4. Copy the raw text from any `.yaral` file inside the `yara-l-rules/` directory and paste it into the editor.
5. Click **Validate** to check syntax correctness, then click **Save & Enable**.

---

## 📝 Disclaimer & License

* **Disclaimer:** These templates and rules are provided as educational resources and operational starting points. Deploying these files does not guarantee absolute legal compliance. Always consult your organization's Chief Compliance Officer or legal counsel.
* **License:** Distributed under the MIT License. See `LICENSE` for more information.

---

## 🔗 Connected Resources

This repository serves as the technical companion code for my ongoing series on LinkedIn regarding enterprise healthcare security automation. Read the full operational breakdowns here:
* [Link to LinkedIn Article 1: Mapping NIST CSF 2.0 to HIPAA]
* [Link to LinkedIn Article 2: Hardening Google Admin Console for Enterprise Healthcare]

## 🛡️ Featured Detections

### 1. Unauthorized External File Sharing
* **Code File:** [`workspace_hipaa_external_share.yaral`](yara-l-rules/workspace_hipaa_external_share.yaral)
* **Framework Mapping:** HIPAA Security Incident Procedures (§ 164.308(a)(6)(i)) | NIST CSF 2.0 RS.MA-01
* **Purpose:** Triggers a HIGH severity alert the moment an internal user shares a Google Doc, Sheet, or Drive file with an unapproved personal email domain.

### 2. Multi-Factor Authentication Deactivation
* **Code File:** [`workspace_mfa_disabled.yaral`](yara-l-rules/workspace_mfa_disabled.yaral)
* **Framework Mapping:** HIPAA Access Control (§ 164.312(a)(1)) | NIST CSF 2.0 PR.AA-01
* **Purpose:** Triggers a CRITICAL severity alert if an administrative action or user setting disables 2-Step Verification (2SV).

### 3. DLP Policy Tampering
* **Code File:** [`workspace_dlp_policy_tampering.yaral`](yara-l-rules/workspace_dlp_policy_tampering.yaral)
* **Framework Mapping:** HIPAA Security Management Process (§ 164.308(a)(1))
* **Purpose:** Alerts security teams instantly if a Data Loss Prevention guardrail is modified, disabled, or deleted.

## 🚀 Quick Start Guide

### Prerequisites
* **Paid subscription** to Google Workspace Enterprise Standard/Plus or Education Standard/Plus (required for Data Integrations).
* A signed **Google Workspace Business Associate Agreement (BAA)**.
* Active tenant access to **Google Security Operations (Chronicle SIEM)**.

### How to Deploy the YARA-L Rules
1. Log in to your **Google Security Operations** console.
2. Navigate to **SIEM Settings** > **Rules Studio**.
3. Click **New Rule**.
4. Copy the raw text from any `.yaral` file in our `yara-l-rules/` folder and paste it into the editor.
5. Click **Validate** to ensure syntax correctness, then click **Save & Enable**.

## 📝 Disclaimer & License

### Disclaimer
These templates and rules are provided as educational resources and operational starting points. Deploying these files does not guarantee absolute legal compliance. Always consult your organization's Chief Compliance Officer or legal counsel.

### License
Distributed under the MIT License. See `LICENSE` for more information.

---

## 🔗 Connected Resources

This repository serves as the technical companion code for my ongoing series on LinkedIn regarding enterprise healthcare security automation. Read the full operational breakdowns here:

* **Article 1:** [Google-Based HIPAA Compliance Framework](https://www.linkedin.com/pulse/google-based-hipaa-compliance-tifanie-charboneau-bytfc)
* **Article 2:** [Hardening Google Admin Console for Enterprise Healthcare (Link Coming Soon)]
Use code with caution.
