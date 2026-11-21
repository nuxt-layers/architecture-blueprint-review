# Capability Record — Events

**Capability:** `events` — generic organised activities and their occurrences, not message transport or timed-job execution.
**Classification:** independent **Domain responsibility**; no assumption of a new repository, service or framework dependency.
**Review status (18 November 2026):** **EVT-01–10 and EVT-12–15 expressly owner-approved conceptually**; EVT-11 excluded/not approved. EVT-15 delegates attendee/attendance records to the separate Attendance candidate ([draft PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79)), not required for standalone Events. Implementation root `CONTRACT.md`, independently verified runtime/CI and Attendance's independent final design are separate future matters.
**Governing baseline:** `nuxt-layers/architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2` (accepted Capability Standard/ADRs incl. 0012/0016/0017/0018). **Blueprint opening:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. [Review protocol](../../review-protocol.md) · [Opening record](../../../reviews/events-review-baseline.md) · [detailed contract and handovers](../../../reviews/events-contract-attendance-and-handover.md).

## Owner-approved definition

**EVT-01:** Events is a distinct, generic Domain capability for organised activities. It is neither an event-message bus nor a background scheduler.

**EVT-02 (owner wording):** “Events owns the lifecycle of explicitly scheduled activities, their occurrences, event-specific programmes, timing, locations, event-specific restrictions and cancellation history. It does not own the underlying domain definition or lifecycle of another domain capability. Other capabilities may compose Events when scheduled activities are required, but do not depend on Events merely to exist.”

**Approved equivalent:** Events is responsible for organised activities, scheduled occurrences, event-specific programmes, times, places, restrictions and lifecycle. Other Domains may associate their records by public contracts without transferring their ownership. A scheduled teaching activity is one optional example, not a special dependency, parent-child relation or curriculum/cohort design decision.

## Owns and excludes

**Events owns:** tenant/organiser-scoped event ID and version; programme and optional session structure/order; draft/published/private/withdrawn visibility; event and occurrence lifecycle including time/zone, changes, cancellations and conclusion; recurrence rule, materialised occurrence and exception IDs; event-specific limits, eligibility restrictions and closure state; organiser/host *references*, location/venue *references*, approved association to external Domain IDs and revisions; impact notifications and reconciliation progress **of its own requested handovers**; provider mapping/authority provenance for its event scope; correction and change history; committed outbox for its own changes.

**Events does not own:** people identity/contact data (Identity/Profile); attendee invitations, RSVP, expected participant roster, entry/check-in/out or verified presence **under approved EVT-15 responsibility separation**; booking commitments, seats, holds, waitlists and financial outcomes (Booking/other nominated owner); venue safety/occupancy certification (real venue/Asset authority; Location supplies place facts within its contract); notification delivery, background execution or approval engine (Notifications/Scheduler/Workflow); any cooperating Domain's outcomes, payment/refund decisions, attendance evidence, audit evidence storage, log sinks, derived reporting or event-message transport (Message Queue).

**Separation rule:** an Event-specific participation limit is not physical occupancy, a reservable seat count, an invitation or admission decision. Events can exist with no Booking, Attendance, external calendar or GUI. An Events record must not internally mirror a peer's authoritative list/ledger.

## Event model, native services and lifecycle

- `Event`: stable organiser-owned activity and optional programme; `Occurrence`: identifiable scheduled instance; `Series`: optional recurrence rule and exceptions; `Session`: optional identifiable component of an occurrence/programme. A one-off meeting needs no artificial recurring series. IDs, parent references, revisions and effective/recorded times are distinct; no circular parent graph (EVT-13 approved).
- Authorised draft creation, edit, programme/session change, publication/unpublication, scheduling/rescheduling, postponement, cancellation, conclusion and attributed correction; immutable history of material published changes.
- Local event time zone and intended wall time, UTC instant and offset where relevant; DST gap/overlap handling, explicit recurrence exceptions, stable materialised occurrence IDs. Clock supplies common temporal semantics (EVT-04 approved).
- Validate current policy, caller/tenant/resource authority, revision and optional venue/booking restrictions before a relevant consequential transition; optional peer unavailability must be visible and must not fabricate firm commitments. An authorised draft can remain editable when a venue is temporarily unverified.
- Native headless functionality independent of external event providers or optional attendance/booking infrastructure; no dual write to provider and local Event in one fictitious cross-domain transaction.
- Events writes its committed state and producer-owned durable outbox atomically; retries and subscriber replays never create a second event/cancellation.

## Public input contract — idealised business operations (EVT-03/10)

| Input surface / caller | Request | Public result and validation |
|---|---|---|
| `createEvent`, `reviseEvent` — authorised organiser/host | Tenant/owner, programme, visibility, schedule intent/zone, event-specific restrictions, external public references, expected revision and operation key | Stable event ID/revision; committed, rejected/conflict, pending or unknown; no unauthorised resource disclosure |
| `publishEvent`, `unpublishEvent` | Event ID, approved publication policy/decision reference, expected version | Published/withdrawn state and version, required restriction/approval failures |
| `addSession`, `reviseProgramme` | Programme/session identity, ordering and source revision | Versioned programme/session IDs, conflict or rule failure |
| `scheduleOccurrence`, `reviseOccurrence`, `postponeOccurrence`, `cancelOccurrence`, `concludeOccurrence` | Event/series/occurrence ref, local time/zone and instant, change reason, proposed affected range, expected revision | New authoritative occurrence/event revision, original/new schedule, transition outcome and peer impact/correlation; **not** peer compensation success |
| `defineEventRestrictions`, `getEventRestrictions` | Event-defined participation limits, policy, closure/eligibility conditions, effective times | Versioned Events-specific restriction, authority/freshness; never booking availability or certified room occupancy |
| `assessChangeImpact`, `requestPeerReconciliation` | Proposed/committed event change, old/new revision, peer scope/typed reference, source constraints | Events-owned impact ID, required peer actions, peer-state progress, incomplete/unknown status; peer results supplied only by their owner |
| `linkDomainReference`, `unlinkDomainReference` | Approved foreign Domain type/id/revision, association purpose and disclosure policy | Typed, revocable association; does not grant foreign-domain mutation |
| `proposeExternalEventChange`, `resolveProviderConflict` — Integrations adapter | Verified provider mapping, authority scope, source revision/ETag, proposed operation and provenance | Accepted/rejected/pending/conflict/unknown, local revision, mapping/sync watermark; external callback alone not authoritative commit |
| `getEvent`, `listEvents`, `getProgramme`, `getOccurrences`, `getEventHistory` | Authorised purpose, tenant/resource filters, event/occurrence reference and optional as-of/version | Redacted, paged current/historical event, programme, time/zone, restriction, lifecycle and source freshness/completeness |
| `exportEventSchedule`, `getProviderSyncStatus` | Authorised event/period/format, provider scope | Permitted export with version and export status; sync checkpoint/conflicts |

**Participant-specific calls are *not* Events commands under approved EVT-15.** Hosts may provide an Attendees tab by consuming Attendance's own public contract. No separate attendee table, invitations or check-in ledger in Events. If Attendance is absent, Events still functions and its participant-related optional GUI is unavailable.

**Contract context (typed fields rather than mandatory universal wrapper):** tenant, organiser/resource scope, trusted caller + assurance and server-side Authorisation decision; event/series/occurrence IDs; expected revision, idempotency/correlation, reason and policy approval/effective version; UTC instant, local wall time/IANA zone/DST disambiguation; external source authority/version; sensitivity/retention; result `committed/rejected/pending/unknown`, stable reason/error code, recovery/read-back instruction. Cross-tenant and forbidden resource access always deny without information leakage.

## Public output contract

| Output from Events | Receiver; meaning |
|---|---|
| `EventDetail`, `ProgrammeDetail`, `OccurrenceSchedule`, `SeriesDefinition` | Organiser, host, permitted consumers; authoritative identity, lifecycle, schedule, zone and revisions, optional typed peer associations |
| `EventRestriction`, `ScheduleChangeImpact` | Booking, Location/resource owner, Attendance or another consumer; Events-specific limits/closures, old/new occurrence IDs/times, revision and peer impact reference; **no reservation guarantee** |
| `EventOperationResult`, `CoordinationStatus` | Caller/operator; source state and peer acknowledgement separately: not-needed, pending, committed, rejected/conflict, unknown |
| `ProviderSyncStatus`, `ExportResult` | Integrations, authorised operator; mapping/reconciliation and safe portability |
| `EventHistory` and authorised event export | Permitted reader/Reporting; as-was and current revisions, corrections, effective/recorded times, scope and provenance |
| Committed Events-owned outbox notifications | Message Queue/authorised subscribers: `EventCreated`, `EventPublished`, `EventChanged`, `OccurrenceScheduled`, `OccurrenceRescheduled`, `OccurrenceCancelled`, `EventCancelled`, `EventConcluded`, `EventRestrictionsChanged`, `EventCorrected`. Minimal source event ID, version, effective/recorded time, source/tenant/correlation and affected references. Not participant or reservation events. |

No exactly-once cross-domain guarantee. Queries have explicit visibility, completeness and last-source-check time; a read does not reserve a place.

## Cooperating capabilities — reciprocal contract and independence

| Peer capability | Events consumes (peer's output) | Events publishes (peer's input) | Authority / failure |
|---|---|---|---|
| **Identity / Authentication / Authorisation** | Organiser/caller ID, authentication/assurance and event-resource permission decision | Event/occurrence ID, affected resource, requested action and decision context | Mandatory protected access checks; no Events permission grants |
| **Clock / Configuration / Privacy / Legal Compliance** | Time/DST rules, effective setting/policy/retention and legal/safety obligations | Event timings, policy use and change references | Mandatory rules never fail open; Clock is not Scheduler |
| **Location and actual venue/Asset authority** | Versioned place identity, zone/accessibility/location facts; venue safety/capacity restrictions **only from actual qualified owner** | Planned/rescheduled/cancelled occurrence times, venue references, restriction impact | Location is not presumed the occupancy certifier; invalid required restrictions stop firm use |
| **Booking or nominated reservation authority** | Checked current holds/commitment impacts, validity/rebooking outcomes, authority/version | Event schedule/restriction source, old/new occurrence, closures/cancellation, impact ID | One pool/interval commitment authority; Events never confirms/releases seats or copies capacity ledger |
| **Scheduler** | Due request acceptance/ID, actual/attempted job execution, retry/cancellation result | Event/occurrence ID, expected revision, requested timed action and due time/idempotency | Scheduler executes tasks but never changes event state without Events checking current authority/version |
| **Workflow / Notifications** | Approved decision or delivery result when composed | Approval request, versioned notification intent with permitted destination reference | Workflow routes; Notifications delivers; neither owns Events source outcome |
| **Integrations** | Authenticated provider operation/change evidence, remote IDs/ETag, checkpoint, verified callback and transport status | Provider-neutral event snapshot, scheduled change/cancel/export request, mapping and accepted local revision | **EVT-08 approved:** Integrations owns credentials/connectors/schema translation; Events owns local event facts or records a declared external-authority status, never silent dual master |
| **Attendance candidate (optional; EVT-15 approved)** | Purpose-authorised participant/RSVP/verified presence summaries and corrections if composed | Event/occurrence ID, schedule, restrictions, lifecycle changes/invalidations | Attendance owns participant roster and presence; no copy of attendee list in Events; Event does not require Attendance to operate |
| **Other Domain consumer (optional)** | Its own independently authoritative reference/constraint/decision | Event schedule, occurrence and event lifecycle | Generic typed public association, no special subtyping |
| **Message Queue** | Delivery/retry/checkpoint signals where exposed | Producer-owned committed Events change envelopes | Queue transports, not event-activity state |
| **Audit** | Evidence receipt and integrity/coverage status | Minimised attributed publication/change/cancellation, privileged access and policy-security outcomes | Audit owns evidential custody, not Event |
| **Logging** | Sanitised diagnostic sink/health status | Technical failure/latency/timeout/version conflict/queue lag, safe correlation | No full participant data or source-event proof |
| **Reporting / Search** | Report refresh/export/index health where offered | Authorised event/occurrence status, revisions, cancellation/schedule histories and invalidation events | Derived analytics and indexes never alter source Events |

**Directed dependency:** event-mutating operations consume host-supplied, versioned peer ports as required by policy, rather than private neighbour imports. Peer-specific GUI adapters are optional; no universal mandatory dependency except justified security/Clock/policy and own storage. Any public extension/presentation composition follows ADR-0016 and remains acyclic.

## EVT-09 — Location, Booking, Scheduler responsibilities

1. **Location/venue owner** supplies real place identity and relevant restrictions, with responsible-source revision and expiry/freshness. Events *never claims* physical-occupancy certification merely because an address resolves.
2. **Booking** owns all nominated commitment decisions and returns impact/acceptance/reconciliation statuses when Event schedule or restrictions change. Events emits the old/new occurrence references and cannot silently void bookings.
3. **Scheduler** receives only idempotent due-work requests and reports execution; Events validates time, expected revision and permissions on every resulting state transition. Late reminders cannot resurrect cancelled occurrences.

## EVT-12 — approved capacity boundary, preserving earlier authority

The approved Booking concept owns reservation/hold/confirmation/release only in its designated pool; other explicitly selected capacity sources have distinct, non-overlapping scope. Events supplies **only** its event-specific limit and restriction revision. A participant intention or roster presence does not allocate a seat. True available places require current event restriction, venue/resource safety and designated reservation-owner commitment checks. During venue/Booking outage, never claim firm capacity or invent cancelled reservations. EVT-12 is owner-approved conceptually. Implementation acceptance must demonstrate competing last-place claims, provider timeouts and a reschedule with active commitments.

## EVT-14 — approved independent transition and coordination protocol

| Events transition | Events authoritative action | Other owner response and source of truth |
|---|---|---|
| Publish | Commit event visibility/programme revision after own validation and required approval | Workflow supplies approvals; venue owner supplies mandatory restrictions; other owners do not publish Events |
| Reschedule | Commit old/new occurrence time, reason, revision and source outbox; mark any peer coordination pending | Booking independently revalidates/amends reservations; Scheduler replaces due jobs; Integrations syncs remote state; venue owner validates revised use |
| Cancel | Commit Events cancellation and attributable history; emit affected occurrence references | Booking independently cancels/releases/rebooks its claims; Notifications delivers messages; Integrations synchronises; commerce owner decides refunds |
| Restriction/venue change | Commit authorised event restriction or location reference with verified external source and revision | Venue authority certifies physical constraints; Booking reassesses own capacity and commitments; no independent Events safety certificate |
| Conclude | Commit event/occurrence conclusion and retained published history | Attendance (if composed) independently verifies presence; other Domains independently decide any service/learning/contractual consequence |
| Correct history | Append successor event revision with reason and effective/recorded dates | Each downstream owner independently evaluates corrections to its own records, retaining original provenance |

**Handover protocol:** on a material source change, publish event/occurrence ID, old/new revision and time/zone, policy/reason, affected partner types, source-event/correlation ID, effective time, privacy classification and requested action. Each partner returns its own resource/operation ID, source revision, `not-needed/pending/committed/rejected/unknown`, reasoning category and reconciliation cursor. Event state and peer state are *never* one atomic distributed transaction. A timeout is unknown, not proven completion or rollback; retries preserve idempotency. The host/coordinator observes pending impacts and assigned operator follow-up. Cross-domain refunds and entitlement changes are not Events operations.

## Security, privacy, independent Diagnostics/Audit/Reporting

Enforce per-event visibility, tenant isolation and server-authorised actions; publish under effective legal/policy restrictions. Security-sensitive publication/cancellation/change, denied access, provider and privileged export need appropriately classified Audit evidence: Events publishes minimised attributable source facts; Audit owns receipt, custody, integrity and review. Logging ingests bounded technical diagnostics, without participant lists, privileged details or authentication secrets; log acceptance does not mean an event committed or an Audit receipt exists. Reporting consumes authorised event history/changes, provides derived metrics and exports with freshness/coverage, never source authority. Missing optional Logging/Reporting must not undo valid Events state. Mandatory Audit capture follows the approved risk-tier fail-closed or explicitly recoverable pending policy. Privacy/Legal Compliance determine applicable limits and retention, Events applies them to its own records.

## Provider-neutral configuration and GUI

Configuration declares and stores approved preferences: event visibility and publication workflow, recurrence, supported time zones/constraints, source authority scope, cancellation policy, reporting/disclosure settings and legal/retention references. Events validates domain semantics and cannot disable mandatory security/legal floors. Native mode includes no mandatory external calendar; external integrations use **published** provider-neutral inward/outward Events ports (EVT-08), not direct provider SDK imports.

Optional GUI: event list/calendar, event/series editor, occurrence/programme editor, venue/time/restriction editor, publication/cancellation dialogs, history, provider sync and change-impact queue. Attendance or booking-specific panels appear only through the host's permitted public-contract composition, without duplicate local Events stores. Accessible WCAG 2.2 AA, internationalised, themed, and server-authorised; headless absence of GUI supported.

## Conceptual acceptance scenarios

1. Create/publish/revise a one-off public event in native mode without Booking, Attendance, external calendar or GUI.
2. Two-day programme with optional parallel sessions; recurring weekly occurrence across a DST transition with an exception.
3. Concurrent organiser amendments: one revision wins, other receives conflict and useful read-back; no lost public history.
4. Cross-tenant/private event disclosure denied through list, detail, history, export and change notification.
5. Physical venue becomes invalid; source freshness/real authority shown, no invented occupancy clearance.
6. Source event capacity 80, venue certified 70, Booking pool already commits 69: no source claims 11 additional guaranteed places; only Booking arbitration can confirm.
7. Event rescheduled after 30 confirmed bookings: Events change committed, Booking impact pending and Scheduler update separately visible; no claim all reservations changed.
8. Cancellation with external provider timeout: Events cancellation and remote unknown co-exist; recover with read-back and idempotent retry.
9. Late repeated Scheduler task cannot reinstate a cancelled occurrence or duplicate an event.
10. If Attendance is composed, Events attendee tab presents authorised Attendance records, not its own participant database; if absent, event scheduling still works.
11. Audit sink unavailable but Logging healthy, and vice versa; record business/evidence/diagnostic statuses independently.
12. Reporting stale after source revision: report indicates outdated completeness; no source Event is changed.
13. Calendar-provider failover/cutover preserves event IDs, source mappings, history, conflict quarantine and explicit authority.
14. Same event linked to an arbitrary third-party domain record by public reference without giving Events power to change that domain.
15. Source event notification delivered twice/out of order: consumer can reconcile latest source revision without duplicating events or effects.

## Decision register

- **EVT-01–10 — owner-approved** (18 Nov 2026); EVT-07 invitation/RSVP functional requirement is delivered by Attendance through public-contract composition under approved EVT-15. EVT-09/10 technical details documented; actual runtime contract/CI not verified.
- **EVT-09 — OWNER APPROVED:** documented Location/venue, Booking and Scheduler public-contract responsibilities; independent implementation verification deferred.
- **EVT-10 — OWNER APPROVED:** independently meaningful idealised public input/output specification and contract requirements recorded. Published implementation root `CONTRACT.md` and independent consumer acceptance not verified.
- **EVT-11 — excluded** (not approved; belongs to another review if relevant).
- **EVT-12 — OWNER APPROVED:** no duplicate capacity ledger; preserve previously approved Booking authority and explicit one-owner-per-pool arbitration.
- **EVT-13 — owner-approved** minimal event/series/occurrence/session hierarchy.
- **EVT-14 — OWNER APPROVED:** explicit event-source versus independent peer change, acknowledgement and reconciliation handover.
- **EVT-15 — OWNER APPROVED:** Events delegates participant/attendee register, invitations/RSVP, check-ins, attendance verification and corrections to independent [Attendance candidate draft PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79), retaining optional GUI and contract association. The Attendance contract itself remains a separate unmerged candidate; no required dependency is introduced.

**Disposition:** Events conceptual contract now covers independent activity lifecycle, explicit input/output and reciprocal port contracts, provider interaction, change handover and acceptance. **Implementation readiness is not claimed**; current-master technical/architecture consistency, CI/mergeability and explicit merge authorisation are still required.

## Attendance ATT-09 — optional accountless event attendee access (18 November 2026)

**Attendance ATT-09 owner-approved; Events EVT-15 already owner-approved in merged PR #67.** [Attendance conceptual guest contract](../attendance/capability-record.md#att-09--owner-approved-secure-accountless-participant-access-18-november-2026) supports a participant with no application account. Events provides the versioned event/occurrence details and cancellation state; Attendance owns invitation/RSVP and activity participation eligibility; Authentication issues/revokes guest sessions and Authorisation enforces narrowly scoped permitted event views. Events never issues bespoke login credentials or reowns an attendee roster. Event cancellation/rescheduling must invalidate/reassess scope, while lawful participation and source event history remain owned separately. Host-composed guest panels respect source confidentiality; absence of Attendance does not prevent Events native operation.

## Cross-capability note — Gaming conceptual review (18 November 2026)

**Gaming (18 November 2026; proposed, not owner-approved):** [Gaming](../gaming/capability-record.md) owns game matches, rules, entrants, rounds and official results; Events retains actual scheduled public/physical event sessions, venue and programme state. Events may supply a versioned session reference, permitted time and availability; Gaming supplies game-specific participation and result references, not bookings or calendar authority. Distinct source revisions and conditional provider absence must be observed; this note does not complete the Events review.

### Gaming portal scope correction — 18 November 2026

**Gaming scope clarification (18 November 2026, owner-provided; detailed decisions proposed):** [Gaming](../gaming/capability-record.md) is a shared game catalogue, launch portal and accepted-score/leaderboard owner, **not** a generic game engine. Independently composed game layers own their own gameplay, session/move/physics state, game rules and original results. Earlier gaming reciprocal wording implying that Gaming owns gameplay, game rounds, adjudication of moves or original raw results is superseded. This owner-supplied distinction takes precedence within this working review; no implementation or published game contract is asserted.


## Reciprocal conceptual interface — Membership (19 November 2026; draft PR #93)

**Status: proposed, not owner-approved or implemented; this does not complete the events review.** [Membership](../membership/capability-record.md) is a candidate *scheme participation* domain distinct from Identity group membership, Subscription plan entitlements, commercial settlement and application access. Events owns actual activity scheduling/attendance/participation records; Membership may supply scheme benefit qualification and receive verified attendance evidence. Membership status does not reserve capacity or prove event attendance. Consume only published public interfaces; no direct package dependency is inferred. Missing, stale, contradictory or unauthorised evidence must not be promoted into confirmed outcomes.
