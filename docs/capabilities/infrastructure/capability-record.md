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

## Reciprocal invariant — verified UTC upstream, separate regional zone interpretation (17 November 2026)

**Owner approved:** Infrastructure must apply a governed, verified and approved internet UTC time source to the host synchronisation service. A regionally located NTP server is selected for trust, resilience and network suitability, *not* to supply a particular local time zone. [Clock](../clock/capability-record.md#approved-invariant--utc-authority-and-local-civil-time-17-november-2026) derives GMT/BST and other regional civil times by applying explicit IANA zone and daylight-saving rules to the host-supplied trusted instant. Infrastructure must surface failure or insufficient assurance rather than assert a source is verified solely because it is listed in a candidate catalogue; exact verification/holdover policy remains technical design.

## Reciprocal note — approved CLK-03/CLK-04 reliability boundaries (17 November 2026)

**Clock conceptual decisions approved; Infrastructure implementation not established.** [Clock's final completeness review](../clock/capability-record.md#final-completeness-review--eight-concerns-resolved-17-november-2026) requires Infrastructure to provide approved verified UTC synchronisation and a clearly evidenced, versioned source-quality status to authorised host consumers: applied versus desired source, authentication result, sync freshness, offset/uncertainty, degraded/holdover/unavailable state, policy version, failure and recovery. An NTP hostname or successful current-time read alone cannot certify trust. Infrastructure owns step/slew corrections, leap-smear compatibility, bounded holdover and recovery mechanics; no tenant source selection. Infrastructure does not own business expiry decisions, monotonic timeout policies or Clock's time-zone conversion. Exact assurance thresholds, synchroniser and host interface remain technical design.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Infrastructure applies and verifies host/backend operational configuration, including NTP/UTC synchroniser. Configuration may offer privileged deployment-level selections only if explicitly approved; tenant/account time preferences never govern shared UTC. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-07 (Option A):** Infrastructure, not Configuration, is authoritative for privileged NTP/NTS provider selection, allowlisting, deployment application, source verification and failure recovery. Require approval/audit evidence in Infrastructure procedures; tenant/account IANA display preferences cannot affect shared UTC. Earlier conditional proposals for Configuration-managed time-source selection are not adopted.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.
