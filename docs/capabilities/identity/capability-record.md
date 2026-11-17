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

## Cross-capability note — Identity and Authentication (15 November 2026)

**Established:** Identity owns opaque principals, standing, tenants and memberships; [Authentication](../authentication/capability-record.md) independently owns credential verification, sign-in identifiers, assurance, sessions and revocation. Identity lifecycle changes requiring access withdrawal must reach Authentication through published IAM integration contracts. **Proposed:** reconcile authenticated principal standing, session revocation propagation, account recovery and service identity references with explicit failure guarantees. **Open:** measured revocation consistency and post-migration ADR-0012 interfaces. Identity's separate conceptual review remains incomplete.

## Cross-capability note — Authorisation decision inputs (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns roles, grants and access decisions; Identity owns principal standing, tenant, groups, memberships and governance facts. No group hierarchy or membership grants unrestricted access. **Proposed:** provide trustworthy, freshness-qualified standing and group-context facts, including suspension/departure invalidation, through public contracts and IAM composition. **Open:** effective revocation bounds, owner-role synchronisation and independently verified ADR-0012 composition. Identity's review remains incomplete.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Identity retains tenant, group, membership and digital group-owner source facts. Approved ORG-01–ORG-08 require secure self-service host-mediated provisioning and multi-context membership without exposing privileged tenant/bootstrap functions. Proposed TEN-03–TEN-08/OWN-01–05 add separately governed *tenant* parentage (not the existing single-parent group tree), active human tenant-owner floor, joint digital ownership, protected transfer/succession, evidence-based disputed recovery and creator provenance. Parentage must never automatically grant child-data access. Exact invariants require an accepted governing amendment; current implementation contract does not expose tenant hierarchy.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.


## Classification reconciliation — Tenancy is an Identity responsibility (17 November 2026)

**Established governing boundary:** Tenant identifiers, tenant isolation/governance, parent–child tenancy (ADR-0017), Identity groups and membership facts belong to Identity; there is no independent `tenancy` capability authority. This preserves the legacy Tenancy reciprocal Billing finding before that redundant candidate directory is eligible for removal.

**Proposed reciprocal input/output boundary:** Billing consumes a trustworthy tenant reference, tenant/entity association and relevant scoped authority where needed, but a tenant or Identity group identifier alone never proves a legal charge issuer, debtor, payer, bill-to party or customer/supplier counterparty. Identity supplies only its authoritative tenant, group and digital-governance references; verified legal-party/contract records require a separately designated owner, not Identity. Billing returns its own charge status and commercial references without modifying tenant or group lifecycle. Cross-tenant commercial queries, charges or exports require independent Authorisation and lawful disclosure checks. Missing or contradictory legal-party evidence holds the affected operation. No direct package dependency or implemented new port is asserted.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Identity owns local opaque principals, standing, tenants and memberships, not civil-identity/KYB verification or assurance that a person is adult, a company officer or authorised seller. Proofing and legal representation evidence owners remain open. If links to verified external identities are kept, require scoped issuer, status, retention and verified subject-binding; do not equate email/domain/group with company authority. Consult the cross-capability review before changing any IAM contract.
