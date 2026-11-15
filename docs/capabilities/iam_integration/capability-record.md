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

## Cross-capability note — Authentication suite choreography (15 November 2026)

**Established:** The IAM suite composes the separate public contracts of [Authentication](../authentication/capability-record.md), Identity, Authorisation and Profile; it does not take ownership of their records. **Agreed conceptual direction:** coordinate account provisioning, suspension/closure and revocation, recovery, service-identity governance, data-subject operations and emergency account lifecycle without private imports. Preserve assurance, recency, session revocation, fail-closed behaviour and ADR-0012's single-call composition objective. **Open:** bounded revocation consistency and verified integration contracts. IAM integration's individual conceptual review remains incomplete.

## Cross-capability note — Multi-step IAM accountability (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** IAM Integration coordinates distinct Authentication/Identity/Authorisation/Profile operations without reowning their facts. **Proposed:** approved multi-step provisioning, suspension, step-up, delegation, recovery and account closure retain source identifiers/correlation and independently qualified receipt status in [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026). The suite must not create a synchronous circular Audit dependency or substitute Audit evidence for originating IAM decisions. Its conceptual review remains incomplete.

## Cross-capability note — Authorisation composition and revocation (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns policy evaluation, role/grant records and access decisions; IAM Integration coordinates trusted Identity and Authentication inputs without taking ownership. **Proposed:** harmonise single-call ADR-0012 composition, role synchronisation, approval choreography, assurance/freshness, emergency restrictions, revocation and retryable cross-capability delivery. **Open:** measured consistency, direct privileged operation trust and no-cycle event choreography. IAM Integration's review remains incomplete.
