# Capability Record — Attendance

**Capability:** `attendance` (new generic Domain capability candidate).
**Classification:** Domain candidate, distinct from Events, Booking, Enrolment, Identity/Profile and Training; no standalone runtime repository or independently released API established.
**Status:** creation and dedicated conceptual review requested by owner 18 November 2026; **ownership model and any amendment to pre-approved peers pending explicit approval**. [Baseline](../../../reviews/attendance-review-baseline.md) · [Review PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79).
**Governing:** `nuxt-layers/architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`, accepted capability standards/ADRs including ADR-0012 and ADR-0016. **Opening blueprint:** `5b6f67be3263586ffea5156f7b23135373ccd734`.
**Evidence:** User identified fragmentation and proposed a single participant/attendance responsibility across the ecosystem. Previous Events EVT-07 permitted lightweight invitation/RSVP in that capability; **amending the owner of those interactions requires an explicit Events decision**, not inferred approval. Booking BK-01–05 and Enrolment ENR-01–07 remain owner-accepted; Training still owns verified learning-participation evidence. Neither source-boundary approval nor implementation is overridden by creating this candidate.

## Purpose

Give an authorised consumer one generic public service to answer **“who is expected to participate in this identified activity, who claimed or was observed present, and which participation/attendance findings have been verified?”** The activity can be represented by Events or any other permitted domain reference; Attendance needs no Events dependency by default.

Distinguish *person* (Identity/Profile authority), *participant relationship* (Attendance proposal), *reservation or entitlement* (Booking or relevant source), *enrolment/admission* (Enrolment), *actual presence observation* (Attendance proposal) and *specialist consequence* (Training or other source). Centralising participant relationships should not force all sources to create duplicate editable attendance rosters; it also must not erase legal or business commitments.

## Proposed ownership and exclusions

**Attendance owns, if approved:** tenant/resource-scoped `ParticipationRecord` identity; typed activity reference and optional occurrence/segment reference; participant references (Identity, approved guest/pseudonym, or permitted other subject); event/activity invitations, responses and non-binding registration intent; expected participation roster; entry/check-in/check-out observations and evidence metadata; attendance status adjudication under stated observation/verification rules; absence only where expectations and coverage establish it; corrections/disputes/lineage; attendee privacy and authorised disclosure controls; versioned aggregate attendance results and source-owned outbox.

**Does not own:** Identity principal and authoritative Profile contact data, guardianship or person master; Events schedule, event programme/venue or lifecycle; Booking reservation party terms, seat holds, allocated capacity or confirmation; Enrolment application/learner-standing and cohort admission; Training meaning/competency/completion decisions or specialist verified learning evidence where separately established; working time/payroll hours; Assessment grades; venue/Asset safety decisions; message transport, general Notifications delivery, provider credentials, technical Logging or Audit custody. A participant reference does not establish a booking, lawful physical access or domain-specific qualification.

**Important participant/party distinction:** Booking must continue to identify requester, payer where relevant, beneficiary and contractual reservation party sufficient to enforce and audit its commitments. Enrolment must keep learner/guardian admission decision references. Attendance can be the owner of the **activity-scoped participant roster and presence history**, but cannot replace these independent records. A multi-person reservation may map to zero, one or many Attendance participation entries; without verified attendee assignment, Booking's party size is not an identified attendee list. The same person can be participant in many activities without merging their independent attendance histories.

## Native services and lifecycle

1. **Register and identify participant:** create or resolve authorised activity-scoped participant ID, typed activity/occurrence, optional verified subject and external booking/admission references; minimise Profile data.
2. **Invitation and intent:** issue/track invitation, acceptance, decline, withdrawal, non-binding registration and authorised permitted walk-ins; delivery handled by Notifications.
3. **Eligibility check:** validate trusted source-owned entitlement or admission via explicit optional Booking, Enrolment or other authority port before controlled entry; never manufacture a booking or admission.
4. **Observations:** accept authorised time-stamped arrival/departure, remote session presence, supervisor attestation or verified provider evidence, distinguishing *reported*, *observed*, *provisionally accepted*, *verified*, *disputed*, *rejected* and *corrected*.
5. **Attendance findings:** calculate presence/late/partial/absent/excused/unknown where applicable policy and credible completeness support it; **missing observations are unknown, not automatic absence**.
6. **Corrections:** append attributed correction with original source, reason, approval evidence, replacement revision and lawful history.
7. **Queries and disclosure:** per-participant and per-activity roster, status, time intervals and safe aggregates with coverage, source freshness and redaction.
8. **Provider and reliability:** verified external attendance inputs through Integrations, local operation without external providers, idempotency, concurrency and producer-owned durable outbox for committed changes.
9. **Governance:** retention, guardian/safeguarding and sensitive attendance/location privacy, tenant isolation, per-action authorisation, audit evidence separate from technical Logging and derived Reporting.

The capability must work with an arbitrary qualified `activityRef` and host-provided policies; no hard requirement for Events, Booking, Enrolment, Training or a specific external LMS.

## Idealised public input contract (conceptual, not exported API)

| Input surface | Authorised request and source | Validation and result |
|---|---|---|
| `registerParticipant` / `resolveParticipant` | Tenant, activity type/owner/id, optional occurrence, opaque subject/guest reference, source registration/booking/enrolment reference and permission context | Unique activity-scope participant ID and revision; unresolved identity or source mismatch yields pending/denied, not implicit authority |
| `inviteParticipant` / `recordResponse` / `withdrawParticipationIntent` | Authorised organiser or subject, invitation/response, approved delivery/consent purpose | Accepted/rejected/pending, response revision; response never reserves capacity |
| `verifyParticipationEligibility` | Participant and activity, relevant source-owner entitlement/admission references, effective policy and time | Eligible/ineligible/pending/unknown with source authority/version; does not create booking/admission |
| `recordCheckIn` / `recordCheckOut` / `recordObservation` | Actor, presence interval/instant/zone, method, source identity/assurance, optional device/provider/evidence reference, idempotency | Observation ID, provisional/verified/pending/denied state, repeat/conflict indicator |
| `verifyAttendance` / `correctAttendance` / `disputeAttendance` | Observation IDs, declared attendance policy, decision actor/assurance, source revision, correction rationale | Versioned attendance finding, coverage and confidence/evidence provenance; history preserved |
| `getParticipant` / `listParticipants` / `getAttendance` / `getAttendanceSummary` | Tenant/activity/occurrence, authorised field-level purpose, time range, pagination/as-of | Redacted records, status, verified intervals, unknown/coverage and source freshness; no broad identity disclosure |
| `applyExternalAttendanceObservation` / `reconcileProviderEvidence` | Verified Integrations-sourced provider event, remote IDs, source version and authoritative scope | Deduplicated accepted/pending/conflict/quarantined result with mapping, provenance and checkpoint |
| `getParticipationHistory` / `exportAttendance` | Approved purpose, effective/as-of scope and retention policy | Traceable history/export, redaction, evidence source, delivery state separate |

All protected commands require server authorisation, caller/assurance, tenant scope, expected version, operation ID, idempotency and policy checks. No raw credential or free-text sensitive medical/reason data in transport events.

## Idealised public output contract

| Outbound | Consumer and meaning |
|---|---|
| Stable participant/roster references | Organiser/host, Events GUI, Booking/Enrolment or other authorised consumer; **participant ID is not a person master or reservation ID** |
| Invitations, non-binding registration and response status | Event/application UI and Notifications requests, with purpose-limited contact reference |
| Attendance observations and findings | Authorised domain consumers, e.g. Training, workplace/service owners; distinguish observed vs verified, interval, completeness, provenance |
| Attendance/participation summaries | Reporting and authorised UI; status counts with denominator, missing-record/coverage warning, small-group/privacy limits |
| Committed owner outbox events | `ParticipantRegistered`, `ParticipationResponseChanged`, `AttendanceObservationRecorded`, `AttendanceVerified`, `AttendanceCorrected`, `ParticipationReferenceInvalidated`; versioned minimal identifiers, source/effective time and tenant scope; duplicate/reorder tolerant |
| Provider/reconciliation and operational status | Integrations and operator; pending/unmatched/conflict/uncertain, no fabricated verification |
| Audit evidence requests and technical diagnostics | Audit gets attributed decision/evidence metadata; Logging gets minimised operational codes; neither owns Attendance results |

## Reciprocal contracts and absence modes

| Capability | Attendance consumes | Attendance supplies | Boundary |
|---|---|---|---|
| **Events (optional)** | Event/occurrence ID, schedule, start/end, cancellation/status, event restrictions and revisions | Expected participant count and authorised roster; invitation/response and attendance finding; source-owned change notification | Events never owns a duplicate participant roster or verification ledger; no Events mandatory dependency |
| **Booking (optional)** | Verified party/reservation entitlement, beneficiary reference, capacity authority and confirmation/cancellation version | Participant-to-reservation reference, response/check-in and presence evidence with authority/coverage | Booking retains original booking parties, commitments, amendments, payment and eligibility decisions |
| **Enrolment (optional)** | Effective admission/learner standing, cohort or activity association, authorised guardian scope and source version | Participating learner reference and attendance observation/finding where permitted | Enrolment keeps formal learner decision, not an independent editable attendee list |
| **Training (optional)** | Any Training-owned learning-activity reference and evidence rules requiring presence provenance | Source-attributed attendance observations/findings, corrections and recheck notice | Training continues independently to judge learning outcomes; **its pre-existing verified learning attendance ownership needs explicit reconciliation** |
| **Identity / Profile** | Trusted subject/guardian identifiers, permitted contact display/consent facts, authorisation context | Activity participation references and safe confirmation requests | Never copy unrestricted person master |
| **Location / venue owner (optional)** | Geographical and check-in location context where legitimately required | Minimum necessary arrival and source context with purpose limitation | No venue physical occupancy certification or surveillance by default |
| **Clock** | Instants/zone/interval/DST semantics | Attendance intervals and temporal provenance | No clock-owned participant status |
| **Configuration / Privacy / Legal Compliance** | Effective participation/retention/verification and safeguarding rules | Status of policy application, purpose/retention classifications | Attendance enforces constraints; cannot create legal authority |
| **Integrations (optional)** | Provider evidence, delivery status, verification, source IDs, replay/checkpoints | Versioned attendance facts and scoped synchronisation requests | Integrations owns credentials/webhook/transport; provider authority explicit |
| **Notifications (optional)** | Delivery result | Invitation/reminder intent and approved recipient reference | Delivery does not establish RSVP or presence |
| **Message Queue (conditional transport)** | Delivery/replay/backlog status | Committed Attendance-owned outbox events | Not the source ledger |
| **Audit** | Accepted/pending/failed evidence receipt and coverage where required | Attribution and security/business decisions, corrections, privileged access and evidence metadata | Audit custody distinct from source attendance |
| **Logging** | Sink health and safe diagnostic result | Minimal error/latency/retry/provider signals, no full people lists | Technical diagnostics only |
| **Reporting** | Report refresh/completion status | Scoped, redacted participant counts/attendance series and revisions | No report-driven attendance mutation |

## Options and decision criteria — shared “people” record

**Option A (recommended, conditional):** Attendance is the shared **activity participant** owner; Booking and Enrolment retain immutable/core reservation/admission party references, legal acceptance and decisions. They may consume Attendance participant IDs if configured, but no required Attendance dependency for native booking/admission. A source may perform a booking for an as-yet unknown group of four: the booking remains authoritative for party size; Attendance roster is not yet four identified people.

**Option B (not recommended):** Attendance is the universal owner of people and all Booking and Enrolment person links. This duplicates Identity/Profile, makes independent booking/admission unavailable without Attendance and weakens evidence of legal/financial commitments.

**Option C:** Each source maintains its own editable expected-person list and pushes it to Attendance. This duplicates lifecycle, creates reconciliation conflicts and can give two sources of RSVP/attendance truth; allow only a narrow *source-native contractual party snapshot* in Booking/Enrolment with clear ownership and no independent attendance verification.

**Approval criteria:** (i) anonymous/unidentified booking of multiple seats; (ii) learner admission without a scheduled activity; (iii) one person attached to multiple independent bookings and events; (iv) invited unbooked free gathering; (v) change/cancelled booking after attendee check-in; (vi) legal guardian/minor access; (vii) stale or absent Attendance service, avoiding mandatory core failure; (viii) denied cross-tenant roster/export and small-group disclosure; (ix) audit history and GDPR deletion/retention rights; (x) verified attendance sourced independently of an Event. Validate authority for every write rather than relying on one shared database list.

## Optional GUI

Attendance can supply standalone organiser attendee/attendance register, invitation responses, check-in/out console, correction/dispute queue, evidence verification and scoped attendance summaries; host may mount these contextually in Events, Booking, Enrolment or other applications via documented optional presentation contracts. GUI is optional, WCAG 2.2 AA and i18n apply, host navigation and Theme Manager styling remain host concerns. Presence of an `Attendees` tab in Events does not make Events the data owner.

## Proposed decisions and review disposition

- **ATT-01:** Independent generic Attendance Domain candidate, no automatic package/deployment. **Requested for creation; detailed authority awaiting approval.**
- **ATT-02:** Activity-scoped participant roster and invitations/RSVP versus generic presence evidence, both independently usable without Events. **Proposed.**
- **ATT-03:** Source references and *not* universal person master, reservation or admission owner. **Proposed.**
- **ATT-04:** Attendance verification/correction lifecycle, provisional/unknown and no false absence. **Proposed.**
- **ATT-05:** Conditional Booking/Enrolment cooperation and no duplicate seat/admission ledger. **Proposed.**
- **ATT-06:** Integrations, security, privacy, Audit/Logging/Reporting and optional GUI. **Proposed.**
- **ATT-07:** Reconcile Training verified learning attendance authority before any transfer of responsibility. **Open.**
- **ATT-08:** Exact public root `CONTRACT.md`, schema/port/security/error definitions and independent CI consumer proof when implementation exists. **Future implementation gate.**

No existing capability implementation or agreed Booking/Enrolment/Training authority is revised simply by publishing this proposal. Events EVT-15 remains an independent review decision to confirm removal of its attendee ownership after this boundary is approved.
