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

## Cross-capability note — Authentication security events (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns authentication outcomes and the originating durable security-event outbox required by ADR-0012; Message Queue transports owner-published messages, not authentication events' business meaning, credentials or source records. **Agreed conceptual direction (AUT-05):** convey appropriately minimised, attributable lifecycle events to authorised consumers such as Audit with explicit delivery, replay, deduplication and failure semantics; successful transport must not be confused with successful authentication or Audit acceptance. **Open:** accepted interoperable public event/acknowledgement contract. Message Queue's own review remains incomplete.

## Cross-capability note — Booking event delivery (15 November 2026)

**Proposed; Message Queue public contract unverified.** [Booking](../booking/capability-record.md) owns durable outbox lifecycle events after committed booking changes, with tenant scope, booking reference, version, event identity and minimal provenance. Message Queue may transport these events and report delivery attempts, backlog and acknowledgement; it never owns reservation status, holds or source event decisions. Consumers must tolerate duplicates/out-of-order delivery, and missing transport must not fabricate successful or failed Booking transitions. Use one-way public ports to avoid cyclic imports.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Configuration owns committed change events and its durable outbox; Message Queue owns transport/retry/replay. Consumers may receive duplicates and must query authorised current values rather than treating events as access grants. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Reciprocal note — Events conceptual review (18 November 2026)

**Events review reciprocal (18 November 2026; EVT-01–10/12–15 owner-approved; event_bus consolidated into Message Queue in master):** [Events](../events/capability-record.md) is the Domain source for calendar/programme activities and owns committed event/session state and its outbox. Message Queue transports Events' minimally scoped committed-change messages; may expose retries/acks/backlog, not schedule/attendance/booking authority. Consumer deduplication and staleness reconciliation required. Avoid treating scheduled activities as transport messages or adding a cyclic direct import.

## Revised Events boundary and decision gates — 18 November 2026

**18 November Events generic-domain boundary — owner-approved, post-event_bus consolidation:** [Events boundary and decisions](../../../reviews/events-refined-boundary-and-decisions.md) identifies `events` as organised activities and scheduled occurrences; `message_queue` carries committed source-owned domain-change messages, with replay/dedup/transport status, not the activity lifecycle or participant commitments. The separate `event_bus` record was removed from master and must not be reintroduced by PR #67. Events retains its authoritative outbox and no implicit transport dependency.

## Reciprocal classification note — Event Bus consolidation (18 November 2026)

**Status: owner-approved EB-05 consolidation documented in [Event Bus review PR #66](https://github.com/nuxt-layers/architecture-blueprint-review/pull/66); Message Queue's detailed public transport interface remains subject to its own review.** [Archived Event Bus classification and idealised contract](../../../reviews/event_bus-consolidation.md) finds no distinct source-of-truth, lifecycle or public contract justifying an independent Event Bus capability. The governing catalogue already assigns outbox-message distribution to Message Queue, and the blueprint maps `event-bus-service` / former `events-queue` to Message Queue. Preserve source-owned durable outboxes and event semantics; Message Queue owns only validated transport, subscriptions, attempts, retry, dead-letter and controlled replay. Transport success is not domain completion or Audit acceptance. Subject to a future Message Queue-specific public-contract review, provide producer/consumer ports, minimised scoped envelopes, clear duplicate/order/uncertainty guarantees and operational state to authorised consumers. Optional operator UI belongs to Message Queue, not a separate Event Bus dashboard. No implementation interface or separate dependency is thereby asserted; the current `nuxt-layers/message-queue` root `CONTRACT.md` was not retrievable.

## Federation — reciprocal conceptual contract (18 November 2026)

**Status: Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69); not an approved implementation API, and does not complete this capability's independent review.** [Federation public contract](../federation/capability-record.md#independent-review-contract-completeness-and-authority-18-november-2026).

Federation owns committed peer/subscription/delivery/checkpoint state and its durable outbox facts; Message Queue may carry these and source-owned publication events to selected subscribers. Message Queue does not own remote peer trust, HTTP exchange, source content, federation cursor semantics, reconciliation or origin authorisation. Duplicates/replay are expected; delivery acknowledgment is not business completion. All cooperation is via public, directional host-composed contracts with scoped failure/absence semantics; preserve existing approvals and avoid package dependency cycles.

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Integrations owns its committed connection/grant/mapping/checkpoint transitions and associated durable outbox; Message Queue only transports owner-originating events and may report delivery attempts. Provider webhooks and provider operation receipts are untrusted/qualified external evidence, not source-of-truth domain events. At-least-once/replay and out-of-order handling require consumer deduplication, and delivery success is not remote business completion. See [Integrations conceptual contract](../integrations/capability-record.md#commands-queries-events-and-shared-invariants), PR #76; proposed, not implemented.


---
# Independent Message Queue conceptual review — 19 November 2026

**Status:** Proposed detailed design on draft PR #94; **not owner-approved**. The preceding Event Bus retirement/consolidation (EB-05) is owner-approved and retained. **Evidence:** governing `architecture-rules/master` `b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint opening `master` `6dac83a03da8704f7945ee1bc894f2248300445a`; `nuxt-layers/message-queue` root `CONTRACT.md` not retrievable and README is only `# message-queue`. No implementation API, deployment, CI, worker behaviour or independent consumer verified. Governing Capability Standard and catalogue are authoritative; this record is not.

## Identity, classification and architectural disposition

**Name:** canonical blueprint directory `message_queue`; governing catalogue name `message-queue`. **Classification: Platform**, a reusable transport and delivery coordination capability, justified by ownership of routing/subscription and delivery-control semantics independent of any producing domain. **Disposition:** retain as one capability; do not revive `event_bus` or create parallel pub/sub ownership. A framework-independent headless core with optional Nuxt adapter and optional operator presentation is a suitable **proposed implementation form**, not a mandated migration. Default modular-monolith deployment; broker/worker split requires operational justification.

**Purpose:** securely and recoverably carry committed messages from source-owned durable outboxes to eligible consumers through provider-neutral public ports, while distinguishing message acceptance, dispatch, consumer acknowledgement and business completion. Supports domain change fan-out and other explicitly authorised transport use cases, without becoming the canonical event store.

**Owns:** transport-specific routing/subscription definitions and their approved revisions; delivery envelope reference and transport identity; delivery attempts, retry scheduling, lease/visibility state, acknowledgements, dead-letter/quarantine state, controlled replay, transport checkpoints and bounded operational metrics; provider mapping and lifecycle evidence where relevant. Holds only the minimum retained payload or pointer necessary to meet stated delivery obligations. **Does not own:** originating domain event definitions/facts, durable producer outbox and source transaction, consumer business decisions or side-effect completion, scheduler due-work decisions, workflow approvals, Notifications recipient/channel business rules, Audit evidential custody, Logging traces, broker/infrastructure provisioning, provider credentials, Federation trust or Events calendar activities. Do not use this service as a generic cross-domain business transaction coordinator.

## Native service, lifecycle and provider boundaries

1. Validate an authenticated, authorised producer registration and declared event schema/version/routing scope. Ingest **committed** producer-outbox items via a documented lease/checkpoint/acknowledgement or equivalent recoverable source port. Direct messages, if supported, need an explicit durably accepted ownership contract; never imply they are producer domain events.
2. Apply tenant/recipient disclosure policy and size/rate/retention limits before persisted acceptance or dispatch. Resolve registered, authorised, version-compatible subscriptions; never route across tenant scopes merely because a tenant is a parent.
3. Distinguish **source pending → transport accepted → dispatch pending → leased/in-flight → acknowledged**, plus **retry-wait**, **quarantined/dead-letter**, **expired/retired** and **unknown acknowledgement**. A producer outbox item is not safely released until the relevant agreed custody/ack boundary is durably reached. An accepted transport record is not evidence that a subscriber committed work.
4. On timeout, lost lease or uncertain provider receipt, reconcile or retry with stable message identity and explicit attempt identity. Duplicates and reordering are possible. Consumer independently deduplicates and checks current authority/version. No exactly-once distributed outcome promise; ordering only within an explicitly supported partition and provider guarantee, never global.
5. Apply bounded exponential backoff with jitter, poison-message isolation, dead-letter retention, circuit-breaking/backpressure and fair tenant quotas; enforce secure replay authorisation, expiry and version support. No automatic infinite retry or cross-tenant payload inspection.
6. Native provider-neutral service remains usable with a documented host-supplied durable store/worker/transport; a small local adapter can serve supported development use, **not** claim durable production guarantees without evidence. Candidate infrastructure options such as Postgres/pgmq or external broker are adapters, **not contractual dependencies or approved product choices**. A Temporal gateway provides connection/worker SDK infrastructure, never owns Queue transport rules. Avoid dual-write holes using producer-owned outbox and recoverable hand-off.
7. Provider selection and migrations require compatibility, credential scoping, backlog drain or reconciliation, checkpoint continuity and rollback. During ambiguous cutover do not assert loss-free migration. Report unknown/degraded/unavailable separately; preserve source pending items and prevent false successful receipt. If durable infrastructure is absent, **fail before claiming acceptance**, while allowing source domain operations to commit according to their own published outbox contract.

## Idealised public inbound contract

| Source and classification | Input / intent | Validation, authority and failure semantics |
|---|---|---|
| Source capability outbox (conditional per producer) | Committed source event ID, owning capability, schema/version, resource revision, scope, minimal payload/reference, correlation, causation, classification and intended routing eligibility; claim/ack checkpoint | Producer owns event fact and outbox. Validate origin, version, scope, duplicate identity and bounds; reject forgery, quarantine invalid material; staleness/out-of-order flagged. A transport acknowledgement never alters source business state. |
| Host composition (essential) | Durable store, worker/transport ports, secret references, bounded configuration, deployment identity and operational readiness | Validate supported adapter security, durability and isolation; absent required ports means unavailable/fail closed, not silent in-memory success. No host-owned bespoke relay or store logic; independently usable published contract and one-call Nuxt adapter where applicable. |
| Authorised subscription owner/consumer (conditional) | Subscribe/unsubscribe/update event types and compatible versions, scoped endpoint/handler, delivery mode, acknowledgement/negative acknowledgement, idempotency key and checkpoint | Authenticate producer/consumer trust, request-time Authorisation and owning-domain restrictions; reject unsupported versions, widening scopes, unknown receipt, duplicate registration and unauthorised replay. Consumer application effects remain its authority. |
| Authorised operator (optional presentation/API) | Pause/resume, redrive/replay, quarantine, retry, inspect redacted status, retention adjustments within floor, approved provider cutover | Strong/recent authentication and specific privileged permission; high-risk bulk replay or destructive purge may require independent Workflow approval; Audit attributable actions. Missing approval denies action; emergency controls cannot override retention/holds. |
| Configuration, Clock, Privacy/Legal Compliance and infrastructure (conditional public context) | Approved scoped transport settings/version, trusted instant and time quality, legal retention/hold and purpose constraints, provider and resource health | Owner applies mandatory floors; missing/contradictory critical constraints place sensitive operation on hold. Browser-local clock or tenant setting cannot grant privileged access or override preservation. |

## Idealised public outbound contract

| Recipient | Output and authoritative meaning | Limits, provenance and uncertainty |
|---|---|---|
| Source owner / publisher | Accepted/rejected/uncertain custody result; stable transport ID, source-event identity and checkpoint, rejection reason; pending/lag/pressure | Authoritative **transport** receipt only. Release outbox according to explicit hand-off guarantee; never imply business transaction or consumer acceptance. |
| Authorised subscriber | Scoped versioned envelope and delivery attempt/lease token, stable source event ID, producer reference and revision, correlation/causation, provenance, effective/commit time and disclosure classification | Source domain owns event meaning. Duplicate/out-of-order delivery possible; replay marked, no implicit action grant; avoid forwarding fields to unauthorised scopes. |
| Consumer / operator | Ack/nack/retry decisions and recorded disposition; status/query of active subscription, backlog, attempt, dead letter and authorised replay | Acknowledgement proves only consumer's **declared transport acceptance boundary**; not business, legal or Audit acceptance. Unknown or partial results explicit, with timestamp, provider observation and completeness. |
| Logging / Observability / Reporting | Redacted structured errors, correlated spans, lag/depth/age, throughput, retry, poison-message and provider-health metrics; authorised aggregates | Telemetry may be sampled/stale, no sensitive raw payload or provider secrets. Reporting derives service metrics, not source-domain facts. |
| Audit | Attributable privileged transport-control, retention, routing/policy and replay events via Audit public intake | Audit owns its receipt, integrity and custody. Queue success is not Audit acceptance; failures and evidence gaps explicit. |
| Host / operational health | Degraded/unavailable/ready status, last observation, provider/configuration revision, backlog and capability-supported limits | Distinguish installed/configured/ready/authorised; unknown is not healthy. |

**Commands:** register/update/revoke subscription, accept committed source item, acknowledge/negative-acknowledge delivery, pause/resume delivery, request bounded redrive/replay, quarantine/release, inspect operational disposition and validated provider hand-over. Each command documents preconditions, caller permission, idempotency, committed versus pending versus unknown result, retry and recovery. **Queries:** authorised delivery/attempt/lag/dead-letter/subscription views with snapshot/as-of time, filters, scope, completeness and redaction. **Events:** Queue owns only transport lifecycle/control facts after durable transport-state commits, through its own outbox where needed; these must not masquerade as source domain change events or recursively cause uncontrolled routing. A delivery attempt is not itself the consumer's domain event.

**Shared invariants:** trusted tenant and actor/service context; explicit resource and producer provenance; source event and subscription schema/version; scoped recipient selection; correlation/causation, deduplication and attempt identities; policy version/effective time, trusted Clock instant; adapter/provider and evidence age; retention/purpose classification; recoverable unknown status. Do **not** require a universal request DTO. Enforce strict least privilege and isolation even for support/admin roles; cross-tenant delegation must be independently authorised. Encrypt confidential transport data in transit/at rest as applicable, redact diagnostics, minimise payload retention, apply lawful purpose and legal holds; selective deletion must not silently break required outbox/audit guarantees. Publish stable failure codes and message keys; version contract changes compatibly.

## Cross-capability directional cooperation and absence

| Capability / owner | MQ receives | MQ supplies | Nature / absence and dependency discipline |
|---|---|---|---|
| Any producer: Authentication, Identity, Booking, Events, Invoice, Configuration, Integrations etc. | Source-owned committed outbox item and source revision | Scoped delivery custody/attempt/failure evidence | Conditional where events are published; source remains authoritative; no direct source database access or reverse package imports |
| Authorised consumer: Audit, Notifications, Search, Reporting, Workflow or domain handlers | Subscription scope/version, acceptance or failure acknowledgement | Source event notification/transport status | Optional per deployment; consumer owns processing and re-query; uninstalled listener cannot be called delivered |
| Identity / Authentication / Authorisation | Trusted tenant/service/caller provenance, assurance and permission verdict | Auditable access/control outcomes, never grants | Essential security via host-composed ports; missing critical decision denies |
| Configuration | Approved effective routing/retry/retention/provider setting reference | Applied version, refusal, operational state | Conditional; hard security floors enforced by MQ |
| Privacy / Legal Compliance | Purpose, disclosure, retention, legal hold constraints with qualified provenance | Minimised processing and control evidence | Conditional by data/purpose/jurisdiction; unknown critical rules hold |
| Clock / Infrastructure / Temporal Gateway | Trusted clock and infrastructure readiness; optional transport/worker adapter | Time-stamped operational dispositions and metrics | Essential trusted time/compatible infrastructure, optional gateway adapter; not Scheduler |
| Scheduler | No intrinsic need for Scheduler to retry a queue delivery; Scheduler-owned due-work messages when explicitly supported | Ordinary transport outcomes for Scheduler consumers | Optional, no cross-service cycle or replacement of Scheduler due-time semantics |
| Workflow | Authorised approval outcome for sensitive operations when policy requires | Domain events as input for orchestration, control/evidence status | Conditional; Workflow owns review/approval state, not delivery |
| Federation / Integrations | Approved external exchange instructions or local committed source events | Qualified outbound/inbound transport receipts only | Conditional; they own provider trust, webhooks, federation checkpoints and mapping |
| Logging / Observability / Audit | Sink/intake contract and operational observability context | Redacted diagnostics, metrics, accountable admin-control events | Separate technical telemetry and evidential custody; absence explicit; no false Audit receipt |

**Directional composition:** producers depend only on their own outbox and published transport-facing contract; host wires Queue adapters and subscriber interfaces; consumers depend on independently versioned source event contracts and Queue delivery port. **Information flow is reciprocal, package imports need not be.** MQ does not depend on a specific producer or consumer implementation. No new `event_bus` or direct shared producer tables.

## Security, governance, presentation and acceptance

Security threats: forged origin, replay amplification, event injection, tenant crossover, payload leakage, misrouting after revoked subscription, poison-message exhaustion, provider credential exposure, missing hand-off, unbounded retention, privilege abuse, high-volume denial of service and silent Audit loss. Apply origin authentication, fine-grained request-time authorisation, schema validation, quotas, redaction, encryption, isolation, independent administration audit, revocation-aware delivery eligibility and secure failure. Events **never confer permissions**; downstream owner evaluates its own current state. OWASP ASVS 5 L2 baseline (L3 critical), GDPR/UK GDPR applicability and qualified legal review are obligations to assess, not claimed certification.

**GUI:** core service headless. Optional operator-only Message Queue dashboard under host-owned sidebar **Capabilities → Message Queue**, with tenant-safe queue/consumer/subscription health, backlog age, delivery/failed/dead-letter counts, redacted attempt detail, scoped filtering, pause/resume and guarded replay; show explicit pending/unknown/failed and last-updated states. Dangerous controls require independent request-time permissions, clear confirmations, optional dual approval and attributable Audit intake. No ordinary end-user dashboard, no separate Event Bus sidebar item, no automatic permission from menu visibility. Use public contract only; host owns routing and installation; Theme Manager semantics, `ui`, WCAG 2.2 AA keyboard/screen-reader, responsive and localised time/labels, safe no-presentation operation. No raw message payload by default.

### Conceptual acceptance scenarios (not tests performed)

| Input | Expected behaviour and output | Authority |
|---|---|---|
| Domain transaction commits; outbox contains event | Recoverably accepts and routes scope-approved event; distinct custody receipt and delivery attempt | Producer owns source event; MQ transport |
| Transport absent on source commit | Producer outbox remains pending; MQ does not claim acceptance or reverse committed business change | Producer outbox; MQ status |
| Duplicate, replayed or re-ordered event | Same source identity preserved; duplicate delivery possible; consumer deduplicates/re-queries revision | MQ delivery; consumer owns effect |
| Tenant B attempts Tenant A subscription/replay | Refusal without information leakage; privileged attempt recorded via Audit interface | Authorisation and MQ control |
| Provider times out after sending | Unknown delivery/custody explicitly reported; bounded reconcile/retry, no exactly-once fiction | MQ transport/provider evidence |
| Bad schema, unauthorised producer, poisoned payload | Reject/quarantine without forwarding; actionable redacted error and operational trace | MQ validates contract |
| Consumer fails or revokes subscription | Backoff/dead letter/stop as appropriate; source state unchanged; no false consumer success | MQ disposition; consumer |
| Authorised replay after corrected handler | Scoped revision-compatible retry; new attempt, same source identity, attributable administrative action | MQ transport; Audit evidence |
| Audit unavailable during admin change | No false Audit acceptance; protected operation follows risk-based fail/hold policy and exposes evidence gap | Audit custody; MQ safe control |
| Provider cutover with retained backlog | Pause/drain/checkpoint/reconcile; uncertain records reported, no silent duplication-free guarantee | Host/provider, MQ checkpoint |
| Unsupported cross-tenant broadcast or promised exactly-once outcome | Explicit refusal/not-supported result | MQ published guarantees |
| No optional GUI or no subscriber installed | Headless transport still works for available configured subscriptions; absent destinations not called successful | Host composition/MQ |

### Proposed review decisions and delivery gates

- **MQ-01 — proposed:** retain single Platform `message-queue`; no independent Event Bus (EB-05 already approved).
- **MQ-02 — proposed:** source capability owns durable event outbox and meaning; Queue owns scoped custody, transport, attempts, subscriptions and controlled replay.
- **MQ-03 — proposed:** at-least-once compatible delivery contract with no cross-boundary exactly-once promise; strict accepted/acknowledged/completed distinction.
- **MQ-04 — proposed:** provider-neutral, independently consumable headless contract; host supplies durable transport, Nuxt adapter follows ADR-0012 one-call/50-line budget if built.
- **MQ-05 — proposed:** request-time isolation, purpose minimisation, redaction, bounded retries/retention and privileged audited replay, with safe unknowns.
- **MQ-06 — proposed:** optional operator GUI only; no separate Event Bus UI.
- **MQ-07 — open owner decision:** whether direct non-outbox application messages are in initial scope, and what *durable acceptance* contract they must meet (recommend **defer** until source ownership/use cases justify).
- **MQ-08 — open owner decision:** default production broker/adapter and durability/service-level envelope (recommend keep provider-neutral specification, select through documented infrastructure acceptance).
- **MQ-09 — technical investigation:** durable outbox-to-custody checkpoint and provider migration under failure; evidence-driven implementation design, not a claim of existing behaviour.
- **MQ-10 — implementation alignment/acceptance:** publish real root `CONTRACT.md`, exported ports, supported delivery modes, storage register, security threat model, independent consumer/CI and minimal host proof. No current deployed/working capability is established.

**Conceptual sign-off:** pending explicit owner resolution/approval. Governing changes require a separate accepted ADR/standard PR if needed. This review does not edit implementation repositories, run tests or permit merger without explicit authorisation.
