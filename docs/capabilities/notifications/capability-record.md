# Notifications — Capability Record

**Capability Name:** `notifications`  
**Classification:** Platform (established governing catalogue classification).  
**Conceptual status:** Proposed independent review, 19 November 2026; **not owner-approved, implementation-verified or operationally accepted**.  
**Availability / installation / configuration / operation / enablement / authorisation:** Not independently verified; these are distinct statuses, not synonyms.  
**Version:** Conceptual contract only; no public contract version asserted.  
**Evidence:** [Review protocol](../../review-protocol.md); governing `architecture-rules/master` at `b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint opening `master` at `6dac83a03da8704f7945ee1bc894f2248300445a`; [opening baseline](../../../reviews/notifications-review-baseline.md). Governing Capability Standard and ADR-0012, ADR-0017, ADR-0018 are accepted. `nuxt-layers/notifications` exists; root `CONTRACT.md` was not retrievable as of review. Accordingly no callable implementation API or operating status is asserted.

## Purpose, justification and ownership

Notifications is the reusable, tenant-scoped **human-attention and notification orchestration** owner: accept a legitimate notice intent from an authorised origin, decide permitted audience/channel/timing under policy and preferences, produce an approved minimal rendering, coordinate channel delivery and retries, and expose an independently comprehensible notification lifecycle. Its value is channel-independent, recoverable notice delivery across many domains, not originating their business decisions. Operates in headless mode without a required GUI; optional inbox and operator consoles consume its public contract.

**Authoritative owned records:** accepted/rejected notice intents and immutable deduplication identity; notice purpose/class, source reference/revision and bounded payload snapshot; target recipient references resolved for a particular context; routing selection and policy/application versions; per-notice/per-channel attempts, retries, suppression, expiry and provider qualification; in-app inbox entry with read/dismiss state *when the channel is configured*; template registrations/notification rendering revisions where not owned as published content elsewhere; notification-specific administrative configuration and delivery evidence. Protect historical provenance and tenant separation. The source domain retains its own event and durable outbox, its records, legal effectiveness and correctness. Notifications owns its own committed lifecycle events/outbox; Message Queue only transports.

**Does not own:** Identity tenants/memberships, Profile contact details, Authentication assurance, Authorisation grants, Privacy consent, Configuration's approved settings, Legal Compliance interpretation, Billing/Booking/Credentials/Workflow decisions, Scheduler task execution, Mailer's email transport or channel-provider credentials, Message Queue's transport receipts, Audit's independent audit record, Reporting derivatives, user-facing published domain content, nor evidence that a human actually read/understood a third-party-channel message. A user-supplied destination address is not a recipient-authorisation decision. Sending is not statutory service without separately evidenced applicable legal rules.

## Native services and lifecycle

1. Register validated notification purpose, eligible originating source, bounded template/content version, allowed channels, data schema, classification and mandatory-versus-optional handling. Do not allow arbitrary untrusted HTML, recipient enumeration or unauthorised domain claims.
2. Receive a scoped intent with stable source event/reference/revision, authorised audience reference, purpose, safe locale/template data, time/expiry, deduplication key and correlation. Verify source legitimacy, tenant, current rights, policy and consent/allowed preference before a sensitive disclosure or delivery attempt. Revalidate at deferred send.
3. Resolve recipient eligibility via relevant public IAM/Profile/Privacy contracts without retaining unnecessary personal contact records. Derive channel choice, quiet hours and alternate paths by governing rules; mandatory notices may override *optional preferences* only where lawful and explicitly approved, never override privacy/security floors.
4. Record accepted/suppressed/rejected/held with reason and version; create eligible channel tasks; render escaped, localised, accessible messages with safe links and no secrets or excess personal information. Acknowledged acceptance means durable custody only, not successful dispatch.
5. Coordinate an attempt through a public Mailer/channel/provider port. Record qualified provider accepted, handed-off, rejected, bounced, failed, rate-limited or indeterminate evidence. Retry with bounded backoff and idempotency where supported; reconcile ambiguous provider outcomes to avoid avoidable duplicates. **No exactly-once or guaranteed-human-receipt promise.**
6. Expose status such as `received → validated → accepted | rejected | suppressed | held → scheduled | ready → attempting → provider-accepted | delivered-evidence | failed | delivery-unknown | expired | cancelled`. Actual status is multi-dimensional by channel; read/dismiss is separate from transport receipt; partial success may coexist with a failed alternate channel. Cancellation cannot retract a message already sent.
7. Preserve bounded history, access-controlled audit evidence and retention/erasure/hold decisions. Replays reuse stable identity; corrections require a new source revision/replacement notice, never silent mutation of a delivered record. Unknown required dependencies hold the notice rather than pretending delivery.
8. **Independent native mode:** support an in-application inbox with persisted pending/read state and no external mail/SMS/push provider, where the application has the required IAM, persistence and delivery context. External delivery is conditional on configured providers; the inbox alone must never be described as an external legal notice.

## Idealised public inbound contract

*These are conceptual authority-level interfaces, not names of implemented functions or a universal request object.*

| Input / source | Supplied facts or instruction; owner | Validation, absence and failure |
|---|---|---|
| Notice intent from Booking/Billing/Identity/Configuration/Credentials/other authorised source (required per notice) | Source event ID, tenant, purpose, recipient/audience reference, source resource+revision, approved data class and expiry; originating domain owns meaning | Confirm registered source/purpose, authorised scope, revision and dedup key; reject untrusted domain assertions, invalid or unknown recipient and cross-tenant intents; staleness => hold/re-resolve |
| Trusted caller and scoped access decision (required for protected commands/reads) | Authentication/IAM caller assurance, Authorisation decision on exact resource; source domain remains responsible for emission permission | Server-side fail closed; an event alone is not permission; privileged resend/export and recipient changes require fresh authorisation |
| Identity and Profile recipient resolution (conditional per delivery) | Current eligible identity/group/role and verified contact destination with permitted disclosure; never Notifications-owned directory | Missing/deactivated/revoked/ineligible recipient suppresses or holds; no fallback to stale personal addresses or tenant parent |
| Privacy and Legal Compliance constraints (conditional, mandatory if applicable) | Consent, opt-out, purpose/retention limits, holds, jurisdiction/effective legal requirements | Uncertain lawful basis or statutory-channel requirement => hold/escalate; preference override must be lawful, not implicit |
| Configuration and user preference context (conditional) | Approved routing rules, channel availability, locale/quiet hours, user channel choice; owners retain source values | Stale/contradictory values => safe hold or allowed default only for explicitly optional choice; cannot disable mandatory floors |
| Template/content registration (required for rendering) | Approved versioned safe content schema/locale/purpose; Publisher/Localisation where applicable own source copy/translations | Reject unsafe placeholders/links, unsupported languages or unapproved claims; fallback only with approved accessible copy |
| Clock and Scheduler (time required; Scheduler conditional on delayed/retry) | Trusted instant, time-zone/expiry semantics and executed task triggers | No local-clock guess for critical deadlines; missed invocation remains pending and observable; replay safe |
| Mailer/channel adapter and Integrations connection (optional per channel) | Provider readiness, configured host secrets, send operation, qualified status callbacks/evidence | Unconfigured channel => unavailable, not sent; provider timeout => delivery-unknown; callback authenticated and correlated |
| Operator commands and authorised recipient actions (conditional) | Cancel pending, permitted resend, mark in-app read/dismiss, resolve hold, view/export scoped history | Expected revision/idempotency, policy, tenant checks; disallow rewriting delivery evidence or cancelling already transmitted message |

## Idealised public outbound contract

| Output / consumer | Authoritative meaning and lifecycle | Provenance, privacy and uncertainty |
|---|---|---|
| Accept/suppress/reject/hold result to originating domain/host | Durable notice custody or explicit refusal, stable notice reference and reason; **not** delivery, consent or domain completion | Include tenant, source event/revision, decision/version and recorded instant; never leak another tenant's recipient |
| Scoped notification status query to source, recipient, authorised operator | Current notification and per-channel lifecycle, next eligible action, attempted/scheduled timing | Bounded freshness and recorded evidence; provider acceptance ≠ end-user delivery; unknown distinct from failed |
| Recipient inbox/read query to authorised recipient and host UI | In-app message visible/acknowledged/dismissed according to Notifications' own state | Viewing an inbox item ≠ receiving third-party message or legally effective acknowledgment; disclosure individually authorised |
| Delivery attempt/qualified provider outcome to originating domain, Audit and operations | Which channel attempted, provider result and evidence reference; does not authorise originating domain transition | Minimise addresses and provider IDs; state time, source, evidence quality, possible duplicates and partial status |
| Committed Notifications lifecycle events via owned durable outbox to Message Queue/subscribers | Accepted, held, suppressed, attempted, status-changed, exhausted, expired, inbox-read facts after local commit | Stable event ID, tenant, notice ID/revision, minimal status/provenance; at-least-once downstream transport, dedup required |
| Scoped operational metrics/exports to Reporting/Audit/authorised operators | Count, backlog, expiry, failure/uncertainty and policy history; not billing/legal business data | Aggregation with tenant isolation; redact message body, recipients, secrets and high-cardinality personal identifiers |
| Provider/channel health and configuration read to host/operator | Configured, unavailable, degraded and last-verified evidence, not an invented healthy status | No secrets; differentiate configured from operational and provider hand-off from actual delivery |

### Command, query and event invariants

**Commands:** submit intent, register/revise notification definition, resolve permitted recipient route, cancel pending, retry/reconcile unknown, scoped recipient read/dismiss and authorised export. Each validates tenant, source/policy version, permission and immutable origin; returns stable previous result for idempotent repeats. **Queries:** by notice ID/source event, authorised recipient inbox, operator queue/channel health and scoped metrics; disclose only current permitted scope with freshness/completeness markers. **Events:** only after Notifications-owned durable commit; never assert that originator's business action occurred simply because a notification was queued. Consumers tolerate duplicate, delayed and out-of-order deliveries and reconcile via authorised queries.

Context is deliberately operation-specific: tenant and optional group, caller/assurance, originating capability/resource/revision, intended recipient reference, purpose, classification, correlation/dedup ID, configuration/consent/policy versions, Clock instant, channel/provider evidence and result uncertainty. No universal object or direct package import is mandated. Sensitive payloads and links must be reauthorised, short-lived and non-enumerating; unsubscribe and suppression may be mandatory depending on purpose/law.

## Cross-capability contracts and dependency direction

| Peer | Input Notifications consumes / output it supplies | Ownership and absence |
|---|---|---|
| Identity, Authentication, Authorisation, Profile | Tenant/eligible target, session assurance, decision, contact/locale → scoped notice status | IAM/Profile own source; protection required; no cross-tenant parent access |
| Privacy, Legal Compliance | Purpose/consent, retention, mandatory notice applicability → delivery evidence to lawful owner | Qualified constraints required where relevant; unknown legal requirement held |
| Configuration, Clock | Approved routing preferences/policy, time semantics → notice of effective policy change, status | Values/time owned by peers; do not overwrite setting or time authority |
| Mailer and optional SMS/push/Integrations | Validated channel send request → qualified hand-off/error status | Mailer/adapter owns transport; unavailable external channel explicit; no circular import |
| Message Queue | Own committed outbox messages → transport acknowledgement/replay data | Transport owner does not own notice intent or domain event; queue failure leaves committed notice pending |
| Scheduler, Workflow | Due-work invocation and separately authorised escalation/approval → pending/failed notice result | Scheduler executes; Workflow decides its own process, never driven by presumed receipt |
| Booking, Billing, Invoice, Course, Assessment, Credentials, Comments Engine | Minimised committed-domain notice intents → status/attempt evidence | Each source owns booking, charge, invoice, award, publication, moderation or appeal decisions |
| Audit, Logging, Reporting, Observability | Independent audit append and sanitised diagnostic/metric context → authorised evidence/read models | Notifications history is not the Audit log; diagnostics are not independent audit proof |
| Localisation, Publisher, Theme Manager/UI | Approved locale/message copy and semantic presentation → rendered, accessible message or inbox feed | Translation/content/theme owned by peers; host provides routes and menu |
| Verification, Moderation, Content Security | Conditional verified contact/recipient and approved safe-content result → notice of independently committed outcome | No accidental disclosure of rejected/hidden sensitive evidence |

Conceptual cooperation is via published ports and host composition; required, optional and conditional status is **per operation**, not an invented hard compile-time dependency. No cyclic direct imports or private schema access. Important parallel drafts: [Mailer #90](https://github.com/nuxt-layers/architecture-blueprint-review/pull/90), [Message Queue #94](https://github.com/nuxt-layers/architecture-blueprint-review/pull/94); proposed reciprocal changes must be reconciled before adoption.

## Configuration, provider neutrality and safeguards

Host chooses supported channels and injects provider secrets only through host secret management. Notifications owns validation and channel-policy interpretation, Configuration owns approved scoped values, Profile owns personal contact/preferences where assigned, Privacy owns consent constraints and Legal Compliance supplies applicable legal-duty evidence. Support native inbox without external providers; adding/removing or switching providers does not rewrite historic evidence or resend without a deliberate policy. External callback authenticity, correlation, spoofing, replay, template injection, phishing links, recipient enumeration, message amplification, cross-tenant data leakage, BCC-like disclosure, contact reassignment, provider account suspension, spam abuse and dead-letter recovery require threat controls. Rate limits/circuit breaking, safe rendering, request-time access decisions and high-risk step-up are conceptual obligations. Follow OWASP ASVS 5 Level 2 (L3 for critical security actions), WCAG 2.2 AA, UK GDPR/Privacy applicability and jurisdiction-specific notice rules without claiming legal compliance. Retention and storage inventory require future implementation `STORAGE-REGISTER.md` reconciliation.

## GUI and host integration (optional presentation, headless core mandatory)

Application sidebar may expose **Notifications** to authorised recipients (inbox, unread count, notification detail, mark read/dismiss, channel choices and privacy controls) and privileged operators (dashboard, pending/held/failed/unknown queue, per-channel evidence, template/route configuration, safe retry/reconciliation, metrics and redacted audit trace). Domain owners use contextual “notification history” panels on their own record views through public scoped queries. The host owns navigation, branding and route selection; Notifications owns notice data; optional capability screens follow ADR-0009/0012 with `presentation: false` and no duplication of host business state. Provide keyboard/screen-reader/contrast WCAG 2.2 AA, translated messages and status, safe non-colour-only failure cues, accessible live updates, responsive layout and Theme Manager semantic tokens. Never expose contact lists, secret material or another tenant's messages in operator menus.

## Conceptual acceptance scenarios

| Input → expected behaviour | Public output / authoritative owner |
|---|---|
| Valid Booking cancellation event with verified recipient → persist idempotently, render allowed content, route inbox/email as configured | Accepted notice ID; later qualified channel status. Booking owns cancellation |
| Duplicate/out-of-order Billing charge notice → same original result, source revision check, no unbounded repeat send | Prior notice/status or held stale revision; Billing owns charge |
| Authorisation revokes a user's tenant access before deferred send → revalidate and suppress disclosure | Suppressed/rejected with minimised reason; IAM owns revocation |
| Parent tenant admin requests child inbox → no implicit right | Denied without disclosure; Authorisation/Identity own access |
| Optional channel consent withdrawn → no fresh optional channel send | Suppressed/alternate permitted channel status; Privacy owns consent |
| Mandatory jurisdiction-specific notice rule unknown → hold and escalate; no false compliance or override | Held/unknown status; Legal Compliance supplies applicability |
| Mailer timeout after hand-off → preserve unknown, reconcile before retry, allow safe duplicate tolerance | Delivery-unknown then evidence-backed outcome; Mailer owns hand-off |
| Scheduler invocation repeats and queue replays event → task/idempotency prevents duplicate owned transition | Same committed notification revision and outbox fact; Scheduler/Message Queue only execute/transport |
| Provider says accepted but no receipt → don't claim human read or domain success | Provider-accepted status only; Notifications owns qualified evidence |
| Template contains unsafe URL or secret placeholder → reject definition/send | Stable invalid-template error; Notifications enforces rendering security |
| Approved in-app-only host with no email provider → notice visible and read state maintained | Inbox status, external channel unavailable; Notifications owns inbox |
| Already sent message cancellation request → reject impossible retraction, optionally initiate new corrective notice | Already-transmitted result; original domain owns correction decision |
| Retention expiry under legal hold → retain minimal evidence per authorised policy, no arbitrary erase | Scoped retention/held status; Privacy/Legal Compliance own constraints |

## Review decisions, uncertainties and implementation alignment

- **Established:** Platform classification, bounded public contracts, server authorisation, capability-owned durable outboxes, provider-neutral composition, tenant isolation, policy authority, WCAG/i18n and privacy baseline from accepted governing rules.
- **Proposed NOT-01:** Notifications owns durable notice intent, routing, in-app inbox and qualified dispatch status, not source domain state or Mailer transport.
- **Proposed NOT-02:** Native inbox is sufficient independent channel for applications with no external send provider; explicit provider-unavailable outcome.
- **Proposed NOT-03:** Preserve accepted-vs-sent-vs-provider-accepted-vs-human-read distinction; retry/replay idempotently without exactly-once promise.
- **Proposed NOT-04:** Mandatory notices follow lawfully qualified, versioned policy; optional user channel/quiet-hour preferences cannot silently suppress legal duty.
- **Proposed NOT-05:** Recipient resolution and revocation checked at send and sensitive view, not permanently copied from original intent.
- **Proposed NOT-06:** Optional public user inbox, operator queue/dashboard, and host-composed contextual status, without mandatory UI dependency.
- **Open NOT-07:** Whether Notifications owns durable per-user preference records beyond notification-specific choices or Profile/Configuration should own all canonical preferences. **Recommendation:** keep canonical source with the designated preference owner; Notifications owns route-decision snapshots only.
- **Open NOT-08:** Which channels beyond in-app and Mailer email are first-class supported, and what verified provider evidence warrants “delivered”. **Recommendation:** version channel-specific evidence levels; do not hard-wire SMS/push.
- **Open NOT-09:** Contractual/statutory proof-of-service and archival responsibility for specific jurisdictions and document classes. **Recommendation:** defer applicability to Legal Compliance/source owner; Notifications records qualified dispatch evidence only.
- **Open NOT-10:** Definition and preservation of re-routing/quiet-hour exceptions during emergency/security incidents. **Recommendation:** enumerate approved purpose classes with documented risk and independent approval.
- **Implementation alignment:** Retrieve/author root `CONTRACT.md`, stable public interfaces/errors/permissions, independent consumer/minimal host and 50-line budget, store/outbox/retention inventory, adapter mappings, abuse/security verification and CI evidence in **separate future implementation changes**. No operational functionality established by this blueprint.
- **Sign-off:** Not approved; conceptual proposals and outstanding owner decisions await review. No tests/builds run; merge requires explicit approval.

---
## Preserved earlier reciprocal material

The following existing dated notes are retained verbatim as historical/provisional evidence, not silently promoted to agreed Notifications interfaces.

# **Capability Record**

## Capability Name:

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

## Purpose

## Classification

## Dependencies

## Optional integrations

## Version

## Availability

## Capabilities offered

## Configuration

## Cross-capability note — Authorisation governance notifications (15 November 2026)

**Status:** Proposed relationship, not a published Notifications consumer. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) can emit selected role/grant changes, approvals, overdue access reviews and security-relevant revocations with safe recipient/context references. IAM/Identity determines current eligible persons/approvers and Profile or an approved contact provider owns addresses. Notifications owns dispatch, delivery/retry and template rendering; sending is not approval, evidence acceptance, revocation completion or confirmation of human receipt. Notifications' conceptual review remains incomplete.

## Cross-capability note — Billing event notification and delivery status (15 November 2026)

**Proposed reciprocal interface, not an implemented Notifications contract.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) may supply deduplicable, versioned notice intents with source event, permitted recipient reference, locale and purpose (charge finalised, dispute outcome, exception). Notifications owns dispatch coordination and may return queued/sent/failed/delivery-unknown result; Mailer or another provider owns channel transport. Billing does not assert that an invoice was legally issued, payment received, notice delivered or viewed merely because an intent was sent. Invoice owns issued-document notice content. Recipients/preferences, mandatory statutory notice rules, sensitive fields, tenant boundaries and reauthorisation must be enforced. Notification outages do not roll back a committed charge but mandatory notices must remain visible/pending under policy.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking conceptual completeness note (15 November 2026; agreed review direction):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) sends minimised and tenant-scoped confirmation, change, cancellation, reminder and exception notification intent with booking event/version, authorised recipient reference, locale and delivery purpose. Notifications owns routing, templates and message-delivery lifecycle, returning accepted/pending/failed results without modifying booking state. Optional delivery failure does not cancel a confirmed reservation; contact verification required before confirmation stays an explicit Booking-side dependency. No confirmed Notifications implementation interface is inferred.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Booking supplies tenant-scoped confirmation, change, cancellation and reminder intent with booking event/version, recipient reference and purpose; Notifications owns delivery orchestration/status and does not alter Booking state. Optional delivery failure does not reverse a confirmed booking. Required verification is a separately checked condition. No currently implemented integration contract is implied.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Supply scoped notices for invitations, proposed/approved ownership transfer, disputed recovery and appeals, policy changes, provisioning/payment problems, renewals, quota and seat warnings. Never treat successful delivery as authority to change governance or proof payment settled; respect privacy/disclosure and delivery uncertainty.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine may produce author/reply/mention, moderation decision and appeal disposition notice intents containing only authorised recipient references, bounded status/message keys and minimal comment links. Notifications owns channel choice, delivery and provider status; delivery does not prove comment publication, enforcement or receipt by a person. Suppress disclosure of hidden content, reporter identity and child-sensitive evidence.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Configuration supplies minimally scoped change-requested, decided and activated facts; Notifications owns authorised recipient delivery, templates and channel execution. Notification success never proves approval or activation. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course emits safe publication/review/withdrawal facts; Notifications owns delivery and retry. Dispatch cannot approve publication, grant enrolment or prove a learner received the message. This note does not complete the separate notifications review.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-09/11 agreed:** Notifications dispatches approved course, session, enrolment, assessment, learner migration or credential status alerts using minimised domain-source facts. Sending does not confer an award, constitute learner admission or demonstrate receipt. This note does not complete the separate notifications review.


## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)).** Notifications delivers opted/required issuance, expiry, revoked, replaced and status-action notices from committed Credentials events with authorised recipient context and minimised details. Delivery failures retry independently; neither successful email nor failed delivery determines whether credential issuance committed.
