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

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking resource discovery interface (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) offers minimised, tenant-scoped, versioned reservable-offering and availability hints for Search indexing. Search may provide candidate discoveries and index freshness/error status, but does not guarantee current capacity, guest disclosure rights or final reservation success. Booking must revalidate authoritative availability and permissions at hold/confirmation; stale/missing index cannot block direct native Booking. Avoid exposing bookings/guest identities in public search indices.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Search indexes minimal, authorised reservable offerings and availability hints; index freshness/coverage must be explicit. Search never confirms slots or grants guest visibility. Booking rechecks live capacity and permissions before committing; Search outage does not block native booking. No currently implemented integration contract is implied.

## Reciprocal decision — redundant Document capability retired (17 November 2026)

**Owner-approved resolution, 17 November 2026:** no separate Document record owner will supply another indexing stream. Search consumes authorised projections from Publisher and the applicable domain record owners and rechecks current access before protected retrieval; a search hit does not grant disclosure. Historical conditional review: [Document](../../../reviews/document-directory-removal-2026-11-17.md).

## Federation — reciprocal conceptual contract (18 November 2026)

**Status: Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69); not an approved implementation API, and does not complete this capability's independent review.** [Federation public contract](../federation/capability-record.md#independent-review-contract-completeness-and-authority-18-november-2026).

Search receives only Federation-validated, locally admitted, provenance-bearing public descriptors plus revision/expiry/withdrawal notifications, via published ingestion ports. Search alone owns derived index application, ranking, result visibility and staleness display. A result does not confer source authority, current availability or resource access; unknown source/withdrawal status is labelled and reconciled. Hub discovery is a host composition, not a Federation query engine. All cooperation is via public, directional host-composed contracts with scoped failure/absence semantics; preserve existing approvals and avoid package dependency cycles.
