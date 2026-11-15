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
