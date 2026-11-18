# Historical Event Bus classification review — 18 November 2026

**Disposition: owner-approved EB-05 (18 November 2026).** This document preserves the conceptual assessment removed from the obsolete `docs/capabilities/event_bus/` candidate directory. The responsibilities described as proposed Message Queue interfaces are not claims of implemented public APIs. Event Bus has no independent capability ownership. See [Message Queue](../docs/capabilities/message_queue/capability-record.md) for the reciprocal note and the future owner-specific contract review.

# Capability Record

## Capability Name:
`event-bus` (actual historical directory: `event_bus`).

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).
**Proposed retirement/consolidation, pending owner approval (18 November 2026).** No separate implementation was verified. A `nuxt-layers/event-bus` repository was not found; this is not proof of non-existence elsewhere. **Do not classify this record as an operational service.** It remains as review evidence until removal is expressly approved.

## Purpose
**Classification gate, not a proposed new service:** decide whether there is independently owned business/platform responsibility distinct from `message-queue`.

**Recommendation EB-01 (proposed): retire this standalone capability candidate.** The accepted governing catalogue assigns transport of capability-published outbox messages to `message-queue`; the working blueprint already maps `event-bus-service` and former `events-queue` to `message-queue`. An in-process pub/sub API, subscription registry, topic routing or change-event fan-out alone does not establish a second data authority. These are transport patterns or Message Queue interfaces, not a new capability.

## Classification
**Not independently justified.** Event-driven collaboration is an architectural pattern implemented by source-owned durable outboxes, the `message-queue` platform capability and host-supplied transports. The separate `events` domain candidate concerns actual scheduled sessions/programmes and is unrelated to event delivery; `scheduler` owns scheduled task invocation, not business event transport.

## Dependencies
No separate Event Bus dependency is proposed. Event producers own their committed changes and durable outboxes; the application composes a published Message Queue transport port and independent authorised consumers. Contract edges remain directed and acyclic. Message Queue must not import producing capability private source or storage.

## Optional integrations
Transport providers, local in-process fan-out, broker adapters and delivery workers are Message Queue infrastructure or internal implementation choices where justified. Do not mandate a second broker, framework, provider SDK or universal event store.

## Version
No Event Bus public contract/version verified. Proposed boundaries below are **idealised Message Queue responsibilities**, not published implementation signatures.

## Availability
The `nuxt-layers/message-queue` repository exists with a minimal README on `master`; no root `CONTRACT.md` could be retrieved on 18 November 2026. Its actual API, coverage, security and operational readiness are **unverified**. No `event-bus` implementation readiness is asserted.

## Capabilities offered
**None separately.** If EB-01 is approved, remove `event_bus` as a standalone candidate from active documentation, retaining this review's decision/provenance in `reviews/`. All justified delivery responsibilities reside in Message Queue, subject to its own full review.

## Configuration
No Event Bus-specific configuration authority. Transport configuration/credentials are host-provided; applicable approved scoped settings follow Configuration and capability policy. Security and delivery floors cannot be weakened by tenant settings.

## Conceptual contract to retain under Message Queue (not an Event Bus contract)

### Idealised public inputs
| Source | Input and purpose | Validation / absence |
|---|---|---|
| Source capability's owned durable outbox | Committed event identity, source and schema version, tenant/resource scope, minimal change facts, correlation/causation and permissible recipient/routing metadata | Validate schema and producer provenance, isolation, payload bounds; never manufacture source events or read private tables; backlog stays visible if delivery unavailable |
| Host/composition | Documented transport provider/worker ports, supported delivery and subscription settings, scoped credentials | Reject unsupported or insecure provider setup; no implicit public publishing or cross-tenant routing |
| Authorised consumer | Declared subscription, supported event versions, acknowledgement/retry/dead-letter or replay requests | Authenticate/authorise access and scope; reject unauthorised subscriptions, unsafe replay or unsupported schema |
| Clock and relevant policy context | Trusted times, expiry/retry policy, retention/Privacy and Legal Compliance constraints | Do not rely on untrusted producer wall clock for security or retention; fail safely when required policy cannot be established |

### Idealised public outputs
| Consumer | Output | Meaning / limits |
|---|---|---|
| Authorised subscribers | Validated, tenant-scoped event envelope and source-owned event facts | Notice of a committed source change, not proof that subscriber work completed; duplicates and reorder are possible |
| Source owner and operators | Enqueue/dispatch/attempt/acknowledgement status, lag, failures, dead-letter and replay status | Transport evidence only; not a second domain outcome or automatically an Audit evidence receipt |
| Logging / Observability | Minimised structured diagnostics, correlation, queue-depth/latency/retry/health measures | No raw secrets, unrestricted payloads, or automatic elevation into accountable Audit evidence |
| Audit (when eligible) | Attributable transport administration/control events and accepted producer events via separately governed Audit intake | Audit owns its own acceptance/integrity/retention; delivery or acknowledgement alone never proves Audit custody |
| Reporting | Authorised operational summaries and aggregated throughput/failure/lag measures | Derived metrics, not a source-owned domain history or compliance certification |

### Commands, queries and events
**Commands:** request authorised subscription, dispatch, acknowledgement, bounded retry, dead-letter review and controlled replay. Validate idempotency keys, version, tenant, purpose and permissions; do not allow arbitrary clients to assert other capabilities' committed domain events.

**Queries:** permitted subscription/configuration status, backlog, delivery attempts, failed messages and replay progress; expose source, freshness/completeness and uncertainty without leaking another tenant's events.

**Events:** source-owned committed domain events originate from source outboxes. Message Queue may own **transport-state** notices such as delivery failure or quarantine, without presenting these as domain events. Delivery is normally at-least-once; no distributed exactly-once guarantee, global ordering promise or universal transaction shared across subscribers.

### Cross-capability relationships
- **Producing capabilities** (for example Authentication, Authorisation, Booking and Configuration): source facts, validation, event schema/version and durable outbox remain theirs; Message Queue supplies transport receipts/status. Commit and publish must be recoverable without losing accepted owner-state changes.
- **Audit:** receives qualified trustworthy assertions through its own public intake; owns evidential custody and coverage, not broker transport.
- **Logging / Observability:** collect redacted technical diagnostics and performance signals; neither is authoritative domain history.
- **Reporting:** uses authorised derived transport measures; business reporting queries authoritative domain sources.
- **Scheduler / Workflow / Notifications:** independently own due-time dispatch, multi-step coordination and recipient delivery respectively. They can consume published messages, but transport does not itself schedule, decide workflows or send user notices.
- **Identity / Authentication / Authorisation / Privacy / Legal Compliance:** supply verified principal/context, access decisions and applicable disclosure/retention controls through host-composed public contracts. Message delivery never grants business permissions.
- **Clock / Configuration / Integrations / infrastructure:** supply time/policy context and optional provider integration; the host selects adapters. No reciprocal import cycle or shared business database is introduced.
- **Events (domain):** owns real-life sessions and programme state, not messages or Message Queue delivery.

### GUI and host integration
**No user-facing Event Bus dashboard or sidebar entry is justified.** Message Queue may optionally expose an **operator-only**, host-composed dashboard from the application's sidebar: tenant-scoped queue health/backlog, subscription status, retries/dead letters, authorised replay with confirmation and an auditable administrative history. Keep native functionality headless; do not expose sensitive event payloads by default. UI uses public Message Queue contracts, Theme Manager tokens, WCAG 2.2 AA, i18n and safe responsive presentation; no separate Event Bus screen or private database access.

### Conceptual acceptance examples (future Message Queue review)
1. Committed source change with healthy transport -> one durable source event, possible repeated delivery -> source remains authoritative.
2. Transport offline at commit -> owner outbox retains pending change; backlog and recovery visible, not a false business failure.
3. Duplicate or out-of-order delivery -> consumer deduplicates by source event identity/version and rechecks source if needed; never grants access from event alone.
4. Tenant B attempts Tenant A subscription/replay -> denied and safely audited.
5. Provider timeout/uncertain acknowledgement -> retry/reconcile without claiming exactly-once or recipient completion.
6. Audit unavailable while queue healthy -> no false Audit receipt; explicit coverage gap and owner-defined safe failure response.
7. Dead-letter replay by unauthorised operator -> denied; authorised replay remains bounded, traceable and version-safe.
8. Events domain creates a scheduled seminar -> Events owns session; Message Queue only carries any published change notice.
9. No Event Bus implementation/package installed -> no loss of authoritative domain functionality; Message Queue's required transport absence is handled per producer's published failure contract.

### Decisions and next steps
- **EB-01 — Proposed, awaiting explicit owner approval:** classify `event-bus` as redundant; do not create a standalone capability or runtime contract.
- **EB-02 — Proposed:** preserve event terminology as an architectural pattern; `message-queue` owns transport, source capabilities own domain events/outboxes.
- **EB-03 — Proposed:** no Event Bus GUI; optional Message Queue operator interface only.
- **EB-04 — Technical/implementation gap:** Message Queue root `CONTRACT.md`, transport and worker contracts, absence/recovery guarantees and minimal consumer proof need independent examination in Message Queue's review.
- **EB-05 — Approval-gated documentation cleanup:** after owner approval, remove the obsolete `event_bus` directory and any remaining candidate-only references without deleting the unrelated `events` domain or existing historical review evidence. Never change `architecture-rules` as part of this PR without separate approval.

**Authority and evidence (18 November 2026):** governing `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint opening `master` `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. Accepted governing catalogue and Capability Standard distinguish source outboxes from transport; all detailed inputs/outputs above are proposed for the future Message Queue public contract, not asserted implemented features. Review PR #66, unmerged.
