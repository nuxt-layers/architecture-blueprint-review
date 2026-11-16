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

**Proposed; no published adapter confirmed.** [Caching](../caching/capability-record.md) offers sanitised per-namespace/tenant-safe aggregate hit/miss/eviction/error rates, source freshness bounds, provider availability and invalidation lag/coverage. Observability owns time-series metrics, traces and alerts, not cache entries, source revisions or access decisions. Instrumentation must avoid keys, values, personal information and cross-tenant inference. An apparently healthy metric never guarantees Authorisation revocation or completed erasure. Degradation must be visible, not silently counted as healthy.
