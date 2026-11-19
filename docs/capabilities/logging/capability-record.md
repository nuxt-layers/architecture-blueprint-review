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

---

# Dedicated Logging conceptual review — 19 November 2026

**Status:** Proposed, non-normative; owner sign-off pending. **Opening governing master:** `b920ce0d8b361de000a6739a16123dbdc56df7a7`; **opening blueprint master:** `6dac83a03da8704f7945ee1bc894f2248300445a`. **Review PR:** [#88](https://github.com/nuxt-layers/architecture-blueprint-review/pull/88). This dedicated section supplements, and does not supersede, the dated reciprocal notes above.

**Evidence classification.** **Established governance:** governing `docs/catalogue.md` classifies Logging as a **Foundation candidate** for structured technical logs, correlation and sinks; separate Audit = accountable security/business evidence; Observability = metrics, traces and health. `docs/security.md` §§6,9,16, `docs/privacy.md`, `docs/capability-standard.md` and accepted ADR-0001, 0008, 0012, 0016, 0017, 0018 govern boundaries, security, contract and policy. **Verified implementation:** direct `nuxt-layers/logging/CONTRACT.md` and `README.md` retrieval returned 404; organisation repository-name search returned no match. No Logging implementation, root contract, API, tests or user interface is verified. Related implementation contract claims remain **unverified**. Other existing notes are not automatically approved Logging behaviour.

## Purpose, classification and independent rationale

**Proposed Foundation capability**, potentially implemented as a small framework-independent logging service with optional Nuxt composition/presentation, not obligatorily as its own repository or a specialised log database. It gives server-side platform and domain producers one safe, consistent, provider-neutral technical diagnostic surface. It applies validated classification, correlation, minimisation/redaction, bounded delivery, retention/access controls, routing and sink-status accounting. The basic native service remains useful with a host-supplied local bounded sink and no cloud vendor.

**Authoritative ownership:** Logging owns the *sanitised diagnostic record it has accepted*, its normalisation and delivery/retention policy, sink routing and technical delivery state, protected diagnostic search/export and operational health assertions qualified by evidence freshness. It does **not** own the truth of the underlying business outcome, originator events/outboxes, access decisions, credentials, incident adjudication, financial records, or other source facts. It cannot certify completeness of all producer activity unless a separately defined bounded coverage handshake actually proves it. Lossy technical diagnostics are never used as substitute for critical Audit guarantees.

**Explicit exclusions:** Audit owns accountable, integrity-checked evidence and investigations/review of that evidence; Observability owns metrics, traces, health histories and alert decisions; Infrastructure/host owns deployment plumbing, time synchronisation and provisioned resource availability; Configuration owns approved scoped settings, not Logging's validation; Privacy/Legal Compliance own specialist constraints; domain producers own their failures and operation results; Integrations owns third-party connection/adapter lifecycle. Logging is not a general event bus, workflow engine, business event store, SIEM certification or universal customer-data search index.

## Native service, lifecycle and failure

A record flows **received → authenticated/context-checked → schema/purpose/classification validated → sanitised → accepted for configured delivery / rejected → buffered or persisted where configured → delivered / retrying / exhausted / dropped / uncertain → expired/erased or legally constrained**. These are distinct states; `accepted` is not proof of remote sink durability, and `delivered` is not proof of business action or Audit custody.

Native services: (1) structured bounded severity/category taxonomy with typed source code and attributes, (2) correlation/causation and time metadata without secret-bearing spans, (3) allowlist-first sensitive-field filtering with documented redaction failure treatment, (4) producer/tenant/namespace/rate controls and anti-injection safe encoding, (5) deterministic sink routing and configurable local fallback, (6) delivery status, overflow/drop counters and safe operator notices, (7) scoped diagnostic query and controlled retention/export, and (8) health/recovery reports including blind spots. Filters must run **before** forwarding to third-party sinks; secrets found after leakage require incident handling and downstream purge/revocation where possible.

Default service failure is **non-blocking to ordinary business operations**, with explicit degraded health and bounded loss; mandatory security/audit preconditions remain the producer/Audit owner's responsibility and must fail closed in their own contract where required. Never silently mark an unverified sink as healthy. No unbounded memory queue or infinite retry. Avoid recursive logging of the sink's own failure: use a separate bounded emergency counter/status channel. Host shutdown flush is best effort with finite deadline, not an exactly-once promise.

## Idealised public inbound contract

| Input source / class | Supplied facts or intent and validation | Requirement; missing, stale, conflicting or invalid semantics |
|---|---|---|
| Server-side capability/host **submit diagnostic** | Typed code, severity, purpose, safe structured fields, component/operation, originating timestamp, opaque correlation/causation and tenant/owning scope when applicable; producer provenance and declared sensitivity; no arbitrary sensitive payload | Core input; authenticate trusted producer via host-composed port; reject malformed/oversized/unclassified/unsafe events with stable reason, never try to parse a business outcome as permission; missing optional context marked unknown |
| **Host runtime and infrastructure context** | Trusted source identity, process/deployment/environment reference, server-resolved tenancy, request trace IDs, host-provided clock/time uncertainty, available sinks/capacity | Required where relevant; caller-provided tenant IDs cannot grant scope; missing trusted clock or sink creates explicit time-quality/availability degradation, not fabricated certainty |
| **Configuration / authorised administrator** | Validated scope, severity thresholds, category allowlists, sampling, retention, sink routes, data-region/export constraints, policy revision and effective time | Conditional; validate against non-configurable security/privacy floors, deny unsafe overrides, apply versioned changes at effective time, preserve prior policy for record provenance |
| **Privacy / Legal Compliance** | Purpose/necessity, retention/deletion and lawful preservation constraints, applicable jurisdiction, legal evidence references and effective version | Conditional according to processing; absent/conflicting mandatory constraints block unsafe retention/disclosure, not all unrelated system activity; never self-assert a legal exemption |
| **Authorisation / Authentication / Identity** | Server decisions, caller assurance/recency, tenant/group ownership and allowed resource scopes | Required for protected query/export/change/delete operations; deny when unavailable, invalid or stale beyond accepted bound; no implicit parent-tenant visibility |
| **Provider adapters / sink acknowledgements** | Provider target, attempt key, receipt/offset if meaningful, retryability, capacity, rejection and verifiable delivery result | Optional external providers; unknown or timeout remains uncertain and may be retried idempotently where supported; never invent final receipt |
| **Clock** | Canonical occurrence/receipt time and timezone semantics plus available source-quality status | Required temporal semantics, host-supplied clock; distinguish origin timestamps from server receipt; bad/missing time quality is explicit |
| **Privacy-rights/retention action** | Qualified scope, eligible record selectors, hold/restriction status, authorised request and effective policy version | Conditional protected command; denied if legal hold or authorisation unknown; acknowledge actual removal/restriction only after completed action |

**No unrestricted browser-origin direct write surface.** Browser faults may reach Logging only via the host's authenticated, purpose-limited, throttled and sanitising collection adapter, if enabled. Enforce server validation and never trust a client-supplied severity or actor identity.

## Idealised public outbound contract

| Public output | Consumer and meaning | Authoritative guarantee and limitations |
|---|---|---|
| **Submit result / diagnostics receipt** | Originating capability/host: accepted, rejected, rate-limited, unavailable or uncertain, stable reason and opaque receipt reference | Logging's *own intake decision only*; remote delivery and domain/Audit outcome are separate |
| **Authorised diagnostic query** | Scoped operations/support users and permitted source owners: bounded filter by tenant, source, severity, category, correlation, time and state | Minimised records with source/receipt times, policy/schema version, sink status, completeness/freshness caveats and redaction; only within explicit authorised resource scope |
| **Delivery/status and coverage view** | Observability/Infrastructure and host: sink ready/degraded/unavailable, queue age, loss/drop sampling, retry backlog and policy/clock quality | Technical measured state, age and unknown/partial coverage; no claim that all business/audit events were collected |
| **Protected export / retention result** | Authorised operator, Privacy/Legal Compliance where applicable: qualified records, lineage, redaction, requested scope, completed/pending/blocked/uncertain | Export is a Logging-derived diagnostic package, never evidence-grade Audit export; legal hold/erasure outcome must be accurately recorded |
| **Committed administrative lifecycle notifications** | Optional Audit/Observability subscriptions via host-composed ports: sink configuration changed, retention action, redaction failure, diagnostics pipeline degraded/recovered | Only after Logging-owned committed change and through owned durable outbox **when downstream receipt is required**; not a replacement for producer-owned significant-event outboxes |
| **Safe developer-facing error codes** | Host and capability clients: invalid schema, forbidden, unsafe field, over limit, sink unavailable, status unknown | No stack trace, protected payload or provider secret in public error |

## Commands, queries, events and context invariants

**Commands:** `submitDiagnostic`, `configureRoutingAndRetention`, `requestScopedExport`, `applyRetentionOrErasure`, `retryEligibleDelivery` and `acknowledgeOperationalWarning` (conceptual names only). Each states caller scope, validated intent, record/policy revision as needed, idempotency reference, accepted-vs-completed outcome and refusal/unknown errors. A producer may not alter another producer's records.

**Queries:** `readDiagnostics`, `readDeliveryState`, `readPipelineHealth`, `readEffectivePolicy` and `readRetentionStatus`; protected reads require server-side Authorisation, least privilege, bounded pagination/window, data minimisation and source/tenant partitioning. Availability/coverage are never silently complete.

**Events:** bounded committed Logging-owned configuration, sink-health threshold transition, enforced retention and eligible protected access/export outcomes may be published where downstream coordination is required. Delivery is **at least once / replay-tolerant** when backed by an outbox, not distributed exactly once. Routine debug lines are not general domain events. Critical audit-worthy Logging administration events require an independent producer-owned outbox/Audit path even if the log sink fails.

**Shared context:** trusted tenant and owner group, authenticated service/actor where legitimate, Authorisation scope/assurance for privileged actions, originating capability and version, operation/source reference, correlation/causation and idempotency key, safe severity/category, policy version and effective time, clock quality, sensitivity/purpose, sink/provider provenance, intake versus delivery outcome. Not a mandatory universal request object. Source and receipt timestamps are distinct. Every persisted row, index and exported item respects isolation and regional obligations. No hidden cross-tenant aggregate disclosure.

**Versioning:** typed diagnostic envelope and code registry are versioned; schema evolution maintains safe compatibility. Removal or semantic change is a contract change. Sanitisation policy changes affect future records prospectively; historical records retain applied-policy provenance subject to rights, lawful preservation and qualified redaction.

## Cross-capability cooperation and acyclic integration

| Owner / relationship | Logging needs | Logging supplies; authority and failure |
|---|---|---|
| **Audit** (optional reciprocal), distinct mandatory security event paths | Only protected diagnostic metadata if independently approved; never raw evidence | Sanitised service failures and correlations; Audit owns evidence custody/integrity, Logging owns sink receipt; avoid mutual imports via published host ports/outboxes |
| **Observability** (optional) | Optional independent health alert/trace references | Pipeline health, loss/lag/retries, bounded correlations; Observability owns metric histories/traces/alerting; outages separately visible |
| **Identity / Authentication / Authorisation** (security-critical query dependency) | Trusted producer/actor/scope/assurance and authoritative access decisions | Sanitised IAM fault/latency/denial codes; no credentials/decision ownership; unavailable Authorisation denies protected operations |
| **Configuration** (optional administration integration) | Approved scoped settings and revision/effective time | Validation/status and change diagnostics; Configuration is not Logging policy-enforcement authority |
| **Clock** (semantics required) | Source and receipt time semantics, quality limits | Clock-quality anomalies and safe correlation; Infrastructure handles NTP, Observability monitors drift |
| **Privacy / Legal Compliance** (conditional normative constraints) | Purpose, minimisation, retention, lawful hold/restriction and qualified applicability | Rights/retention completion or uncertainty; neither Logging nor technical policy decides legality |
| **Infrastructure / host** (composition required) | Bounded sink, durable storage if configured, secret supply, health surfaces, regional placement, recovery | Sink and queue status; host owns environment/provider deployment, not Logging record semantics |
| **Integrations** (optional provider adapter) | Approved third-party connection/transfer permissions and adapter lifecycle | Routing, retry and delivery diagnostics; provider acceptance is not business completion |
| **Message Queue / Scheduler / Workflow** (optional) | Host-composed delivery/retry or scheduled lifecycle operations where justified | Typed delivery/retry errors and bounded status; no required new MQ, scheduler or workflow runtime for native Logging |
| **Reporting / Search** (optional) | Scoped derived-view request and disclosure rules | Sanitised aggregates/diagnostic references only; Reporting owns reports; Search cannot bypass live access or become the log store |
| **Domain capability producers** (optional port) | Typed safe diagnostics, source identity, purpose and context | Submit result, safe diagnostic inquiry; source owns business state, event outcomes and outbox guarantees |

**Absence behaviour:** optional producer-to-Logging ports may be absent without changing producers' native business contract; an explicitly enabled Logging deployment still requires safe local sink/capacity or declares itself unavailable. External exporters, APM, tracing backends, remote search and SIEM are optional. Avoid direct dependency cycles by composing shared public contracts at host; do not import each producer implementation into Logging.

## Security, privacy, operational policy and storage

- **Secret exclusion:** never log credentials, passwords/verifiers, tokens, API keys, private signing material, passkeys, recovery codes, session cookies or payment instrument data. By default exclude raw request/response bodies, query strings, arbitrary user-entered content, email/phone/address, sensitive URLs and policy predicates. Restrict IP/user-agent/device/location identifiers to explicitly justified, minimised cases. Hashes can still be identifiers; hashing alone does not make information anonymous.
- **Pre-sink controls:** safe allowlists, structured encoding, length caps, log-forging/injection resistance, safe exception typing, deterministic redaction and tests with seeded secrets; prevent tenant-label spoofing, malicious cardinality, amplification and diagnostic denial of service. Do not expose internal stacks or arbitrary dynamic queries to untrusted viewers.
- **Access:** server-side, resource-aware Authorisation for all protected reads, exports, erasure/hold operations and policy changes; separation of platform operator, tenant-scoped support and source owner; privileged export/retention changes require heightened assurance and accountable Audit evidence. Tenant parentage and host admin roles never grant automatic customer access.
- **Retention:** differentiated by purpose/classification, minimal default retention and expiry, regional placement, backup lifecycle, erasure/restriction propagation and lawful preservation as qualified by Privacy/Legal Compliance. A tenant cannot override mandatory statutory/security constraints; operators cannot arbitrarily disable mandatory evidential flows by turning Logging off.
- **Storage:** a future implementation must publish actual host-supplied sink/store inventories, isolation, exact data and retention in root `STORAGE-REGISTER.md` and standalone `CONTRACT.md`; no invented database, cloud service or retention duration is asserted. Core diagnostics may be ephemeral, but persistent sinks trigger the governing store requirements.
- **Time and reliability:** use Clock semantics and distinct producer/ingestion/delivery timestamps; do not claim synchronised trusted UTC without quality evidence. Capture protected configuration changes in Audit by a separate reliable mechanism. Verify finite buffering, backpressure, loss visibility and process restart semantics.
- **Data protection:** lawful bases, DPIA/notice/consent where applicable are jurisdiction-specific determinations; Logging does not grant itself blanket consent exemptions. External sink transfers require provider, purpose and region approval, plus verified deletion/withdrawal behaviour. No regulatory certification is claimed.

## GUI and headless integration

**Headless operation is primary**. **Optional restricted diagnostics console**, mounted via the host's sidebar → Logging dashboard pattern only for authorised operational personnel; no ordinary end-user menu by default. Sections: time-bounded searchable diagnostic list with safe correlation navigation; source/category/severity filters; sink delivery/queue/drop health and uncertainty; redaction/retention policy versions; approved sink configuration; protected export and retention actions with confirmations and attributable Audit trail. Distinguish view/search role, tenant-scoped support, deployment operator and platform super-administrator; **deployment-wide sink configuration and protected cross-tenant diagnostics restricted to host super-administrators**, with exceptional customer access separately scoped and recorded. Technical diagnostics screens must not expose secrets or Audit evidence by default.

Apply server-side access before data retrieval; hide unavailable actions only as UX convenience. Use Theme Manager tokens and shared UI, WCAG 2.2 AA, keyboard/screen-reader operation, accessible status and uncertainty cues, BCP 47/CLDR messages and Clock formatting, responsive desktop/tablet layouts. The host owns navigation; Logging provides public read/actions, never browser access to internal stores. Representative host is `nuxt-layers-test/application-test-template`; no GUI is implemented or verified.

## Conceptual contract acceptance scenarios

| Input → behaviour | Output → authoritative owner |
|---|---|
| Trusted producer submits safe, typed diagnostic → validate/sanitise and queue to bounded local sink | Accepted receipt with independent delivery status → Logging; operation result remains producer-owned |
| Invalid schema, oversized payload or secret-bearing field → reject or apply provably safe configured field policy | Stable reason with no leaked payload → Logging |
| Caller attempts other tenant's diagnostic query/export → deny before query; no count/timing inference beyond authorised bounds | Forbidden, no records → Authorisation decides; Logging enforces |
| Sink unavailable after intake → finite retry/drop; distinguish accepted from delivered and mark unknown | Explicit backlog/loss/uncertain status → Logging, optional Observability presentation |
| Producer retries with same idempotency reference → documented dedupe scope or safe duplicate presentation | No invented exactly-once claim; receipt/delivery status → Logging |
| External sink acknowledges then times out response → reconcile if possible without assuming delivery | Uncertain delivery and provenance → Logging/provider evidence |
| Logging sink down during business transaction → no fabricated rollback or Audit receipt | Source transaction outcome unchanged; producer/Audit guarantees independent |
| Audit unavailable but Logging healthy → do not certify security evidence | Independent Audit gap/failed evidence → Audit; Logging healthy only for own pipeline |
| Retention expiry or qualified erasure with no hold → delete/anonymise within declared lifecycle; export respects restriction | Completed/pending/blocked/unknown, immutable outcome evidence where required → Logging/Audit respectively |
| Clock degraded, timestamps conflict or source stale → retain qualified times and show uncertainty | Provenance and unknown timing confidence → Clock/Logging |
| Unauthorised user requests routing changes or global diagnostics → refuse, optionally emit safe denial | No policy change; Authorisation decision plus Audit-worthy attempt |
| Customer requests raw tokens, Audit evidence write, business reversal or universal cross-tenant export → refuse unsupported action | Explicit unsupported/forbidden result → source, Audit and IAM remain owners |

## Proposed decision register — owner approval required

- **LOG-01 — Foundation capability boundary:** adopt a distinct contract-owning technical diagnostic Foundation capability, irrespective of independent repository or Nuxt packaging. **Recommendation: approve.**
- **LOG-02 — Native mode:** host-composed bounded local sink by default; external log service optional, provider-neutral and not a prerequisite. **Recommendation: approve.**
- **LOG-03 — Logging/Audit/Observability split:** evidence-grade assertions go to producer-owned outbox and Audit; Logging owns diagnostic intake/delivery; Observability owns metric/trace/alert aggregation. **Recommendation: approve.**
- **LOG-04 — Record taxonomy and safe intake:** versioned typed codes, allowlist-first sanitisation, authenticated server producers, bounded client adapter only when explicitly configured. **Recommendation: approve.**
- **LOG-05 — Reliability and backpressure:** non-blocking best-effort default for normal diagnostics, finite buffers/retries, observable loss, independent mandatory evidential flows, explicit accepted-versus-delivered states. **Recommendation: approve.**
- **LOG-06 — Governance:** purpose-sensitive retention, regional and data-rights constraints; tenant-scoped authorisation and non-overridable security floors; policy provenance. Exact durations and provider selection are deployment-specific. **Recommendation: approve.**
- **LOG-07 — GUI:** headless first; optional role-controlled console, with installation-wide privileged administration reserved to host super-administrators and no inferred child-tenant access. **Recommendation: approve.**
- **LOG-08 — Event/export interface:** only Logging-owned committed admin/lifecycle facts via an outbox where necessary, and safe scoped exports; no general business-message bus. **Recommendation: approve.**

**Open technical and implementation follow-ups (not owner conceptual decisions):** specific TypeScript/public entrypoint and stable error vocabulary; envelope field classification table and severity registry; safe emergency fallback and end-to-end drop accounting; provider-neutral sink adapter contracts and data-region controls; per-purpose retention schedule with legal review; actual `CONTRACT.md` and `STORAGE-REGISTER.md`; security threat model; secret-canary/isolation and failure-injection tests; host composition/GUI accessibility acceptance. Confirm cross-capability port names and relevant active PRs without turning conceptual interfaces into invented runtime APIs.

**Sign-off:** LOG-01–LOG-08 are **proposed only**, not owner-approved. This conceptual design is ready for owner evaluation but is **not** published implementation, accepted architecture change or authority to merge.
