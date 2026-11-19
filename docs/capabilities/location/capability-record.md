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

## Events interface reciprocity — 18 November 2026

**Events EVT-09 (18 November 2026; technical interface requirement):** [Events](../events/capability-record.md) needs a place/venue reference, location and suitable versioned location restrictions from Location, with physical occupancy/fire/accessibility suitability obtained from the actual authoritative venue/Asset owner where Location does not own those facts. Events supplies planned occurrence time, status, change/cancellation and affected location references. Missing essential current safety restrictions cannot be presented as authorised occupancy. No direct domain-store access or Events takeover of location/venue facts. [Decision and contracts](../../../reviews/events-contract-attendance-and-handover.md).


## Reciprocal interface — Logistics conceptual review (19 November 2026, draft PR #89)

**Proposed; not owner-approved or implemented.** Logistics consumes qualified Location place/address references and may attach versioned origin/destination and observed route/checkpoint provenance. Location owns canonical place, geometry, precision and revisions; Logistics owns shipment movement evidence. Current Location PR #87 is provisional, so retain a pending interface reconciliation and never treat geocoding as proof of delivery. See [Logistics proposed public contract](../logistics/capability-record.md#dedicated-logistics-conceptual-review--19-november-2026-draft-pr-89). No approval or completion of this capability's independent review is implied.
