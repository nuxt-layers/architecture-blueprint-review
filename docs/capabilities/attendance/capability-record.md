# Capability Record — Attendance

**Capability:** `attendance` (new generic Domain capability candidate).
**Classification:** Domain candidate, distinct from Events, Booking, Enrolment, Identity/Profile and Training; no standalone runtime repository or independently released API established.
**Status:** creation and dedicated conceptual review requested by owner 18 November 2026; **detailed Attendance ownership proposals pending explicit approval; Events EVT-15 delegation already owner-approved and merged**. [Baseline](../../../reviews/attendance-review-baseline.md) · [Review PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79).
**Governing:** `nuxt-layers/architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`, accepted capability standards/ADRs including ADR-0012 and ADR-0016. **Opening blueprint:** `5b6f67be3263586ffea5156f7b23135373ccd734`.
**Evidence:** User identified fragmentation and proposed a single participant/attendance responsibility across the ecosystem. Events EVT-15 **was owner-approved and merged in PR #67**: participant/attendee register, invitations/RSVP, check-ins, verification and corrections belong to the Attendance interface when composed, and Events remains independent without it. EVT-07 invitation/RSVP functional availability is preserved through optional Attendance composition. Booking BK-01–05 and Enrolment ENR-01–07 remain owner-accepted; Training still owns verified learning-participation evidence. Neither source-boundary approval nor implementation is overridden by creating this candidate.

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
| **Events (optional; EVT-15 approved)** | Event/occurrence ID, schedule, start/end, cancellation/status, event restrictions and revisions | Expected participant count and authorised roster; invitation/response and attendance finding; source-owned change notification | Events EVT-15 approved delegation; Events never owns a duplicate participant roster or verification ledger; no Events mandatory dependency |
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
- **ATT-07:** Reconcile Training verified learning attendance authority before any transfer of responsibility. **Open owner decision; no transfer inferred.**
- **ATT-08:** Exact public root `CONTRACT.md`, schema/port/security/error definitions and independent CI consumer proof when implementation exists. **Future implementation gate.**

No existing capability implementation or agreed Booking/Enrolment/Training authority is revised simply by publishing this proposal. Events EVT-15 **is already owner-approved and merged in Events PR #67**. This establishes Events' exclusion of attendee authority, but does not itself approve Attendance ATT-01–08 or override Training TRAIN-01.

## 18 November 2026 — latest-master reconciliation and strengthened contract

**Verified current baselines:** governing `architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master@7edabf7ae8b44e2c3b2242be7689ea0c471bcb90` (Events PR #67 merged after this branch began). **EVT-15 is owner-approved**, while Attendance ATT-01–08 remain separately proposed/open. Events' participant tab is a host-composed view of Attendance, never a parallel writable Events roster.

### Source-authority resolution: observations versus educational adjudication

**Recommended ATT-07 reconciliation (owner approval still required):** Attendance owns *generic* activity participation and factual presence observations, source verifications and corrections; Training owns *educational* interpretation of presence against Course requirements, verified **learning-participation evidence** as a training-domain determination, competency and programme completion. A Training determination may cite immutable Attendance observation/finding IDs, revisions, attestors and coverage; that does **not** allow Attendance to issue a learning achievement. Where Training collects specialist instructor evidence without Attendance, its native learner-evidence lifecycle continues (TRAIN-01/04) and must not become a duplicate generic event attendee register. A training session may be rostered in Attendance while its course participation and requirements remain independently determined in Training. When Attendance is absent, Training's previously approved independent native evidence/verification continues; when Training is absent, Attendance can verify general presence without inventing learning evidence. Training's published authority must be reconciled separately and its prior approval preserved.

**Roster/entitlement invariants:** participant intent, registration, reservation and effective admission are four distinct assertions; none alone proves another. A reservation count is not a roster of identified humans. A guardian's legal relationship or permission must come from the qualified source, not an Attendance guest flag. Multi-activity references may point to one opaque subject but retain independent purpose, authority, tenant and lifecycle.

### Public contract precision and recovery semantics

| Interface family | Required inbound facts and trust | Authoritative outbound result / uncertain state |
|---|---|---|
| Participant association and invitation | Typed activity owner/id/revision, purpose and tenant, subject or consented pseudonymous guest, initiator permission, delivery/response correlation | Stable activity-participant ID, invitation intent/RSVP state/version, linked source assertions; no capacity or admission guarantee; unknown identity remains unresolved |
| Observation capture and checking | Valid actor/attestor role and assurance, instant/interval with IANA zone and disambiguation, observation method, source/evidence ID, expected revision and idempotency key | Recorded observation and its *own* validation/verification state; duplicate gives prior logical result; conflicting evidence quarantined/disputed; no automatic absence |
| Attendance adjudication/correction | Applicable effective attendance rules, coverage, attestation, underlying observation versions, authorised reviewer and reason; any mandatory domain-specific source decision is checked separately | Revisioned generic attendance finding with `observed/verified/disputed/unknown`, coverage and as-of; successor record retains provenance and a supersession link; cannot decide qualification, wages, booking entitlement or Training achievement |
| Roster and interval queries | Authorised tenant, activity, occurrence/segment, permitted purpose, scope, as-of time and pagination | Minimised redacted snapshot, explicit confidence/freshness/coverage and opaque references; unauthorised/mismatched scope returns no disclosure |
| Source/provider reconciliation | Trusted Integrations origin, mapping, source revision, confidence and allowed delegation, replays/cursor | Accepted, duplicate, pending, quarantined or conflict result; provider timeout means unknown and reconciliation required, never verified by default |
| Outbox and downstream consumption | Committed source revision, source-event ID, schema version, tenant, type, effective/recorded time, permitted consumer purpose | At-least-once-safe notification and consumer read-back; notifications are *facts*, never automatic commands or permissions; Audit custody, Logging delivery and Attendance decision remain separate statuses |

Command acceptance **does not** imply final verification, delivery or peer-side completion. Denials must not leak existence across tenants. Every consequential correction records the predecessor, actor or approved deterministic rule, authority, reason class and decision time. Missing required validation returns `rejected`, `pending` or `unknown` with recoverable explanation, never success-by-default. Outbox publication must be transactionally coupled to Attendance-owned committed state under accepted ADR-0012, with replay-safe consumers and no promise of exactly-once distributed delivery. Do not define a mandatory universal envelope or private datastore coupling.

### Conceptual acceptance matrix (design criteria, not tests run)

| Scenario / input | Expected result | Domain authority |
|---|---|---|
| Free event with invitation and RSVP, no Booking | Roster and response recorded; no seat allocation or guaranteed admission | Attendance; Events owns schedule |
| Four-seat anonymous booking | Booking remains valid as reservation party of four; zero verified named attendees until associated | Booking, then Attendance |
| Enrolment to course without session | Enrolment standing exists independently; no invented Attendance presence | Enrolment |
| Training instructor verifies lesson outcome with optional Attendance absent | Training native evidence can be verified under its policy; no mandatory Attendance runtime | Training |
| Event is rescheduled/cancelled with active registrations | Events revision becomes authoritative; Attendance flags affected invitations/observations for version-aware reassessment, never silently deletes historical presence | Events schedule; Attendance records |
| Supervisor submits duplicate or conflicting check-in | Idempotent replay reuses result; contradiction awaits authorised review, preserves both observations | Attendance |
| Offline mobile device submits delayed interval across DST | Preserve measured instant, claimed local wall time/zone, source uncertainty and ingestion time; do not manufacture continuous duration | Clock semantics; Attendance evidence |
| No observations but incomplete capture | Unknown, not absent; denominators and coverage exposed | Attendance |
| Invalid guardian permission, revoked actor or cross-tenant export | Deny and minimise disclosure, appropriate evidence recorded, no implicit participant access | Identity/Authorisation/qualified guardian source |
| Provider goes offline then returns inconsistent historical data | Pending/unknown, quarantined conflict and versioned operator reconciliation; no automatic proof of presence | Integrations transports; Attendance decides |
| Verification correction after Training consumed old evidence | Attendance publishes successor/correction; Training re-evaluates its own derived learning participation, never direct mutation of Training's ledger | Attendance; Training |
| Audit down, Logging up (and reverse) | Separately reflect evidence custody and diagnostics; mandatory risk-based evidence capture fails closed or uses expressly approved recoverable pending state | Attendance/Audit/Logging |
| Request to certify room occupancy, allocate seat, pay wages or award a qualification | Unsupported or directed to correct public owner; no false side effect | Venue/Booking/Time & Attendance/Qualification |

### GUI and host composition acceptance

The optional **Attendance** sidebar dashboard serves a headless-equivalent scoped organiser register, invitation/RSVP queue, accessible check-in/out controls, uncertain/late-provider observation queue, evidence verification, corrections/disputes, authorised exports and privacy-aware aggregates. A learner or participant sees only permitted personal invitations/responses and attendance history. Event-specific **Attendees** views use the same Attendance public contract, with activity/occurrence identifiers from Events and no shadow tables. Distinguish provisional versus verified, absent versus unknown, as-of coverage, source revisions and denied/unsupported actions using text as well as accessible status cues; keyboard-only workflows, WCAG 2.2 AA, BCP 47 locale formatting, Theme Manager tokens and responsive layouts are required. Host owns navigation and optional composition; Attendance owns domain-state changes.

### Remaining gates

- **ATT-01–06:** proposed conceptual ownership and service contract awaiting owner sign-off; new candidate requested, not an implementation.
- **ATT-07:** owner decision on exact Training-vs-Attendance learning participation authority, preserving owner-approved TRAIN-01/04 and independently operable Training.
- **ATT-08:** future root `CONTRACT.md`, IAM/permission matrix, durable outbox/schema, provider contract and independent consumer acceptance; no target implementation repository or published runtime contract verified.
- **Current-master consistency:** Events EVT-15 approved and merged; independent optional Events/Attendance composition remains acyclic conceptually. Protected merge requires explicit owner approval, checks and updated branch reconciliation. No implementation tests or builds run.

### Distinct Time & Attendance boundary

`time-attendance` is a separately owner-approved conceptual employment/work-time responsibility, not an alternative name for this candidate. A generic Attendance check-in or presence interval is **not** an approved timesheet, paid time, break classification, employment shift, payroll input or legal working-hours determination. When explicitly composed, Time & Attendance may consume purpose-authorised, versioned presence observations as evidence and independently validate work context, break rules, approval and corrections. Attendance may consume an activity reference or employer-authorised observation only within a declared purpose; neither owner directly rewrites the other's ledger. A Time & Attendance outage must not suppress an otherwise valid generic Attendance record; missing Attendance must not disable Time & Attendance's independent evidence workflow. The existing approved `time-attendance` candidate remains unchanged.

## ATT-09 — owner-approved secure accountless participant access (18 November 2026)

**Decision status: owner-approved conceptual requirement; not an implemented IAM feature.** Attendance MUST support activity-scoped participants who have **no full application account**. It owns participation associations and relevant access-entitlement *business facts* (invitation/response, activity/booking/enrolment reference, intended recipient, current eligibility, withdrawal, cancellation and resource revision), **not** session credentials, identity proof or access-policy decisions. A guest invitation or Attendance participant ID is never, by itself, an authentication credential, an Authorisation grant or proof of lawful admission.

**Public inputs to Attendance:** (a) Booking/Enrolment or activity owner supplies authorised participant/beneficiary and applicable status, revision, expiry/withdrawal, declared purpose and contact-delivery reference; (b) IAM host supplies authenticated guest-session subject/assurance and a resource-specific Authorisation decision; (c) approved guardian/representative authority and privacy policy where applicable. Unknown or invalid source standing fails closed for protected actions; generic RSVP and booking/admission remain distinct.

**Public outputs:** an opaque, tenant-and-activity-scoped participant reference, invitation/claim request and a **revocable, narrow access-eligibility assertion** for IAM to evaluate (permitted activity, allowed operations, original authoritative source, status, revision and expiry). The assertion is *input* to Authorisation, never itself a permission. Source status change emits minimised invalidation/reassessment facts; Authentication separately invalidates affected guest sessions/credentials and Authorisation reevaluates current resource scope on each protected request. Delivery occurs via Notifications; sending an email proves neither identity nor participant acceptance.

**Authentication/Authorisation division:** Authentication owns short-lived, single-use challenge/token lifecycle, verified possession or stronger proof when required, guest-session continuity/expiry/revocation, assurance and anti-replay. Authorisation owns server-side permitted operations, resource scoping, revocation evaluation and denial under stale/unknown evidence. Session mechanisms must avoid access tokens in persistent/leaky URLs, apply secure transport/cookie handling, rate limits and stronger verification for sensitive data; possession of an emailed link alone is not guaranteed real-world identity. The host composes IAM and Attendance public ports without private shared tables, permanent-account requirement or dependency cycles.

**Use cases:** anonymous four-seat booking does not identify four people; organiser may invite named attendees later through lawful contact channels. A guest joining three activities obtains independently scoped access for each; same contact address does not prove shared identity. Guardian access requires verified representation, not a free-text parent label. Where email is unavailable, only policy-approved alternative or assisted access is permitted. Later full-account linking must verify control of relevant participant claim and the destination principal, preserve original provenance and never expose other organisations' records. Withdrawal revokes future access but does not silently delete lawful history. Guest views, as available through the host, use Events/Course/Booking/Enrolment public APIs for their own details; Attendance never copies course material, payments, grades or provider secrets.

### ATT-10 — owner-approved distributed guest-access history authority (18 November 2026)

**Owner-approved conceptual decision:** distribute history by its authoritative meaning rather than creating one guest-history master. This approves ownership and historical integrity, not implementation readiness or any specific retention duration.

| History class | Owner / public output | Non-ownership and retention |
|---|---|---|
| Activity participant, invitation, response, check-in/out, verification, corrections and later account-link reference | **Attendance:** immutable lineage of activity-local participation states, source revisions and permissible as-of history | A revoked/expired guest credential or merged account does **not** delete or rewrite valid participation evidence |
| Challenges, proof methods/assurance, session issuance, refresh, termination/revocation and credential security | **Authentication:** purpose-minimised session/challenge history and security status | No copy of full participant roster or indefinite challenge-secret retention; never retain raw bearer secrets in history |
| Scope grants, permitted/denied evaluations and effective policy versions | **Authorisation:** current resource-policy/grant authority and decision metadata as appropriate | Audit owns durable evidential custody for significant decisions; high-volume ephemeral checks need not become an unrestricted personal browsing timeline |
| Trusted digital principals, optional verified account link and standing | **Identity:** reference/relationship history when subject is legitimately resolved | A no-account guest is **not** automatically an Identity user/group or verified natural person; no person deduplication by email alone |
| Contact attributes, communication preferences, data-subject requests | **Profile** where a compatible subject/contact contract exists, else separately designated purpose-limited contact owner | Do not invent a universal Profile row or mandatory full account for an unknown guest |
| Security-relevant issuance, access/revocation, privileged correction/export, breaches and accountable decision evidence | **Audit:** tamper-evident receipt, integrity, minimised actor/resource/revision and permitted retention | Audit is not a substitute for any domain's authoritative business history; Logging remains technical diagnostics |
| Reservation/legal financial history, admission/standing, achieved learning and credential claims | **Booking**, **Enrolment**, **Training** and other owners respectively | Attendance cannot mutate or purge peers' lawful records |

**Correlation and access history:** a subject may have independently scoped pseudonymous guest references across multiple activities. Any cross-activity link or later Identity-account claim must be established by verified binding and explicit permitted purpose, with lineage of old/new scoped identifiers, assurance, effective/recorded times, actor, source authority and revocation. Linking creates a **referential association**, not a destructive merge or retroactive alteration of the original claimant. No automatic cross-tenant correlation or discovery, including through error messages. A host may assemble a purpose-authorised participant history by querying source owners; it must indicate incomplete/stale/revoked history and must not maintain a second authoritative ledger.

**Retention and data-subject rights:** expire/revoke credentials promptly on scope withdrawal; retain source domain records only for justified purposes under Privacy/Legal Compliance policy, with distinct schedules for raw challenges, security evidence, booking commitments and attendance findings. Support access, rectification, restriction, lawful erasure and legal hold via owner-specific public workflows; erased personal attributes should not leave recoverable secrets in events/logs. De-identification, corrected attribution and historic evidence preservation must be reconciled case by case, not assumed universally lawful. Access to past activity through an expired credential is denied until newly authorised, although lawful history may remain.

**Threat and failure acceptance:** leaked/stolen invitation, token replay, forwarded invitation, reused email address, stale Booking/Enrolment status, guest revocation during an active session, cross-tenant claim, child/guardian change, account-link hijack, provider outage and right-to-erasure requests all require explicit denial/step-up/recovery and non-disclosure outcomes. Accountless access is optional to a particular host's composition but mandatory as a supported Attendance use case once the published conceptual contract is implemented. No implementation or release acceptance is asserted.
