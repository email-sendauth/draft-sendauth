# SENDAUTH: Per-Send Sender Identity Verification for Email

**An IETF Internet-Draft (draft-cocchiaraley-dispatch-sendauth-00)**

---

## The Problem: Email's Missing Authentication Layer

DKIM, SPF, and DMARC verify that a *domain* authorized a message. They say nothing about whether the *person* behind the keyboard authorized it. Once a user's OAuth token is cached on a device, anyone with physical or remote access to that device can send as them — silently, indefinitely, and indistinguishably from a legitimate message.

This gap fuels business email compromise (BEC), the most costly category of cybercrime. The FBI's Internet Crime Complaint Center reports BEC losses exceeding **$55 billion** since 2013, with over **$2.9 billion** in 2023 alone. Existing defenses catch domain spoofing. They cannot catch an attacker sending from a legitimately authenticated session.

## What SENDAUTH Does

SENDAUTH extends RFC 6409 (email submission) so that a Mail Submission Agent can require real-time sender identity verification at the point of MAIL FROM. It defines two attestation levels:

- **Level 1 — User Verification.** A WebAuthn/FIDO2 ceremony confirms the credential holder was physically present at send time. Proves a person — not just a cached token — initiated the send.

- **Level 2 — Message Authorization.** The attestation cryptographically binds the sender identity, envelope recipients, and a content digest. The credential holder approved *this specific message*.

A downstream **Sender-Verification-Result** header carries the verification status (verified, authorized, machine, none), giving receiving operators a new signal for filtering and trust decisions.

Programmatic senders — service accounts, mailing lists, transactional systems — are carved out via a separate submission class. No disruption to automated mail flows.

## Why Operators Should Act Now

**Trust differentiation.** Operators whose messages carry "sender authorized" indicators gain a concrete reputation advantage. In a world of AI-generated phishing and deepfake social engineering, provable human intent behind a message is a premium signal. Early adopters define the standard; late movers comply with it.

**The STIR/SHAKEN precedent.** Carriers did not volunteer for caller ID verification. Consumer trust in voice calls eroded until the TRACED Act (2019) mandated STIR/SHAKEN (RFC 8224/8225/8226). Email is on the same trajectory. The question is whether operators shape the standard or react to legislation.

**Infrastructure already exists.** WebAuthn/FIDO2 is built into every modern laptop, phone, and browser. Platform authenticators (Touch ID, Windows Hello, Android biometrics) mean no hardware tokens required. The verification ceremony is sub-second and familiar to users.

**Compliance flexibility.** SENDAUTH is designed for incremental adoption. Operators can deploy Level 1 first, offer Level 2 as a premium capability, and extend timelines for legacy clients. The programmatic carve-out ensures automated systems are unaffected from day one.

## Next Steps

The draft targets submission to the IETF Datatracker ahead of IETF 118 (November 2026). We are seeking operator feedback on deployment considerations, attestation-level priorities, and interest in early interoperability testing.

**Contact:** Christopher Cocchiaraley — cc15000@gmail.com
**Draft:** github.com/email-sendauth/draft-sendauth
