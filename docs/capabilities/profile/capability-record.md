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


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-05 (Option B):** Configuration's account scope is limited to explicitly registered **non-personal operational** settings with one named authority. Profile remains sole owner of personal identity details and individual locale/time-zone preferences; Configuration must not use its general account mechanism to create parallel Profile records. Theme Manager owns effective theme. This decision does not assert an implementation migration.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.

## Employment reciprocal conceptual interface — 17 November 2026

**Status: Proposed in [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59), not a completed Profile review.** Profile owns general personal/contact data and individual preference/rights interfaces. Employment owns employer-scoped engagement terms, assessments and confidential personnel evidence; it may consume purpose-approved Profile data by reference and return qualified, restricted data-subject access/correction/erasure dispositions without copying all personnel records into Profile. Employment records may require separately justified retention or legal holds. An employer's membership or administrative role does not grant access to all worker details. See [Employment record](../employment/capability-record.md).


## Attendance ATT-09 — guest privacy and contact-data boundary (18 November 2026)

**Owner-approved accountless-access requirement, proposed public-port alignment:** [Attendance](../attendance/capability-record.md#att-09--owner-approved-secure-accountless-participant-access-18-november-2026) has an activity participant reference, not an implicit full Profile or verified person. Profile remains personal-data authority **where a supported guest/subject contract exists**; otherwise the host must designate a separate purpose-limited, tenant-isolated contact-data authority, with no duplicate unrestricted Profile store. Attendance requests approved contact/delivery references, not arbitrary replicated personal details. Data-subject access, correction, erasure/restriction and legal hold coordinate with each source owner; guest-session expiry does not delete lawful attendance facts. **Owner-approved ATT-10 (18 November 2026)** keeps data access/retention histories source-owned, with Audit custody of minimised accountable evidence. No new Profile implementation capability is claimed.

## Attendance ATT-11 — standards reference for guest personal information (18 November 2026)

**Status:** Standards applicability note proposed in Attendance PR #79 (18 November 2026); ATT-09/ATT-10 are owner-approved, but ATT-11 standards mapping is not separately approved. References are design guidance unless an accepted governing rule or applicable law already makes a control mandatory. No implementation, certification or new dependency implied.

**Apply:** [ISO/IEC 27701:2025](https://www.iso.org/standard/27701) and applicable [UK GDPR / ICO storage-limitation guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-protection-principles/a-guide-to-the-data-protection-principles/storage-limitation/) to minimal guest contact data, permitted purpose, visibility, subject rights, retention and secure removal. Profile supplies personal attributes only where its public subject contract permits; otherwise use a specifically designated purpose-limited contact-data owner. Attendance records must not silently become a second person master; Accountless participant access does not compel a permanent Profile. Historical records and data-rights decisions remain separately owned under ATT-10.

## Gaming public handles — reciprocal conceptual note (18 November 2026)

**Status: Owner requirement; detailed design proposed, no implemented API.** [Gaming](../gaming/capability-record.md#26-public-gaming-handle--new-owner-requirement-detailed-policy-proposed) will own a public, non-personally-identifying *pseudonymous gaming handle*, its visibility and the stable game-player reference used for Gaming scores. Profile retains ordinary personal information, privacy-sensitive attributes and its established rights/disclosure contract; Gaming must not expose Profile or Identity account identifiers in public leaderboards. A securely authorised private linkage and applicable privacy/rights workflows are required; public display names do not imply a verified real-world identity. Renames/withdrawal must propagate to derived projections. This does not complete the Profile review.



## Reciprocal conceptual note — IAM Integration (18 November 2026)

**Status: Proposed under [IAM Integration draft PR #73](https://github.com/nuxt-layers/architecture-blueprint-review/pull/73); not a new published implementation contract or owner approval.** Profile remains authoritative for personal data, purpose-specific disclosure and personal-data request/erasure lifecycle. IAM Integration supplies verified Identity references and rights-request coordination over public owner parts; it consumes qualified export, correction, disclosure, anonymisation and legal-hold dispositions without duplicating personal data or claiming all source records erased. See [IAM Integration conceptual public contract](../iam_integration/capability-record.md).


## Identity reciprocal conceptual interface — 18 November 2026

**Status: proposed Identity alignment, [draft PR #74](https://github.com/nuxt-layers/architecture-blueprint-review/pull/74), 18 November 2026; no new published API.** Identity provides stable opaque local principal references and purpose-scoped standing/closure notifications; Profile retains all person/contact/display data and user rights in its own lifecycle. Identity directory queries must not copy Profile attributes, and Profile visibility must independently enforce context/disclosure constraints. Unknown identifier or unqualified cross-tenant request is not permission to disclose. See [Identity conceptual contract](../identity/capability-record.md#idealised-public-outbound-interfaces).
