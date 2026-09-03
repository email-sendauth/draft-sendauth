# Reply to John C Klensin — SENDAUTH Architectural Points

**Status:** Sent
**Date:** September 2, 2026
**To:** john-ietf@jck.com
**Cc:** dispatch@ietf.org, emailcore@ietf.org
**Subject:** Re: [dispatch] DISPATCH guidance requested / Per-send sender identity verification for SMTP submission (SENDAUTH)

---

John,

I appreciate your feedback. If the work develops enough substance and support to warrant its own working group, it would be ideal. For now, I'm following the Dispatch thread and have introduced the proposal on mailmaint to see where interest and feedback cluster. I am working to understand the level of demand through operator outreach and engagement.

The draft proposes a Sender-Verification-Result header protected by DKIM. As you noted, this is the originating domain asserting that it performed a verification. There is no third-party attestation. STIR/SHAKEN has governance infrastructure (STI-PA, delegated certificates) that provides such attestation, but email has no equivalent root of trust.

SENDAUTH's value is at the originating domain, not the receiver. For example, a compromised account at example.com that sends fraudulent wire instructions would be stopped at submission. The message never enters the mail stream. That first-party benefit exists whether or not any receiver ever inspects the header. Receiver-side consumption of the assertion remains a challenge and outside the draft's scope.

As for the MUA boundary, the proposal specifies what happens between MUA and MSA (the protocol extension, the challenge-response, the attestation format) without addressing how the MUA obtains the user's verification. This is modeled on RFC 6409 where the MSA requires authentication, but how the MUA obtains credentials from the user is a local matter. It is also consistent with RFC 5321 §2.1.

In your view, what would a credible receiver-side trust model for a submission-time assertion need to look like? Is there an architecture that avoids requiring email to replicate STIR's governance infrastructure?

Christopher D. Cocchiaraley
cc15000@gmail.com
