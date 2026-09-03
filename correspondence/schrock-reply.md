# Reply to Iman Schrock — Protocol Flow Fix

**Status:** Draft for review
**Date:** September 3, 2026
**To:** dispatch@ietf.org
**Context:** Reply to Iman's feedback on Level 2 protocol flow and verb inconsistency

---

Iman,

Good catches, both of them. The draft claimed no new SMTP verbs while defining SENDAUTH and SENDAUTH-AUTHORIZE as commands — that's a plain contradiction. And you're right that returning 334 after the DATA terminating dot violates RFC 5321 §4.3.2. The same class of problem existed at Level 1, where the draft issued 334 in response to MAIL FROM outside of an AUTH exchange. Both are fixed in 4f4e692 (https://github.com/email-sendauth/draft-sendauth/commit/4f4e692).

I've adopted your suggestion to move the authorization before DATA. The revised flow:

1. MAIL FROM succeeds normally (250)
2. SENDAUTH challenge-response exchange (Level 1 — sender identity verification)
3. RCPT TO (all recipients)
4. SENDAUTH-AUTHORIZE — MUA transmits a signed authorization binding identity, accepted recipients, and a canonical digest of the message content it is about to submit
5. DATA — MSA accepts the message, compares received content against the authorized digest, and replies with 250 or rejects

The verb claim is replaced with an accurate declaration of the two new commands, and the IANA section now registers them.

One open question your fix surfaces: if the MUA computes the message digest before DATA, which headers are covered by the canonical digest? Headers routinely added or modified by MUA software after composition — Message-ID, Date, Received — would cause nondeterministic verification failures if included. DKIM faced a version of this with its canonicalization algorithms (RFC 6376, Section 3.4). Do you have a view on what the right boundary is?

I also agree with your point about keeping downstream signaling separate. The SVR header is now MAY rather than MUST — the draft scopes receiver-side consumption as future work pending a relay-safe trust model.

Christopher

