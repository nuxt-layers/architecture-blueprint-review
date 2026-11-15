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

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking recurrence and time-zone semantics (15 November 2026):** [Booking](../booking/capability-record.md#recurring-reservations--booking-owns-the-series-not-scheduler) owns optional recurrence patterns, bounded occurrence expansions and conflict-safe confirmed reservations; Clock owns civil-time/instant/time-zone/DST conversion and ambiguity semantics, not reservations or execution. A recurring-series creation does not guarantee future occurrences. Every occurrence reports its own confirmation, effective interval and origin/exception. No Clock contract change is asserted.
