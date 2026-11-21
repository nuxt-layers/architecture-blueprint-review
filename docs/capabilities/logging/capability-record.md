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


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Logging owns sanitised technical diagnostic logs, not accountable settings history. Configuration emits safe error/correlation/status only; material change evidence goes separately to Audit. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not implemented or approved. [Conceptual interface](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Only privacy-minimised error codes, timings and correlations belong in technical logs; no raw drafts, secret fields or content. Source owners remain authoritative for business records.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Content Security supplies redacted diagnostic failure, latency, correlation and provider error information without copying risky raw content, secret/hash datasets or private reporter identities. Logging owns operational logs, not independent audit proof or scanning status authority.

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed logging review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Course emits structured, redacted operational diagnostics for validation, provider outages, revision conflicts and publication failures with correlation IDs. Logging owns technical diagnostics/sinks; Course owns domain history and Audit owns evidential custody. Do not record learner rosters, private draft contents or credentials in technical logs.

## Training reciprocal Logging interface — 18 November 2026

**Status: TRAIN-07/08 owner-approved; Logging independently remains a proposed/incomplete contract.** [Training's Audit/Logging public-contract boundary](../training/capability-record.md#train-0708-approval-and-explicit-auditlogging-public-contract-boundary-18-november-2026): Training emits only typed, bounded, sanitised operational diagnostics for training-input validation, duplicate submissions, provider/verification timeouts, reconciliation, retry/outbox failures, lag, denied operations and technical errors. Permitted payload: error/operation code, severity, timing, safe provider class, opaque correlation and minimal tenant scope. Never ingest raw assessments, learner transcripts, personal evaluator remarks, sensitive data or credentials by default. Logging owns sink routing/retention and may report accepted/dropped/rejected/unknown/sink unavailable where its future public contract supports that. Logging has **no** right to modify Training findings and its acknowledgement never replaces Audit evidence receipt or proves a completed learner outcome. Logging outages and Audit-capture failures are independently reportable; no mandatory bidirectional direct imports.



## Reciprocal conceptual contract — Credentials (18 November 2026)

**Status: CRED-01–16 owner-approved conceptual boundary; CRED-17 framework selection pending (18 November 2026, PR #62).** Credentials supplies sanitised structured operation/provider failures, status-check timeout, retry/idempotency, outbox lag, key or mandate verification error, correlation and safe tenant context through a public diagnostic sink. Logging returns bounded acceptance/failure/health where exposed; it owns diagnostics/sinks/retention, never credential issuance, authoritative proof status or Audit evidence. Keep signed tokens, keys, claimant details, secret provider responses and raw credentials out of routine logs. Optional logging outage must not fabricate issuance, remove mandatory Audit coverage or block otherwise valid business operations. A full Logging public CONTRACT.md remains to be designed/verified.

## Reciprocal note — Events conceptual review (18 November 2026)

**Events review reciprocal (18 November 2026; EVT-01–10/12–15 owner-approved; implementation unverified):** [Events](../events/capability-record.md) emits minimised, structured diagnostics for timetable validation conflicts, scheduling failures, provider sync and outbox backlog with safe correlations; Logging owns diagnostic sinks, not event programme, reservation decisions or Audit custody. No attendee lists/contact details in routine log payloads. Logging outages never silently convert an Events commit into failure.

## Events interface reciprocity — 18 November 2026

**Events approval and attendance boundary (18 November 2026):** [Events](../events/capability-record.md) sends only sanitised operational errors/latency, provider sync failures, scheduling retries, version conflicts and queue lag with safe correlation. Logging returns supported sink acceptance/unavailable and health signals. It must not ingest attendee lists, invitations, location-sensitive personal histories or access secrets; log receipt is not an Events commit or Audit evidence. [Contract detail](../../../reviews/events-contract-attendance-and-handover.md).

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** Export rendering exposes safe technical warnings, conversion outcome and correlation for diagnostics without source documents, secrets, raw personal data or generated bytes. Logging owns sanitised technical telemetry; Audit separately owns selected accountable disclosure evidence from the calling export workflow. Neither logs nor renders authorise a transfer. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.

## Federation — reciprocal conceptual note (18 November 2026)

**Status:** Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69), not a published implementation contract or completed independent review. See [Federation conceptual contract](../federation/capability-record.md).

Federation supplies sanitised technical diagnostics for protocol negotiation, denied fetches, retry, replay and reconciliation with scoped correlation IDs. Logging owns logs, not authoritative exchange state or Audit evidence. Exclude source private payloads, keys and tokens; technical log outages cannot convert indeterminate delivery to success. Public directional ports, explicit absence modes and acyclic package dependencies apply.


## Reciprocal conceptual note — Help capability (18 November 2026)

**Status:** HELP-01–04 owner-approved conceptual direction; this specific intake/GUI elaboration is proposed in [Help PR #72](https://github.com/nuxt-layers/architecture-blueprint-review/pull/72), not an implemented adapter or replacement for this capability's future full review. [Help public contract](../help/capability-record.md#approved-direction-elaboration--published-contracts-standards-libraries-and-gui-18-november-2026).

Help sends redacted diagnostic codes, mapping/Publisher failures, latency and permitted correlation IDs through Logging's public intake. Logging owns sinks and diagnostic retention, not help mappings or authoritative Audit evidence. Avoid raw searches, page bodies, secret context, full URLs and unnecessary subject identifiers. Logging outages must not make an otherwise valid Help lookup fail.



## Reciprocal conceptual interface — IAM Integration (18 November 2026)

**Status: Owner-approved conceptual direction in IAM Integration review PR #73; not a verified Logging implementation contract.** IAM Integration supplies minimised, structured diagnostics for suite composition failures, member port outages, retry/reconciliation stages, unavailable access decisions and correlation identifiers. Logging receives these only through its published input port and owns diagnostic sink, access, retention and search; it may return diagnostic references or controlled delivery status. Authentication tokens, credentials and private Profile data are excluded. Logging must not be represented as Audit custody or as the original IAM decision. See [IAM Integration idealised public contract](../iam_integration/capability-record.md). Do not add a direct package dependency on IAM Integration merely for these event/read-model relationships.


## Identity reciprocal input/output — 18 November 2026

**Status: recommended Identity reciprocal elaboration, 18 November 2026, [draft PR #74](https://github.com/nuxt-layers/architecture-blueprint-review/pull/74); not a verified Logging API.** Identity emits minimised structured diagnostics for principal/tenant/group operation failure, directory latency/staleness, approval and provider refusal categories, outbox/maintenance backlog and correlation, without secrets, raw invitation tokens or legal evidence. Logging owns sink routing, redaction, retention and delivery state, not Identity's committed state or Audit evidence. An optional logging sink failure does not prove or undo a source mutation and cannot grant access. See [Identity extended review](../identity/capability-record.md#extended-review--published-interfaces-observability-standards-library-suitability-and-gui-18-november-2026).


## Infrastructure reciprocal interface — 18 November 2026

**Proposed reciprocal review — 18 November 2026:** Infrastructure's [proposed interface](../../../reviews/infrastructure-conceptual-architecture.md) supplies sanitised incident/operation correlation and diagnostics; Logging owns technical sinks and structured logs, not security approval, secrets, independent Audit acceptance or authoritative provider completion. Failure remains explicit; proposed only.

## Integrations reciprocal interface — 18 November 2026

**Status: owner-approved conceptual Integrations direction INT-01–06 in [draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76), not a verified published API or approval of this capability's independent review.** Integrations supplies minimised technical diagnostics (adapter/operation reference, safe correlation, rate limits, provider timeout, retry, callback rejection and degraded status) to Logging's public intake; Logging owns diagnostic sinks, routing, redaction and log retention, and may supply sink-health/error responses. Never log tokens, webhook secrets, confidential bodies or cross-tenant identifiers. Logging receipt cannot establish remote completion or Audit evidence; its unavailability must be visible without silently changing a connector transaction. [Integrations proposed contract](../integrations/capability-record.md#reciprocal-logging-audit-and-reporting-public-interfaces); approved INT-01–06 direction, interfaces not implemented.


## Inventory reassessment reciprocal proposal — 18 November 2026 (PR #81)

**Status: proposed, not approved or implemented.** Inventory supplies technical diagnostics—correlation, latency, rejected quantity commands, provider lag, reconciliation failures and outbox-health signals—through public telemetry boundaries. Logging owns operational log ingestion/retention, **not** Inventory movement or business audit evidence. No broad serial, commercial price, party identity or sensitive custody disclosure in technical logs. This is a proposed interface; no implementation claimed. See the [Inventory reassessment contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md) and [Inventory record](../inventory/capability-record.md#renewed-conceptual-design-challenge--18-november-2026-draft-pr-81). This note preserves earlier approvals in this capability and does not complete its independent review.


### Inventory manufacturing traceability — owner-approved conceptual reciprocity (18 November 2026; PR #81)

**Approved Inventory-side conceptual requirement:** Scanner connectivity, failed/out-of-sequence scans, stale position projections, WIP queues, rejected quantity changes, replays and provider lag supply redacted technical correlation/health to Logging. Do not place secrets, full barcode contents, detailed supplier/tenant commercial records or sensitive personal information in technical logs; Logging cannot update material state. This note approves the **Inventory-side requirement only**, does not change this capability's independent approval status or claim a running integration. See [shop-floor flow and public contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026).


### Inventory operator usability and correction reciprocity — 18 November 2026 (PR #81)

**Inventory owner-approved RINV-09–12; RINV-13 proposed, not separately approved:** RINV-09–12 are Inventory-owner approved. Proposed operator UX RINV-13 must display plain-language status, not raw exception stacks. Logging receives redacted diagnostic signals for offline scanner connectivity, latency, duplicate scans, sync backlogs, failed movement validation and exceptional recovery; do not use technical telemetry as a covert worker-performance ranking or give it stock-state authority. See [Inventory operator adoption contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#approved-final-traceability-refinements-and-operator-adoption-design--18-november-2026). This does not revise independent approvals or claim an implemented UI.

## Invoice reciprocal public interface — 18 November 2026

**Status:** Invoice conceptual design approved, INV-01–06 closed (18 November 2026); Logging's full contract is still unverified. [Invoice](../invoice/capability-record.md#reciprocal-contract-with-logging-audit-and-reporting) publishes minimised diagnostics for issue validation, number conflicts, provider timeout/unknown outcome, replay rejection and outbox/delivery errors with opaque correlation. Logging owns sinks, severity and delivery, never invoice records, source outbox or Audit proof. Full financial documents, personal/tax/bank details and provider secrets must be excluded. Logging absence never means an invoice was not issued; preserve business/audit resilience separately.

## Job position-only reciprocal interface — 20 November 2026

**Status: Conceptual, following owner-approved JOB-01–09, not an existing adapter.** **Job reciprocal conceptual input:** Job's position domain would send bounded, sanitised technical diagnostics (validation/revision conflict, operation failure, storage/outbox health and safe correlation IDs) through Logging's published port. Logging would own diagnostic sink/retention and may return delivery/health status, not position results or durable Audit evidence. No full position descriptions, confidential grade data or unneeded personal identifiers in logs. Job business operation remains owned by Job even when optional logging is unavailable. [Plain-English contract review](../../../reviews/job-public-contract-standards-and-gui.md); no published Logging root contract was verified.


## Recruitment reciprocal contract proposal — 20 November 2026

**Status: Proposed in [Recruitment draft PR #99](https://github.com/nuxt-layers/architecture-blueprint-review/pull/99), not owner-approved or implemented.** Recruitment supplies redacted diagnostics and correlation/health data; Logging must not collect CVs, protected characteristics or confidential assessments in routine logs. Cooperation uses published contracts/host ports, without private state or mandatory cyclic imports. [Recruitment record](../recruitment/capability-record.md).
