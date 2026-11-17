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

## Cross-capability note — Authentication data and retention (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns sign-in identifiers, credentials, sessions and their security metadata; Privacy owns relevant retention and personal-data policy. **Agreed conceptual direction (AUT-11):** Authentication minimises collection, applies classified and lawfully bounded retention, cooperates in coordinated account closure and data-subject handling without transferring record ownership, and documents disclosures to external identity providers. Privacy requirements cannot be overridden by an optional provider. **Open:** exact data classes, retention periods and jurisdiction-specific obligations. Privacy's own conceptual review remains incomplete.

## Cross-capability note — Authorisation record minimisation (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns access records and changes, not Profile personal details; Privacy defines relevant rights, collection and lawful retention constraints. **Proposed:** minimise principal identifiers, decision and denial metadata; govern security evidence retention, subject export/erasure and legal holds without hiding critical access provenance or making indefinite storage the default. **Open:** precise lawful periods, evidence classifications and necessary restricted disclosures. Privacy's review remains incomplete.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking participation and guest-data interface (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) uses only necessary participant references, authorised contact/verification, acting-for proof and policy-constrained guest association; Privacy owns purpose, disclosure, lawful retention, data-subject rights and restrictions. Booking returns attributable correction/erasure/retention disposition without silently voiding lawful reservation history. Account closure, sensitive appointment metadata and guest access tokens require independent scoped handling, not unrestricted profile copies. No Privacy implementation contract is asserted.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Booking consumes lawful data-purpose, disclosure, retention and data-rights constraints for registered and guest participants; Booking retains only necessary party associations and returns attributable retention/correction/erasure disposition without silently rewriting reservation obligations. No currently implemented integration contract is implied.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Define and supply data-purpose/consent, cookie, retention, rights and lawful disclosure constraints to Identity governance and commercial onboarding; keep real-world authority evidence purpose-limited and protect disputed persons. Cookie/notice publication through Publisher is not consent enforcement. Owner recovery and data export must respect third-party personal data and legal holds.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Cross-capability note — Proposed Caching derived-copy lifecycle (16 November 2026)

**Agreed conceptual boundary; implementation unverified.** [Caching](../caching/capability-record.md) consumes applicable classification, purpose, retention/erasure, legal-hold and regional restrictions through published authority boundaries and supplies scoped deletion/eviction/reconciliation status with explicit partial completion. Privacy and Legal Compliance retain policy/obligation ownership; originating capabilities retain source records and disposition facts. Cached copies, restored snapshots and provider-held derivatives must respect privacy lifecycle and residency. Unverifiable provider compliance means refuse storage, not assume consent or compliance.

**Approved conceptual boundary (16 November 2026):** Backend independence never weakens region, purpose, retention or derived-copy deletion obligations. Caching supplies qualified purge/erasure progress and failure evidence through published interfaces; policy and legal authority remain with their owners, and Caching retains ownership only of cache validity and operational state.

