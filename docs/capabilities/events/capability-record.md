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

**Booking session and recurring reservation boundary (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) consumes Events-owned session definitions, applicable capacity and closure/blackout versions, then owns the booking-specific time/seat commitments only in an explicitly assigned booking-authority scope. Events retains event programme and event lifecycle; Booking returns reserved-seat/attendance references only where authoritative. Multiple source owners must provide verified commitments before compound booking confirmation. Recurring Booking occurrences do not alter Events-owned session definitions. No Events implementation claim.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Events owns event programme, sessions and capacity-source restrictions; Booking manages seat/time commitments within a designated reservation authority. Sessions and recurring occurrences are not interchangeable. Compound reservations require verified resource-owner commitments before Booking confirmation. No currently implemented integration contract is implied.

## Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)

**Status: Owner-agreed boundaries, no independently completed events review or implemented API.** [Course](../course/capability-record.md) and [Assessment candidate](../assessment/capability-record.md): **COURSE-09 agreed:** Events owns actual educational session instances, times, venues, host/resource references and event lifecycle; Course owns reusable curriculum/version and Enrolment owns cohort learner allocation. A teaching session is not a background Scheduler task. Events supplies venue/physical limits and authoritative session availability through a public interface; Enrolment/Booking composes independent constraints without a second source of truth. Self-paced courses need no Events record.

## Cross-capability note — Gaming conceptual review (18 November 2026)

**Gaming (18 November 2026; proposed, not owner-approved):** [Gaming](../gaming/capability-record.md) owns game matches, rules, entrants, rounds and official results; Events retains actual scheduled public/physical event sessions, venue and programme state. Events may supply a versioned session reference, permitted time and availability; Gaming supplies game-specific participation and result references, not bookings or calendar authority. Distinct source revisions and conditional provider absence must be observed; this note does not complete the Events review.
