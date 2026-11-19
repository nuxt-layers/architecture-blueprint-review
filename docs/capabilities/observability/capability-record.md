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

## Cross-capability note — Observability versus Audit (14 November 2026)

**Established:** The governing catalogue distinguishes Observability's metrics, traces and operational health from Audit's proposed evidential record. **Proposed:** Observability may show Audit intake backlog, verification outages, coverage gaps and degraded state via [Audit](../audit/capability-record.md)'s owner-provided status; it cannot represent a healthy metric as proof of evidential integrity or ingest evidential content by default. **Open:** authorised diagnostic disclosures and critical alert routing. Observability's conceptual review remains incomplete.

## Cross-capability note — Asset operational signals (15 November 2026)

**Status: Proposed relationship only; Observability's conceptual review remains incomplete.** [Asset](../asset/capability-record.md) may expose aggregate latency, outbox backlog, Audit capture-pending count, provider degradation, failed transfer/reconciliation and inspection/renewal scheduler health. Observability owns metrics/traces and alert status, not asset lifecycle, diagnostic log records or evidence integrity. Do not disclose raw licences, people/contract terms or precise live-location telemetry; a healthy dashboard does not prove Audit receipt, inspection compliance or legal entitlement.

## Cross-capability note — Authorisation control health (15 November 2026)

**Status:** Proposed relationship; not a published Observability API. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) may expose aggregate decision latency, denied/unavailable counts, verified standing freshness, expiry/maintenance health, source outbox backlog, role/grant revision propagation and Audit capture gaps through safe operational indicators. Observability owns metrics/traces and alerts, not access decisions or evidence custody. Never emit full permission-policy predicates, sessions or sensitive resource attributes; a healthy metric does not certify tenant isolation, revocation or evidential completeness. Observability's conceptual review remains incomplete.

## Cross-capability note — Proposed Caching performance and invalidation health (16 November 2026)

**Agreed conceptual boundary; adapter unverified.** [Caching](../caching/capability-record.md) offers sanitised per-namespace/tenant-safe aggregate hit/miss/eviction/error rates, source freshness bounds, provider availability and invalidation lag/coverage. Observability owns time-series metrics, traces and alerts, not cache entries, source revisions or access decisions. Instrumentation must avoid keys, values, personal information and cross-tenant inference. An apparently healthy metric never guarantees Authorisation revocation or completed erasure. Degradation must be visible, not silently counted as healthy.

**Approved conceptual boundary (16 November 2026):** Observability consumes backend-independent, bounded measurements of live health, hit/miss ratios, latency, capacity, freshness and invalidation lag, and owns metric histories and alerts. Caching remains owner of contemporaneous operational cache validity; telemetry is not proof of revoked access or successful erasure.


## Cross-capability note — Clock and infrastructure time synchronisation (17 November 2026)

**Proposed relationship reflecting owner-approved Clock boundaries; Observability review incomplete.** [Clock](../clock/capability-record.md#owner-approval-and-ntp-governance-clarification-17-november-2026) provides temporal semantics and injected time source. Infrastructure operates the host's time synchroniser; Observability owns authorised live and historical source availability, offset/drift, uncertainty, synchronisation freshness, faults and threshold alerts, without claiming the server time is cryptographically verified from a hostname alone. Infrastructure's optional operator GUI may consume these metrics through an explicitly published read contract; Logging owns diagnostic records and Audit owns accountable administrative changes. Failure/degradation must be represented explicitly and not silently counted as healthy.

## Reciprocal note — Approved NTP source classes and operator diagnostics (17 November 2026)

**Clock boundaries approved; no implemented Observability adapter asserted.** [Clock's UTC-source policy](../clock/capability-record.md#approved-utc-source-classification-and-geographic-selection-17-november-2026) distinguishes national UTC laboratories, NTS-authenticated public services, and geographically routed community pools. Observability should expose authorised live and historical source health, applied source identity, authenticated/unverified state, measured offset, drift, uncertainty, synchronisation freshness, recent failures and alarms to Infrastructure's optional operator screen. Configuration governs source choice, Infrastructure operates synchronisation, Logging records technical faults and Audit receives privileged changes; a green status is not itself proof of cryptographically assured or legally certified time.

## Reciprocal note — CLK-03/CLK-04 trusted-time health and clock adjustments (17 November 2026)

**Agreed Clock relationship; no implemented read port asserted.** [Clock's final completeness review](../clock/capability-record.md#final-completeness-review--eight-concerns-resolved-17-november-2026) delegates time-source health, quality-measurement freshness, offset/drift/uncertainty histories, synchronisation loss, degraded/holdover status, restoration and clock-adjustment alerts to Observability using Infrastructure-originated telemetry. Publish only authorised, bounded health data to host/administrative consumers; an observed metric is not a cryptographic proof. Operational alerts cannot substitute for server-side policy checks on each security-sensitive operation. No raw cross-tenant clock data, secrets or private timestamps by default.


## Infrastructure reciprocal interface — 18 November 2026

**Proposed reciprocal review — 18 November 2026:** Infrastructure's [conceptual host status contract](../../../reviews/infrastructure-conceptual-architecture.md) supplies qualified resource readiness, provider health, UTC synchronisation quality and failure/recovery observations, with evidence age, source and explicit unknown/degraded semantics. Observability owns telemetry, metrics, alerts and historical presentation, not infrastructure control or provider truth. Pending INF-01/03/05; no Observability implementation is asserted.


## Logging dedicated-review reciprocal note — 19 November 2026

**Status: Proposed, non-normative; pending owner approval of LOG-01–LOG-08.** See [Logging conceptual public contract](../logging/capability-record.md#dedicated-logging-conceptual-review--19-november-2026).

**Proposed Logging PR #88 relationship:** Logging exposes bounded safe sink availability, accepted-versus-delivered status, backlog, loss/drop/retry, policy quality and correlated diagnostic references through public scoped status. Observability owns alerting, metric/tracing histories and health presentation, not log record custody. An alert or green chart is not an Audit receipt or proof of complete diagnostics. Exchange through host-composed ports/events without cyclic package imports.
