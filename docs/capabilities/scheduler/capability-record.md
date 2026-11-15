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

## Cross-capability note — Authorisation expiry and review maintenance (15 November 2026)

**Status:** Proposed optional scheduling interaction. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) already publishes `runAuthorisationMaintenance` for expiring assignments/changes and reporting overdue reviews. Scheduler may trigger and monitor idempotent maintenance using trusted server composition, but must not own access policy, role state or grant an expired permission because the maintenance job was delayed. Every decision still checks effective expiry and standing. Scheduler's review remains incomplete.

## Cross-capability note — Billing run scheduling and idempotent execution (15 November 2026)

**Proposed reciprocal interface, not an existing Scheduler adapter.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) owns billing periods, due-run eligibility, commercial state and duplicate finalisation protection. Scheduler may submit a permitted due-cycle trigger with scope, stable job/idempotency key, scheduled/actual time and retry context, and receive run accepted/held/completed/failed status and next-due hint; Clock owns date/time-zone/period semantics. Overlapping, late or repeated triggers cannot charge a period twice. Scheduled execution never bypasses Billing's own authorisation, rate evidence or audit-capture guarantees; standalone/manual Billing remains possible without Scheduler or a specific backend.

## Cross-capability note — Booking expiration and reminders (15 November 2026)

**Proposed reciprocal relationship; no Scheduler interface is assumed to exist.** [Booking](../booking/capability-record.md) owns hold expiry, eligibility for transition, booking status and idempotent maintenance action. Scheduler may invoke a due handler and report execution attempts, providing scheduled/actual time, tenant scope and stable operation identity; Booking returns accepted/expired/no-op/failed status and next-due hints. Delay or absence of Scheduler does not extend an expired hold: Booking validates time and state on its own commands and reads. Clock supplies temporal semantics. Reminder sending is separate from authoritative expiry.
