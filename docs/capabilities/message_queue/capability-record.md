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

## Cross-capability note — Authentication security events (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns authentication outcomes and the originating durable security-event outbox required by ADR-0012; Message Queue transports owner-published messages, not authentication events' business meaning, credentials or source records. **Agreed conceptual direction (AUT-05):** convey appropriately minimised, attributable lifecycle events to authorised consumers such as Audit with explicit delivery, replay, deduplication and failure semantics; successful transport must not be confused with successful authentication or Audit acceptance. **Open:** accepted interoperable public event/acknowledgement contract. Message Queue's own review remains incomplete.

## Cross-capability note — Booking event delivery (15 November 2026)

**Proposed; Message Queue public contract unverified.** [Booking](../booking/capability-record.md) owns durable outbox lifecycle events after committed booking changes, with tenant scope, booking reference, version, event identity and minimal provenance. Message Queue may transport these events and report delivery attempts, backlog and acknowledgement; it never owns reservation status, holds or source event decisions. Consumers must tolerate duplicates/out-of-order delivery, and missing transport must not fabricate successful or failed Booking transitions. Use one-way public ports to avoid cyclic imports.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Configuration owns committed change events and its durable outbox; Message Queue owns transport/retry/replay. Consumers may receive duplicates and must query authorised current values rather than treating events as access grants. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Reciprocal note — Events conceptual review (18 November 2026)

**Events review reciprocal (18 November 2026; EVT-01–10/12–15 owner-approved; event_bus consolidated into Message Queue in master):** [Events](../events/capability-record.md) is the Domain source for calendar/programme activities and owns committed event/session state and its outbox. Message Queue transports Events' minimally scoped committed-change messages; may expose retries/acks/backlog, not schedule/attendance/booking authority. Consumer deduplication and staleness reconciliation required. Avoid treating scheduled activities as transport messages or adding a cyclic direct import.

## Revised Events boundary and decision gates — 18 November 2026

**18 November Events generic-domain boundary — owner-approved, post-event_bus consolidation:** [Events boundary and decisions](../../../reviews/events-refined-boundary-and-decisions.md) identifies `events` as organised activities and scheduled occurrences; `message_queue` carries committed source-owned domain-change messages, with replay/dedup/transport status, not the activity lifecycle or participant commitments. The separate `event_bus` record was removed from master and must not be reintroduced by PR #67. Events retains its authoritative outbox and no implicit transport dependency.

## Reciprocal classification note — Event Bus consolidation (18 November 2026)

**Status: owner-approved EB-05 consolidation documented in [Event Bus review PR #66](https://github.com/nuxt-layers/architecture-blueprint-review/pull/66); Message Queue's detailed public transport interface remains subject to its own review.** [Archived Event Bus classification and idealised contract](../../../reviews/event_bus-consolidation.md) finds no distinct source-of-truth, lifecycle or public contract justifying an independent Event Bus capability. The governing catalogue already assigns outbox-message distribution to Message Queue, and the blueprint maps `event-bus-service` / former `events-queue` to Message Queue. Preserve source-owned durable outboxes and event semantics; Message Queue owns only validated transport, subscriptions, attempts, retry, dead-letter and controlled replay. Transport success is not domain completion or Audit acceptance. Subject to a future Message Queue-specific public-contract review, provide producer/consumer ports, minimised scoped envelopes, clear duplicate/order/uncertainty guarantees and operational state to authorised consumers. Optional operator UI belongs to Message Queue, not a separate Event Bus dashboard. No implementation interface or separate dependency is thereby asserted; the current `nuxt-layers/message-queue` root `CONTRACT.md` was not retrievable.

## Federation — reciprocal conceptual contract (18 November 2026)

**Status: Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69); not an approved implementation API, and does not complete this capability's independent review.** [Federation public contract](../federation/capability-record.md#independent-review-contract-completeness-and-authority-18-november-2026).

Federation owns committed peer/subscription/delivery/checkpoint state and its durable outbox facts; Message Queue may carry these and source-owned publication events to selected subscribers. Message Queue does not own remote peer trust, HTTP exchange, source content, federation cursor semantics, reconciliation or origin authorisation. Duplicates/replay are expected; delivery acknowledgment is not business completion. All cooperation is via public, directional host-composed contracts with scoped failure/absence semantics; preserve existing approvals and avoid package dependency cycles.

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Integrations owns its committed connection/grant/mapping/checkpoint transitions and associated durable outbox; Message Queue only transports owner-originating events and may report delivery attempts. Provider webhooks and provider operation receipts are untrusted/qualified external evidence, not source-of-truth domain events. At-least-once/replay and out-of-order handling require consumer deduplication, and delivery success is not remote business completion. See [Integrations conceptual contract](../integrations/capability-record.md#commands-queries-events-and-shared-invariants), PR #76; proposed, not implemented.


## Legal Compliance review worklists are not transport queues — 20 November 2026

**Owner-approved conceptual Legal Compliance boundary; not an implemented contract.** [Legal Compliance use-case exploration](../legal_compliance/capability-record.md) distinguishes domain-owned pending human legal review cases and optional Workflow approval tasks from Message Queue transport. Legal Compliance commits and owns its legal source/interpretation, hold, obligation and review transitions and emits durable outbox facts; Message Queue routes/delivers/retries these events to authorised subscribers without determining legal validity or retaining human approval dossiers. Delivery acknowledgement is not legal approval, physical hold enforcement, regulator acceptance or evidence review. Legal Compliance remains independently capable of native review without using Message Queue as its worklist; any mandatory downstream acknowledgement remains explicit. No direct package dependency cycle is implied.
