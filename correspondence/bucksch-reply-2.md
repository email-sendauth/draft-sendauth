# Reply to Ben Bucksch — Policy-Triggered Framework

**Status:** Sent
**Date:** September 3, 2026
**To:** dispatch@ietf.org
**Context:** Reply to Ben's follow-up pushback on UX cost, passkey ecosystem lock-in, and hardware assumptions

---

Ben,

You raise a fair point about the cost of per-send verification for routine email. The current draft revision addresses this. SENDAUTH now defines an Enforcement Policy, a local configuration that determines which sessions require per-send verification. The default is full enforcement, but operators can narrow the scope to specific accounts or roles.

A hospital could require SENDAUTH for medical records staff. A financial institution could require it for accounts authorized to issue wire instructions. The verification occurs when operator policy says the level of risk justifies it, rather than for every email. The policy is evaluated at challenge time, so it can only condition on what the MSA knows at that point, never recipients or content, which arrive later in the SMTP sequence.

Passkey ecosystem lock-in is not a SENDAUTH concern. The portability of credentials across platforms is a question for the FIDO Alliance and the platform vendors, and my understanding is that progress is happening there. With respect to the hardware assumptions, the draft requires MSAs to advertise at least two attestation mechanisms, including a PIN fallback for environments without biometric hardware.

iMessage actually does per-message cryptographic sender identity verification. Every message is signed with the sender's device key. The process is invisible because Apple controls the client, the protocol, and the key distribution. As a federated protocol with no single vendor controlling MUA, MSA, and key infrastructure, email cannot achieve that. SENDAUTH is the mechanism to get iMessage-grade sender identity binding in a federated architecture. The user-facing ceremony is what a federated protocol requires to verify sender identity on a per-message basis.

Christopher
