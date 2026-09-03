# Email Fraud & Sender Impersonation: FBI IC3 and FTC Data Brief

**Purpose:** Quantify the operational gap that SENDAUTH (per-send sender identity verification) addresses — fraud that occurs *after* domain-level authentication succeeds, where an authorized account sends messages from the wrong human sender.

**Compiled:** September 2026

---

## 1. FBI IC3 — Business Email Compromise (BEC) Annual Losses

BEC is the single most relevant crime category: it involves unauthorized persons sending email through legitimate, authenticated accounts to redirect funds or exfiltrate data. Every BEC message sent from a compromised account passes SPF, DKIM, and DMARC.

### Year-Over-Year Trend (4 years)

| Year | BEC Complaints | Adjusted Losses   | YoY Change |
|------|---------------:|-------------------:|-----------:|
| 2022 | 21,832         | $2.74 billion      | —          |
| 2023 | 21,489         | $2.94 billion      | +7.3%      |
| 2024 | 21,442         | $2.77 billion      | −5.8%      |
| 2025 | 24,768         | $3.05 billion      | +10.1%     |

**Three-year total (2023–2025): ~$8.76 billion** in reported BEC losses alone.

Sources:
- FBI IC3, *2025 Annual Report* (April 2026): https://www.ic3.gov/AnnualReport/Reports/2025_IC3Report.pdf
- FBI IC3, *2024 Annual Report*: https://www.ic3.gov/AnnualReport/Reports/2024_IC3Report.pdf
- FBI IC3, *2023 Annual Report*: https://www.ic3.gov/annualreport/reports/2023_ic3report.pdf
- FBI IC3, *2022 Annual Report*: https://www.ic3.gov/AnnualReport/Reports/2022_ic3report.pdf

### Key 2025 Report Metrics

- **$3.046 billion** — BEC losses in 2025 (2nd-highest crime category behind investment fraud)
- **$122,000+** — average loss per BEC complaint
- **86%** of BEC funds moved via wire transfer or ACH — deep inside financial workflows
- **2.5%** of total IC3 complaints but **~15%** of all reported losses
- BEC was the **#1 most financially destructive enterprise-targeted cyber threat** in the U.S.
- **$20.877 billion** — total IC3-reported cybercrime losses in 2025 (+26% YoY)

Source: [RedSift analysis of IC3 2025 Report](https://redsift.com/blog/fbi-ic3-2025-report-email-fraud); [Rexxfield BEC analysis](https://rexxfield.com/bec-by-the-numbers-2025-ic3-report/)

### Cumulative BEC Losses (Historical)

- **$55.5 billion** in exposed losses documented by IC3 between October 2013 and December 2023 across 305,033 domestic and international incidents.
- **$17.1 billion** cumulative since BEC first appeared in IC3's 2015 report — a **1,025% increase** over the decade.

Source: FBI IC3 PSA, *"Business Email Compromise: The $55 Billion Scam"* (September 2024): https://www.ic3.gov/PSA/2024/PSA240911

---

## 2. Combined Email-Origin Fraud (2025 IC3)

When three email-exploiting crime types are combined, the picture worsens:

| Category                | 2025 Losses     | YoY Trend       |
|-------------------------|----------------:|:----------------|
| BEC                     | $3.046 billion  | +10% from 2024  |
| Government Impersonation| $797.9 million  | ~2x from 2024   |
| Phishing/Spoofing       | $215.8 million  | 11x over 2 yrs  |
| **Combined**            | **~$4.06 billion** | **+46% from 2024** |

These three categories represent approximately **19% of all 2025 cybercrime losses**.

Source: [RedSift IC3 2025 analysis](https://redsift.com/blog/fbi-ic3-2025-report-email-fraud)

### AI-Enhanced BEC (Emerging)

- 22,364 complaints cited AI involvement, totaling **$893 million** in losses.
- **$30.2 million** specifically attributed to BEC with a confirmed AI component (deepfake voices, AI-generated text).
- This is expected to grow dramatically as generative AI matures.

Source: FBI IC3, *2025 Annual Report*

---

## 3. The Authentication Gap: Domain-Level vs. Sender-Level

### What DMARC Solves and What It Does Not

DMARC (with SPF and DKIM) authenticates the **domain**, not the **human sender**. The FBI explicitly defines BEC as attacks carried out when a subject "compromises legitimate business email accounts through social engineering or computer intrusion techniques."

**Key data points on the gap:**

- **When an attacker sends from a compromised account, SPF passes, DKIM passes, and DMARC passes.** The message is indistinguishable from a legitimate email at the protocol level. (Source: [Adaptive Security, "BEC vs EAC"](https://www.adaptivesecurity.com/blog/bec-vs-email-account-compromise))

- **Only 35–44% of large U.S. organizations** have full DMARC enforcement (p=reject) as of 2025 — but even with enforcement, compromised-account BEC is unaffected because the sending domain is genuinely authorized. (Source: [RedSift IC3 2025 analysis](https://redsift.com/blog/fbi-ic3-2025-report-email-fraud))

- **Domains with DMARC enforcement see 86% fewer spoofing incidents** — but BEC from compromised accounts is *not* domain spoofing. (Source: Agari/Fortra research)

- **Account takeover fraud cost U.S. consumers $16 billion in 2024**, with a 24% year-over-year increase. (Source: [Adaptive Security, "Email Account Takeover Trends 2026"](https://www.adaptivesecurity.com/blog/email-account-takeover-trends))

### The Operational Scenario SENDAUTH Addresses

The IC3 defines BEC/EAC attack flow:

1. Attacker gains credentials (phishing, social engineering, credential stuffing, physical device access)
2. Attacker sends email **through the victim's authenticated MUA or webmail session**
3. The MTA accepts the message — SPF/DKIM/DMARC all pass
4. Recipient acts on a message that appears fully authenticated

**No existing standard verifies whether the human pressing "Send" is the authorized account holder.** SENDAUTH proposes closing this gap with per-send identity verification at the MUA layer.

---

## 4. FTC Complaint Data on Email-Based Fraud

### FTC Consumer Sentinel Network (2024 Data Book, published March 2025)

- **$12.5 billion** total reported fraud losses in 2024 (+25% over 2023)
- **1.13 million** identity theft reports
- **845,806** imposter scam reports
- **Email was the #1 contact method** for fraud for the second consecutive year
- **$502 million** in reported losses from email-initiated fraud specifically
- **$789 million** in government imposter scam losses (+$171 million from 2023)

Source: FTC, *Consumer Sentinel Network Data Book 2024*: https://www.ftc.gov/reports/consumer-sentinel-network-data-book-2024

### FTC 2025 Preliminary Data

- **3,025,103** fraud complaints (+1.46% from 2024)
- **$15.86 billion** total fraud losses (+24% from 2024)
- **1,358,253** identity theft reports (+31% from 2024)
- **1,005,012** imposter scam complaints (+19% from 2024)

Source: [Experian, "U.S. Fraud and Identity Theft Losses Topped $15.8 Billion in 2025"](https://www.experian.com/blogs/ask-experian/identity-theft-statistics/)

---

## 5. Verizon DBIR — Email as Attack Vector

From the *Verizon 2025 Data Breach Investigations Report*:

- **Phishing used in 57%** of social engineering incidents
- **Pretexting (including BEC) in 30%** of social engineering incidents, nearly doubled from prior years
- **Human element contributed to 60%** of all breaches
- **22% of breaches** involved compromised credentials as the initial vector
- Email security gateways block 80% of credential/session phishing — but BEC from authorized accounts **bypasses gateways entirely**

Source: [Abnormal AI analysis of Verizon 2025 DBIR](https://abnormal.ai/blog/verizon-2025-dbir-key-takeaways)

---

## 6. Insider Threat Dimension

The SENDAUTH use case extends beyond external attackers to insider misuse — anyone with physical or session access to an authenticated email client:

- **68% of organizations** experienced 21+ insider incidents per year in 2025 (up from 57% in 2024)
- **Malicious insider breaches cost $4.92 million per incident** — higher than phishing, ransomware, or BEC
- **53%** of insider incidents caused by negligent employees; **27%** by malicious insiders; **20%** by credential theft
- **77%** of organizations experienced insider-driven data loss in the past 18 months

Sources: [Exabeam, "46 Insider Threat Statistics"](https://www.exabeam.com/explainers/insider-threats/46-insider-threat-statistics-you-must-know/); [SpaceLift, "59 Insider Threat Statistics"](https://spacelift.io/blog/insider-threat-statistics)

---

## Summary: The Quantified Problem SENDAUTH Addresses

| Metric | Value | Source |
|--------|-------|--------|
| Annual BEC losses (2025) | $3.05 billion | FBI IC3 2025 |
| 3-year BEC total (2023–2025) | ~$8.76 billion | FBI IC3 |
| Cumulative BEC (2013–2023) | $55.5 billion | IC3 PSA 2024 |
| Combined email-origin fraud (2025) | $4.06 billion | FBI IC3 2025 |
| Account takeover losses (2024) | $16 billion | Adaptive Security |
| FTC email-initiated fraud losses (2024) | $502 million | FTC Sentinel 2024 |
| FTC total fraud losses (2025) | $15.86 billion | FTC/Experian |
| Avg. BEC loss per incident | $122,000+ | FBI IC3 2025 |
| BEC funds via wire/ACH | 86% | FBI IC3 2025 |
| DMARC adoption (full enforcement) | 35–44% | RedSift |
| DMARC spoofing reduction | 86% fewer | Agari/Fortra |
| BEC from compromised accounts stopped by DMARC | **0%** | By definition |

**The core argument:** Domain-level authentication (SPF/DKIM/DMARC) has reduced domain spoofing by up to 86% where deployed — but it is structurally incapable of preventing the $3+ billion/year BEC problem, which operates *through* legitimately authenticated accounts. SENDAUTH proposes the missing layer: per-send verification that the human initiating a message is the authorized account holder, enforced at the MUA before the message reaches the MTA.
