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

## Cross-capability note — Identity and Authentication (15 November 2026)

**Established:** Identity owns opaque principals, standing, tenants and memberships; [Authentication](../authentication/capability-record.md) independently owns credential verification, sign-in identifiers, assurance, sessions and revocation. Identity lifecycle changes requiring access withdrawal must reach Authentication through published IAM integration contracts. **Proposed:** reconcile authenticated principal standing, session revocation propagation, account recovery and service identity references with explicit failure guarantees. **Open:** measured revocation consistency and post-migration ADR-0012 interfaces. Identity's separate conceptual review remains incomplete.

## Cross-capability note — Authorisation decision inputs (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns roles, grants and access decisions; Identity owns principal standing, tenant, groups, memberships and governance facts. No group hierarchy or membership grants unrestricted access. **Proposed:** provide trustworthy, freshness-qualified standing and group-context facts, including suspension/departure invalidation, through public contracts and IAM composition. **Open:** effective revocation bounds, owner-role synchronisation and independently verified ADR-0012 composition. Identity's review remains incomplete.
