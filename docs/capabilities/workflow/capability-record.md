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

## Cross-capability note — Authorisation versus process approvals (15 November 2026)

**Status:** Proposed reciprocal; [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) owns permission checks and access-role/grant change governance, while Workflow owns any independently justified business process execution/approval choreography. Task assignment or a workflow step never silently grants a role; a permission decision does not mean business approval was completed. Authorisation's approved change and step-up/approver requirements remain in its own contract; cross-capability coordination uses explicit interfaces and no cycles. Workflow's conceptual review remains incomplete.

## Cross-capability note — Billing approval and charge-finality boundary (15 November 2026)

**Proposed reciprocal interface, not an implemented Workflow dependency.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) may request material waiver, credit, override, authority transfer or dispute approval with opaque charge reference, amount/risk class, policy version, required decision deadline and separation-of-duties constraints. Workflow/Process owns routing/task state and returns attributable approved/rejected/expired/pending outcome and approver/delegation references; Authorisation still supplies effective access decisions, and Billing owns the commercial transition and validates result, currency/limits, expiry, version and critical Audit policy before finality. Workflow unavailability holds actions dependent on mandatory approval but must not disable ordinary independent Billing. Neither engine nor a specific Temporal adapter is mandated.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking approval and recurrence interface (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) may require a versioned and expiry-bound approval for reserved capacity. Workflow coordinates approval routes/assigned work and returns attributable approved/rejected/delegated/expired outcomes; Authorisation decides who qualifies; Booking rechecks capacity and eligibility before confirmation. An approval cannot itself reserve capacity or extend a hold indefinitely. Delayed/revoked authority is rechecked. No mandatory Workflow runtime is imposed on bookings without approvals.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Workflow coordinates requested Booking approvals and returns versioned decision/expiry/delegation evidence; Authorisation decides the approver's authority and Booking revalidates resource capacity before confirming. Approval alone does not confirm or reserve capacity. No currently implemented integration contract is implied.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Coordinate high-risk approvals, succession/recovery, policy activation, paid onboarding, confirmed payment-to-entitlement-to-provisioning, retries and compensation using owner commands/results. Own execution/checkpoint state only, never Identity tenancy, legal applicability, Order commitment, Payment settlement, Subscription entitlement or domain record truth. Duplicates/out-of-order signals must reconcile, not repeat a charge or tenant creation.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course requests configured revision review and consumes approval evidence; Workflow owns process choreography, Course alone commits publication after permission and safety checks. An approval task is not learner admission. This note does not complete the separate workflow review.

## Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)

**Status: Owner-agreed boundaries, no independently completed workflow review or implemented API.** [Course](../course/capability-record.md) and [Assessment candidate](../assessment/capability-record.md): **COURSE-11 agreed:** Workflow coordinates configured course review, sign-off, migration and qualification review *processes*, not Course publication state or awards. Course validates approval evidence and commits its own publication transition after Authorisation and required legal/content-safety gates. The approval workflow cannot create external award authority.
