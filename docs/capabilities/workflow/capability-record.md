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
