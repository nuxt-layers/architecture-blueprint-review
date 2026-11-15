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
