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

## Cross-capability note — Authorisation revocation and derived cache safety (15 November 2026)

**Status:** Proposed interaction, not an established cache dependency. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) publishes decision context and source-role/grant changes; the current contract does not cache decisions across requests and requires strong Identity standing for high/critical permissions. Any future caching adapter must honour tenant partitioning, policy/resource revisions, expiry and membership-derived revocation with measurable freshness, refusing unsafe stale allows. Caching cannot own policy/role data or turn a cached decision into permanent authority. Caching's review remains incomplete.
