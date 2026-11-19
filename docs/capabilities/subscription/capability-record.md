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

## Cross-capability note — Subscription versus Billing (15 November 2026)

**Agreed conceptual relationship: BIL-02 approved on 15 November 2026; implementation remains unverified.** [Subscription](../subscription/capability-record.md) owns plan/entitlement, approved subscription start/end, pause, renewal and cancellation state. [Billing](../billing/capability-record.md#idealised-public-inbound-contract) consumes versioned subscription facts and owns period assessment, rating, prorating, billing-run results and charge state. Billing supplies charge/status references but cannot grant or revoke entitlements; Subscription does not assert invoice issuance or settlement. Disputed/out-of-order changes require explicit effective-date policy and reconciliation. No implementation dependency has been authorised.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy refinements proposed, implementation not assumed.

Own versioned feature, tier, seat, storage and renewal entitlements for service-consuming tenants; not memberships, payments or technical provision. Bill-to party may differ from tenant. Publish explicit pending/effective/expired states for scoped activation.

See [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md) for conceptual inbound/outbound authority, absence, failures and acceptance. No package dependencies inferred.


## Reciprocal conceptual interface — Membership (19 November 2026; draft PR #93)

**Status: proposed, not owner-approved or implemented; this does not complete the subscription review.** [Membership](../membership/capability-record.md) is a candidate *scheme participation* domain distinct from Identity group membership, Subscription plan entitlements, commercial settlement and application access. Subscription owns its separate subscription plan, renewal and entitlement state; Membership owns admission, scheme terms and participation/benefit qualifications. Either may supply versioned public facts to the other as needed, never duplicate term authority or equate a scheme renewal request with subscription activation. Consume only published public interfaces; no direct package dependency is inferred. Missing, stale, contradictory or unauthorised evidence must not be promoted into confirmed outcomes.
