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

## Cross-capability note — Audit of privileged infrastructure changes (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** The host/infrastructure owner controls deployment, secret provision, backups, restores and provider selection, while Audit owns accepted accountability evidence and integrity statements. **Proposed:** trusted control-plane producers emit selected sensitive migration, restore, privilege and capture-control events to [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026); Audit reports checkpoint/rollback ambiguity and does not claim local-only proofs survive complete administrator compromise. Operational log sinks remain Logging. Infrastructure's conceptual review remains incomplete.

## Cross-capability note — Clock source synchronisation and operator GUI (17 November 2026)

**Conceptual Clock direction owner-agreed; Infrastructure review incomplete.** [Clock](../clock/capability-record.md#owner-approval-and-ntp-governance-clarification-17-november-2026) retains the typed synchronous `now()` consumer port and never becomes an NTP client/daemon. Infrastructure operates OS time synchronisation, provider reachability, NTS authentication where supported, fallback/holdover and applied-policy status; Configuration may supply a privileged approved provider policy. A shared host clock cannot be changed by tenant or Profile preferences. Infrastructure/host owns the optional authorised **Time synchronisation** operator screen, reading measured status from Observability. Record server/source revision, offset/freshness and failure state; surface alerts and accountable privileged changes through Observability/Audit respectively. Do not mix leap-smeared and non-smeared time sources; provider trust cannot be inferred solely from DNS name. Implementation interfaces and assurance thresholds remain deferred.

## Reciprocal note — Approved host UTC authority and synchronisation boundary (17 November 2026)

**Clock ownership approved; Infrastructure integration remains conceptual.** See [Clock's UTC-source classification](../clock/capability-record.md#approved-utc-source-classification-and-geographic-selection-17-november-2026). Infrastructure owns selecting/applying NTP/NTS policy to OS synchronisers, source authentication and reachability, compatible leap-second/smear handling, fallback/holdover, failure recovery and applied policy revision. Approved national authority candidates include UK NPL's UTC(NPL) public internet service, US NIST; Cloudflare offers NTS; regional volunteer NTP Pool DNS such as `uk.pool.ntp.org` and `europe.pool.ntp.org` are not national laboratories. Confirm live endpoints, permitted use and security properties before any production selection. Host location and assurance—not tenant civil time zone—govern source choice. The optional **Time synchronisation** operator screen belongs to Infrastructure/host presentation, with safe settings from Configuration, health/history from Observability and server-side operator access checks. Clock's `now()` stays a host-supplied synchronous port, not a per-request NTP fetch.
