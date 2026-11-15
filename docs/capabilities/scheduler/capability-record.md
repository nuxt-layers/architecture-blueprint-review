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
