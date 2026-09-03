# M3AAWG Research — SENDAUTH Engagement Strategy

**Date:** September 2, 2026
**Purpose:** Research for Christopher Cocchiaraley to engage M3AAWG as a venue for presenting the SENDAUTH Internet-Draft to email operators.

---

## 1. What is M3AAWG?

The **Messaging, Malware and Mobile Anti-Abuse Working Group (M3AAWG)** is a technology-neutral global industry association founded in 2004. It provides a collaborative, trusted forum where industry stakeholders work together to fight and prevent online abuse — including botnets, malware, spam, phishing, DoS attacks, and other forms of exploitation.

M3AAWG has **200+ members worldwide** representing more than **one billion mailboxes**. Members include ISPs, communications service providers, social networking companies, hosting/cloud providers, antivirus/security vendors, email service providers, hardware/software vendors, major brands, invited experts, government agencies, and academic institutions.

**Four Strategic Priorities (reorganized February 2026):**
1. **Communications & Content** — Securing the Conversation
2. **Platform & Infrastructure** — Hardening the Stack
3. **User & Endpoint** — Protecting the Edge
4. **Policy & Regulations** — Applying the Expertise

Each priority has a dedicated Committee with Chairs, Vice Chairs, and Special Interest Groups (SIGs).

**Website:** https://www.m3aawg.org/

---

## 2. Membership — Major Email Operators

M3AAWG's membership includes the operators who would need to implement SENDAUTH. Full roster: https://www.m3aawg.org/about/roster

### Sponsor Members ($25,000/year — board seats)
- **Google LLC**
- **Microsoft Corporation**
- **Yahoo**
- **Amazon Web Services**
- **Meta Platforms**
- **Adobe Systems**
- **AT&T**
- **Comcast**
- **LinkedIn**
- **Orange**
- **Proofpoint**
- **VeriSign Inc.**
- **Valimail**

### Full Members ($12,500/year — voting rights)
- **Apple Inc.**
- **Cisco Systems Inc.**
- **Mimecast**
- **Netcraft**
- **Spamhaus**
- **Oracle Marketing Cloud**
- **Tucows Inc.**
- **Brevo**
- **dotdigital**
- **Internet Initiative Japan (IIJ)**

### Notable Supporter Members ($5,000/year)
- Akamai Technologies
- Capital One
- Charter Communications
- DuckDuckGo
- GoDaddy.com LLC
- HubSpot
- JPMorgan Chase & Co.
- Klaviyo Inc.
- Mailchimp (by Intuit)
- Rakuten Group Inc.
- Shopify
- Sophos Ltd
- Swisscom
- Zoho Corporation
- ActiveCampaign, AWeber, Braze, Customer.io, dmarcian, MailChannels, and many more

### Academic & Nonprofit Members ($1,000/year)
- University of Wisconsin-Madison
- Cyber Defence Alliance
- Internet Archive
- CERT.br/NIC.br
- Global Cyber Alliance
- The World Bank

**Key takeaway for SENDAUTH:** Google, Microsoft, Yahoo, Apple, Comcast, and AT&T — the operators whose implementation is critical for SENDAUTH adoption — are all M3AAWG members. This is the primary industry venue where they discuss email authentication collectively.

---

## 3. Upcoming Meetings

### NEXT: 68th General Meeting
- **Dates:** October 26–29, 2026
- **Location:** Paris, France
- **Venue:** Paris Marriott Rive Gauche Hotel
- **Registration:** Opens week of August 24, 2026
- **Registration fee:** $600 USD (early) / $750 USD (late, after October 21)
- **Hotel rate cutoff:** September 30, 2026
- **Registration contact:** registration@m3aawg.org
- **Attendance:** 400–600 participants typical
- **URL:** https://www.m3aawg.org/events/68th-general-meeting

### Future Meetings
| Meeting | Dates | Location |
|---------|-------|----------|
| 69th General Meeting | February 15–18, 2027 | Vancouver, Canada |
| 70th General Meeting | June 14–17, 2027 | Dublin, Ireland |

M3AAWG holds three general meetings per year, rotating among North America, Europe, and occasionally other regions.

---

## 4. How to Become a Member

**Application page:** https://www.m3aawg.org/join

### Membership Tiers and Annual Dues

| Tier | Annual Dues | Key Benefits |
|------|-------------|--------------|
| Sponsor | $25,000 | Board position, all Full Member benefits |
| Full Member | $12,500 | Voting rights, board eligibility, document approval |
| Supporter | $5,000 | Committee participation, no voting rights |
| Academic Institution | $1,000 | Committee access, multiple attendees |
| Nonprofit Institution | $1,000 | Same as Academic |
| Academic Individual | $500 | For professors/researchers, references required |

### Application Process
1. Submit online application at https://www.m3aawg.org/join
2. Describe your "active role in protecting users, networks, or platforms from online abuse"
3. Detail experience in detection, mitigation, and defense strategies
4. Review takes up to **21 business days**; additional information may be requested
5. Board of Directors must approve all memberships
6. Annual dues invoiced; payment required within 45 days
7. **New members cannot publicly display M3AAWG logos or claim membership for their first 12 months**

### Recommendation for SENDAUTH Author
An individual IETF author without an organizational affiliation could potentially:
- Apply as an **Academic Individual** ($500) if affiliated with a university
- Seek sponsorship from an existing member organization to attend as their guest
- Present as a non-member via the Call for Proposals (see Section 5) — M3AAWG accepts external proposals

---

## 5. How to Present at M3AAWG

**Call for Proposals page:** https://www.m3aawg.org/events/call-for-proposals
**Submission portal:** https://www.m3aawg.org/members/meeting-submission-forms

### Submission Deadlines

| Meeting | Deadline |
|---------|----------|
| **68th (Paris, Oct 2026)** | **August 10, 2026** — LIKELY PASSED; check for late submissions |
| 68th specialized topics | September 22, 2026 |
| 69th (Vancouver, Feb 2027) | December 1, 2026 |
| 70th (Dublin, Jun 2027) | April 19, 2027 |

### Session Types
- **Standard Sessions/Panels:** Single speaker or panels (up to 6 people), 30–40 minutes with Q&A
- **Lightning Talks:** 10–15 minutes, up to 10 slides, meant to spark ideas or rally the community around an issue
- **Training Sessions:** Educational content
- **Keynotes:** Featured presentations

### Submission Requirements
- Proposals must align with M3AAWG's priorities and focus areas
- Review "Presentation/Training Session Requirements" PDF before submitting
- Currently limited to **in-person sessions only**
- Contact: https://www.m3aawg.org/contact-us

### SENDAUTH Presentation Strategy
1. **Lightning Talk** is the ideal entry point — 10–15 minutes to introduce the concept to operators
2. **Target the 69th meeting (Vancouver, February 2027)** — deadline December 1, 2026 gives time to prepare
3. **Frame it under "Communications & Content" priority** — aligns with "Securing the Conversation"
4. **Angle:** Position SENDAUTH as complementing DMARC enforcement — addressing the gap that DMARC authenticates domains but not whether the individual sender was authorized by the account holder to send that specific message

---

## 6. Existing M3AAWG Work on Email Authentication

### Published Best Practices and Documents

1. **M3AAWG Email Authentication Recommended Best Practices** (September 2020)
   - Covers SPF, DKIM, DMARC, and ARC deployment
   - URL: https://www.m3aawg.org/sites/default/files/m3aawg-email-authentication-recommended-best-practices-09-2020.pdf

2. **M3AAWG Technology Summaries: Email Authentication** (September 2023)
   - Reference guide covering SPF (RFC 7208), DKIM (RFC 6376), DMARC (RFC 7489)
   - URL: https://www.m3aawg.org/ts_emailauthentication

3. **M3AAWG DMARC Authentication Checklist**
   - Aims to reconcile gaps and enhance email security
   - Recognized by industry (Valimail, DuoCircle have written about it)

4. **M3AAWG Sender Best Common Practices (Version 3.0)**
   - Comprehensive guidelines for legitimate senders
   - Covers authentication implementation, list management, bounce handling, complaint processing
   - URL: https://www.m3aawg.org/SendingDomsBCP

5. **Establishing Trust in Email: Best Common Practices for Authenticating Email Messaging** (blog)
   - URL: https://www.m3aawg.org/blog/establishing-trust-in-email-best-common-practices-for-authenticating-email-messaging

### Gap Analysis — Where SENDAUTH Fits

M3AAWG's current authentication framework focuses on:
- **Domain-level authorization** (SPF: which servers can send for a domain)
- **Domain-level signing** (DKIM: proving message integrity and domain association)
- **Policy alignment** (DMARC: binding SPF/DKIM to the visible From: address)
- **Chain of custody** (ARC: preserving authentication through forwarding)

**What M3AAWG does NOT currently address:**
- **Per-sender authorization** — whether the individual using an account was authorized by the account holder to send that specific message
- **Account compromise detection** — authentication passes even when an attacker controls the account
- **Delegated sending verification** — confirming the human behind a "send" action is the legitimate account owner

This is precisely the gap SENDAUTH fills. M3AAWG's own documentation acknowledges that "despite deploying DMARC at the enforcement level, there are different ways by which impersonators can pass authentication" — this is a natural opening for the SENDAUTH conversation.

---

## 7. Key Contacts and Leadership

### Board Officers (2025–2026 term)

| Role | Name | Organization | Relevance |
|------|------|-------------- |-----------|
| Executive Director | Amy Cadagin | M3AAWG | Operational lead since 2006 |
| Board Chair | Tom Bartel | Validity | Email/security focus; Growth & Development Co-Chair |
| Board Co-Vice Chair | Severin Walker | Vade | Messaging security, incident response; former Chair |
| Board Co-Vice Chair | Mary Youngblood | — | Network abuse, trust & safety |
| Board Treasurer | Sam Silberman | Constant Contact | Email standards; founding member (2005) |
| Assistant Treasurer | Connie Klingelhoefer | AT&T | DNS, DDoS, infrastructure security |

### Emeritus Leaders
- Jerry Upton — Executive Director Emeritus (founded M3AAWG 2004)
- Michael O'Reirdan — Chairperson Emeritus
- Chris Roosenraad — Chairperson Emeritus

### Expert Advisor
- **Paul Vixie** — Internet pioneer, recently joined as Expert Advisor. Creator of BIND, key figure in DNS infrastructure. Highly relevant given DNS's role in email authentication.

### Key People to Engage for SENDAUTH

1. **Sam Silberman (Constant Contact)** — As Treasurer and founding member focused on email standards, he understands the authentication ecosystem deeply and has industry credibility.

2. **Tom Bartel (Validity)** — Board Chair with email and security focus. Validity provides email deliverability tools, so authentication gaps directly affect their business.

3. **Severin Walker (Vade)** — Former Chair, messaging security and incident response expertise. Vade deals with compromised-account abuse daily.

4. **Paul Vixie** — Expert Advisor with deep DNS/Internet standards credibility. Could provide valuable technical validation.

5. **Amy Cadagin** — Executive Director; the practical contact for navigating proposal submissions and introductions.

### Contact Channels
- General inquiries: https://www.m3aawg.org/contact-us
- Registration: registration@m3aawg.org
- Proposal submissions: https://www.m3aawg.org/members/meeting-submission-forms

---

## 8. Recommended Engagement Plan

### Immediate Actions (September 2026)
1. **Check if 68th meeting (Paris) specialized topic deadline (September 22) is still open** — submit a lightning talk proposal for SENDAUTH if possible
2. **Register for the 68th meeting** — registration opens week of August 24; attend even without presenting to network with operators
3. **Review M3AAWG's presentation requirements PDF** before submitting

### Near-Term (October–December 2026)
4. **Attend Paris meeting (October 26–29)** — have hallway conversations with authentication-focused attendees
5. **Submit proposal for 69th meeting (Vancouver, February 2027)** by December 1, 2026 deadline
6. **Consider M3AAWG membership** — Supporter ($5,000) gives committee access where authentication discussions happen

### Positioning
- Frame SENDAUTH as **complementary to DMARC**, not a replacement — M3AAWG has invested heavily in DMARC adoption
- Emphasize the **operational gap** M3AAWG's own documents identify: authentication passing despite account compromise
- Use M3AAWG's language: "Securing the Conversation" aligns with per-send verification
- Cite M3AAWG's published acknowledgment that impersonators can pass existing authentication

---

*Sources: m3aawg.org (about, roster, join, events, leadership, blog, best practices documents). Research conducted September 2, 2026.*
