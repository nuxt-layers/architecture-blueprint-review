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

## Cross-capability note — Authorisation-aware discovery (15 November 2026)

**Status:** Proposed reciprocal; Authorisation's existing contract publishes `listAuthorisationVisibleGroups`, not universal permission for returned records. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) can supply verified visible group scopes for Search to prefilter results; the domain/resource owner supplies authoritative per-item attributes and permissions. Search owns derived indexing and query behaviour, and must constrain pagination, snippets, facets, aggregates, caching, tenancy and export to avoid indirect disclosure. Per-item action checks and revocation remain required. Search's conceptual review remains incomplete.

## Cross-capability note — Billing charge discovery versus authoritative reads (15 November 2026)

**Proposed reciprocal relationship, not an implemented Search connector.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) can publish a minimised, versioned, tenant/party-scoped search projection and invalidation events; Search owns derived indexing, ranking and permitted query results, not authoritative charge/period state. A search hit is only a discovery reference: Billing independently authorises the detail read, field disclosure and current state. Stale indexes, revoked access, held corrections, tenant separation and sensitive customer references must not leak through suggestions, counts, facets or snippets. When Search is unavailable Billing's own authorised queries remain available; index freshness and uncertainty should be explicit.
