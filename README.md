# Google Workspace Hardening for HIPAA Compliance

This repository contains production-ready detection rules, templates, and configurations designed to harden Google Workspace environments. It enables healthcare providers to natively integrate logs into Google Security Operations (formerly Chronicle SIEM) to maintain compliance under federal frameworks.

## 📌 Overview

Managing Electronic Protected Health Information (ePHI) requires continuous monitoring and strict administrative safeguards. The configurations provided here map directly to **NIST CSF 2.0** and the **HIPAA Security Rule (45 CFR § 164.308)**. 

This project provides enterprise IT Administrators and Security Operations Center (SOC) teams with "copy-paste-deploy" utilities for:
* **Real-Time Prevention:** Utilizing Google Workspace Data Loss Prevention (DLP) to block leaks before they happen.
* **Post-Event Alerting:** Utilizing YARA-L rules in your SIEM platform to alert security teams of compliance violations.

---

## 📂 Repository Structure

* `dlp-policies/` — Contains raw Regular Expression (Regex) templates to copy-paste directly into the Google Workspace Admin Console.
* `yara-l-rules/` — Specialized detection logic files (`.yaral`) built for Google Security Operations (Chronicle SIEM).

---

## 🚀 Quick Start Guide

### Prerequisites
1. **Google Workspace:** Paid subscription to Enterprise Standard/Plus or Education Standard/Plus (required for Data Ingestion and DLP rules).
2. **Legal Baseline:** A signed Google Workspace Business Associate Agreement (BAA).
3. **SIEM Access:** Active tenant access to Google Security Operations (Chronicle SIEM).

### 🛠️ Setup Instructions

#### 1. Real-Time Prevention: Google Workspace DLP Setup
To proactively block users from typing or sharing ePHI inside Google Docs, Sheets, or Drive:
1. Log into your **Google Workspace Admin Console**.
2. Navigate to **Security > Access and data control > Data protection**.
3. Click **Manage Detectors**, then select **Create Custom Detector**.
4. Choose **Regular Expression (Regex)**.
5. Open any configuration file inside the `dlp-policies/` folder of this repository, copy the pattern, and paste it into Google's regex field.
6. Create an active DLP Rule using your new detector to define your enforcement action (e.g., *Block external sharing* or *Warn user*).

#### 2. Post-Event Alerting: YARA-L Rules Setup
To monitor audit logs for compliance violations after they occur:
1. Log in to your **Google Security Operations** console.
2. Navigate to **SIEM Settings > Rules Studio**.
3. Click **New Rule**.
4. Copy the raw text from any `.yaral` file inside the `yara-l-rules/` directory and paste it into the editor.
5. Click **Validate** to check syntax correctness, then click **Save & Enable**.

---

## 🛡️ Featured Detections & Policies

### 1. Unauthorized External File Sharing
* **File:** `yara-l-rules/workspace_hipaa_external_share.yaral`
* **Framework:** HIPAA § 164.308(a)(6)(i) (Security Incident Procedures) | NIST CSF 2.0 RS.MA-01
* **Purpose:** Triggers a **HIGH** severity alert the moment an internal user shares a Google Doc, Sheet, or Drive file with an unapproved personal email domain (e.g., `@gmail.com`, `@yahoo.com`).

### 2. Multi-Factor Authentication Deactivation
* **File:** `yara-l-rules/workspace_mfa_disabled.yaral`
* **Framework:** HIPAA § 164.312(a)(1) (Access Control) | NIST CSF 2.0 PR.AA-01
* **Purpose:** Triggers a **CRITICAL** severity alert if an administrative action or user setting disables 2-Step Verification (2SV), creating an immediate identity gap.

### 3. DLP Policy Tampering Detection
* **File:** `yara-l-rules/workspace_dlp_policy_tampering.yaral`
* **Framework:** HIPAA § 164.308(a)(1) (Security Management Process)
* **Purpose:** Alerts security teams instantly if an administrator or compromised account modifies, disables, or deletes an active Data Loss Prevention safeguard.

### 4. Healthcare DLP Regex Identifiers
* **File:** `dlp-policies/healthcare_dlp_regex_templates.json`
* **Framework:** HIPAA § 164.514 (Protected Health Information Identifiers)
* **Purpose:** Custom regular expressions designed for the Google Admin Console to scan Google Docs for National Provider Identifiers (NPI), ICD-10 medical codes, and Medical Record Numbers (MRN).

---

## 🔗 Connected Resources

This repository serves as the technical companion code for an ongoing series on LinkedIn regarding enterprise healthcare security automation. Read the full operational breakdowns here:

* [Article 1: Google-Based HIPAA Compliance Framework & Mapping NIST CSF 2.0](https://linkedin.com) *(Insert actual link)*
* [Article 2: Hardening Google Admin Console for Enterprise Healthcare](https://linkedin.com) *(Insert actual link)*

---

## 📝 Disclaimer & License

### Disclaimer
These templates and rules are provided as educational resources and operational starting points only. Deploying these files does not automatically guarantee absolute legal HIPAA compliance. Always consult your organization's Chief Compliance Officer, internal legal counsel, or security auditing team to verify full compliance requirements.

### License
Distributed under the **MIT License**. See the `LICENSE` file for more details.
