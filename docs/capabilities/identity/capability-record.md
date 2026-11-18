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


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Verification is now an owner-approved *candidate* for claims and issuer-status lifecycle. Identity continues to own opaque local principals, tenant/group memberships and standing; a civil identity, age or company verification claim does not create, merge or alter these automatically. Verify local subject bindings through public contracts and minimise third-party evidence.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); not an accepted public contract. See [conceptual record](../comments_engine/capability-record.md).

Comments Engine uses stable Identity subject/tenant/group references and status-change signals but never duplicates identities, personal data, group membership or representation. Source-owned author attribution must honour revocation, erasure and tenant isolation. Guest and remote identities require separately defined trust/provenance, not fabricated local identity records.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Identity owns trusted tenant/group/account IDs, memberships, ancestry and closing state; Configuration consumes those facts to scope its own settings and history. A setting never grants membership or authorisation, and unknown/closing scopes block protected changes. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-05/06 (Options B/C):** Identity remains authoritative for account and resource-associated tenant/group identities, membership, group lifecycle and any registered group ancestry; Configuration does not create an alternative user profile or generic resource hierarchy. Resource-specific settings require their *own domain's* stable resource identifier and lifecycle/authority checks.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.

## Employment reciprocal conceptual interface — 17 November 2026

**Status: Proposed in [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59), not an Identity API amendment.** Identity owns principals, tenant/group structures, membership and digital governance, none of which proves employment or legal employer-of-record. Employment consumes scoped standing and identifier facts and provides dated worker-engagement status signals; departures must coordinate revocation and access reviews through published IAM contracts rather than silently deleting memberships or sessions. Tenant/group identifiers do not establish the employing legal entity. Access to remuneration/personnel records requires separate Authorisation and Privacy checks. See [Employment public contract](../employment/capability-record.md).

## Cross-capability review note — Enrolment (owner-accepted conceptual)

**Enrolment reciprocal interface (owner-accepted; 18 November 2026; [Enrolment review PR #60](https://github.com/nuxt-layers/architecture-blueprint-review/pull/60)).** Identity supplies stable learner/guardian/representative identity references and independently verified authority where supported; Enrolment owns educational admission state, not Identity group membership, tenant hierarchy, guardian relationship or permission. Host-composed scoped authorised lookups must avoid student-data duplication or implied cross-tenant access. Guardian proof and eligibility remain conditional, provenance-bearing. This note is non-normative and cannot claim new Identity published APIs.


## Reciprocal conceptual note — IAM Integration (18 November 2026)

**Status: Proposed under [IAM Integration draft PR #73](https://github.com/nuxt-layers/architecture-blueprint-review/pull/73); not a new published implementation contract or owner approval.** Identity remains authoritative for opaque identifiers, group/tenant/membership lifecycle, owner governance, pending changes and source outbox. IAM Integration consumes only its public directory, lifecycle, governance and outbox surfaces; it supplies verified Authentication-subject and Authorisation-decision adapters, status/reconciliation and coordinated calls. Revocation and tenant restriction must remain safe under delivery delay; this note does not introduce an Identity dependency on the integration package. See [IAM Integration conceptual public contract](../iam_integration/capability-record.md).
