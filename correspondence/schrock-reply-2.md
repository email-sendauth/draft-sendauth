# Reply to Iman Schrock — Canonicalization, Reply Codes, Policy

**Status:** Draft for review
**Date:** September 3, 2026
**To:** dispatch@ietf.org
**Context:** Reply to Iman's follow-up on canonicalization, 235 reply code, ABNF, and policy scope

---

Iman,

Adopted on all points.

On canonicalization: the draft now specifies that the MUA freezes the complete RFC 5322/MIME byte sequence — including generated Date and Message-ID, CRLF-normalized — and computes the digest before dot-stuffing. The MSA reverses SMTP transparency and compares before applying any RFC 6409 mutations or adding its own fields (Received, DKIM-Signature, ARC, Authentication-Results, SVR). Those fields fall outside the authorization by processing order, not by header enumeration. The envelope is bound separately: exact MAIL FROM, then every accepted RCPT TO in order, preserving parameters and duplicates. DKIM relaxed canonicalization is explicitly rejected as too permissive.

On the reply code: corrected. The SENDAUTH challenge now uses a 334 intermediate reply. 235 appears only as the completion reply after successful verification. The draft also adds ABNF for the SENDAUTH command syntax and a line-length rule for the base64-encoded attestation (4096-octet maximum, with RFC 3030 chunking as the fallback for larger payloads).

On policy scope: the draft now defines a SENDAUTH Enforcement Policy. The default is full enforcement for all human-context sessions, but operators can narrow to account-level or role-level subsets. The policy can only condition on what the MSA knows at challenge time — the authenticated identity, the sender address, and account metadata — never recipients or content, which arrive later in the SMTP sequence. Within the policy scope, enforcement is mandatory with no soft-fail mode. The Downgrade Resistance section and the compromised-account language are updated accordingly.

Christopher
