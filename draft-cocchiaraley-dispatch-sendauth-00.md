---
title: "The SENDAUTH Extension for SMTP Message Submission"
abbrev: "SENDAUTH"
category: std
updates: 6409

docname: draft-cocchiaraley-dispatch-sendauth-00
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Applications and Real-Time"
workgroup: "Dispatch"
keyword:
  - email
  - authentication
  - sender verification
  - SMTP
  - biometric
  - FIDO2
  - WebAuthn

author:
  - fullname: Christopher Cocchiaraley
    email: cc15000@gmail.com

normative:
  RFC2119:
  RFC4954:
  RFC5321:
  RFC6409:
  RFC8174:
  W3C-WebAuthn:
    title: "Web Authentication: An API for accessing Public Key Credentials Level 2"
    author:
      org: World Wide Web Consortium
    date: 2021-04
    target: https://www.w3.org/TR/webauthn-2/

informative:
  RFC6376:
  RFC7208:
  RFC7489:
  RFC8224:
  RFC8225:
  RFC8226:
  RFC8617:
  TRACED-Act:
    title: "Telephone Robocall Abuse Criminal Enforcement and Deterrence Act (TRACED Act)"
    author:
      org: United States Congress
    date: 2019-12
    target: https://www.congress.gov/bill/116th-congress/senate-bill/151
  FIDO2:
    title: "FIDO2: Web Authentication (WebAuthn)"
    author:
      org: FIDO Alliance
    target: https://fidoalliance.org/fido2-2/fido2-web-authentication-webauthn/
  BOD-18-01:
    title: "Binding Operational Directive 18-01: Enhance Email and Web Security"
    author:
      org: Department of Homeland Security / CISA
    date: 2017-10
    target: https://www.cisa.gov/news-events/directives/bod-18-01-enhance-email-and-web-security

--- abstract

This document defines the SENDAUTH extension to SMTP message
submission {{RFC6409}}. SENDAUTH enables a Mail Submission Agent
(MSA) to require real-time sender identity verification — via
biometric challenge, PIN, or hardware authenticator — at the point
a message is submitted for delivery. The extension distinguishes
between human-initiated submission, which requires per-send
verification, and programmatic submission, which authenticates via
machine credentials. SENDAUTH is designed to close the gap between
session-level authentication (login) and per-action identity
assurance (send), addressing a class of impersonation that existing
email authentication standards (SPF, DKIM, DMARC) do not cover.

--- middle

# Introduction

## Problem Statement

{{RFC6409}} defines the protocol by which a Mail User Agent (MUA)
submits messages to a Mail Submission Agent (MSA) for delivery.
Section 4.3 of {{RFC6409}} requires the MSA to enforce
authentication (typically SMTP AUTH per {{RFC4954}}), but this
authentication establishes only that the session was initiated by a
credentialed user. It does not verify that the person composing and
sending a given message within that session is the authorized account
holder.

Modern MUAs (webmail interfaces, desktop email clients, mobile apps)
manage SMTP connections, authentication, and credential storage
transparently. Session credentials — OAuth tokens, stored passwords,
OS keychain entries — are available to the MUA without per-action
user interaction. An unauthorized party with physical access to an
unlocked device can compose and send a message through the MUA's
graphical interface; the MUA will open a fresh SMTP connection,
authenticate using the stored credentials, and submit the message
on the attacker's behalf — all without any identity challenge.

This threat operates at the MUA layer, not the SMTP connection
layer. Connection-level mitigations — such as shortening SMTP
connection lifetimes or requiring re-authentication per connection —
do not address this gap, because the MUA will establish a new
authenticated connection transparently each time the user (or an
unauthorized party) clicks Send.

The gap is between "the MUA has credentials to authenticate" and
"the person pressing Send is the person those credentials belong
to."

Existing email authentication mechanisms (SPF {{RFC7208}}, DKIM
{{RFC6376}}, DMARC {{RFC7489}}) operate at the domain level and do
not address individual sender identity at the point of submission.

## Scope

This document addresses sender identity verification at the
submission layer — the interaction between MUA and MSA as defined in
{{RFC6409}}. It does not modify SMTP relay behavior ({{RFC5321}}) or
domain-level authentication mechanisms (SPF, DKIM, DMARC), which
remain complementary.

## Relationship to STIR/SHAKEN

The STIR framework ({{RFC8224}}, {{RFC8225}}, {{RFC8226}}) solved an
analogous problem for voice telephony: verifying that the party
initiating a call is authorized to use the claimed calling number.
SENDAUTH applies the same conceptual approach — per-action identity
attestation within a decentralized communication system — to email
submission. The STIR framework was subsequently mandated by the
TRACED Act {{TRACED-Act}}, establishing the precedent that
standards-based identity verification can be imposed by legislation
on a decentralized communication ecosystem. A similar standard-then-
mandate approach succeeded for domain-level email authentication
when DHS Binding Operational Directive 18-01 {{BOD-18-01}} required
DMARC deployment across federal domains.

## Conventions and Definitions

{::boilerplate bcp14-tagged}

The following terms are used in this document:

MUA (Mail User Agent):
: The email client software through which a human composes and sends
  messages.

MSA (Mail Submission Agent):
: The server that accepts messages from the MUA for delivery, as
  defined in {{RFC6409}}.

Sender Presence Attestation (SPA):
: A cryptographic proof, generated in real time, that the authorized
  account holder was physically present and actively consented to the
  send action.

Human Submission Context:
: A submission session initiated by a human user through an
  interactive MUA.

Programmatic Submission Context:
: A submission session initiated by automated software (transactional
  email systems, mailing list servers, CI/CD pipelines, etc.) using
  machine credentials.

# The SENDAUTH Extension

## SMTP Service Extension

The SENDAUTH extension is registered as an SMTP service extension
with the following properties:

EHLO keyword:
: SENDAUTH

Parameters:
: Supported attestation mechanisms, presented as a space-separated
  list. Initial values are FIDO2, PIN, and MACHINEAUTH.

Verb:
: No new SMTP verbs are defined. SENDAUTH modifies the behavior of
  the existing MAIL FROM command.

An MSA that supports SENDAUTH MUST advertise it in its EHLO response.
An MSA that advertises SENDAUTH MUST enforce sender identity
verification for all Human Submission Context sessions.

## Protocol Flow — Human Submission

The following illustrates the SMTP session flow when SENDAUTH is
advertised and the session is a Human Submission Context:

~~~ smtp
C: EHLO client.example.com
S: 250-submission.example.com Hello client.example.com
S: 250-AUTH PLAIN LOGIN
S: 250-SENDAUTH FIDO2 PIN MACHINEAUTH
S: 250 OK

C: AUTH PLAIN dXNlckBleGFtcGxlLmNvbQBwYXNzd29yZA==
S: 235 2.7.0 Authentication successful

C: MAIL FROM:<user@example.com>
S: 334 SENDAUTH challenge [base64-encoded-challenge-data]

C: SENDAUTH [mechanism] [base64-encoded-signed-attestation]
S: 250 2.0.0 Sender identity verified

C: RCPT TO:<recipient@example.org>
S: 250 2.1.5 OK

C: DATA
S: 354 Start mail input
C: From: User <user@example.com>
C: To: Recipient <recipient@example.org>
C: Subject: Example message
C: Date: Tue, 01 Sep 2026 10:00:00 -0400
C:
C: Message body.
C: .
S: 250 2.0.0 OK
~~~

Upon receiving the MAIL FROM command, the MSA issues a SENDAUTH
challenge instead of immediately accepting the sender address. The
challenge contains a server-generated nonce and the list of acceptable
attestation mechanisms. The client responds with a signed Sender
Presence Attestation (SPA) using one of the advertised mechanisms.

If the attestation is valid, the MSA responds with 250 and proceeds
normally. If the attestation is invalid or absent, the MSA MUST
reject the MAIL FROM command with a 530 reply code:

~~~ smtp
S: 530 5.7.1 Sender identity verification required
~~~

## Protocol Flow — Level 2 Message Authorization

When the MSA advertises Level 2 support and the MUA supports it,
the protocol includes a second attestation phase after the message
has been transmitted. This binds the user's approval to the specific
message content and recipients:

~~~ smtp
C: EHLO client.example.com
S: 250-submission.example.com Hello client.example.com
S: 250-AUTH PLAIN LOGIN
S: 250-SENDAUTH FIDO2 PIN MACHINEAUTH LEVEL2
S: 250 OK

C: AUTH PLAIN dXNlckBleGFtcGxlLmNvbQBwYXNzd29yZA==
S: 235 2.7.0 Authentication successful

C: MAIL FROM:<user@example.com>
S: 334 SENDAUTH challenge [base64-encoded-challenge-data]

C: SENDAUTH FIDO2 [base64-encoded-signed-attestation]
S: 250 2.0.0 Sender verified (Level 1)

C: RCPT TO:<recipient@example.org>
S: 250 2.1.5 OK

C: DATA
S: 354 Start mail input
C: From: User <user@example.com>
C: To: Recipient <recipient@example.org>
C: Subject: Example message
C: Date: Tue, 01 Sep 2026 10:00:00 -0400
C:
C: Message body.
C: .
S: 334 SENDAUTH-AUTHORIZE [base64-encoded-digest-challenge]

C: SENDAUTH-AUTHORIZE [base64-encoded-signed-authorization]
S: 250 2.0.0 Message authorized and accepted
~~~

The MSA computes a canonical digest over the authorization identity,
the complete envelope-recipient set, and the message content. The
MUA independently computes the same digest, presents it to the user
for approval via a second authenticator challenge, and transmits the
signed authorization. The MSA compares the digest in the
authorization against its own computation; if they match and the
signature is valid, the message is accepted. If they do not match,
the MSA MUST reject the message:

~~~ smtp
S: 550 5.7.1 Message authorization failed
~~~

## Protocol Flow — Programmatic Submission

When the MUA authenticates using machine credentials (API key, OAuth
client credentials with a machine scope designation, or a dedicated
service account), the MSA MUST classify the session as a Programmatic
Submission Context and MUST NOT issue a SENDAUTH challenge.

~~~ smtp
C: EHLO automator.example.com
S: 250-submission.example.com Hello automator.example.com
S: 250-AUTH PLAIN LOGIN
S: 250-SENDAUTH FIDO2 PIN MACHINEAUTH
S: 250 OK

C: AUTH PLAIN [machine-credentials]
S: 235 2.7.0 Authentication successful (machine context)

C: MAIL FROM:<noreply@example.com>
S: 250 2.0.0 OK
~~~

The MSA determines the submission context based on the credential
type used during SMTP AUTH. Machine credentials are distinguished
from human credentials through one of the following mechanisms:

- A dedicated authentication mechanism identifier (e.g., AUTH
  MACHINEAUTH)
- OAuth scope metadata indicating a machine client
- Administrative designation of specific accounts as service accounts

The MSA records the submission context (human-verified or
machine-authenticated) in the message's authentication results.

## Sender Presence Attestation Format {#spa-format}

The Sender Presence Attestation (SPA) is a signed assertion based on
the WebAuthn AuthenticatorAssertionResponse structure
{{W3C-WebAuthn}}, adapted for the SMTP submission context.

SENDAUTH defines two levels of attestation, reflecting the
distinction between recent user verification and message
authorization:

### Level 1: Recent User Verification {#level-1}

The Level 1 SPA confirms that the credential holder was present
at send time. It binds the following elements:

- The sender's registered credential (public key) associated with the
  email account
- A server-generated challenge (nonce) provided in the SENDAUTH
  challenge
- A timestamp indicating when the verification occurred
- An action indicator confirming real-time user presence

Level 1 verification occurs at the MAIL FROM phase. It proves
that a WebAuthn ceremony occurred but does not bind the
attestation to the specific message content or recipients.

### Level 2: Message Authorization {#level-2}

The Level 2 SPA confirms that the credential holder approved the
specific message being submitted. In addition to the Level 1
elements, it binds:

- The authorization identity of the sender (per {{RFC4954}},
  Section 5)
- The complete SMTP envelope-recipient set (all RCPT TO addresses)
- A canonical digest of the message content as submitted

Level 2 verification requires a two-phase protocol flow. The
initial WebAuthn ceremony occurs at MAIL FROM (Level 1). After
the client has issued all RCPT TO commands and transmitted the
message via DATA, the MUA computes a digest over the authorization
identity, the envelope-recipient set, and the message content,
and presents this digest to the user for approval via a second
authenticator challenge. The resulting attestation is transmitted
to the MSA, which compares the bound values against the completed
transaction before final acceptance.

Implementations MUST support Level 1. Support for Level 2 is
RECOMMENDED. The MSA advertises supported levels in its EHLO
response (e.g., SENDAUTH FIDO2 PIN MACHINEAUTH LEVEL2).

### Attestation Encoding

The attestation is encoded as a CBOR {{?RFC8949}} structure and
transmitted base64-encoded within the SENDAUTH response.

The full specification of the attestation format, including the CBOR
schema and signature algorithm requirements, is to be developed in
coordination with the FIDO Alliance {{FIDO2}}. The attestation MUST
NOT convey biometric data; it conveys only a signed proof that a
biometric or knowledge-factor check succeeded on the client device,
consistent with the WebAuthn privacy model.

## Fallback Authenticators

An MSA that advertises SENDAUTH MUST advertise at least two
attestation mechanisms. Implementations MUST support:

FIDO2:
: Biometric or hardware security key verification via the WebAuthn
  API. This is the RECOMMENDED mechanism.

PIN:
: A knowledge-factor fallback for devices or environments that lack
  biometric hardware. The PIN is verified locally on the client
  device (not transmitted to the server); the attestation confirms
  that PIN verification succeeded.

Additional attestation mechanisms MAY be registered through the IANA
"SENDAUTH Attestation Mechanisms" registry defined in {{iana}}.

## Credential Registration

Before SENDAUTH can be used, the account holder MUST register at
least one authenticator credential with the MSA. The registration
process MUST be at least as strong as the account's primary
authentication:

- Registration MAY occur during initial account setup.
- Registration MAY be initiated through a re-authentication ceremony
  (the user re-enters their password or completes a multi-factor
  challenge before registering a new authenticator).
- The MSA MUST allow multiple credentials per account (e.g., a
  biometric credential on a phone and a hardware key as backup).
- The MSA MUST provide a mechanism for credential revocation.

# Sender-Verification-Result Header Field {#svr-header}

A new message header field, Sender-Verification-Result, is defined
for messages that have undergone SENDAUTH processing. The MSA MUST
add this header to all messages it accepts for delivery.

The field carries one of the following values:

verified:
: Recent user verification succeeded (Level 1). The credential
  holder was present at send time, but the attestation is not bound
  to the specific message content or recipients.

authorized:
: Message authorization succeeded (Level 2). The credential holder
  approved this specific message, including the authorization
  identity, envelope-recipient set, and message content.

machine:
: The message was submitted in a Programmatic Submission Context
  using authenticated machine credentials. No per-send biometric or
  knowledge-factor challenge was performed.

none:
: The MSA does not support SENDAUTH, or the message was received via
  relay (not submission). This value MUST NOT be added by an MSA that
  advertises SENDAUTH; it is intended for messages transiting
  infrastructure that predates SENDAUTH deployment.

The MSA MUST sign the Sender-Verification-Result header as part of
the domain's DKIM signature ({{RFC6376}}). Receiving MTAs SHOULD
disregard this header if DKIM verification fails.

Receiving MUAs MAY use the Sender-Verification-Result header to
display a trust indicator to the recipient. The indicator SHOULD
distinguish between "verified" (the credential holder was present)
and "authorized" (the credential holder approved this specific
message). Implementations SHOULD NOT display an "authorized" or
equivalent badge for messages that achieved only Level 1
verification, as this would overstate what the ceremony proves.

# Security Considerations

## Replay Attacks

The server-generated challenge (nonce) included in the SENDAUTH
challenge MUST be single-use and time-bounded. The MSA MUST reject
any attestation that references an expired or previously used nonce.
The RECOMMENDED maximum nonce lifetime is 60 seconds.

## Downgrade Resistance

An MSA that advertises SENDAUTH MUST NOT accept human-context
submissions without a valid attestation. The extension does not
define a "soft fail" mode for human submissions. A client that does
not support SENDAUTH cannot submit messages through an MSA that
requires it for human contexts.

During the transition period, MSA operators MAY choose whether to
advertise SENDAUTH. Once advertised, enforcement is mandatory.

## Header Integrity

The Sender-Verification-Result header is protected by DKIM signing.
Receiving MTAs SHOULD disregard this header on messages where DKIM
verification fails, to prevent an attacker from injecting a
fraudulent "pass" value.

Additionally, the MSA SHOULD remove any pre-existing
Sender-Verification-Result header on incoming submissions before
adding its own, to prevent a submitting client from injecting a
false value.

In message forwarding and mailing list scenarios, the Authenticated
Received Chain (ARC) protocol {{RFC8617}} may be used to preserve
the original Sender-Verification-Result across intermediaries that
re-sign the message.

## Privacy Considerations

The Sender Presence Attestation does not convey biometric data. It
conveys a signed proof that a biometric or knowledge-factor check
succeeded on the client device. No biometric template, fingerprint
data, facial geometry, or PIN value is transmitted to the MSA or
included in the message. This is consistent with the WebAuthn privacy
model ({{W3C-WebAuthn}}, Section 14).

The Sender-Verification-Result header discloses whether a message
was sent by a human or a machine. This metadata is visible to all
parties who handle the message in transit and to the recipient.
Operators should consider whether this disclosure is appropriate for
their use case.

## Relationship to Existing Authentication

SENDAUTH is additive. It does not replace SMTP AUTH ({{RFC4954}}),
SPF ({{RFC7208}}), DKIM ({{RFC6376}}), or DMARC ({{RFC7489}}).
These mechanisms continue to operate independently and remain
necessary for session authentication and domain-level verification
respectively.

The layered authentication model is:

| Layer | Mechanism | What It Verifies |
|:------|:----------|:-----------------|
| Session | SMTP AUTH (RFC 4954) | Credentials to open a session |
| User Presence | SENDAUTH Level 1 (this document) | Credential holder was present at send time |
| Message Approval | SENDAUTH Level 2 (this document) | Credential holder approved this specific message |
| Domain | SPF / DKIM / DMARC | Authorized sending infrastructure |

# IANA Considerations {#iana}

This document requests the following IANA registrations:

## SMTP Service Extension Registration

Registration of the SENDAUTH keyword in the "SMTP Service Extensions"
registry:

| Field | Value |
|:------|:------|
| Keywords | SENDAUTH |
| Description | Per-send sender identity verification |
| Reference | [this document] |

## SENDAUTH Attestation Mechanisms Registry

IANA is requested to create a new registry titled "SENDAUTH
Attestation Mechanisms" with the following initial entries:

| Mechanism | Description | Reference |
|:----------|:------------|:----------|
| FIDO2 | Biometric or hardware security key via WebAuthn | [this document] |
| PIN | Local knowledge-factor verification | [this document] |
| MACHINEAUTH | Machine credential (programmatic context) | [this document] |

New entries in this registry require Specification Required
({{?RFC8126}}, Section 4.6).

## Header Field Registration

Registration of the Sender-Verification-Result header field in the
"Permanent Message Header Field Names" registry:

| Field | Value |
|:------|:------|
| Header Field Name | Sender-Verification-Result |
| Protocol | mail |
| Status | standard |
| Reference | [this document] |

--- back

# Acknowledgments
{:numbered="false"}

The author thanks the participants of the IETF Dispatch, DMARC, and
emailcore working groups for their review and feedback.

The STIR/SHAKEN framework and the TRACED Act provided essential
precedent for the approach taken in this document.

The FIDO Alliance's work on WebAuthn and FIDO2 provided the
authenticator framework on which the Sender Presence Attestation
is based.
