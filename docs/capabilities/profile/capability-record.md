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

## Cross-capability note — Authentication and personal-data lifecycle (15 November 2026)

**Established:** Profile owns ordinary personal attributes and personal-data rights; [Authentication](../authentication/capability-record.md) separately owns necessary sign-in identifiers, authenticators and session security records. **Agreed conceptual direction (AUT-11):** coordinate data-subject access, account closure, minimised exports and permitted erasure through IAM public contracts; Profile does not directly mutate Authentication's records, and routine exports never disclose credential secrets or verification material. **Open:** verified hand-off and lawful retention/exception handling. Profile's conceptual review remains incomplete.

## Cross-capability note — Evidence attribution and subject-rights boundary (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** Profile owns personal attributes, disclosure rules and rights handling; Audit owns minimised, attributable evidence, custody and independent integrity. **Proposed:** [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026) receives qualified subject references and applicable erasure/hold constraints, and returns protected disposition/history without copying full profiles. Account closure must not silently erase lawful evidence or grant retroactive disclosure. Historic identity resolution may be unavailable/restricted. Profile's conceptual review remains incomplete.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking participant reference and data-rights interface (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) should consume authorised Profile contact/participant references where available and return minimally necessary booking association and data-rights disposition. Profile remains authoritative for personal attributes; Booking owns reservation party roles and conditional minimal guest contact custody. Booking must not create a parallel personal directory, infer delegated rights from contact matching or expose personal booking history on unrelated screens. Conceptual proposal only.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Booking uses authorised Profile contact references where possible and must not create a parallel personal directory. Guest-specific minimal contact custody and closure/erasure follow Privacy policy; Booking remains authoritative for the booking's participant roles, not profile attributes. No currently implemented integration contract is implied.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Profile remains authoritative for personal locale, time zone, theme-related personal preferences and personal identity details. Configuration may provide platform/tenant/group defaults; generic account scope does not license duplicating Profile data. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.
