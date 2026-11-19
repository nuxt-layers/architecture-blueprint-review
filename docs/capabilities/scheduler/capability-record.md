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

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Scheduler may trigger Booking-owned expiry/reminder/recurrence maintenance; Booking owns series patterns, bounded occurrences, capacity commitments and changes. Late or missing Scheduler triggers cannot extend expired holds or establish an unconfirmed future booking. No currently implemented integration contract is implied.

## Cross-capability note — Clock conceptual public contract (17 November 2026)

**Proposed, not yet owner-approved.** [Clock](../clock/capability-record.md#idealised-public-output-interfaces-conceptual-contract) supplies typed canonical instants, zone/DST interpretation, calendar-versus-elapsed arithmetic and deterministic time injection. Scheduler owns registered triggers, due execution and retry/attempt state; business capabilities own underlying due-rule interpretation and outcomes. Clock neither schedules nor sends domain events. If a trusted time source or required zone/rules are unavailable, Scheduler must not fabricate execution authority. No concrete adapter is claimed.

## Reciprocal note — approved Clock adjustment and assurance boundaries (17 November 2026)

**Owner-approved CLK-03/CLK-04 direction; Scheduler design still incomplete.** [Clock final completeness review](../clock/capability-record.md#final-completeness-review--eight-concerns-resolved-17-november-2026) distinguishes UTC wall-clock deadlines from monotonic duration measurement. Scheduler consumes trusted host time and separately qualified source assurance for applicable operations; it does not assume time readings cannot step forward/backwards, or that a scheduled trigger fires exactly once. On host adjustment, outage, leap-policy change or tzdb revision, Scheduler must reconcile missed, late and duplicate attempts; originating domain handlers own idempotency, actual eligibility and authoritative outcomes. Calendar/zone conversion stays with Clock; no new Clock implementation API is claimed. This supersedes the earlier reciprocal Clock note's **proposed, not yet owner-approved** wording for Clock ownership, but does not approve Scheduler implementation.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Scheduler invokes due Configuration tasks; Configuration alone determines eligibility, idempotency, activation, expiry, retention and outbox transitions. Missed jobs remain explicitly pending/overdue. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Employment workforce-time boundary — 17 November 2026

**Status: Proposed reciprocal clarification arising from owner-approved EMP-03 in [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59); Scheduler's own review is not complete.** This `scheduler` is an infrastructure/platform timed-work facility for registered background triggers, execution attempts, retries and failure handling. It does **not** own planned staff shifts, rosters, attendance, time cards, legal working-time compliance or payroll hours. Employment owns contractual working patterns and entitlement; the separate, owner-approved conceptual Domain candidate `time-attendance` owns actual clock/timesheet evidence; neither Employment nor Scheduler owns that source. Workforce Scheduling, if independently justified, would own planned shifts; Scheduler may invoke timed reminders or reconciliation only through domain public commands. A scheduled tick is not proof that a person worked. See [Employment conceptual contract](../employment/capability-record.md).


**Employment EMP-03 owner-approved refinement:** The previously proposed nested Employment Time & Attendance approach has been superseded by the independently owned conceptual [Time & Attendance Domain candidate](../../../proposals/time-attendance-ownership.md). The existing `scheduler` remains infrastructure timing only. This does not assert that a workforce-rostering or time-attendance implementation exists.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Scheduler may invoke Course's idempotent timed publication/retirement commands; Scheduler owns timing/retry, Course owns transitions and authorisation. Late or duplicate jobs cannot grant access. This note does not complete the separate scheduler review.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-09/11 agreed:** Scheduler runs idempotent time-triggered work, not education sessions (Events), learner cohorts (Enrolment) or assessment marks. Scheduled Course publication/withdrawal must revalidate current permissions and safeguards; late jobs cannot reauthorise an invalid curriculum. This note does not complete the separate scheduler review.

## Events interface reciprocity — 18 November 2026

**Events EVT-09/14 (18 November 2026; proposed interface clarification):** Events owns activity schedule, occurrence state, recurrence meaning and effective changes. Scheduler receives explicit, idempotent due-work requests with event/occurrence reference, expected Events revision, due time and policy; returns schedule acceptance, execution attempt, actual time, failure/delay and retry context. Only Events may authorise and commit its event transition after checking the current revision. Late, repeated or cancelled Scheduler jobs never override source event state. Scheduler is not a calendar/event or attendance owner. [Contract detail](../../../reviews/events-contract-attendance-and-handover.md).


## Message Queue reciprocal conceptual interface — 19 November 2026

**Status: proposed in [Message Queue draft PR #94](https://github.com/nuxt-layers/architecture-blueprint-review/pull/94), not an approved API or implemented integration.** [Message Queue conceptual contract](../message_queue/capability-record.md#independent-message-queue-conceptual-review--19-november-2026) retains transport-only authority: originating capabilities own committed events and durable outboxes; Message Queue owns scoped subscriptions, transport custody, attempts, redrive/dead-letter and qualified acknowledgements. **Scheduler owns due-time work and execution triggers; MQ delivery/retries are not Scheduler jobs. Any Scheduler source event follows its own outbox and never gives MQ authority to execute scheduled work.** No mutual direct package import is implied. Existing approved decisions remain unchanged; detailed MQ-01–10 decisions are not owner-approved.


## Message Queue reciprocal review — 19 November 2026

**Proposed in [draft PR #94](https://github.com/nuxt-layers/architecture-blueprint-review/pull/94); not an implemented or approved public API.** [Message Queue conceptual contract](../message_queue/capability-record.md#independent-message-queue-conceptual-review--19-november-2026): Scheduler owns due-time execution; Queue retries and transport are not scheduled jobs. MQ can convey Scheduler's source-owned outbox changes, but never invokes work or alters the schedule outcome. Source capabilities own durable outboxes and event meaning; MQ owns scoped routing, custody, attempts, retry, dead-letter and replay. Duplicates, unknown receipts and scoped authorisation must be handled through public directional host-composed ports without cyclic imports. Preserve previous approvals.
