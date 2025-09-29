# Task-2: Phishing Email Analysis

## 📌 Table of Contents
- [About](#about)
- [Objectives](#objectives)
- [Steps Performed](#steps-performed)
- [Results](#results)
- [Findings](#findings)
- [Screenshots](#screenshots)
- [Recommendations](#recommendations)

---

## About
This folder contains the analysis of a **sample phishing email** (fake Bradesco “Livelo points expiring” campaign).  
The goal of this task was to analyze the raw email headers, URLs, and authentication checks **without opening links or attachments**, and to determine whether the email is phishing.

---

## Objectives
- Safely obtain and inspect a suspicious email.  
- Analyze email headers for sender spoofing.  
- Check SPF, DKIM, and DMARC results.  
- Extract and verify embedded URLs.  
- Summarize indicators of compromise (IOCs).  
- Provide remediation recommendations.

---

## Steps Performed
1. **Collected the email sample** from the `phishing_pot` GitHub repo.  
2. **Analyzed headers** using MXToolbox / Google Admin Toolbox.  
   - Checked `From`, `Return-Path`, and `Authentication-Results`.  
3. **Verified SPF/DKIM/DMARC** → all failed.  
4. **Extracted embedded URL**:  
   - Found `https://blog1seguimentmydomaine2bra.me/`.  
   - Checked with VirusTotal and WHOIS → flagged as suspicious.  
5. **Confirmed sending IP** (`137.184.34.4`) → DigitalOcean VPS, not a bank server.  
6. **Collected verdicts** from scanners (SpamAssassin, VirusTotal).  
7. **Documented findings** and recommendations.

---

## Results
- Email is **confirmed phishing**.  
- **Spoofed sender**: pretends to be Bradesco (`@atendimento.com.br`).  
- **Authentication failed**: SPF/DKIM/DMARC not valid.  
- **Suspicious URL**: unrelated `.me` domain.  
- **Originating IP**: not owned by Bradesco.  
- **Lure**: fake claim of loyalty points expiring to trick users into clicking.

---

## Findings
Key Indicators of Phishing:
- From: `"BANCO DO BRADESCO LIVELO" <banco.bradesco@atendimento.com.br>`  
- Return-Path: `root@ubuntu-s-1vcpu...`  
- SPF: TempError, DKIM: none, DMARC: TempError  
- CompAuth: fail  
- Malicious URL: `blog1seguimentmydomaine2bra.me`  
- VPS Sender IP: `137.184.34.4`  

---

## Screenshots
- `screenshots/header-analysis.png` — header details  
- `screenshots/spf-dkim-check.png` — SPF/DKIM/DMARC results  
- `screenshots/verdicts.png` — scanner verdicts  
- `screenshots/findings-edit.png` — final findings file

---

## Recommendations
- Do not click suspicious links or trust reward/urgency emails.  
- Block IP `137.184.34.4` and domain `blog1seguimentmydomaine2bra.me`.  
- Enhance filtering for spoofed `@atendimento.com.br`.  
- Educate users about reward/point-expiration phishing tactics.  
- Report sample to anti-phishing feeds and security team.

---
