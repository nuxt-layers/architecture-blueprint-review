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

## Cross-capability note — Billing commercial charges versus payment execution (15 November 2026)

**Proposed reciprocal interface, not a completed Payment Gateway review.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) may provide charge ID/amount/currency and a separately authorised collection intent when a valid payment workflow exists. Payment Gateway owns credential handling, authorisation, capture, payment/refund execution and provider read-back; Billing consumes only verified statuses, idempotent transaction references and permitted exceptions. Accounting remains authoritative for ledger posting and settlement reconciliation; a finalised charge is neither a captured payment nor recognised revenue. Unknown gateway response requires provider reconciliation before retry, and a commercial credit does not itself transfer a refund. Collections, dunning, split settlement and payout owner/policy require separate review.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy refinements proposed, implementation not assumed.

Own verified payment-provider authorisation/capture/refund/unknown outcome, never trust checkout success redirect. Return attributable evidence to Order/Subscription/host onboarding; repeated callbacks require idempotency and read-back.

See [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md) for conceptual inbound/outbound authority, absence, failures and acceptance. No package dependencies inferred.
