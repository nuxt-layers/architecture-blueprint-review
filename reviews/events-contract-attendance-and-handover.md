# Events — approved decisions, attendee management and contract clarification (18 November 2026)

**Status:** **EVT-01–10 and EVT-12–15 owner-approved conceptually** (18 November 2026), EVT-11 excluded. EVT-15 places the attendee/attendance register in the separate candidate ([PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79)); its own detailed contract remains subject to independent review. Input/output and peer handover below express approved Events boundaries, not runtime exports.

## 1. Approved status and narrow Domain boundary

Events independently owns its scheduled activity, occurrences, event-specific programme, timing, location references, event restrictions and lifecycle. It may be optionally composed with *any* other Domain capability via stable public reference and no ownership transfer. In this document other Domains appear only as generic consumers or as a limited example, not as parents/subclasses or direct dependencies.

- **EVT-03 approved:** explicit public input commands, read/query outputs, domain events, versioned results, validation, permissions and unknown/failure outcomes.
- **EVT-04 approved:** safe recurrence, time zones/DST, reschedule/cancellation/exception handling, versioned history and cross-domain impact notices; not a cross-domain rollback mandate.
- **EVT-05 approved:** autonomous headless service and optional accessible, internationalised Events dashboard/programme/calendar, with host-owned navigation and semantic Theme Manager styles.
- **EVT-06 approved:** risk-scoped access, privacy, legal/safety rules, retention, provider neutrality and separate logging, auditing and reporting outcomes.
- **EVT-07 approved in principle:** invitation/RSVP workflows approved in the event ecosystem; **EVT-15 places their authoritative records and attendance operations in the Attendance candidate** rather than creating an Events-side people list.
- **EVT-08 approved:** external calendar/event services through a **published bidirectional, provider-neutral Events ↔ Integrations contract**, authority mapping, sync/revisions, conflict handling, revocation and portable recovery. Integrations owns connection, credentials, provider-specific translations/webhooks and transport; Events owns validation, committed event state and authoritative business decision for Events-controlled scopes. Where an external provider is explicitly authoritative for a bounded scope, Events records provenance/uncertainty and does not invent local success or covertly switch authority.
- **EVT-13 approved:** lightweight optional hierarchy (Event, Series, Occurrence, Session), stable distinct identifiers; one-off Event need not manufacture a complex series/session tree. No cycles; preserve exception/history semantics.
- **EVT-11 removed/out of scope.**

## 2. EVT-09 — three peer contracts, not one venue scheduler

| Peer | Input Events needs | Events output | Owner and required failure rule |
|---|---|---|---|
| **Location** (and authoritative venue/Asset/resource owner where relevant) | Stable place/resource reference, zone/location details, accessibility/location-relevant constraints, effective change/restriction status, provenance and revision; any actual physical capacity certification must come from its real owner, not inferred from geocoding | Planned activity at a location, occurrence time, change/cancellation, authorised impact reference | Location is not automatically an occupancy/fire-safety authority. Stale or unknown *mandatory* restrictions block firm approval/confirmation; event drafts can remain editable |
| **Booking** | Capacity-authority identity, held/confirmed commitments, safe aggregate availability, verified impact/acknowledgement for change, reconciliation status | Event/occurrence ID, date/time, event-specific ceiling, closures, amendment/cancellation revision and requested impact assessment | Booking owns booking commitments only in its designated pool. No event-side duplicate reservation or silent cancellation. Conflict/unknown results require explicit reconciliation |
| **Scheduler** | Accepted/rejected scheduling request, job ID, planned/actual run time, attempt/failure/delay status | Timed maintenance/reminder/recurrence materialisation request with event/occurrence ID, expected revision, due time, idempotency; Events remains final validator of triggered command | Scheduler executes jobs, never owns event programme/time or meaning. A delayed/duplicate trigger must not change an event without current Events validation; no scheduler availability is required to read or manually change an event |

**EVT-09 outcome gate:** a venue becomes restricted while 30 bookings exist and a reminder job is due. The three separate source decisions and impacts must be demonstrable; no unverified occupancy claim, overbooking, hidden cancellation or stale timer acceptance.

## 3. EVT-10 — minimum public `CONTRACT.md` structure

The implementation must publish an independently usable public contract with *business semantics* and later implementation-specific signatures, stable names, versions and errors. The following are **illustrative logical operations**, not confirmed exports.

| Inbound public operation | Required input meaning | Authoritative output |
|---|---|---|
| `createEvent` | Tenant/organiser, programme, schedule/zone, access scope, caller and operation key | Event ID, draft state, revision, committed/invalid/rejected/unknown |
| `reviseEvent`, `publishEvent` | Event ID, intended changes, expected revision, approval/authority context | New revision, publication status, conflicts and reason |
| `scheduleOccurrence`, `reviseOccurrence`, `cancelOccurrence`, `concludeOccurrence` | Event/series/occurrence ID, time/zone, change reason, impact scope and expected revision | Affected occurrences, committed status, historical lineage and impact status |
| `queryEvents`, `getEvent`, `getOccurrence`, `getSchedule` | Tenant/resources, viewing purpose, permission context, effective/as-of time and filters | Authorised paged/filtered event, programme, occurrence, schedule and permitted revision history with freshness/completeness |
| `getEventRestrictions`, `assessEventChangeImpact` | Event/occurrence, required location/capacity source references, proposed change | Events-owned rules/limits, checked source versions, outstanding uncertainties, **not** a guaranteed free seat |
| **Delegated attendee requests (optional host composition)** | Host supplies Event/occurrence reference and authorised participant context to the separate Attendance contract | Attendance owns invitation/RSVP outcome; **not** an Events command or event-owned attendee row |
| **Attendance candidate contract (not an Events input):** `registerParticipant`, `recordCheckIn`, `recordCheckOut`, `correctAttendance`, `listParticipants` | See attendee decision below; not yet approved | Owner-scoped attendee/observation records with provenance and uncertainty |
| `proposeExternalChange`, `resolveSyncConflict`, `getProviderMappingStatus` | Approved Integrations adapter, source ID/revision/authority, signed or verified change evidence and operation key | Accepted/rejected/conflict/pending result; local revision, external mapping and sync checkpoint |
| `requestEventExport`, `getEventHistory` | Purpose/permissions, scope, effective/as-of interval, format | Redacted, versioned event state and traceable history; delivery success separate |

**Published outgoing change notifications:** versioned `EventCreated`, `EventPublished`, `OccurrenceScheduled`, `OccurrenceRescheduled`, `OccurrenceCancelled`, `EventCancelled`, `EventConcluded`, `EventRestrictionChanged`, `EventCorrected` ; participant/attendance events belong to Attendance only. These are **semantics**, not fixed TypeScript strings. Emitted only on committed Events-owned state through source-owned durable outbox. Consumers tolerate duplicates/reordering and query current authorised state.

**Shared public envelope/metadata as needed**, not a universal mandatory request shape: tenant/resource scope; caller/assurance and independent server authorisation; event/occurrence and affected domain association IDs; expected revision; idempotency/correlation; source/provider authority and revision; effective versus recorded time and IANA zone; privacy/disclosure/retention class; outcome `accepted` versus `committed`, `pending`, `rejected`, `unknown`; documented error code, `messageKey`, recovery/retry/read-back instruction. No direct private schema or provider SDK types. Errors cannot leak an undisclosed event's existence.

**Required `CONTRACT.md` sections:** purpose/ownership, package/public entry points, installation and one-call host composition/50-line budget (where applicable), required/optional services and absence behaviour, permissions, operation shapes and results, queries, domain event schemas and transport, configuration, time/recurrence, multi-tenant/privacy/retention, Integrations ports, location/Booking/Scheduler ports, attendance choice, failure/recovery, GUI/headless options, change compatibility and independent acceptance scenarios. It must remain sufficient without reading internal source files. Do not assert a current implementation.

## 4. EVT-12 — preserve earlier capacity declarations

**Earlier accepted Booking position remains governing within its declared authority:** Booking owns reservation intent, holds/confirmations, capacity ledger and release; other designated owners may hold other explicit pools, but **only one reservation-commitment authority for the same pool/scope/interval**. Events can set event-specific participation restrictions and supply source revisions; that does **not** make Events the physical occupancy certifier or the bookable capacity ledger.

**No automatic broad transfer:** an Events restriction change issues a versioned change/impact notice; the designated booking owner determines which reservations are invalid, pending, affected or rebooked. An Events cancellation does not directly refund, cancel, reschedule or free the booking owner's commitments.

**EVT-12 approved; implementation acceptance checks:** scope of non-bookable free attendance; whether a participant's RSVP consumes a scarce place (if yes, this is a Booking/designated capacity contract, not mere Events RSVP); all applicable event, location/venue and booking constraints at confirmation; concurrent last-place races and pending/unknown provider state; one owner of each ledger; independent notifications of compensation. **No revision to approved Booking decisions proposed.**

## 5. EVT-14 — precise change authority, impact and handover

| Transition | Events alone may do | Other authority must decide | Required Events outbound and receiving response |
|---|---|---|---|
| Draft edit or publish | Validate policy/permissions, write its own event revision; publish only when mandatory restrictions satisfied | Workflow approves if required; venue owner supplies safety facts | Committed revision, source IDs, publication status, policy/approval references; peer acknowledgement is not Events commitment |
| Reschedule occurrence | Record old/new time, revision, reason and Events status, with `coordination pending` where applicable | Booking revalidates holds/confirmed commitments; Location/resource owner checks new use; Scheduler updates timed jobs; Integrations synchronises external entry | `OccurrenceRescheduled` includes old/new revision/time/zone and impact reference; each peer returns accepted/applied/conflict/unknown with its own resource/version |
| Cancel activity/occurrence | Set Events cancellation status/reason/effective time; preserve historical record and outbox | Booking decides reservation changes/releases; payment/commerce owner decides refunds; Notifications sends; Scheduler cancels due jobs; Integrations processes external update | `Event/OccurrenceCancelled`, affected references, urgency/impact and idempotent correlation; peer reconciliation records independently |
| Venue becomes unavailable | Record verified restriction and visibility/eligibility change, or pending unverified state | Actual venue/Location/Asset owner decides venue facts; Booking decides booking impact | Restriction-source reference/version, effective date and event impact status; never self-certify occupancy |
| Event completed | Record Events-owned conclusion only; no event-level check-in observations or attendance records | Booking owns service booking outcome where designated; any specialist capability independently verifies its domain result | Concluded event revision and minimal safe attendance *observation* reference (only if EVT-15 approved); no automatic third-party outcome |
| Historical correction | Append superseding Events revision and original reference, protect prior as-was view | Other owners decide whether their own outcomes need amendment | `EventCorrected`, original/successor IDs and reasons, authorised affected scope; explicit downstream acknowledgement/reconciliation |

**Transactional rule:** Events' state and its durable outbox are atomic *within Events*; no promise of atomic commits across Events, Booking, Scheduler, Integrations or Reporting. Handover tracks each peer's `not-required/pending/accepted/committed/rejected/unknown` status with source revision, correlation and reconciliation owner. A peer timeout is **unknown**, never assumed completed or rolled back. Events cannot rewrite another owner's status. Consumers must perform independent permission/policy validation before mutating their own state. A completed Events cancellation and unfinished Booking compensation may coexist and must be visible to operators.

**EVT-14 approved; implementation verification gate:** one reschedule while 30 people have confirmed bookings, one cancellation after notification provider outage, one occurrence changed during external sync, one late Scheduler trigger, and one correction after event completion. Confirm original/new IDs, source revisions, which owner performs each operation, subscriber deduplication, uncertainty and redacted Audit/Reporting visibility.

## 6. EVT-15 — approved separation from independent Attendance candidate

**Status:** EVT-15 source-of-truth separation is owner-approved. [Attendance conceptual PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79) remains a separate draft; its prospective record is not yet on `master`. Events may refer to its *public* contract when available without requiring Attendance to run.

Under the recommended boundary, **Events owns no list of people**: no invitations, RSVPs, expected-attendee roster, entry/check-in/out, physical presence or attendance evidence. It owns event/occurrence identity, schedule, programme, event-specific restrictions and lifecycle. Attendance owns the **activity-scoped participant relationship** (not Identity/Profile's person master), invitation/RSVP register, check-in/out observations, verification and correction history. Booking retains any independently authoritative reservation/entitlement record and party/beneficiary; Enrolment retains its independent admission/learner-standing decision; neither is replaced with an Attendance row. A limited Booking party count cannot be inferred as the same number of individually identified attendees.

**Events → Attendance:** typed event/occurrence ID, version, time zone, programme/segment references, event-specific restrictions, published/cancelled/rescheduled/concluded state with old/new revision and effective time; minimally disclosed permission scope. **Attendance → Events (optional read/display):** authorised participant summaries, RSVP counts, check-in status and verified attendance with source revision, coverage and missing-data flags. No direct private table access, no mandatory Events→Attendance package dependency, and no double write of participant state. An Events UI may mount Attendance's public Attendees/Check-in screens; absence of Attendance disables those optional functions but not Events.

**No attendance proof from the Events lifecycle alone:** event `concluded` does not assert who attended, a Booking reservation does not prove entry, an RSVP does not guarantee capacity, and a recorded check-in does not confer specialist domain outcome.

**Implementation acceptance:** free event without Booking, ticketed event, invitation-only event, anonymous walk-in, uncertain/offline scan, recurring occurrence, correction/dispute, minors/guardians, booking cancellation after entry and no Attendance installation. Provider trust, privacy and effective source ownership must be explicit. EVT-07 approved the *availability* of invitation/RSVP workflows in the event ecosystem; final relocation to Attendance is a proposed owner amendment under EVT-15.

## 7. Cross-capability diagnostic/evidence/analytics contracts

| Peer | Events outbound (peer input) | Peer outbound (Events may consume) | Authority boundary |
|---|---|---|---|
| **Logging** | Minimal structured errors, denied/invalid operations where appropriate, retries, scheduling/connector failures, event/occurrence correlation, outbox lag without attendee PII | Diagnostic accepted/dropped/unavailable, sink status where supported | Log delivery neither commits an Event nor constitutes Audit evidence |
| **Audit** | Classified actor/resource/action/attempt or committed event revisions and event-sensitive attendee/access actions; source/causation/effective time and minimised provenance | Evidence receipt pending/accepted/rejected/unknown; integrity/completeness/review status | Audit owns evidential custody, not Events activity records; mandatory capture assurance separate from log |
| **Reporting** | Authorised versioned programme/schedule/status and suitably scoped attendance/RSVP counts **only from the separate Attendance owner when composed under EVT-15**, with event changes for refresh | Report execution/refresh/export status, freshness/completeness and authorised snapshot reference | Reporting derives analytics, not event state or person-level rights; attendance not inferred from bookings |
