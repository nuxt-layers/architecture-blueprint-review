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


## Reciprocal classification note — Event Bus consolidation (18 November 2026)

**Status: owner-approved consolidation through [Event Bus review PR #66](https://github.com/nuxt-layers/architecture-blueprint-review/pull/66); owner approval pending.** [Archived Event Bus classification and idealised contract](../../../reviews/event_bus-consolidation.md) finds no distinct source-of-truth, lifecycle or public contract justifying an independent Event Bus capability. The governing catalogue already assigns outbox-message distribution to Message Queue, and the blueprint maps `event-bus-service` / former `events-queue` to Message Queue. Preserve source-owned durable outboxes and event semantics; Message Queue owns only validated transport, subscriptions, attempts, retry, dead-letter and controlled replay. Transport success is not domain completion or Audit acceptance. Subject to a future Message Queue-specific public-contract review, provide producer/consumer ports, minimised scoped envelopes, clear duplicate/order/uncertainty guarantees and operational state to authorised consumers. Optional operator UI belongs to Message Queue, not a separate Event Bus dashboard. No implementation interface or separate dependency is thereby asserted; the current `nuxt-layers/message-queue` root `CONTRACT.md` was not retrievable.
