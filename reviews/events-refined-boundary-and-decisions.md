# Events — approved boundary and remaining decisions

**Status (18 November 2026): EVT-01–10 and EVT-12–15 owner-approved conceptually; EVT-11 excluded.** Events input/output, Location/Booking/Scheduler and Integrations interfaces, Booking capacity authority, explicit peer reconciliation and attendee separation are agreed; implementation verification and the separate Attendance candidate review remain outstanding. See [approved handover details](events-contract-attendance-and-handover.md). This is a blueprint record, not an implementation contract. [Events record](../docs/capabilities/events/capability-record.md) · [Draft PR #67](https://github.com/nuxt-layers/architecture-blueprint-review/pull/67).

**Governing:** `architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint opening `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`; current subsequent baseline `5b6f67be3263586ffea5156f7b23135373ccd734`. Follow accepted ADR-0012 and ADR-0016; no direct private coupling or duplicate authority.

## Owner-approved decisions

**EVT-01 — Approved:** Retain `events` as a distinct, generic **Domain capability** for organised activities, not a transport/message-bus or background scheduler. Distinct responsibility does not compel an independent repository, package or deployment.

**EVT-02 — Approved (owner wording):** "Events owns the lifecycle of explicitly scheduled activities, their occurrences, event-specific programmes, timing, locations, event-specific restrictions and cancellation history. It does not own the underlying domain definition or lifecycle of another domain capability. Other capabilities may compose Events when scheduled activities are required, but do not depend on Events merely to exist."

Equivalent summary accepted: "Events is a generic Domain capability responsible for organised activities, their scheduled occurrences, event-specific programmes, timing, locations, restrictions and lifecycle. Other domain capabilities may associate their records with Events without transferring ownership of those records."

**Application:** Events owns its event/occurrence/series/session facts, revisioned status and event-specific capacity *constraints*. It does not own another capability's definition, rights, reservations, evidence or business outcomes. A scheduled teaching session is merely one optional Events interaction example; educational run/cohort design is deliberately outside this review.

## Remaining decisions and evaluation criteria

| ID | Issue to decide | Criteria / recommendation |
|---|---|---|
| **EVT-03 — Approved** | Which **public commands, queries, event notifications and results** must Events publish? | Authorised create/revise/publish/postpone/cancel/finish; versions, history, revisions, clear error/unknown results, idempotency and source-owned outbox. Keep implementation types and private stores out of the contract; accept only when a standalone consumer can integrate using the public interface. |
| **EVT-04 — Approved** | How should recurrence, time zones, edits, cancellation and failure behave? | Distinguish event, occurrence, session and recurrence exception; handle daylight-saving ambiguities; preserve change history; avoid silently changing existing reservations and show pending/unknown coordination. Test one-off, recurring, partially cancelled and already booked activities. |
| **EVT-05 — Approved** | Must Events work without a GUI, and which optional screens belong to it? | Recommend a fully usable headless service plus optional Events dashboard, calendar/programme editor, lifecycle controls and operator exceptions. Host owns navigation, Theme Manager governs appearance, and access/WCAG/i18n requirements apply. |
| **EVT-06 — Approved** | What security, privacy, compliance and provider rules apply? | Tenant/resource-scoped server authorisation, minimally necessary person/location data, effective legal/safety restrictions, controlled retention, verified external provenance, permissioned exports, separate Audit/Logging/Reporting and visible provider failure. Security/legal floors cannot be lowered by configuration. |
| **EVT-07 — Approved function, ownership separated by approved EVT-15** | How are invitations and RSVP available for an event? | Attendance candidate owns invitations, RSVP and check-in records under the owner-approved EVT-15 boundary; Events supplies public event/occurrence references and may display Attendance through host composition. No Events people list; RSVP is never a reserved place. |
| **EVT-08 — Approved** | Can a connected external calendar/event system own the activity? | Recommend explicit primary authority per scope, local stable references, revisions, sync provenance, conflict/retry/withdrawal and portable recovery. No hidden two-way master; test provider outage, concurrent edits, duplicate webhook and provider exit. |
| **EVT-09 — Approved** | Which sources establish venue limits and who coordinates cancellation effects on Booking? | Events owns only event-specific restrictions; venue/resource owner certifies physical safety/eligibility; Booking or another designated capacity owner holds commitments. Define versioned constraint checks, impact notice/acknowledgement and uncertainty before final confirmations. |
| **EVT-10 — Approved** | What evidence proves an actual public `CONTRACT.md` can be consumed independently? | Publish operations, permission/error codes, dependency absence modes, versioning, outbox, minimal one-call/50-line host composition where applicable, threat/GUI evidence and independent consumer CI acceptance. No tests/builds run in this conceptual review. |
| **EVT-12 — Approved** | Does Events itself ever reserve capacity, or only publish event restrictions? | Recommend *no competing Events reservation ledger*: one designated capacity authority handles claims. Test final-seat race, conflicting venue and event limits, stale constraints, reservation rescheduling and consumer reconciliation. Events may still limit participation in its own programme without promising seats. |
| **EVT-13 — Approved** | What is the smallest event/series/occurrence/session model? | Recommend optional hierarchy: a simple event can be a single dated occurrence; recurring or multi-session activities add explicit series, occurrences and sessions only when needed. Test conferences with parallel sessions, recurring seminars, daylight-saving and historical versioning; prevent circular nesting. |
| **EVT-14 — Approved** | What happens across capabilities when Events changes/cancels an activity? | Recommend Events emits committed changes with revision/impact references; other owners re-evaluate their own obligations, without automatic cross-domain rollback, refund, grant or cancellation. Test a changed event with active bookings and partial provider failure. |

**EVT-11 — Not approved, removed:** Course offering/run versus Enrolment cohort ownership is not an Events design decision. No alternative, gate or dependency based on EVT-11 is retained here.

## Public conceptual contract — concise

**Inputs to Events:** authorised create/change/publish/cancel/finish commands; schedule and recurrence details (time zone, programme, session, venue/reference); event-specific rules; typed external-domain references and current revisions; effective access/privacy/legal policies; venue/resource limits where relevant; verified external-provider change evidence; optional Booking impact results.

**Outputs from Events:** authoritative event/series/occurrence/session read models, schedule/status/current and historic revisions, publication/visibility, event-specific restrictions and change/impact notices; explicit command outcome and stable errors; committed minimal change events from its owned durable outbox; permitted event exports and provider sync/reconciliation state. These do **not** grant access, reserve places, certify physical safety or decide another domain outcome.

**Shared guarantees:** tenant isolation; server-side authorisation; valid time-zone semantics; optimistic revision checks and idempotency; versioned, redacted, source-attributed values; distinct `committed`/`pending`/`rejected`/`unknown`; duplicate/out-of-order subscriber tolerance. No universal request object or exactly-once distributed delivery promise.

## Other capabilities: required information and supplied facts

| Counterpart | Input needed by Events | Output from Events | Boundary |
|---|---|---|---|
| Identity / Authentication / Authorisation | Organiser/caller resource references, assurance and permission decision | Own event resource/action reference, attributable decision context | Protected operations always authorised at server; no identity or grants owned by Events |
| Clock | Instants, time-zone/DST and recurrence validation | Event-effective dates/times, zone and revisions | Clock supplies shared time semantics |
| Configuration / Privacy / Legal Compliance | Effective approved settings, data use/retention/disclosure and mandatory restrictions | Event policy usage, bounded lawful processing and classified outputs | These authorities retain policy/legal source |
| Location / Asset / venue or resource owner (conditional) | Venue identity, physical availability/eligibility, capacity and restriction revision | Event scheduled-usage/impact references | No Events declaration of independent occupancy/safety authority |
| Booking / designated commitment owner (conditional) | Commitment/impact/reconciliation status | Versioned session/time and event-specific eligibility/closure restrictions | One reservation authority; no duplicate seat ledger |
| Workflow / Scheduler (conditional) | Approved decision, timed-task completion if used | Approval requests, dated task instructions and change references | Workflow owns approval routing; Scheduler executes jobs |
| Integrations / external providers (optional) | Validated upstream IDs/revisions, verification and sync status | Event snapshots, change/withdrawal requests | Explicit scope and precedence |
| Notifications (optional) | Delivery result/status | Authorised notification intents and recipient references | Events does not deliver |
| Message Queue (conditional transport) | Delivery/replay/backlog diagnostics | Outbox messages about committed Events facts | MQ transports, not domain-authoritative |
| Logging / Observability (optional diagnostics) | Sanitised sink/operational health result | Error codes, correlation, retries, provider/scheduling failures, outbox lag | Diagnostics not business/audit proof |
| Audit (risk/policy-required evidence) | Verified evidence receipt/integrity/coverage state | Attributable creation/publication/change/cancel/privileged access events and provenance | Audit owns evidence custody, Events owns activity fact |
| Reporting / Search (optional) | Authorised report status, query context or index staleness | Permission-scoped event counts, event/session histories, cancellation/schedule details and change invalidation events | Reporting owns aggregates, exports and report definition; no private table access |

For a general Event, no external specialist domain such as Course is mandatory. Related domains may optionally associate their own references without transferring ownership.

## Logging, Audit and Reporting — reciprocal input/output contracts

| Peer | Events → peer (peer's input) | Peer → Events (peer's output) | Never infer |
|---|---|---|---|
| **Logging** | Sanitised technical failures, latency/retry classes, provider/queue health, correlation and bounded tenant scope | Accepted/dropped/unavailable diagnostic status, safe sink/health reference where offered | A written log does not prove an Event was committed or audited |
| **Audit** | Minimal attributable security/business records: actor, event/resource ID, operation, committed/denied outcome, revision, timestamp, evidence source, retention class | Accepted/pending/rejected/unknown evidence receipt, custody integrity/completeness and permissioned review evidence | Audit acceptance does not create/cancel an Event or establish legal compliance |
| **Reporting** | Authorised, versioned event/session data and status history; permissioned aggregates at safe grain; committed change notifications for refresh | Report identifier/definition, execution/delivery state, last refresh, source coverage/freshness, authorised export links | Reporting totals cannot change event records or grant access; stale/incomplete reporting must remain visible |

**Failure independence:** an Events update, Logging diagnostic, Audit evidential receipt and Reporting refresh are **four different outcomes**. Optional Logging/Reporting failure does not undo a committed Events change; mandatory Audit capture must follow an explicit approved risk-tier fail-closed or recoverable-pending policy. Retry/replay must not duplicate domain state or evidence.

## Conceptual acceptance

One-off event; public conference with parallel sessions; recurring seminar and DST exception; event-only operation without Booking or GUI; booking confirmation against current event and venue restrictions; cancellation after reservations; external sync outage; denied cross-tenant read; duplicate command/event; Audit unavailable with Logging healthy and vice versa; report refresh delayed while Event source remains correct.

**Current decision status:** EVT-01–10 and EVT-12–15 owner-approved; EVT-11 excluded. Runtime root contract, CI and Attendance's independent review are unverified. This document records no new implementation repository, released service, provider adapter or legal certification. Recheck latest masters, diff, CI and protected branch requirements before any explicitly authorised merge.


## Latest approved decisions and attendance gap (18 November 2026)

**EVT-03–08 and EVT-13 were expressly approved by the owner.** EVT-08 must expose Interfaces to the independent Integrations capability; EVT-09 coordination includes Location, Booking and Scheduler; EVT-10 requires an independently usable public input/output specification. EVT-12 must preserve earlier accepted Booking/capacity authority rather than create another reservation ledger. EVT-14 needs explicit source-owner impact and compensation responsibilities. EVT-15 is the newly identified attendee/attendance responsibility **not yet owner-approved**; see [the focused technical and ownership analysis](events-contract-attendance-and-handover.md). Existing broad references to EVT-03–08 and EVT-13 as open in this historical review are superseded by this note.


## Final Events/Attendance separation proposal (18 November 2026)

Events input/output and independent peer handover are now fully described in [the current Events capability record](../docs/capabilities/events/capability-record.md). Draft [Attendance PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79) owns the proposed reusable activity-participant register; EVT-15 owner-approved transferring invitation/RSVP and attendee authority outside Events; the separate Attendance candidate remains draft. Do not interpret older intermediate text in this review as authorising two competing attendee registers, an Events-owned check-in ledger, or a mandatory Attendance package dependency. EVT-09/10 detailed contract design is documented; EVT-12/14 owner-approved, subject to current-master technical/architectural integration checks.
