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

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Integrations owns its committed connection/grant/mapping/checkpoint transitions and associated durable outbox; Message Queue only transports owner-originating events and may report delivery attempts. Provider webhooks and provider operation receipts are untrusted/qualified external evidence, not source-of-truth domain events. At-least-once/replay and out-of-order handling require consumer deduplication, and delivery success is not remote business completion. See [Integrations conceptual contract](../integrations/capability-record.md#commands-queries-events-and-shared-invariants), PR #76; proposed, not implemented.
