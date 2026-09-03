# SENDAUTH Cold Outreach Drafts

Prepared September 2026 for building the operational case per Eric Rescorla's request for evidence of operator interest.

---

## 1. Google / Gmail Security Team

**To:** security@google.com (or relevant Gmail/Workspace security contact)
**Subject:** IETF Draft — Per-Send Sender Verification for SMTP Submission (SENDAUTH)

Hi,

I'm reaching out because Gmail is uniquely positioned to evaluate — and potentially benefit from — a proposal I've brought to the IETF: SENDAUTH, an SMTP submission extension that adds real-time sender identity verification at MAIL FROM.

The problem is narrow but real: once a user's OAuth token is cached in an MUA, anyone with physical access to that device can send as that user without challenge. SPF, DKIM, and DMARC verify domains and message integrity, but none of them verify that the person hitting "send" is the account holder. SENDAUTH closes that gap.

The extension defines two attestation levels. Level 1 requires user verification (biometric or PIN via WebAuthn/FIDO2) before the MSA accepts a message. Level 2 adds message authorization, binding the sender's identity to recipients and a content digest. Programmatic senders are carved out — automated systems authenticate via machine credentials and are unaffected.

Google already operates WebAuthn infrastructure at scale for account sign-in, and has led industry adoption of DMARC and BIMI. SENDAUTH would extend that same infrastructure to the point of send. The precedent here is STIR/SHAKEN for voice: the standard existed before the TRACED Act mandate, but operator engagement was what moved it from draft to deployment.

The draft is in early IETF discussion on the mailmaint list, and I'm building the operational case for implementability.

- Draft: https://github.com/email-sendauth/draft-sendauth
- IETF discussion: https://mailarchive.ietf.org/arch/msg/dispatch/ELzDGpNZYiQoOWe9oElCsBOBppY/

Would your team be interested in reviewing the draft and providing feedback on implementability? Even a brief assessment of feasibility from Google's perspective would be valuable.

Best regards,
Christopher Cocchiaraley
cc15000@gmail.com

---

## 2. Microsoft / Outlook Security Team

**To:** secure@microsoft.com (or relevant Exchange Online/Outlook security contact)
**Subject:** IETF Draft — Per-Send Sender Verification for SMTP Submission (SENDAUTH)

Hi,

I'm writing to share an IETF proposal that addresses a gap in email authentication I think Microsoft's email security team would find relevant: SENDAUTH, an SMTP submission extension for per-send sender identity verification.

Today, SMTP AUTH and OAuth establish that a session belongs to a credentialed user, but they don't verify that the person composing each message is the account holder. Once credentials are cached in Outlook or another MUA, anyone with device access can send without challenge. SPF, DKIM, and DMARC don't cover this — they operate at the domain and message-integrity layer, not the sender-identity layer.

SENDAUTH adds a verification step at MAIL FROM. Level 1 attestation requires user verification via WebAuthn/FIDO2 (biometric, PIN, or hardware key) before the MSA accepts the message. Level 2 adds message authorization, binding the verified identity to recipients and content. Programmatic senders — automated pipelines, service accounts — are carved out and unaffected.

Microsoft already supports passkeys and FIDO2 across Entra ID and consumer accounts, and has been a leader in email security standards. SENDAUTH would leverage that existing authenticator infrastructure for per-send assurance. The closest precedent is STIR/SHAKEN for telephony, where operator engagement with the standard preceded the regulatory mandate.

The draft is in early IETF discussion, and I'm building the operational case — specifically, gathering operator perspectives on implementability.

- Draft: https://github.com/email-sendauth/draft-sendauth
- IETF discussion: https://mailarchive.ietf.org/arch/msg/dispatch/ELzDGpNZYiQoOWe9oElCsBOBppY/

Would your team be interested in reviewing the draft and providing feedback on implementability? Understanding the Exchange Online perspective would be particularly valuable.

Best regards,
Christopher Cocchiaraley
cc15000@gmail.com

---

## 3. Apple Mail / iCloud Mail Team

**To:** product-security@apple.com (or relevant iCloud Mail contact)
**Subject:** IETF Draft — Per-Send Sender Verification for Email (SENDAUTH)

Hi,

I'm reaching out about an IETF proposal that aligns closely with something Apple already does well: requiring biometric verification at the point of transaction.

SENDAUTH is an SMTP submission extension that adds real-time sender identity verification at MAIL FROM. The concept is straightforward — the same way Apple Pay requires Face ID or Touch ID before authorizing a payment, SENDAUTH requires user verification before the mail server accepts a message for delivery. Right now, once an email account is configured on an iPhone or Mac, anyone with device access can send as that user without challenge. Existing standards (SPF, DKIM, DMARC) verify domains and message integrity but not the person hitting send.

The extension defines two attestation levels. Level 1 requires biometric or PIN verification via WebAuthn/FIDO2. Level 2 adds message authorization, binding identity to recipients and content. Automated senders are carved out — no disruption to programmatic systems.

Apple controls both the MUA (Mail.app) and the authenticator hardware (Secure Enclave, Face ID, Touch ID) across iOS and macOS. That vertical integration makes Apple uniquely positioned to implement per-send verification seamlessly. The precedent is STIR/SHAKEN for voice calls, where the standard preceded the regulatory mandate — operator engagement is what moved it forward.

The draft is in early IETF discussion, and I'm gathering operator perspectives on feasibility.

- Draft: https://github.com/email-sendauth/draft-sendauth
- IETF discussion: https://mailarchive.ietf.org/arch/msg/dispatch/ELzDGpNZYiQoOWe9oElCsBOBppY/

Would your team be interested in reviewing the draft and providing feedback on implementability? Apple's perspective on the MUA-side integration would be especially useful.

Best regards,
Christopher Cocchiaraley
cc15000@gmail.com

---

## 4. Generic Template (Email Operators / Security Companies)

**To:** [Contact]
**Subject:** IETF Draft — Per-Send Sender Verification for SMTP Submission (SENDAUTH)

Hi,

I'm reaching out about an IETF proposal I think [Organization] would find relevant: SENDAUTH, an SMTP submission extension that adds real-time sender identity verification at the point of send.

The gap it addresses: SMTP AUTH establishes that a session belongs to a credentialed user, but it doesn't verify that the person composing each individual message is the account holder. Once credentials are cached in an MUA, anyone with device access can send without challenge. SPF, DKIM, and DMARC operate at the domain and message-integrity layer — none of them verify sender identity at the MUA layer.

SENDAUTH extends RFC 6409 with a verification step at MAIL FROM. Level 1 attestation requires user verification (biometric, PIN, or hardware key via WebAuthn/FIDO2) before the MSA accepts a message. Level 2 adds message authorization, binding the verified identity to recipients and a content digest. Programmatic senders are carved out — automated systems authenticate via machine credentials and are unaffected.

The closest precedent is STIR/SHAKEN for voice telephony: the standard was developed before the TRACED Act mandate, but it was operator engagement that moved it from proposal to deployment. SENDAUTH is at a similar early stage — in active discussion on the IETF mailmaint list, with feedback from several IETF participants. I'm now building the operational case for implementability.

- Draft: https://github.com/email-sendauth/draft-sendauth
- IETF discussion: https://mailarchive.ietf.org/arch/msg/dispatch/ELzDGpNZYiQoOWe9oElCsBOBppY/

Would your team be interested in reviewing the draft and providing feedback on implementability? [One sentence on why their specific perspective matters.]

Best regards,
Christopher Cocchiaraley
cc15000@gmail.com
