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

## Cross-capability note — Authorisation governance notifications (15 November 2026)

**Status:** Proposed relationship, not a published Notifications consumer. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) can emit selected role/grant changes, approvals, overdue access reviews and security-relevant revocations with safe recipient/context references. IAM/Identity determines current eligible persons/approvers and Profile or an approved contact provider owns addresses. Notifications owns dispatch, delivery/retry and template rendering; sending is not approval, evidence acceptance, revocation completion or confirmation of human receipt. Notifications' conceptual review remains incomplete.

## Cross-capability note — Billing event notification and delivery status (15 November 2026)

**Proposed reciprocal interface, not an implemented Notifications contract.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) may supply deduplicable, versioned notice intents with source event, permitted recipient reference, locale and purpose (charge finalised, dispute outcome, exception). Notifications owns dispatch coordination and may return queued/sent/failed/delivery-unknown result; Mailer or another provider owns channel transport. Billing does not assert that an invoice was legally issued, payment received, notice delivered or viewed merely because an intent was sent. Invoice owns issued-document notice content. Recipients/preferences, mandatory statutory notice rules, sensitive fields, tenant boundaries and reauthorisation must be enforced. Notification outages do not roll back a committed charge but mandatory notices must remain visible/pending under policy.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking conceptual completeness note (15 November 2026; agreed review direction):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) sends minimised and tenant-scoped confirmation, change, cancellation, reminder and exception notification intent with booking event/version, authorised recipient reference, locale and delivery purpose. Notifications owns routing, templates and message-delivery lifecycle, returning accepted/pending/failed results without modifying booking state. Optional delivery failure does not cancel a confirmed reservation; contact verification required before confirmation stays an explicit Booking-side dependency. No confirmed Notifications implementation interface is inferred.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Booking supplies tenant-scoped confirmation, change, cancellation and reminder intent with booking event/version, recipient reference and purpose; Notifications owns delivery orchestration/status and does not alter Booking state. Optional delivery failure does not reverse a confirmed booking. Required verification is a separately checked condition. No currently implemented integration contract is implied.
