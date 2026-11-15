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
