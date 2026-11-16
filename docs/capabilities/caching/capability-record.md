# Capability Record — Caching

**Capability:** `caching`  
**Status:** **Proposed** Foundation capability; conceptual review for owner approval. Not implemented, accepted as a new governing architecture decision or production-ready.  
**Evidence checked:** 16 November 2026. Governing `nuxt-layers/architecture-rules` `master` at `eaca8cfd33e292a43e9552ad8e2946295e168472`; blueprint `master` at `ddb0ce6a6fbd2f442a3767636c08dd8fd10ab927`.  
**Implementation evidence:** No `nuxt-layers/caching` repository or root `CONTRACT.md` was confirmed by repository discovery; do not infer public exports or behaviour.  
**Conceptual sign-off:** CACHE-01–03 approved on 16 November 2026; additional provider, monitoring and service-offering follow-up proposals remain under review.

## Purpose and architectural classification

**Established:** The governing [catalogue](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/catalogue.md) lists Caching as a **Foundation candidate**: “Cache provider ports, expiration and invalidation; source capabilities remain authoritative.” Accepted [ADR-0012](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/decisions/ADR-0012-trivial-composition.md), [ADR-0016](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/decisions/ADR-0016-controlled-layer-specialisation-and-composition.md), [Security §16](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/security.md) and [Privacy](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/privacy.md) govern composition, isolation, source authority, derived-copy integrity, erasure and residency.

**Proposed:** Provide a reusable, provider-neutral **derived-result acceleration and freshness-control boundary**. Consumers opt in to caching specific results and declare the owning source, scope, dependencies and permitted staleness. Caching enforces lifecycle, isolation, invalidation and coherent failure semantics; it never upgrades a cached copy into an authoritative fact or grants access. The core is headless and usable without Nuxt. A separate package, deployment, cache server or persistent store is **not** presumed.

### Architectural classification and ownership gate

| Gate | Finding |
|---|---|
| Distinct responsibility | Shared safe reuse, expiry, invalidation, provenance and degradation of derived values across capability boundaries |
| Authority | Owns validity **of cached copies**, not validity of originating business data or security policy |
| Presentation/composition alternatives | Not merely a GUI or host composition: shared invariants apply to multiple independent consumers |
| Stateless library alternative | A small library could implement local memoisation; it cannot alone guarantee cross-worker invalidation/operational visibility where required. Independent Foundation responsibility provisionally retained, implementation form deferred |
| Persistence | None required for the conceptual boundary; optional ephemeral/derived entries and operational metadata. No business source-of-truth table |
| Contract and dependencies | Consumers use a published provider-neutral port. Origin capabilities publish permitted source versions/invalidation facts. Host connects adapters without cycles |
| Security/GUI | Server-side protected operations; no end-user screens required. Optional administrative diagnostics only |
| Disposition | **Proposed: retain Foundation capability**, with implementation kind evaluated against a minimal framework-independent package and optional shared backing service |
| Evidence status | Candidate in governing catalogue, no verified implementation `CONTRACT.md`; conceptual approval still pending |

## Ownership, exclusions and native behaviour

**Caching owns (proposed):** cache entry lifecycle (absent, loading/coalescing where supported, valid, expired/stale, invalidated, unavailable); interpretation of declared freshness constraints; tenant/group/visibility partition enforcement; cache-specific entry metadata (identity, source/revision, creation, expiry, validation and invalidation state); authorised purge/invalidation operations; safe provider fallback and status; aggregated diagnostic counters. A successful write means a derived copy was handled, **not** that source data was committed.

**Caching does not own:** original domain records, business transactions, IAM memberships, authorisation decisions or policy, personal data lifecycle policy, source revisions, authoritative search indexes, report definitions, rendered content, HTTP response policy of the host, the authoritative audit trail, technical Logging, Observability, provider credentials or infrastructure provisioning. The source capability determines whether a value is cacheable and its maximum permissible staleness; Caching may impose stricter constraints but cannot loosen them.

**Proposed native minimum:**
1. Register/describe an opt-in cache use case: owning capability, logical namespace, data classification, scope dimensions, purpose, source-dependency or revision model, maximum TTL and consistency class. Default to no cache for undeclared or unsafe data.
2. Read a scoped derived value with explicit hit/miss/stale/rejected/unavailable status; enforce scope, declared policy and age before return; report value provenance and limitations.
3. Write/refresh a value only from a trusted source-owner path or authorised consumer, enforcing source version and declared freshness ceilings; reject older revision replacement, ambiguous ownership and unapproved sensitive material.
4. Invalidate a key, group, namespace, source revision or affected tenant/subject scope through an authenticated, bounded operation; prevent old in-flight fills or out-of-order event replay from resurrecting an invalidated value.
5. Expire entries predictably, bound capacity, support bounded background refresh and revalidation only where the source permits; prefer fail-closed/no-result on an unprovably current security-sensitive value.
6. Support safe read-through composition and duplicate refresh coalescing as optional optimisations, never as a guarantee of exactly-once source work or delivery.
7. Expose safe operational health and per-namespace visibility, including hit ratio, miss, staleness, invalidation lag, rejected values, evictions and provider outages without leaking keys or source payloads.
8. Recover from provider outage, cold start, restore, region migration and replay by treating uncertain values as misses and revalidating at the source.

**Lifecycle:** `absent → valid → expired/stale or invalidated → evicted`; refresh creates a new source-qualified generation. `unavailable` is a provider/service condition, not proof of value freshness. “Stale” is a disallowed read state by default; a source-approved bounded stale response is a separate, explicitly qualified outcome. Cache loss is permitted; original business state remains intact. Do not invent durable business events for routine cache fills/evictions.

## Idealised public inbound contract

All rows are **Proposed logical inputs**, not implemented functions or universal request objects. “Essential” means essential to an operation of the stated kind, not a mandatory compile-time dependency.

| Source | Information / command supplied | Purpose; authority and validation | Requirement; failure behaviour |
|---|---|---|---|
| Source capability / authorised consumer | Cache-use declaration: logical namespace, purpose, owner, classification, permitted scope dimensions, key input/fingerprint, source revision model, TTL ceiling and consistency mode | Source owns truth and cacheability; validate namespace ownership, configuration provenance, permitted sensitivity and completeness of all result-affecting inputs | Essential to use; reject unknown declarations |
| Trusted host / Identity | Resolved tenant, owning group, subject or authorised audience context; tenant lifecycle changes | Identity owns tenant/group and membership facts; never trust a bare client-supplied ID or assume parent-tenant access | Essential for protected entries; missing or contradictory scope → deny/miss |
| Authentication / Authorisation / source owner | Verified caller and access decision, effective scopes, assurance, resource constraint and policy revision or permitted capability-owned verification | IAM owns session/access standing; origin domain owns resource-specific restrictions. Re-check at read/action boundary as required; cache does not decide new permissions | Conditional to protected reads; uncertain/expired security context → refuse cached disclosure |
| Source owner | Validated value, version/ETag/equivalent monotonic lineage, source timestamp, dependency scope, permitted lifetime | Owning source is authoritative; validate schema/limits, revision order, classification and tenant | Essential for fill; no qualified source → miss/unavailable, not invented value |
| Source owner via event transport or direct port | Committed update, removal, revocation, reclassification, transfer, key rotation, erasure or invalidation with source identity/version | Source owns change; verify origin, scope, revision, duplication and causality; do not treat an event as authorisation | Conditional; delayed delivery must respect source risk bound; mark affected cache uncertain when unable to guarantee it |
| Configuration / legal-compliance / privacy | Approved tenant/host limits, security floors, retention, region, allowed data categories and effective versions | Configuration owns declared values; policy owners own applicable restrictions. Reject any setting that weakens mandatory ceilings | Conditional; unknown mandatory policy → no unsafe retention or disclosure |
| Host adapter / optional external provider via Integrations | Provider capability/health, region, isolation, availability and error evidence | Caching owns abstract validity; provider owns transport/storage mechanics only | Optional; provider failure → classified miss/degraded, never silent stale allow |
| Authorised operator / source owner | Purge, disable, reconcile, warm-up or scoped inspection command with reason/correlation | Check delegated permission, source ownership, bounded effects and protected audit evidence | Optional operational command; unauthorised/overbroad → reject |

These are **source facts** (source versions, IAM context), **commands** (get, put, invalidate, purge), **external evidence** (provider status) and **configuration/policy context** (limits and restrictions) respectively. None independently supplies business authority.

## Idealised public outbound contract

| Output / conceptual service | Consumers | Meaning and authority | Status, provenance and disclosure |
|---|---|---|---|
| Cache-use/namespace registration result | Source owner, composition root | Acceptance of declared cache semantics, **not** source truth | accepted/rejected; declaration version, scope; configuration privileged |
| Scoped lookup result | Authorised consumer | `hit`, `miss`, `stale-permitted`, `invalidated`, `rejected` or `unavailable`; a hit contains a derived copy **only** | Source owner/version, computed/validated time, expiry, audience, freshness class; return value only after access/disclosure checks |
| Store/refresh result | Source owner or delegated adapter | Value stored, superseded, ignored as older, refused or provider uncertain | generation/version, accepted bounds; never equate with source transaction success |
| Invalidation/purge receipt | Authorised origin or operator | Requested scope accepted, applied, pending, partially applied or uncertain; distinct from confirmed propagation | Scope, source revision, generation barrier, correlation, coverage/lag; no premature global-complete claim |
| Scoped cache status/health | Operators, Observability, source capabilities | Availability, invalidation lag and hit/miss/error rates; may indicate need to bypass cache | Sanitised, tenant-safe aggregates, timestamp, coverage; no raw keys, credentials or personal payloads |
| Cache-specific lifecycle signal (only when needed) | Operators/consumers | Invalidation propagation failure, cache unusable, affected-namespace state or purge outcome; **not** a domain event | Deduplicable identifier, source and operation refs, status/provenance; event redelivery possible |
| Evidence/diagnostics | Audit, Logging, Observability, Reporting under their own contracts | Security-sensitive purge/configuration access and incident evidence to Audit; sanitised technical diagnostics to Logging; performance/health metrics to Observability; aggregate data to Reporting | Explicitly separate intake acknowledgement, delivery and source outcome; purpose-limited disclosure |

**Commands:** describe/use a cache namespace; `lookup`; `store/refresh`; `invalidate`; `purge`; `disable/enable` or `reconcile` where authorised. A lookup is a query; store and invalidation are operational commands, not business operations. **Queries:** value lookup, safe scope/health, declaration/effective-policy status. **Events:** do not publish routine hit/miss/fill/eviction as domain events; use exceptional state/propagation signals where actionable. Source owners publish their own committed change events from their durable outboxes; Message Queue only delivers.

## Shared context and contract invariants

Shared context is **conceptual, not one universal DTO**: origin capability, tenant and owning-group scope, trusted caller/audience when relevant, source resource reference and version, normalized result-affecting inputs, locale/timezone where they change result, allowed classification, effective configuration/policy versions, source commit time, validation time, generation, correlation/idempotency identity, effective retention/region and provider identity.

**Established mandatory floors:** [Security §16.3](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/security.md) requires keys partitioned by tenant and all inputs affecting results (including caller scope where relevant); Authorisation decisions cannot outlive Authorisation's allowed consistency bound. Stores remain server-protected and tenant/group isolated. [Security §§16.5–16.6](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/security.md) requires idempotent/out-of-order-safe derived update handling, erasure reaching caches, documented retention and region compliance. [Privacy](https://github.com/nuxt-layers/architecture-rules/blob/eaca8cfd33e292a43e9552ad8e2946295e168472/docs/privacy.md) requires storage inventory including caches.

**Proposed additional contract guarantees:**
- Cache keys are scoped opaque identifiers derived from *all* semantic result inputs; prohibit inter-tenant reads, cross-user leakage, privilege widening and key enumeration. Protect sensitive raw keys in logs and metrics.
- TTL is an upper bound, **not** proof that an unchanged original remains valid. Cache validity is the intersection of source freshness, security standing, effective policy, region and relevant invalidation/version knowledge.
- Security-sensitive changes take precedence over performance. Where revocation speed cannot be guaranteed, protected operations bypass cache or fail closed; a cache hit never overrides an Authorisation deny or missing source-owned business invariant.
- Duplicate, delayed, out-of-order and replayed invalidations cannot re-authorise or reinsert superseded content. Invalidation/barrier status must expose partial or uncertain outcomes.
- A value may be **cached** yet **not currently disclosable**. Scope and read purpose must be evaluated against live/qualified rights. One caller's permission must never imply another's.
- No exactly-once cross-worker guarantee, global atomic purge, zero-lag freshness or replay-proof source authority is promised without independent evidence. Faults are stable typed outcomes, not leaked internal exceptions.
- Cache unavailable must not turn a denied action into an allowed one; source fallback is allowed only through the source capability's authorised public contract.
- Cache disposal and erasure must also address backups/provider retention, subject rights, contractual data region and historical restore. The source owner remains responsible for deciding record disposition; Caching executes derived-copy cleanup and provides evidence.

## Cross-capability relationships

All relationships below are **proposed** unless governing requirements are explicitly identified. A relationship does not impose an import or package dependency.

| Capability / party | Inputs to Caching | Outputs from Caching | Absence / ownership |
|---|---|---|---|
| Any source capability (e.g. Booking, Billing, Publisher, Asset) | Authoritative results, changed-source events, revision, scope, allowed freshness | Derived scoped lookup, fill, invalidation status | Optional acceleration; source operates normally without cache and retains all business authority |
| Identity | Resolved tenant/group/subject and lifecycle/standing revision | Scoped invalidation support | Missing verified tenancy → no protected value; Identity owns memberships |
| Authentication | Caller/session assurance and session changes | Qualified cached display/reference data, never session authority | Failed session standing → deny/bypass; Authentication owns sessions |
| Authorisation | Access decision, scopes, policy revision/revocation consistency requirements | No unrestricted decision cache; safe invalidation and limited qualified acceleration only if Authorisation permits | Missing/uncertain access → fail closed; [existing reciprocal note](../authorisation/capability-record.md) |
| Configuration | Versioned effective cache settings and scope | Effective cache policy/status | Safe defaults or disable cache; configuration ownership remains external |
| Privacy / Legal Compliance | Data classification, rights/retention/holds/residency obligations | Purge completion/partial failure evidence | No storage contrary to mandatory restriction |
| Message Queue | Delivery of committed source-outbox invalidations | Consumer acknowledgements/failures, not new business events | Delivery loss beyond permitted freshness → bypass/deny, reconcile source versions |
| Scheduler / Workflow | Conditional refresh/maintenance execution or approvals where justified | Scoped tasks, outcome references and health | Core correctness independent of maintenance scheduling; no domain workflow ownership |
| Integrations / infrastructure / host | Optional provider binding, capabilities, secrets and region | Provider-neutral operations, health and status | Native minimal local/host-provided operation; no forced external provider |
| Audit | Capture requirements and source-specific accountability context | Authorised purge/config/security actions and evidence refs | Do not assert Audit recorded anything until acknowledged; define risk-specific fail behaviour |
| Logging | Technical sink | Sanitised hits/misses/errors, latency and correlation | Logging outage must not claim a source or cache business failure |
| Observability | Metric/trace ingestion contract | Safe efficiency and invalidation-lag signals | No mandatory dependency for source correctness |
| Reporting | Authorised aggregate metric demand | Aggregated cache service/usage/performance measures | Reporting never owns cache or original domain facts |
| Search / SEO / Publisher | Published source revisions, address/status changes and per-purpose output declarations | Safe derived representation invalidation | Search index, content and publication authority remain with their own owners |
| Clock | Trusted time and timezone semantics where semantically relevant | Time-qualified expiry and provenance | Clock ambiguity triggers conservative expiry; no new time authority |

**Dependency discipline:** Source owners expose ports/events without importing Caching. Caching does not import IAM, domain packages or private stores; the host wires published contracts and provider adapters. Both public-contract and Nuxt extension edges must remain jointly acyclic under ADR-0016.

## Configuration, security, external modes and recovery

**Native/default proposal:** in-process/host-supplied provider-neutral caching with safe expiry and local invalidation; if it cannot satisfy a consumer's required cross-instance freshness, **disable that use case or bypass caching** rather than pretend global coherence. Larger deployments may opt into a shared provider through host composition or Integrations. The provider handles storage/transport, not validation authority. This is not a recommendation to create a new database or Redis deployment.

**Settings:** allow tenant/namespace limits for TTL maxima, object size, data sensitivity, capacity, region, refresh/background work, stale-read eligibility, invalidation lag ceiling, provider selection and visibility. Mandatory source/IAM/legal floors override configurable preferences. Unsupported guarantees must be explicitly refused.

**Provider selection/transition:** expose provider capability and region compatibility, fallback modes, isolation proof, current generations and transition state. Switching providers must cold-start or reconcile against authoritative source versions; never treat imported entries as verified simply because they were present in another provider. External providers cannot become a second authority for source facts.

**Outage:** classified failure; optional authorised direct source read, safe miss, or fail closed according to risk. **Delayed events:** retain generation/version barriers, detect gaps where feasible, and expire/bypass until reconciled. **Restore:** treat snapshot copies as suspect and verify effective source/policy version and region. **Erasure:** revoke affected entries across all active copies and record incomplete disposal separately from request acceptance. **Capacity:** bounded eviction is a performance event, not data loss.

## Presentation and application-test-template

**Proposed:** Caching is **headless by default** and requires no end-user screen, CRUD interface or mandatory sidebar item. Optional, separable *administrator/operator* presentation could provide:
- Cache status: provider health, tenant-safe capacity, miss/hit/stale rate, invalidation lag and clearly labelled degraded conditions.
- Namespace detail: owner, purpose, classification, effective policy and source/revision age **without exposing payloads or secret keys**.
- Restricted operations: scoped invalidate/purge/disable with impact preview, confirmation, permission check and audit outcome.
- Diagnostics: error and latency trends, recent partial invalidations and reconciliation status.

The **host** owns navigation, routes and branding. If enabled in a representative test application, a host-owned `Caching` sidebar entry could open its optional dashboard within the common shell; no automatic registration or production route is asserted. Source and role restrictions must apply on the server as well as to screen visibility. Support headless mode, WCAG 2.2 AA, localisation and Theme Manager semantic vocabulary. Do not modify the test template in this review. Its root `CONTRACT.md` was not confirmed by the attempted retrieval, so the representative navigation pattern is blueprint evidence, not a claimed tested API.

## Conceptual contract acceptance scenarios

| Scenario / input | Expected behaviour / output | Authoritative owner |
|---|---|---|
| 1. Normal cacheable read, valid qualified source value | Initial miss, authorised source read/fill, subsequent scoped hit with source version/expiry | Source owns original; Caching owns entry validity |
| 2. Domain update after a cached Booking availability read | Committed version/invalidation makes old generation unusable; next read checks Booking | Booking |
| 3. Tenant/user/scope crossover with a known key | No cross-scope disclosure or informative key enumeration; reject/miss | Identity/Authorisation for scope; Caching for isolation |
| 4. Invalid declaration/TTL beyond source ceiling | Reject with policy/validation reason, do not store | Source policy and Caching contract |
| 5. Duplicate or reordered change and refresh | Same or older revision cannot restore removed/superseded value | Source version; Caching generation |
| 6. External provider outage | Classified unavailable/miss; source-backed fallback only if authorised; no unsafe stale allow | Source and IAM |
| 7. Restore from an old snapshot | Entries with uncertain current revision/policy are invalidated or revalidated | Source and IAM |
| 8. Subject erasure, tenant region change or legal hold | Targeted purge/migration according to policy; report pending/partial status and lawful exceptions | Privacy/Legal Compliance and originating source |
| 9. Reporting consumes service metrics | Receives sanitised tenant-authorised aggregates with coverage/time, not raw keys or cached transactions | Caching metrics; source facts remain elsewhere |
| 10. Unsupported request for strong consistency on an eventual-only provider | Explicit unsupported/rejected or bypass; no false guarantees | Source's consistency contract and Caching |
| 11. Authorisation membership revocation during TTL | Cached sensitive allow cannot outlive authorised revocation bound; live recheck/bypass/deny | Authorisation and Identity |
| 12. Operator purge while an old refresh is in flight | Old refresh cannot resurrect prior generation; purge receipt records actual propagation status | Caching |

## Architectural issues, approval and acceptance register

| ID | Type / status | Question or required action | Recommendation |
|---|---|---|---|
| CACHE-01 | **Agreed conceptual direction (approved 16 Nov 2026)** | Retain independently bounded Foundation capability versus consolidate as stateless library/provider adapter? | **Retain the conceptual capability** for cross-consumer validity/invalidation invariants, but require evidence before creating a separate repository or stateful service |
| CACHE-02 | **Agreed conceptual direction (approved 16 Nov 2026)** | Minimum cross-instance invalidation guarantee and whether shared coordination is mandatory for selected risk classes | Make guarantees **per use case**, fail closed/bypass where provider cannot prove them; quantify revocation/lag with source owners during technical design |
| CACHE-03 | **Agreed conceptual direction (approved 16 Nov 2026)** | Should bounded stale-while-revalidate ever be permitted, and for which classes? | Opt-in only for explicitly source-approved low-risk public/non-sensitive representations; forbid for sensitive authorisation and critical domain mutations |
| CACHE-04 | **Technical investigation** | Evaluate library-only, in-process, PostgreSQL-backed and optional shared-store adapters, including cost, concurrency, region and failure semantics | Benchmark later; **no provider choice or database mandated here** |
| CACHE-05 | **Implementation/contract work** | If implemented, publish independent root `CONTRACT.md`, one composition operation, typed statuses/permissions, capacity and provider requirements | ADR-0012/0016 compliance; verify 50-line Nuxt adapter budget if applicable |
| CACHE-06 | **Acceptance/verification** | Prove tenant/group isolation, IAM revocation, version barriers, late refresh, erasure, residency, redaction, outages and degraded operation | Negative/chaos scenarios and measurable freshness evidence before production claims |
| CACHE-07 | **Established requirement** | Respect source authority, §16 cache-key/retention/security floors and documented storage register | No owner approval needed to restate governing rule |

**Approval discipline:** CACHE-01–03 are owner-approved conceptual decisions dated 16 November 2026; see approval register below. CACHE-04–06 are not questions requiring conceptual owner approval. No accepted ADR is amended by this record.

## Architectural consequences and handover

- **No governing changes are made here.** Caching remains a governing **Foundation candidate** pending owner review.
- The blueprint catalogue/register should retain candidate status until a separately authorised classification decision; do not mark it implemented or operational.
- Existing [Authorisation reciprocal note](../authorisation/capability-record.md) is preserved. Additional reciprocal notes can summarise a **proposed**, not implemented, cache boundary without completing those capabilities' alphabetical review.
- A consuming capability can opt out entirely and must not silently depend on Caching for its authoritative correctness.
- Technical design must settle adapter choice, detailed contracts, concurrency/propagation, operational sizing, concrete APIs, tests and whether any UI is justified.
- **Next alphabetical directory:** verify against the current `docs/capabilities/` tree before proceeding; this review does not assert a successor without directory verification.


## Owner approvals — 16 November 2026

**Agreed conceptual directions (owner explicitly approved):**
- **CACHE-01:** Retain Caching as a bounded **Foundation capability** owning shared cache-validity and invalidation rules, with no presumption that it needs its own repository, database, standalone process or Nuxt Layer. Independently evaluate implementation kind during technical design.
- **CACHE-02:** Apply source-specific, risk-sensitive freshness and consistency. Where a backend cannot meet a source's cross-instance invalidation/revocation bound, bypass the cache or refuse the unsafe result. Do not promise universal instant invalidation.
- **CACHE-03:** Allow bounded stale-while-revalidate **only on explicit source-owner opt-in** for low-risk public/non-sensitive representations; reject stale disclosure for security decisions and critical domain mutations.

These approvals settle the architectural direction only; they do not establish implementation compliance, select a provider, or authorise merging a PR. The earlier table's `CACHE-01`–`CACHE-03` “Open” labels describe the *pre-approval proposal* and are superseded by this approval register.

## Follow-up investigation — provider neutrality, PostgreSQL and open-source options (16 November 2026)

**Owner-approved conceptual requirements (16 November 2026):** Caching must expose one backend-independent public service contract; backend selection, provider-specific lifecycle, secrets, connection management and performance remain behind host-composed adapters. Consumers must not embed Redis, SQL, wire-protocol or vendor-specific operations in their conceptual interface.

Evaluate a lightweight in-process adapter, a PostgreSQL-backed adapter and a separately deployed Redis-compatible adapter; select per use case and permitted consistency. **PostgreSQL-first evaluation is preferred but not yet a binding implementation selection**; no extension or independent datastore is mandated. Candidate research:
- PostgreSQL `UNLOGGED` tables can hold disposable derived values but are truncated after crash and are not replicated. They are unsuitable as the sole home for durable evidence or historical operational metrics: https://www.postgresql.org/docs/18/sql-createtable.html
- `pg_ivm` incrementally maintains eligible materialised views, not arbitrary cross-capability key-value entries: https://github.com/sraoss/pg_ivm
- `pg_cron` can schedule maintenance, but must not displace Scheduler's contractual scheduling authority: https://www.enterprisedb.com/docs/pg_extensions/pg_cron/
- `LISTEN/NOTIFY` is useful for low-latency hints, **not** a durable invalidation journal. Reconcile through committed source versions/outboxes after missed delivery: https://www.postgresql.org/docs/current/sql-notify.html
- `Valkey` (BSD-3-Clause), `Garnet` (MIT), `KeyDB` (BSD-3-Clause) are permissive Redis-compatible separate services; **none is itself a PostgreSQL extension**. Compare licensing, maintenance, workloads, region support and operational cost: https://github.com/valkey-io/valkey ; https://github.com/microsoft/garnet ; https://github.com/Snapchat/KeyDB
- `Redis 8` offers AGPLv3 plus source-available alternatives; copyleft/network obligations need deliberate legal review. `Dragonfly` current source-available licensing requires specific restrictions review and must not be classified as permissive open source: https://redis.io/blog/what-is-valkey/ ; https://github.com/dragonflydb/dragonfly/blob/main/LICENSE.md
- `PgCache` is an interesting PostgreSQL-proxy/extension combination but is pre-1.0 and Elastic-License-2.0 source-available, not a general-purpose cache abstraction or a permissive baseline: https://github.com/PgCache/pgcache

Preserve this provider comparison as **technical investigation**; do not convert it into mandatory infrastructure, a provider dependency or a premature licence compliance assertion.

## Approved conceptual direction — operational state, Audit, Logging, Observability and Reporting

**Owner-approved conceptual responsibility boundaries (16 November 2026); technical implementation and retention decisions remain open:**
1. **Caching owns its live operational state**: provider health, cache namespaces, entry generation/version, scope, expiry, invalidation progress/coverage, failures and sufficient bounded counters to diagnose operation. Avoid storing every lookup as a durable record; cache entries and real-time counters are disposable except for security-critical coordination barriers whose durability must be analysed against risk.
2. **Logging** receives sanitised structured *technical diagnostics* (timeouts, cache misses when meaningful, failed refresh, provider errors, evictions, correlation). Logging owns log sinks, retention and technical search. No raw values, sensitive cache keys or subject data.
3. **Audit** receives attributable *security/material governance actions and outcomes*: privileged configuration changes, purge/disable, attempted unauthorised inspection, mandatory erasure/invalidation failures and recovery. Audit owns evidence integrity, retention and reporting of receipt. Ordinary cache hits are not individually required audit records; distinguish accepted purge, completed purge and acknowledged Audit capture. Define risk-specific behaviour if required evidence cannot be recorded.
4. **Observability** receives bounded live and historical metrics/traces: hit/miss ratio, value age, lookup/refresh latency, errors, capacity, invalidation lag and provider health. It owns telemetry aggregation, alerting and history; Caching remains authoritative only for its contemporaneous operational state. Protect tenant-scoped cardinality and inference.
5. **Reporting** consumes authorised, minimised time-window aggregates and provenance from Caching/Observability under their public contracts, producing user-facing historical comparisons, capacity/cost/performance trend reports, and incomplete-data warnings. Reporting owns report definitions and artefacts, not source entries or live cache authority.
6. **Presentation:** optional host-linked operator dashboard for live health/performance, namespace details, scoped maintenance and historical trend links. The host controls navigation; live metrics are not a substitute for verified security/freshness guarantees. Optional headless mode remains valid.

**Additional acceptance scenarios:** healthy cache with Logging sink down; Audit unavailable during risk-critical purge; provider temporarily inaccessible while Observability continues to show historical health; partial invalidation after interrupted worker; cross-tenant dashboard/aggregate inference attempt; Reporting unavailable while caching continues; recovery from an `UNLOGGED` cache loss without losing mandatory evidence; loss of `LISTEN/NOTIFY` hint followed by source-version reconciliation.

## Approved conceptual requirement — single public offering and minimum consumer needs

Expose one **provider-neutral headless capability service** through host composition; this is a *conceptual service shape*, not a prescribed TypeScript API:
- **Describe/register use case:** consumer identity, source owner, namespace, data class, scope and all key-affecting inputs, dependency/revision schema, freshness/stale policy and declared fallback.
- **Lookup:** validated caller/scope and logical key/context → hit, miss, source-qualified permitted stale or typed denial/unavailable, with source version/time, age, expiry and permitted disclosure; never infer source permission from a cached hit.
- **Fill/refresh:** trusted source-qualified value/version/context → accepted, superseded, rejected, uncertain with entry generation. A cache fill is not a domain commit.
- **Invalidate/purge:** trusted source change (prefer durable outbox) or authorised administrative operation → scoped propagation status (accepted/pending/completed/partial/uncertain), version barrier and evidence reference; older in-flight refresh cannot recreate invalid content.
- **Inspect/status:** effective policy and provider capabilities/health, safe operational statistics and provenance for an authorised tenant/namespace.
- **Optional subscribe:** cache-specific operational incidents or materially changed state, not duplicative domain events or routine hit/miss traffic.

Consumers depend only on this conceptual port, *not* directly on a Redis client or PostgreSQL schema. A source-capability contract declares cacheability and necessary invalidation facts; Caching consumes them without importing the source's implementation. The composition root connects a backend, source-version provider and any permitted IAM/policy inputs. One documented composition operation and self-contained consumer contract are required if implemented under ADR-0012. No dependency cycles or direct source-table reads.

**Further decisions still open:** the division of live per-instance counters versus durable aggregated history; specific critical invalidation acknowledgement semantics under multiple workers; choice and operational cost of adapters; exact security audit-capture outage policy. These should be resolved during targeted architectural/technical design, without reopening approved CACHE-01–03.


## Follow-up owner approval — 16 November 2026 (backend neutrality, telemetry and consumer contract)

**Agreed conceptual direction:** The project owner explicitly approved the recommendation to make Caching backend-agnostic and to supply its services to consumers through one provider-neutral, host-composed public contract, while separating responsibility for operational state, Logging, Audit, Observability and Reporting. This approval covers the responsibility and interface boundaries described immediately above; it does **not** select PostgreSQL, a PostgreSQL extension, Redis-compatible technology, a database/schema, hosting topology, a metric store or any implementation API.

**Normative compatibility:** The governing security/Privacy constraints, ADR-0012 single-call composition and ADR-0016 acyclic public-contract and Nuxt extension dependencies remain binding. Provider options remain technical research, with PostgreSQL-first **evaluation preference**, not compulsory PostgreSQL use. No source capability may be required to import a Caching implementation or provider library; opting out must preserve source correctness.

**Operational data boundary:** Caching owns the authoritative *present operational status* of its own entry validity, provider state and invalidation work. It supplies structured, privacy-minimised events/measurements; Logging owns diagnostics, Audit owns accountable evidence, Observability owns telemetry time-series/alerts, and Reporting owns authorised analytical reports and historical presentation. Live dashboard information and historical reports may coexist without assigning the same durable record to multiple authorities. Routine cache reads/fills do not automatically create permanent audit records. Explicitly distinguish a requested, applied, propagated and verified purge.

**Pending technical/assurance work (not owner architectural questions):** provider adapter requirements and extension/licence evaluation; risk-specific distributed invalidation confirmation and source-version barriers; instrumentation and metric aggregation granularity; history retention/cost policies; mandatory security evidence capture and outage response; performance benchmarking; contract acceptance through an independent consumer; optional operator UI and server-side authorised operations. Respect the policy authority of Configuration, Privacy, Legal Compliance and source owners in selecting any defaults.

**Reciprocal documentation:** Agreed architectural interaction boundaries are reflected in the [Logging](../logging/capability-record.md), [Audit](../audit/capability-record.md), [Observability](../observability/capability-record.md), [Reporting](../reporting/capability-record.md), [Configuration](../configuration/capability-record.md) and [Privacy](../privacy/capability-record.md) records. The existing [Authorisation](../authorisation/capability-record.md) revocation/cache safety note remains relevant and is not duplicated. None of these notes constitutes that neighbour's complete conceptual review or a verified runtime contract.
