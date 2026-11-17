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

## Cross-capability note — Logging versus Audit (14 November 2026)

**Established:** The governing catalogue distinguishes Logging's structured technical diagnostics/correlation/sinks from Audit's proposed tamper-evident business/security evidence and review. **Proposed:** Logging may provide correlation and operational failure signals to [Audit](../audit/capability-record.md), but debug logs are not by default authoritative evidential records. Audit does not own Logging's sinks or general log lifecycle. **Open:** event mapping, classifications, sensitive-data minimisation and failure alerts. Logging's full conceptual review remains incomplete.

## Cross-capability note — Authentication operational logging (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns credentials, sign-in attempts and outcomes, session lifecycle, security controls and authenticated principal assertions; Logging supplies structured technical diagnostics and correlation, not authoritative security-event custody or the originating Authentication facts. **Agreed conceptual direction:** Authentication emits only purpose-limited, sanitised operational signals for authentication errors, provider outages, throttling, maintenance and degraded health, with suitable correlation references and controlled diagnostic access. Logs must not expose passwords or verifiers, session/bearer tokens, passkeys or recovery secrets; IP addresses, user agents and identifiers require data minimisation, classification, access controls and retention. Authentication's significant security outcomes flow through its owned durable event mechanism for [Audit](../audit/capability-record.md), not by promoting ordinary logs into authoritative evidence. **Open:** diagnostic taxonomy, correlation/redaction policy, retention, outage behaviour and whether Logging is an independent capability rather than an infrastructure integration. Logging's own conceptual review remains incomplete.

## Cross-capability note — Audit input/output boundary (15 November 2026)

**Status: Proposed relationship only; Logging's conceptual review remains incomplete.** The fuller contract direction is recorded in [Audit](../audit/capability-record.md#explicit-auditlogging-integration-boundary).

- **Logging owns** structured technical log records, correlation and operational sinks. Its diagnostic success does **not** constitute a durable Audit evidence receipt, source business confirmation or evidential integrity verification.
- **Audit owns** accepted evidence, its provenance, integrity/coverage checks, controlled review, retention and disclosure; it may emit safe technical diagnostics to an optional Logging provider without relying on that provider to safeguard evidential state.
- **Inbound to Audit:** only classified, producer-verified, minimised technical/security/control assertions under Audit's governed event definitions, with origin, outcome and applicable tenant scope; never automatic bulk ingestion of raw debug logs.
- **Inbound to Logging:** bounded Audit diagnostics, non-sensitive failure codes and permitted correlation identifiers. No direct access to Audit's protected evidence store.
- **Absence/failure:** both capabilities operate independently; dual outages or incomplete capture remain separately visible. Host composition must avoid mandatory bidirectional imports, private storage access or cycles.
- **Open for Logging's future review:** typed source-event eligibility, diagnostic interfaces, sink failure contract, redaction, severity mapping and optional event forwarding without promoting free-text logs into authoritative audit evidence.

## Cross-capability note — Asset diagnostics and accountability (15 November 2026)

**Status: Proposed relationship; Logging's full conceptual review remains incomplete.** [Asset](../asset/capability-record.md) owns asset state, lifecycle and originating business events. It supplies only purpose-limited structured diagnostics for invalid commands, conflicts, storage/outbox failures, external licensing/telemetry outages, scheduling and inter-capability handover errors, including permitted opaque correlation and source-operation references. Logging owns diagnostic sinks and technical delivery results; neither log success nor failure proves an Asset business outcome, a durable [Audit](../audit/capability-record.md) receipt or evidential verification. Exclude licence keys, raw contract/IP content, sensitive location/assignment histories, and full request bodies. Logging may be absent without removing Asset's native functions or mandatory audit capture; preserve independent outage status. Severity taxonomy, retention and sink interfaces remain for Logging's own review.

## Cross-capability note — Authorisation diagnostics (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns access decisions and role/grant/change events; Logging owns structured technical diagnostics, correlation and sinks, not access decisions or Audit custody. **Proposed:** minimise and sanitise denial/error, dependency-outage, latency and staleness signals; keep operational telemetry distinct from mandatory accountable [Audit](../audit/capability-record.md) evidence. **Open:** denial-volume controls, sensitive-data classification, retention and failure paths. Logging's review remains incomplete.

## Cross-capability note — Authorisation operational diagnostics and Audit separation (15 November 2026)

**Status:** Proposed deeper interface, not a verified Logging API. [Authorisation](../authorisation/capability-record.md#deep-interface-review--authorisation-audit-and-logging-15-november-2026) may emit safe, purpose-limited diagnostics for decision failures, permission/risk category, dependency outages, clock/Identity staleness, latency, maintenance and event backlog with permitted opaque correlation. Logging owns severity, retention, sink routing and technical delivery state, never effective permission, source outbox evidence or [Audit](../audit/capability-record.md) receipt. The present optional best-effort denial sink is **not** a substitute for mandatory selected security-event evidence. Logs must exclude tokens/credentials, private policy attributes, unneeded personal identifiers and protected payloads; apply tenant partitioning, data minimisation and bounded volumes. Independently report Logging and Audit outages, without making a successful log write proof of an access decision or Audit custody. Logging's conceptual review remains incomplete.

## Cross-capability note — Billing operational diagnostics (15 November 2026)

**Agreed conceptual relationship: Billing BIL-01–BIL-06 approved on 15 November 2026; implementation remains unverified.** [Billing](../billing/capability-record.md) supplies minimised, structured diagnostics about invalid usage/rates, duplicate protection, provider failures, billing-run timeouts, reconciliation and outbox delivery, with opaque correlation and operation references. Logging owns diagnostic formatting/sinks/retention, not Billing records or Audit evidence; do not log raw invoices, personal/bank information, complete usage data, secrets or sensitive dispute submissions. A successful log write is not proof of charge commitment, invoice issuance or settlement. Billing's business invariants remain enforced if an optional diagnostic sink is unavailable.

## Cross-capability note — Billing structured diagnostic interface (15 November 2026)

**Status:** Proposed detailed specialist interface consistent with approved Billing BIL-01–BIL-06 and BIL-S06; Logging's full conceptual review and public implementation contract remain open. See [Billing's detailed Audit/Logging interface](../billing/capability-record.md#detailed-billingauditlogging-interface-review-15-november-2026).

- **Inbound from Billing:** Typed and bounded diagnostics about invalid rate/usage/period, rejected duplication, billing-run latency/partial failure, invoice or accounting handoff, provider timeout/authority reconciliation, outbox and Audit capture backlog, access-denial category and safe correlation/causation. Billing remains authoritative for its own operation result; Logging owns technical log record, safe severity mapping, sink routing and diagnostic retention.
- **Outbound to Billing:** Where a documented Logging interface provides it, report diagnostic acceptance, drop/rejection, sink-unavailable or uncertain status and permitted aggregate health. This is neither a durable Audit receipt nor evidence of charge finalisation, invoice issue, ledger posting or payment settlement. Optional Logging failure does not ordinarily roll back Billing's correctly authorised committed state.
- **Protection:** Minimise and redact tenant/party-sensitive data; prohibit raw invoice/usage/dispute contents, credentials, payment instruments, full request bodies and private access policies by default. Apply bounded payload/rate, purpose, tenant isolation, access control, lawful retention and injection-safe formatting. Source/operation identifiers should be opaque, not necessarily directly resolvable by unauthorised users.
- **Failure distinction:** Expose Billing-owned business state, Audit capture/coverage/integrity state and Logging delivery/health separately, including simultaneous outages. Logging cannot elevate a free-text line to trusted Audit evidence, and a healthy log sink cannot authorise a critical Billing action lacking mandated Audit guarantee.
- **Acceptance:** provider timeout; failed billing run; replay/deduplication; Logging down with Audit healthy; Audit down with Logging healthy; both unavailable; protected financial export denied; scoped diagnostic read must not disclose another tenant's data.

No mandatory Logging package dependency, concrete schema, sink provider or implementation change is introduced here.

## Cross-capability note — Booking technical diagnostics (15 November 2026)

**Proposed relationship, not a verified implementation contract.** [Booking](../booking/capability-record.md) may emit sanitised structured diagnostics for capacity contention, stale supply, hold expiry, retry/idempotency collision, provider timeout, reconciliation, projection lag and queue delivery with purpose-limited correlation and source/tenant scope. Logging owns diagnostic processing, sinks and retention; Booking keeps reservation history and outbox; Audit keeps evidential custody. Do not log guest/contact details, provider credentials, authentication secrets or sensitive reasons for attendance. A successful log write proves neither Booking confirmation nor Audit receipt. Sink failure must be visible and must not create a second booking authority.

**Booking approval clarification (15 November 2026):** Booking BK-01–BK-05 are approved in principle. [Booking's specialist Logging interface](../booking/capability-record.md#booking--logging--operational-diagnostics) requires safe structured signals for contention, invalid time/supply, expiry, retries/idempotency, connector/webhook failures, provider timeout, reconciliation delay, outbox lag and sanitised error correlation. Logging owns safe sinks, retention and diagnostic access, not reservation outcomes or Audit evidence. Guest identities, appointment reasons, credentials and payment information must not enter routine logs. Diagnostic outage must not create double bookings, hide critical Audit failure or falsely imply an authoritative confirmation. Logging's future full review is not pre-empted.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy refinements proposed, implementation not assumed.

Sanitised operational failures for governance, commercial provisioning and quota activation, with correlation and no credentials/privileged evidence leakage. Source outcomes belong to Identity/commercial owners and evidential custody to Audit.

See [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md) for conceptual inbound/outbound authority, absence, failures and acceptance. No package dependencies inferred.

## Cross-capability note — Proposed Caching diagnostics (16 November 2026)

**Agreed conceptual boundary; adapter unverified.** [Caching](../caching/capability-record.md) may supply sanitised cache hit/miss/error, expiry, eviction, provider failure and invalidation-lag diagnostics with opaque correlation and appropriate tenancy. Logging owns structured technical records/sinks; Observability owns metrics/traces, Audit owns accountable evidence, and source capabilities own business outcomes. Never log raw cached values, sensitive keys, credentials, policy predicates or personal data. Logging sink failure does not establish cache failure or audit completion; no mandatory package coupling.

**Approved conceptual boundary (16 November 2026):** Caching publishes only bounded, sanitised operational diagnostics through a host-composed, provider-independent public port. Logging decides technical record delivery and retention, not cache validity. This approval does not establish a Logging adapter or a mandatory direct package dependency.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine offers structured diagnostic codes, safety-assessment failures, rate-limit signals, queue/outbox lag, notification/withdrawal reconciliation and opaque correlation. Logging owns technical sinks/retention; Comments Engine owns content/state transitions; Audit owns attributable evidence; Reporting owns aggregates. Do not log raw comment body, private moderator case, reporter identity, URLs containing tokens or unredacted personal data. Sink failures cannot silently become comment clearance or successful Audit custody.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not implemented or approved. [Conceptual interface](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Only privacy-minimised error codes, timings and correlations belong in technical logs; no raw drafts, secret fields or content. Source owners remain authoritative for business records.
