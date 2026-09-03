# SENDAUTH -- Potential Sympathetic Contacts in Email Security

Research compiled September 2026 for outreach on draft-cocchiaraley-sendauth
(per-send sender identity verification for SMTP submission).

---

## 1. Valimail

**Overview:** Leading email authentication company, inventor of hosted DMARC (2015)
and DMARC-as-a-service (2021). Preferred DMARC platform by Microsoft. Also
created the fully automated BIMI solution (Valimail Amplify). DigiCert company.

### Key Contacts

**Seth Blank -- Chief Technology Officer**
- Co-chair of IETF DMARC Working Group
- Chair of AuthIndicators Working Group (BIMI)
- Author of ARC (Authenticated Received Chain)
- Co-Vice Chairperson of M3AAWG; co-chair of M3AAWG Election Security SIG
- LinkedIn: https://www.linkedin.com/in/sethblank/
- IETF profile: active on dmarc@ietf.org mailing list
- **Why sympathetic:** As DMARC WG co-chair and ARC author, Seth has spent years
  working at the frontier of email authentication. He understands intimately
  where domain-level auth stops and individual sender gaps begin. ARC itself was
  an attempt to extend the authentication chain. He is the single most important
  industry contact for SENDAUTH.

**Alexander Garcia-Tobar -- CEO & Co-Founder**
- Previously at Agari, ValiCert, Sygate
- Co-founded the AuthIndicators Working Group (BIMI) in 2015
- Publicly stated Valimail's mission is to "authoritatively address the root
  attack vector (89%) of email fraud, phishing, brand abuse, and impersonation"
- LinkedIn: https://www.linkedin.com/in/alexgarciatobar/
- **Why sympathetic:** His framing of email authentication as addressing
  impersonation (not just domain spoofing) is aligned with SENDAUTH's goals.

**Kuldip Pabla -- Leadership team**
- Engineering leadership role at Valimail

### Alignment with SENDAUTH

Valimail has publicly positioned itself around eliminating email impersonation.
Their work on BIMI (tying visual brand identity to authenticated domains) shows
interest in going beyond basic SPF/DKIM/DMARC. However, all their current work
is domain-level. SENDAUTH's per-sender verification would represent a natural
"next layer" for their platform. Seth Blank's IETF leadership makes him the
ideal person to engage first.

### How to Reach

- IETF DMARC WG mailing list (Seth is co-chair)
- M3AAWG conferences and mailing lists
- Valimail blog comment section / "Authenticated Answers" interview series
- LinkedIn direct messages
- IETF meetings (Seth regularly presents)

---

## 2. dmarcian

**Overview:** First company dedicated to DMARC, founded in 2012 by Tim Draegen,
primary author of the DMARC specification. Self-funded, mission-driven (B Corp
certified). Operations in five countries. Focused on making DMARC accessible
to everyone, not just large enterprises.

### Key Contacts

**Tim Draegen -- Founder & President**
- Primary author of the DMARC specification
- Co-inventor of DMARC (multi-year project culminating in 2012 public release)
- Left his job immediately after DMARC was published to found dmarcian
- LinkedIn: https://www.linkedin.com/in/tdraegen/
- Active in the DMARC community and at IETF
- **Why sympathetic:** As DMARC's author, Tim understands both the power and
  the limitations of domain-level authentication better than almost anyone.
  His mission-driven approach (B Corp, self-funded, focused on accessibility)
  suggests openness to ideas that strengthen the email ecosystem. He would
  understand exactly where SENDAUTH fits in the stack.

**Ash Morin -- Team member**
- Active in dmarcian's EMEA operations and customer-facing work

### Alignment with SENDAUTH

dmarcian's entire mission is strengthening email authentication. Tim Draegen
personally knows where DMARC's design boundaries are (it was a deliberate
choice to operate at domain level). He has publicly discussed DMARC's evolution
through blog posts and the "Email, Duh!" content series. A conversation with
Tim about what comes *after* domain-level enforcement -- i.e., per-sender
verification -- would be a natural extension of his life's work.

### How to Reach

- IETF DMARC mailing list
- dmarcian blog / "Email, Duh!" series
- dmarc.org community (dmarcian maintains strong ties)
- LinkedIn
- M3AAWG events

---

## 3. Agari (now Fortra Email Security)

**Overview:** Email security company now part of Fortra (formerly HelpSystems),
combined with Clearswift, PhishLabs, and Terranova Security. Specializes in
DMARC authentication, BEC defense, and AI-powered threat detection. Named
leader in Frost Radar for email security.

### Key Contacts

**John Wilson -- Senior Fellow, Threat Research (Fortra)**
- Examines campaigns and tactics in BEC and email impersonation attacks
- Regularly publishes research on impersonation techniques
- **Why sympathetic:** His research directly documents the gaps that SENDAUTH
  addresses -- where authenticated domains are still exploited through
  compromised accounts and authorized-sender impersonation.

**Doug Jones -- Chief Business Development and Strategy Officer**
- Joined Agari to drive strategic growth in email security

### Alignment with SENDAUTH

Agari/Fortra has published extensively on BEC protection, explicitly noting
that domain authentication alone cannot stop compromised-account attacks.
Their blog post "How to Protect Against BEC from Inception to Inbox"
acknowledges that attackers exploit gaps in email authentication systems.
SENDAUTH directly addresses the compromised/unauthorized sender scenario
that their threat research team documents.

### How to Reach

- Fortra Email Security blog (emailsecurity.fortra.com)
- Conference presentations (RSA, Black Hat, M3AAWG)
- LinkedIn
- John Wilson publishes threat research regularly

---

## 4. Proofpoint

**Overview:** Major enterprise email security platform. Extensive BEC/EAC
(Email Account Compromise) research. Documented a 45% surge in BEC attacks
and increased domain spoofing. Publicly acknowledges that traditional email
security leaves gaps for account takeover and impersonation.

### Key Contacts

**Ryan Kalember -- EVP, Cybersecurity Strategy**
- Leads global threat research team
- 20+ years in information security
- Publicly stated: "Unless you do a number of steps to authenticate your
  email, pretty much anyone can send an email as you"
- Regularly speaks at cybersecurity conferences
- LinkedIn: https://www.linkedin.com/in/kalember/
- **Why sympathetic:** His public statements explicitly acknowledge the sender
  identity gap. Proofpoint's own research shows domain auth is necessary but
  insufficient. SENDAUTH could be positioned as a standards-based solution
  to a problem his team has documented extensively.

### Alignment with SENDAUTH

Proofpoint's research has identified three core impersonation tactics that
bypass domain-level auth:
1. Display name spoofing (attacker modifies From name, not domain)
2. Lookalike domains (confusingly similar domains)
3. Compromised accounts (legitimate credentials used for BEC)

Tactic #3 is exactly what SENDAUTH addresses. Proofpoint has noted that
"traditional email security... does not fully evaluate communication
patterns, relationship history, or identity risk." SENDAUTH's per-send
verification is a protocol-level solution to the compromised account problem.

### How to Reach

- Proofpoint Threat Research blog
- Conference circuit (RSA, Black Hat, Gartner Security)
- LinkedIn (Ryan Kalember is publicly active)
- Proofpoint publishes annual "State of the Phish" and BEC reports

---

## 5. Fastmail

**Overview:** Privacy-focused email provider based in Australia. Technically
sophisticated, deeply involved in IETF standards work. Bron Gondwana (CEO)
responded skeptically to SENDAUTH but remains an important contact given
Fastmail's role in email standards.

### Key Contacts

**Bron Gondwana -- CEO**
- Co-chair of IETF JMAP and EXTRA Working Groups
- Author of RFC 8474 (IMAP Object Identifiers)
- Co-author of DKIM2 specification (draft-ietf-dkim-dkim2-spec)
- Author of draft-gondwana-email-mailpath (next-hop path for email delivery)
- Implemented ARC in open source (Mail::DKIM Perl module)
- Email: brong@fastmailteam.com (public IETF profile)
- **Status:** Responded skeptically to SENDAUTH. However, his deep engagement
  with email authentication evolution (DKIM2, ARC, Mailpath) means he is
  thinking about exactly these problems. His skepticism may be about
  mechanism rather than goals.

### Alignment with SENDAUTH

Bron's work on DKIM2 and Mailpath shows he is actively working on the next
generation of email authentication. DKIM2 addresses replay attacks and
chain-of-custody -- related but different problems from per-sender verification.
Mailpath addresses routing integrity. SENDAUTH could be positioned as
complementary to these efforts, addressing the submission-side gap that
DKIM2 does not cover (DKIM2 is about transit authentication, not sender
identity at submission time).

### How to Reach

- IETF mailing lists (dmarc, ietf-dkim, jmap, extra)
- IETF meetings (regular presenter/participant)
- Fastmail blog
- Already engaged -- continue the conversation

---

## 6. Independent IETF Researchers and Contributors

### John Levine -- Independent Consultant & Expert Advisor

- Author or co-author of 10 RFCs
- Senior Technical Advisor / Expert Advisor at M3AAWG
- Member of ICANN Security and Stability Advisory Committee
- Active on IETF mailing lists since 2004
- Expert witness in email-related cases
- Website: https://www.johnlevine.com/
- LinkedIn: https://www.linkedin.com/in/johnlevine/
- **Why important:** John is one of the most respected voices in email
  standards. His opinion carries enormous weight on the IETF dmarc and
  emailcore lists. Getting his technical feedback (even critical) early
  would be valuable. He has deep knowledge of the gaps in current auth.

### Murray Kucherawy -- Meta (formerly Facebook)

- Author/co-author of 33 RFCs
- Editor of RFC 6376 (DKIM Signatures -- the foundational DKIM document)
- Former IETF Area Director (Applications and Real Time)
- Led IETF working groups: MARF, WEIRDS, DMARC
- Co-author of DKIM2 BOF request (draft-kucherawy-dkim2)
- Author of draft-kucherawy-dkim-rcpts (DKIM recipients)
- IETF profile: datatracker.ietf.org/person/superuser@gmail.com
- **Why important:** Murray's track record (33 RFCs, former AD, DKIM editor)
  makes him one of the most influential people in email standards. His
  draft-kucherawy-dkim-rcpts work on binding DKIM to recipients shows
  interest in tighter sender-recipient binding -- conceptually related to
  SENDAUTH's goals.

### Alessandro Vesely -- Independent Contributor

- Editor of RFC 9991 (DMARC Failure Reporting)
- Author of draft-vesely-dmarc-mlm-transform (restoring From: after
  DMARC rewriting by mailing list managers)
- Active on dmarc@ietf.org mailing list
- **Why important:** His work on MLM transforms shows deep concern about
  the practical consequences of domain-level auth policies. Someone who
  cares about restoring individual sender identity after MLM processing
  would naturally be interested in per-sender verification at submission.

### Wei Chuang -- Google

- Co-author of DKIM2 specification
- Author of draft-chuang-dkim2-dns (DKIM2 DNS specification)
- Works on email authentication at scale (Google processes billions of
  messages daily)
- **Why important:** Google's buy-in is critical for any email authentication
  standard. Wei's involvement in DKIM2 shows Google is actively investing
  in next-generation email auth. Google's 2024 bulk sender requirements
  already pushed the industry toward stricter auth -- they may be receptive
  to per-sender verification as a next step.

### Tobias Herkula -- GMX / WEB.DE / mail.com (1&1 Mail & Media)

- Senior Product Owner, Mail Security
- Focuses on email authentication and sender behavior monitoring
- LinkedIn: https://www.linkedin.com/in/tobiasherkula/
- **Why important:** Represents a major European email provider perspective.
  His work on sender behavior analysis is complementary to SENDAUTH --
  behavioral signals plus cryptographic per-sender auth would be a powerful
  combination.

---

## 7. Other Email Security Companies

### Red Sift (OnDMARC)

- UK-based email authentication platform
- Strong enterprise and MSP adoption
- Website: https://redsift.com/
- **Relevance:** As a DMARC platform, they have the same strategic interest
  as Valimail in extending authentication beyond domain level. Monitor for
  thought leadership on individual sender verification.

### PowerDMARC

- Comprehensive email authentication suite
- G2 Leader for DMARC Software (Spring 2024)
- Has published articles on "email sender identity" that go beyond basic
  domain auth
- Website: https://powerdmarc.com/
- **Relevance:** Their article "What Is Email Sender Identity And Why It
  Matters For Email Security" explicitly discusses sender identity as
  distinct from domain authentication -- conceptually aligned with SENDAUTH.

### Sendmarc

- South Africa-based email authentication platform (founded 2018)
- Published detailed DKIM2 coverage showing interest in next-gen auth
- Website: https://sendmarc.com/
- **Relevance:** Their DKIM2 content shows they track emerging standards
  closely. Could be interested in SENDAUTH as another emerging standard.

### Darktrace

- AI-powered cybersecurity company
- Published "Navigating Email Security Gaps Beyond DMARC" explicitly noting
  that DMARC cannot detect compromised-account attacks
- **Relevance:** Their analysis of "beyond DMARC" gaps aligns perfectly
  with SENDAUTH's problem statement. Their blog is a useful citation for
  the SENDAUTH motivation document.

---

## 8. Related IETF Work to Monitor

### DKIM2 (draft-ietf-dkim-dkim2-spec)

- Authors: Bron Gondwana (Fastmail), Wei Chuang (Google), Richard Clayton (Yahoo)
- Addresses replay attacks, chain-of-custody, transit authentication
- SENDAUTH is complementary: DKIM2 covers transit, SENDAUTH covers submission
- The DKIM WG mailing list (ietf-dkim) is a natural venue for SENDAUTH discussion

### SMTP Client Identity (draft-storey-smtp-client-id)

- Defines "CLIENTID" SMTP extension for MFA-like identity verification
- Directly related to SENDAUTH's problem space (per-client identity at submission)
- Author could be a natural ally or the drafts could be harmonized

### Mailpath (draft-gondwana-email-mailpath)

- Bron Gondwana's proposal for specifying next-hop delivery path
- Addresses routing integrity, complementary to sender identity

---

## 9. Key IETF Mailing Lists for Engagement

| List | Focus | Key People Active |
|------|-------|--------------------|
| dmarc@ietf.org | DMARC WG | Seth Blank (co-chair), Alessandro Vesely, John Levine, Tim Draegen |
| ietf-dkim@ietf.org | DKIM/DKIM2 WG | Bron Gondwana, Wei Chuang, Murray Kucherawy, Tobias Herkula |
| emailcore@ietf.org | Core email protocols | Various email standards contributors |
| dispatch@ietf.org | New work proposals | Broader IETF community |

---

## 10. Recommended Outreach Priority

### Tier 1 -- Engage First
1. **Seth Blank (Valimail)** -- DMARC WG co-chair, ARC author, most aligned
2. **Tim Draegen (dmarcian)** -- DMARC author, mission-driven, understands the gaps
3. **John Levine** -- Respected voice, early feedback prevents missteps

### Tier 2 -- Engage After Initial Feedback
4. **Murray Kucherawy (Meta)** -- 33 RFCs, DKIM editor, enormous influence
5. **Wei Chuang (Google)** -- Google's buy-in is critical
6. **Bron Gondwana (Fastmail)** -- Already engaged, continue dialogue
7. **Alessandro Vesely** -- Active contributor, cares about sender identity

### Tier 3 -- Industry Outreach
8. **Ryan Kalember (Proofpoint)** -- BEC research validates the problem
9. **John Wilson (Fortra/Agari)** -- Threat research alignment
10. **Tobias Herkula (GMX)** -- European provider perspective

### Conferences for Face-to-Face Contact
- **IETF meetings** (next scheduled meetings -- check ietf.org/meetings)
- **M3AAWG** (Messaging, Malware and Mobile Anti-Abuse Working Group)
- **RSA Conference** (broader security, Proofpoint/Fortra presence)
- **Email Innovations Summit** / **Inbox Expo** (email industry events)

---

## 11. Key Arguments to Lead With

When approaching these contacts, frame SENDAUTH around:

1. **The BEC gap:** Domain authentication (SPF/DKIM/DMARC) does not prevent
   authorized users from sending as other authorized users on the same domain.
   This is the #1 exploited gap in BEC attacks via compromised accounts.

2. **Complementary to DKIM2:** DKIM2 addresses transit authentication and
   replay attacks. SENDAUTH addresses submission-side sender identity. They
   solve different halves of the same problem.

3. **Natural next step after Google/Yahoo bulk sender requirements (2024):**
   The industry accepted stricter domain-level auth. Per-sender verification
   is the logical next layer.

4. **Already a de facto practice:** Many mail submission agents already verify
   that the authenticated user is authorized to send as the claimed From
   address. SENDAUTH standardizes and strengthens this existing behavior.
