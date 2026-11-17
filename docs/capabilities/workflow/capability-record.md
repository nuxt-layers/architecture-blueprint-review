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


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Workflow may orchestrate approver work and return verified decision evidence; Configuration owns its own request/decision/activation lifecycle, risk evaluation and final revalidation. Workflow failure remains pending, not approved. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed contract alignment in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not a completed workflow review, normative rule or implementation change. See [Content Editor conceptual boundary](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Content Editor may show Publisher-bound review/approval states and invoke permitted source requests; Workflow retains review routing and sign-off authority, Publisher validates approval digest/version before publishing. The editor cannot interpret an old approval as current.
