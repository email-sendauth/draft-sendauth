# SENDAUTH: Per-Send Sender Identity Verification for SMTP Submission

**Internet-Draft:** `draft-cocchiaraley-dispatch-sendauth-00`

**Author:** Christopher Cocchiaraley (cc15000@gmail.com)

**Status:** Individual submission, pre-Datatracker — referred to [mailmaint](https://www.ietf.org/mailman/listinfo/mailmaint) by Dispatch, seeking community feedback

---

## Overview

This repository contains an Internet-Draft proposing the **SENDAUTH extension** to SMTP message submission ([RFC 6409](https://www.rfc-editor.org/rfc/rfc6409)). SENDAUTH enables a Mail Submission Agent (MSA) to require real-time sender identity verification — via biometric challenge, PIN, or hardware authenticator — at the point a message is submitted for delivery.

### The Problem

Existing email authentication standards (SPF, DKIM, DMARC) verify **domains**, not **individuals**. SMTP AUTH ([RFC 4954](https://www.rfc-editor.org/rfc/rfc4954)) verifies identity at session login, but not at send time. Modern email clients manage connections, authentication, and credential storage transparently — an unauthorized party with physical access to an unlocked device can send messages through the client's interface, and the client will authenticate on their behalf without any identity challenge. The threat operates at the MUA (email client) layer, and connection-level mitigations do not address it.

### The Proposal

SENDAUTH defines:

- A `SENDAUTH` SMTP service extension with challenge-response at the point of `MAIL FROM`
- A **Sender Presence Attestation (SPA)** format building on WebAuthn/FIDO2
- Two submission classes: **Human** (per-send biometric/PIN/key verification) and **Programmatic** (machine credentials, exempt from per-send challenge)
- A `Sender-Verification-Result` header field for downstream trust signaling
- Mandatory fallback authenticators (PIN, hardware security key) for devices without biometric hardware

### Precedent

The approach parallels **STIR/SHAKEN** ([RFC 8224](https://www.rfc-editor.org/rfc/rfc8224), [8225](https://www.rfc-editor.org/rfc/rfc8225), [8226](https://www.rfc-editor.org/rfc/rfc8226)), which solved the analogous caller ID spoofing problem for voice telephony and was mandated by the **TRACED Act** (2019).

---

## Repository Contents

| File | Description |
|------|-------------|
| `draft-cocchiaraley-dispatch-sendauth-00.md` | The Internet-Draft in kramdown-rfc format |

## Building

To convert the draft to xml2rfc and render outputs:

```bash
gem install kramdown-rfc
kramdown-rfc2629 draft-cocchiaraley-dispatch-sendauth-00.md > draft-cocchiaraley-dispatch-sendauth-00.xml
xml2rfc draft-cocchiaraley-dispatch-sendauth-00.xml --html --text
```

You can also validate using the [IETF Author Tools](https://author-tools.ietf.org/).

## Feedback

This draft is in the early feedback stage. Comments, questions, and suggestions are welcome:

- **Open an issue** on this repository
- **Email the author** at cc15000@gmail.com
- **Discussion on the IETF mailmaint mailing list:** [mailmaint@ietf.org](mailto:mailmaint@ietf.org) ([archive](https://mailarchive.ietf.org/arch/browse/mailmaint/))
- **Original Dispatch thread:** [archive](https://mailarchive.ietf.org/arch/msg/dispatch/ELzDGpNZYiQoOWe9oElCsBOBppY/)

## License

This document is subject to BCP 78 and the IETF Trust's Legal Provisions Relating to IETF Documents. See the [IETF Trust Legal Provisions](https://trustee.ietf.org/license-info) for details.
