# Configuration — Capability Conceptual Record

**Status:** Conceptual review proposed for owner decision (17 November 2026); non-normative. Existing reciprocal approvals are preserved below. **Class:** Foundation (governing catalogue). **Published implementation:** [nuxt-layers/configuration](https://github.com/nuxt-layers/configuration/blob/master/CONTRACT.md), contract version 1, implementation alignment incomplete. **Review:** [PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53). **Baseline:** governing master `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint master `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`.

## Purpose, independent justification and classification

Configuration is the Foundation capability responsible for the **registered, schema-validated, scoped, approved settings that describe or govern the configurable aspects of a deployment, tenant or group** and for resolving their effective values with traceable provenance. The governing catalogue describes the facts a site, tenant or group states about itself, changed through approvals. The published implementation additionally exposes limited account-scoped values. A setting is not thereby an authoritative business fact, policy interpreter, entitlement, permission, legal determination or personal-profile record.

It is independently justified by its schema registry, scope resolution, constrained inheritance, risk-graded change control, recorded revisions and history, change transitions and read/disclosure semantics. A capability consumer should obtain approved effective values through a documented port, not rediscover Configuration's persistence or reconstruct precedence.

**Authority classification:** Foundation is established. The separation of capability responsibility, Nuxt packaging, optional presentation and deployment is governed by the Capability Standard and ADR-0001/0009/0012/0016. This review neither changes a governing ADR nor asserts the conceptual proposals here are implemented.

## Ownership and exclusions

| Configuration owns | Other authority / exclusion |
|---|---|
| Declared setting catalogue: key, schema, allowed scopes, visibility, sensitivity, risk, override/inheritance rule, default, activation restrictions | Domain owners define meanings, permitted choices, validation beyond schema and enforcement; the host supplies deployment choices |
| Approved values, their owning context, revisions, source/approval provenance, effective and retired state | Identity owns tenants, groups, hierarchy, memberships and lifecycle; Profile owns personal identity attributes and preferences |
| Bounded effective-value resolution and per-key provenance for an authorised context | Authorisation owns access decisions; Authentication owns sessions and assurance; neither is inferred from settings |
| Configuration change requests, decisions, delays, digest/concurrency control, activation and change history | Workflow may orchestrate independent review, Audit owns independent evidence; operational Logging is not audit |
| Its own persistence, lifecycle housekeeping, domain events and durable outbox | Message Queue transports committed events, Scheduler runs tasks; they do not own configuration facts |
| Controlled public, member and server disclosures, export/import of its settings, and scope disposal | Legal Compliance determines applicable duties; Privacy owns specialised privacy constraints; Publisher owns published policy documents |
| Site/organisation descriptors **only insofar as they are registered settings**, such as displayed site name and approved contact references | Site Hosting owns hostname verification/routing and certificate/proxy operation; no unilateral tenant assignment via a value |
| Optional host-level selection references for external services where declared | Integrations owns provider connections, secrets and synchronisation; Infrastructure owns applying infrastructure configuration |

**Invariants:** mandatory security and legal floors cannot be weakened through a setting, no undeclared keys or secret values in ordinary settings, no cross-tenant inheritance, no authorisation inherited from group lineage, no implicit tenant-parent hierarchy inheritance, no auto-escalation on unknown context, no personal Profile duplication, and no settings-only change of an authoritative domain lifecycle. The proposed tenant hierarchy and policy taxonomy in governing ADR-0017/0018 are **not accepted** on the inspected master (both files say “Proposed for acceptance”); apply them as provisional review guidance, not binding amendments.

## Native service and information lifecycle

**Established in published contract:** host-declared namespaced schema settings plus reserved site/organisation/contact/social/legal/seo keys; platform, tenant, standard group and limited account scopes; deployment and declared defaults; locked deployment settings; group lineage inheritance when declared; effective per-key provenance; public/member/server visibility; risk-graded change requests, approval/rejection/cancellation, delayed application, history, export/import, retention, tenant/group/account disposal and Identity lifecycle reconciliation. Validations reject duplicate/reserved keys, undeclared values and invalid defaults at registration. Supported distinctions must remain as documented, not broadened by inference.

**Conceptual lifecycle:** declare/version → validate registration and deployment constraints → propose scoped revision with justification and expected digest → authorise requester → assess effect/risk → independent approval or prescribed delay/hold → revalidate authority, context and expected revision → schedule/apply → emit committed change event and immutable reference to its evidence → supersede/retire/expire → retain or dispose under authorised retention/hold policy. Rejection, cancellation and conflicting revisions do not become effective. An accepted request is not necessarily an activated value.

**Resolution:** separate account-context and group-context operations, not an invented combined universal hierarchy. Established account path is account → tenant → platform → deployment → default; established group path is group → eligible nearest ancestor where `inherits: lineage` → tenant → platform → deployment → default. Locked keys resolve from deployment. Authoritative tenant identity is derived from trusted host context. A setting's availability at a scope does not imply authority to read it; effective values carry source scope and revision. Tenant-parent inheritance is **not** established.

**Failure/recovery:** unregistered/invalid keys fail validation; unknown/unauthorised tenant or group does not fall through to another scope; unresolved essential policy prevents protected action rather than selecting a permissive default; unknown approval, stale digests, closing scopes and insufficient assurance fail closed. Idempotent retry must retrieve the authoritative request/result before deciding whether to reapply. Timeouts or delivery failures do not imply activation or rollback. A permitted rollback is a newly authorised revision, preserving history; delayed/held changes are revalidated at activation. Retention/deletion respect independently determined holds.

## Idealised public inbound interfaces

These are conceptual surfaces, **not claims of implemented callable names**. Required/optional is relative to the named operation, not a mandatory Nuxt package import.

| Input and origin | Meaning and authority | Validation; absence/uncertainty |
|---|---|---|
| Setting declarations from the host and relevant domain owners (required for each registered key) | Key, version, type/schema, allowed scopes, default, visibility, confidentiality, risk, inheritance, lock and effective-policy boundaries. Domain owner remains authority for meaning | Reject duplicates, reserved keys, schema/default mismatch, weakening protected floors and incompatible version migrations; no arbitrary unknown key |
| Deployment configuration from trusted host (conditional) | Locked or fallback non-secret values and deployment selection; host owns its decision | Validate before registration/exposure; do not let tenant override locked choices; missing locked source is unconfigured, not editable |
| Trusted tenant/group/account references and Identity lifecycle/lineage (required for scoped operations) | Identity is source of tenant/group/account existence, membership, ancestry and closing state; no client-asserted tenancy | Verify trusted identity/scope and compatible revision; unknown, stale, contradictory or closing contexts refuse protected writes |
| Caller evidence from Authentication and permission decision from Authorisation (required for protected operations) | Authenticated identity, assurance/recency, authorised action on exact target resource; Configuration owns operation-specific policy | Deny absent/unknown/failed decisions, service identity self-approval, insufficient step-up, self-approval and control conflicts; server rechecks on activation |
| Change commands from authorised actors and/or Workflow (required for mutation) | Target, declared key/value patch, expected revision/digest, justification, stable request/correlation ID, decision/approval evidence and requested effective time | Revalidate schema, permission, risk, separate approver and current ownership; conflict or replay returns stable prior state rather than silently overwriting |
| Legal Compliance, Privacy and domain constraint evidence (conditional, mandatory where applicable) | Non-overridable policy floors and lawful retention, consent, hold or domain admissibility; interpretation remains with owner | Unknown mandatory restrictions block the risky act; provider terms never override law/security |
| Clock `now()` and Scheduler invocation (clock required logically; scheduler when delayed change/expiry exists) | Trusted effective instant and work trigger; Configuration decides its own state transition | Reject invalid/ambiguous schedules and duplicate task executions; missing job execution is observable pending, not presumed complete |
| Import document or prior exported snapshot (optional) | Proposal of validated values and provenance, never direct replacement of approvals | Validate schema/version, target/authority, sensitive contents, conflict and per-key risk; refuse unsafe unknown fields |
| Integrations/Infrastructure provider references (optional/conditional) | Connection reference and permitted deployment selection, not credentials or proof of provider health | Unavailable provider is explicit; do not claim provider activation solely from changed selection |

## Idealised public outbound interfaces

| Output / authorised consumers | Guarantee and permitted conclusion | Provenance, disclosure, uncertainty |
|---|---|---|
| **Setting catalogue** to host, authorised administrators and consumer capability | Registered supported keys, schema version, scopes, defaults, change risk and disclosure limits; not domain legality | Versioned registration; withhold restricted schemas/metadata where revealing them increases risk |
| **Resolved effective values** to trusted domain servers, host, optional authorised viewers | Current approved value for explicitly selected context, with per-key effective source, revision, time and policy constraints | Respect visibility and tenant/group/account isolation; “default” means declared default, not independently authorised domain policy |
| **Scope snapshot and revision** to authorised administrator and change validators | Owned setting records and current expected digests suitable for optimistic concurrency | Never leak hidden values via differences, reason codes, existence or timing |
| **Change request/decision/activation result** to authorised requester, approver, Workflow | Distinct pending, awaiting approval/hold, rejected, cancelled, scheduled, active, superseded, invalid/conflicted, or unavailable outcomes | Includes request identifier, risk, decision source, effective version/time; accepting a request is not activating it |
| **Committed domain events** via own durable outbox to Message Queue and authorised subscribers | Facts such as change requested, decided, activated, retired and scope disposed, after committed state transition | Idempotency/event IDs, tenant/scope, key/revision/effective time; avoid actual sensitive values and personal data; replay possible |
| **History and audit correlation** to authorised administrators and Audit | Revisions, who requested/approved/applied, why, when and what scope, adequate to establish accountable change trail | Audit owns independently retained accountable evidence; Logging receives sanitised diagnostics only |
| **Export and disposal result** to authorised tenant/data-rights workflows | Configuration-owned values/history within permitted scope and documented retention/deletion result | Scope isolation, legal holds, redaction and completion status; other domains export their own data |
| **Operational status** to Observability/operator | Safe health of registry, store, relay, pending maintenance or provider problems | No secrets, personal values or unauthorised tenant existence disclosure |

An effective value **does not certify** the legality of a policy, the presence of a provider, the granting of access, the existence of a financial posting or the success of a domain operation. Every downstream decision remains the consuming owner's responsibility.

## Command, query and event interaction model

- **Commands:** declare/validate catalogue (trusted composition), request change, approve/reject, cancel, schedule/activate where permitted, export/import-as-request and dispose. Bind to trusted caller and exact scope, expected revision, idempotency and evidence; return typed refusal/unavailable/conflict statuses. Higher-risk approval cannot be bypassed by reconfiguring approval policy in the same request.
- **Queries:** describe catalogue, resolve authorised effective values, read scope, outstanding changes, history, provenance and provider-selection references. Return freshness/completeness/unknown status; do not use privileged server query as an unguarded browser API. Explicitly forbid client-selected arbitrary account ID reads.
- **Events:** business facts committed by Configuration with capability-owned durable outbox; consumers handle duplicate/out-of-order deliveries and fetch fresh authoritative state when needed. No exactly-once network guarantee, no event-implied authorisation. Message Queue owns delivery, not these facts.
- **Unsupported:** generic policy evaluation, access grants, domain-rule execution, secrets vault, arbitrary cross-tenant value access, tenant-parent inheritance by default, legal status adjudication, infrastructure daemon management and automatic domain migration triggered solely by a settings edit.

Shared conceptual context is **selective**, not a new universal request object: trusted caller/assurance and tenant, optional group or account, declaration version and effective revision, source scope/provenance, request/correlation/idempotency, decision digest, Clock instant and relevant retention/constraint evidence.

## Cross-capability relationships and dependency discipline

| Cooperator | Information Configuration requires / receives | Configuration supplies | Boundary / absence mode |
|---|---|---|---|
| Identity | Trusted tenant/group/account identifiers, group ancestry, membership/lifecycle, owning resource | Scope-associated selected settings; lifecycle cleanup status | Identity authoritative; fail closed on unknown scope; no shared hierarchy |
| Authentication / Authorisation | Caller assurance/recency and server resource/action decision | Policy selections and provenance where declared; no tokens/grants | Require trusted ports and recheck; settings do not confer permissions |
| Profile | Personal preferences and authority boundary via host composition only | Tenant/group defaults and eligible setting projection | Profile remains sole personal locale/time-zone/name authority; avoid second preference master |
| Clock | Trusted instant; date/zone/pattern validation via host-composed interface when needed | Approved bounded presentation defaults and optional privileged time-source policy reference | Clock formats/validates; not owned by Configuration; NTP execution Infrastructure-owned |
| Theme Manager / UI | Presentation contract/tokens, current effective theme through host | Configuration administrative display values | Theme Manager owns effective theme; no shadow theme state |
| Site Hosting / Publisher / SEO / Localisation | Verified routing/hostname, published content and linguistic/domain constraints where applicable | Approved site descriptor, display metadata and registered preferences | Hostname value not proof of ownership; documents and translations owned elsewhere |
| Workflow / Scheduler / Notifications | Approval evidence, timed execution, delivery result | Pending change, activation status, events and approver notification intent | Workflow orchestrates, Scheduler executes, Notifications delivers; Configuration remains state owner |
| Message Queue / Audit / Logging / Observability | Delivery acknowledgment and operational/retention constraints | Durable events, accountable change facts, sanitised diagnostics, health | Independent Audit evidence distinct from logs and Configuration history |
| Legal Compliance / Privacy | Applicable non-negotiable duties, holds and privacy limits | Approved setting references and change provenance | No self-asserted compliance; refuse when necessary restrictions unknown |
| Integrations / Infrastructure / Caching | Provider support/health and allowable operational ceilings | Registered, constrained provider selection, cache/retention limits | Selection not activation; source owner enforces stronger bounds |
| Accounting / Booking / Billing / Invoice / commercial domains | Domain schemas, applicability/validation, policy minima, transition results | Approved scoped domain-setting selections and versions where declared | Domain retains transaction/contract facts; no universal policy or automatic retroactive rule rewrite |
| Federation / Content Security / Moderation / Comments Engine | Publishing/disclosure safeguards, content policy floors and safe choices | Approved per-context feature/presentation settings and versions | Source capability controls publishing, moderation, acknowledgements and delivery |

**Edges:** Configuration uses host-injected shared identity/decision/clock/context interfaces and its own store; domain owners consume its resolution surface through host composition. These are public-port interactions, **not mandatory cyclic package imports**. Provider interaction is host selected. No automatic downstream requirement is asserted for every cooperator.

## Security, privacy, compliance and provider governance

Server-side authorisation at every protected read/write/activation, tenant isolation including inherited values, verified scope origins and risk-calibrated approval/step-up. Protect administrative policies against “weaken then exploit”, last-owner takeover and unauthorised deployment override. Require least-privilege data projection, no sensitive values in events/logs, targeted rate limits, safe error indistinguishability, CSRF/origin protection, auditable approvals and explicit recovery. Mandatory baseline: OWASP ASVS 5.0 L2 (L3 as appropriate for critical operations), WCAG 2.2 AA, BCP 47/ECMA-402 internationalisation. Apply UK GDPR/GDPR as relevant with qualified legal interpretation; Configuration is not legal opinion.

**Provider-neutrality:** host selects persistent provider and external service references within supported contract; own schema, migrations, data export and failure handling remain Configuration's responsibility. Current implementation documents a PostgreSQL composition; no claim of arbitrary provider support. External secret material stays in host/Integrations secure management, never editable ordinary setting values.

**Observed implementation alignment gaps (published root CONTRACT.md):** no one-call ADR-0012 composition, no minimal-host acceptance, host-written adapter assembly required, and shared `decide` shape not exposed as prescribed; the privileged `getConfiguration` path requires explicit host authorisation. The contract describes deployment-only operation without persistence and refuses mutation; do not advertise it as full operational mode. It names `provideConfigurationDeployment` as actual deployment ingestion despite legacy documentation references. Deployment-key and account-Profile ownership caveats remain unresolved. These are future implementation work, not edits authorised by this PR.

## Conceptual GUI and host presentation

**Requires optional administrative presentation; supports headless operation.** Use the representative host's sidebar → **Configuration dashboard** pattern: the host owns navigation and route mounting. Expose scoped Settings view, registered-key search/filter, effective value vs inherited/default source, current version, permitted editor with risk and explanation, propose-change/compare view, approver queue and decision justification, scheduled/held changes, immutable revision history and approved rollback, import/export and retention/health notices. Display tenant/group context explicitly; high-risk changes show separate approval, assurance and activation. Public site descriptors may render contextually without an admin dashboard.

**Current published screens:** `/configuration` and `/configuration/changes` with configurable paths, pages enabled switch and components; explicit `presentation: false` adapter **not yet offered**. Prefer optional separable presentation under ADR-0009 without implying it exists. Use Theme Manager semantic tokens, accessible forms/dialogues/keyboard/focus states, screen-reader provenance and status, responsive layouts, i18n message keys, no untrusted HTML, private no-store admin responses and secure origin checks. An unauthorised user must neither see controls nor learn another tenant exists; server remains authoritative.

## Conceptual input → outcome acceptance scenarios

| Input / circumstance | Expected behaviour / output | Authoritative owner |
|---|---|---|
| Declared valid tenant key + authorised low-risk proposal | Validate, activate or govern per risk, return effective revision and provenance | Configuration |
| Group inherited key with nearest eligible ancestor | Resolve approved effective group value and ancestor provenance, without granting ancestor resource access | Configuration; Identity owns ancestry |
| Account request with supplied other person's ID | Refuse or expose only authorised own context, no arbitrary account value | Configuration / Authentication / Authorisation |
| Locked deployment key requested for tenant overwrite | Validation refusal; deployment value remains effective | Host selection; Configuration enforcement |
| High-risk policy change requested and self-approved | Hold/refuse, require independent qualified approval and revalidate before activation | Configuration with IAM evidence |
| Value changed after request or duplicate delivery | Digest conflict; idempotent replay does not double-apply; authoritative version readable | Configuration |
| Mandatory law/security/domain restriction absent or contradictory | No permissive fallback; explicit unresolved/unavailable result and safe blocked downstream operation | Legal/Privacy/domain owner; Configuration guards selection |
| Approved setting selects failed external connector | Selection remains traceable; no false operational “connected” guarantee; consumer reports separate failed activation | Configuration / Integrations |
| Delayed change with scheduler outage | Remains pending/overdue, then rechecked and applied once; emits committed event | Configuration / Scheduler |
| New host request from other tenant's hostname/group | Trusted tenant mapping and authorisation prevent disclosure or write | Site Hosting / Identity / Configuration |
| Tenant closure, account erasure or legal hold | Authorised scoped disposal/export with hold-aware evidence; avoid erasing another domain's record | Identity / Privacy / Legal Compliance / Configuration |
| Consumer attempts generic access grant from setting | Unsupported; Authorisation alone makes access decision | Authorisation |
| Headless consumer from public contract | One-call composition target and constrained authorised reads; detect actual composition gap in future CI | Configuration / host |

## Decision register, evidence and sign-off

- **Established (governing):** Foundation classification, bounded authority, provider-neutral contract consumption, explicit acyclic dependencies, ADR-0012 composition and outbox, IAM server authorisation, accessibility/security/privacy floors.
- **Documented but not independently acceptance-verified:** current `nuxt-layers/configuration/CONTRACT.md` scopes, permissions, change states, public functions, HTTP API, presentation and known gaps. No implementation tests or private-code audit performed.
- **Agreed prior conceptual relationships:** those explicitly marked approved in dated reciprocal notes below (not necessarily approval of this entire review).
- **Proposed for owner approval (CFG-01):** Configuration as authoritative registered-setting/resolution and revision owner, not generic policies evaluator.
- **Proposed (CFG-02):** typed effective-value response with provenance/version/time and explicit unknown or unavailable, distinguishing approval from activation.
- **Proposed (CFG-03):** source-owner validated domain constraints and safe handling of staleness/rollback and protected changes.
- **Proposed (CFG-04):** reciprocal public-port relationships and optional GUI/dashboard surface; no new direct circular imports.
- **Owner-approved (CFG-05, Option B; 17 November 2026):** Retain Configuration's bounded account scope only for explicitly registered, non-personal account-specific operational settings. Profile retains personal information, personal locale/time-zone preferences and other Profile-owned attributes; Theme Manager retains the effective theme. Every key has a declared authoritative owner. Existing published account scope is not permission to duplicate those owners. Missing or inconsistent owner declarations prevent activation.
- **Owner-approved (CFG-06, Option C; 17 November 2026):** Allow *proposed* explicitly registered resource-specific configuration contexts only through domain-owner-approved public interfaces defining stable opaque resource identifier/type, authority, allowed keys/scopes, lifecycle, validation and effective-time semantics. Configuration owns approved setting values, revisions and provenance; the domain owns resource existence, ownership, deletion/transfer/retirement, policy interpretation and enforcement. No generic resource hierarchy, automatic resource/tenant-parent inheritance or new implemented scope is inferred. Reuse of retired display names never transfers settings.
- **Owner-approved (CFG-07, Option A; 17 November 2026):** Infrastructure owns server NTP/NTS source selection, deployment changes, allowlisting, operating-system application, verification and failure handling. Configuration must not become the authoritative store or admin surface for time-source policy merely because it is configurable. Infrastructure privileged changes still require appropriate approval, change provenance and Audit evidence. Tenant/group/account display-zone choices cannot influence shared UTC synchronisation. A future narrowly scoped Configuration interface needs a separate explicit architecture decision.
- **Owner-approved (CFG-08, Option B; 17 November 2026):** Version setting declarations and preserve historical definition/value/provenance and effective periods. Require explicit compatibility/migration plans, validation before activation, controlled staging, re-authorisation for changed semantics and conflict reporting. The domain owner decides how to interpret/convert a value and whether previously committed domain records may change; Configuration manages its own accepted value/revision/activation lifecycle. Rollback is a new evidenced governed transition, not silent history mutation. Unknown or incompatible versions fail safely.
- **Implementation alignment:** one-call ADR-0012 host, exact shared ports, minimal host, separated headless presentation, acceptance and future public contract changes need separately authorised implementation work.
- **Conceptual sign-off:** **pending owner review**. Proposal is not a claim of operational readiness or statutory compliance.

---

## Owner decisions — CFG-05 to CFG-08 (17 November 2026)

**Approval:** Project owner expressly selected CFG-05 **B**, CFG-06 **C**, CFG-07 **A**, CFG-08 **B**. This approves the conceptual choices, **not** implementation, governing ADR amendments, conceptual sign-off of CFG-01–04, or merge.

### CFG-05 — B: bounded account settings

Account-specific operational settings remain permissible *only* when the key is registered as non-personal, has a single explicit domain authority, and an authorised account scope. Profile remains authoritative for personal identity data and personal locale/time-zone preferences; Theme Manager for effective theme. No second personal-preference store is created. The current Configuration account-scope API documents a mechanism, not ownership of every account-related preference. A forbidden, ambiguous or duplicate owner is rejected, not chosen by precedence.

### CFG-06 — C: domain-controlled resource-specific settings

Propose an opt-in **domain-registered resource context** public contract (not implemented today), identifying resource type, stable domain-owned opaque ID, declared eligible keys, owning authority, authorised target, lifecycle reference and version. Domain owner validates resource existence, ownership, access, transfer/retirement and business meaning; Configuration validates its own declaration and governs approved values, activation, source/version and history. Resolution never follows an invented universal hierarchy, tenant-parent relationship or display-name match. Closed/transferred/retired resource contexts require explicit revocation/migration decisions and may not be silently reused. No automatic direct package dependency; the host mediates public interfaces.

### CFG-07 — A: Infrastructure controls UTC synchronisation sources

Infrastructure owns privileged NTP/NTS source policy selection **and** application/verification. Domain/tenant/user setting pages do not edit shared server time providers. Trusted Clock instant and per-user display time-zone semantics remain distinct. Require bounded privileged Infrastructure changes, approver segregation where relevant, provenance, observability and Audit, but do not store the authoritative source selection in Configuration. Older provisional Clock/Configuration proposals below are historical alternatives superseded for **Configuration's chosen ownership** by this decision, without rewriting independently approved Clock invariants. Any future Configuration-managed approval interface is a separate proposal.

### CFG-08 — B: versioned declarations and controlled migration

Configuration retains declaration identity/schema version, value revision, approval evidence, effective interval and supersession history. Before adopting changed types/meaning/scopes, a domain-approved converter or explicit new selection is required, with dry-run-style impact assessment at the conceptual level, staged activation, unresolved/conflicting cases held, and attributable replay-safe completion. Historic evaluations use the version effective at that instant; a new revision does **not** retroactively alter an existing booking, invoice or other committed domain record. Domain owners control compatibility meaning and domain data migrations. Rollback creates a new revision; rollback to an invalid/unsafe schema is refused. No promise of an implemented generic migration engine.

**Additional approved invariants deriving from CFG-06/08:** resource identity must be authoritative and stable across rename/retirement; historical setting meaning must remain reconstructable by definition version, effective value and provenance.

---

## Prior reciprocal findings (preserved, with their original approval status)

## Review notes — Accounting settings, frameworks and delegated authorities (14 November 2026)

**Status: Provisional conceptual note, not a completed Configuration specification.** The published `nuxt-layers/configuration/CONTRACT.md` provides schema-declared settings, scoped effective values and provenance, but explicitly reports its current composition limitations. Do not infer new accounting-specific settings already exist.

- **Established boundary:** Configuration stores **validated effective selections and provenance**, not posted financial journals, authoritative books, credentials or a determination that an accounting treatment is lawful.
- **Proposed accounting settings:** Per tenant or appropriate accounting-entity context, resolve the approved reporting framework/version, fiscal-year preferences where permitted, tax regime/election references, financial policy references, accounting/Invoice authority selections and relevant provider connection identifiers. Each key needs a published schema, authorisation, scope, visibility, change risk and effective-date policy.
- **Do not assume scope support:** Configuration's current contract exposes platform/tenant/group/account and its defined precedence; an *accounting entity* is a business domain object, not one of those scopes by definition. The host/Accounting must explicitly map and authorise any effective entity context or decide whether Accounting owns a domain-specific selection record.
- **Controls:** Mandatory Legal Compliance restrictions and Accounting posting invariants cannot be overridden by configurable defaults. Changing provider or framework is a controlled business transition with approval, provenance, effective dates, validation and reconciliation—not merely a preference toggle.
- **Proposed relationships:** [Accounting](../accounting/capability-record.md), [Legal Compliance](../legal_compliance/capability-record.md), [Integrations](../integrations/capability-record.md), [Invoice](../invoice/capability-record.md).
- **Open:** which settings belong in Configuration versus Accounting-owned financial-policy records; how do entity-level keys, approved elections, historical versions and migration cut-over state resolve without a new generic settings service?

### Cross-capability relationships and evidence status

- **Verified:** Configuration's public contract supports declared keys and scoped effective values with provenance; it does not establish Accounting-specific keys or accounting-entity scoping.
- **Proposed:** Domain-approved policy selections and provider references through public, host-supplied interfaces only.
- **Next review gate:** Complete Configuration's individual alphabetical conceptual review and verify current published contract before formalising new keys or service edges.

### Cross-capability note — Authentication policy configuration (15 November 2026)

**Established:** Configuration owns scoped setting values, resolution and provenance within its published contract; [Authentication](../authentication/capability-record.md) owns the validation and enforcement of sign-in, session and assurance policy. **Agreed conceptual direction (AUT-01/AUT-06):** mandatory security floors cannot be weakened by configuration; permitted stricter tenant/application/operation settings require documented precedence, version and activation. **Open:** exact registered schemas, scope compatibility, activation, rollback and active-session effects. Configuration's separate conceptual review remains incomplete.

## Cross-capability note — Authorisation policy configuration (15 November 2026)

**Established:** Configuration owns declared scoped settings and provenance; [Authorisation](../authorisation/capability-record.md) owns permission meanings, secure policy floors, role/grant models and access enforcement. **Proposed:** governed selections, revisions, effective dates and rollback may reuse published Configuration interfaces where they fit, but complex Authorisation definitions retain their owning capability's invariants. **Open:** versioned policy schema, precedence, activation, approval and absence behaviour. Configuration's review remains incomplete.

## Cross-capability note — Booking policy configuration (15 November 2026)

**Proposed reciprocal relationship; Booking has not been implemented.** [Booking](../booking/capability-record.md) will consume approved, scoped and versioned settings for booking windows, duration, holds, cancellation/attendance rules, waitlists, visibility, channel/provider selection and retention. Configuration owns declaration, scope, effective-value resolution and provenance; Booking validates its domain rules, applies effective policies and retains the decision/version reference on each affected booking. An invalid or missing mandatory setting must not allow overselling or bypass legal/authorisation constraints. Changes affecting previously confirmed commitments need explicit Booking transition rules; no second Booking preference store in Configuration.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Store only registered, approved, scoped/versioned values and provenance for permissible organisation/archetype, service selections and bounded governance rules. Do not own legal obligations, business domain decisions, Identity ownership or entitlement decisions. Security floors locked by authoritative owners cannot be weakened by custom policy. Complex governance instruments and domain rule versioning remain open; published Configuration contract is not a universal policy interpreter.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Cross-capability note — Proposed Caching policy and freshness (16 November 2026)

**Agreed conceptual boundary; no implemented adapter or new Configuration authority asserted.** [Caching](../caching/capability-record.md) consumes Configuration's approved scoped, versioned cache limits (where declared), including maximum retention, provider availability and permitted refresh preferences. Configuration owns setting declarations, scope, precedence and effective provenance; a source capability and mandatory security/privacy restrictions define stronger freshness and disclosure constraints. Caching supplies effective operational configuration, rejected/unsupported setting outcomes and sanitised health; absence or uncertainty disables unsafe caching rather than widening TTL or access. No package dependency inferred.

**Approved conceptual boundary (16 November 2026):** Host-composed backend selection and supported namespace settings are exposed through a provider-neutral caching interface. Configuration retains declared setting provenance and precedence; Caching/source security ceilings cannot be weakened by tenant preference. PostgreSQL is an evaluation preference, not a compulsory provider.


## Cross-capability note — Clock conceptual public contract (17 November 2026)

**Proposed, not yet owner-approved.** [Clock](../clock/capability-record.md#idealised-public-input-interfaces-conceptual-contract) validates temporal values, named zones, DST interpretation, formats and the host's effective presentation overrides. Configuration owns declared, approved, scoped/versioned settings and provenance; Profile owns personal locale/zoneinfo; the composition host resolves precedence and passes permitted values. No Clock preferences persistence or direct Configuration dependency is implied; invalid settings are explicitly rejected. The Clock implementation's existing six optional host-declared preferences are not built-in Configuration keys.

## Cross-capability note — Clock NTP source selection (17 November 2026)

**Conceptual direction agreed for Clock, integration not implemented.** [Clock](../clock/capability-record.md#owner-approval-and-ntp-governance-clarification-17-november-2026) keeps its injected trusted `now()` port. Configuration may govern *deployment-level*, privileged, allowlisted NTP/NTS provider selection and source-policy revisions, with approved authority/provenance; it does not manage the NTP daemon, assert synchronisation health or permit tenant/user preferences to change shared host time. Infrastructure applies approved choices; Observability reports measured status; Audit accounts for privileged changes. Whether a deploy-time only source should instead remain purely host/infrastructure configuration is a Configuration/Infrastructure integration question for their reviews.

## Reciprocal note — Approved UTC source policy and NTP selection (17 November 2026)

**Clock conceptual boundary approved; Configuration implementation unverified.** See [Clock's source-classification and provider-selection contract](../clock/capability-record.md#approved-utc-source-classification-and-geographic-selection-17-november-2026). Configuration may own approved, revisioned **host/deployment-scope** permitted NTP/NTS source selections, authority, security requirements and precedence, if infrastructure wishes to expose change governance through its public contract. It does not own time synchronisation, offset/accuracy telemetry or the optional operator diagnostics dashboard; Infrastructure applies and verifies OS synchroniser settings, Observability owns health, Audit owns accountable changes. A tenant/account's display time zone or Profile preference has no authority to alter a shared host's NTP policy. National time authorities (e.g. NPL), NTS-capable public services and regional pools are distinct source classifications; none is an IANA time zone. Deployment-only static configuration remains a permitted design alternative until Configuration and Infrastructure independently approve their integration.

## Reciprocal invariant — UTC-source policy versus time-zone preferences (17 November 2026)

**Owner approved:** Configuration's optional privileged host/deployment source policy may select only sources that satisfy approved verification/assurance requirements; it must not reinterpret NTP geographic regions as local time zones. The effective IANA display zone is a separate authorised preference or business-rule context supplied to [Clock](../clock/capability-record.md#approved-invariant--utc-authority-and-local-civil-time-17-november-2026). Changing a tenant's display zone must never change or grant authority over the shared host's UTC synchronisation source. Infrastructure owns source verification and operating-system application.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); not an accepted public contract. See [conceptual record](../comments_engine/capability-record.md).

Configuration provides versioned scoped discussion settings such as target classes, comment/edit windows, guest policy, pre-moderation, rate limits, retention and federation choices. Comments Engine enforces its own domain constraints under effective policy and statutory/security floors; Configuration does not own comment status or override decisions of Legal Compliance/Authorisation. Unknown mandatory policy version must not silently enable posting.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not implemented or approved. [Conceptual interface](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Configuration owns setting scope, approval, persistence and policy semantics. Editor's generic formatted-field UI may be reused for authorised Configuration fields, without assuming domain state or grants.

## Content Security — reciprocal interface (17 November 2026)

**Status:** Proposed in [Content Security PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55); concurrent configuration draft review is provisional and must be reconciled before integration. See [Content Security record](../content_security/capability-record.md).

Configuration owns approved, scoped versioned scanner-profile preferences and provider budget settings within non-overridable security/legal floors; Content Security validates supported checks and executes assessments, while source owners enforce publication holds. Effective values, version, expiry and unavailable/invalid handling must be surfaced; Configuration must not become an arbitrary scanning policy interpreter.

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed configuration review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Configuration resolves approved, scoped course authoring, catalogue visibility, review, language, provider and effective-policy selections with provenance. Course owns enforcement and meaning of its own domain rules, and statutory/security minima remain non-overridable. Provisional PR #53 may affect shared presentation and precedence contracts; reconcile before merge.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-11 agreed:** Configuration resolves organisation-approved options for reviews, safeguarding, delivery, migration and retention with precedence; Legal Compliance and Privacy supply non-overridable restrictions. Course, Assessment and Credentials enforce their own rules. Accreditation and delegated awarding authority are externally evidenced facts, not configuration preferences. This note does not complete the separate configuration review.

## Events interface reciprocity — 18 November 2026

**Events EVT-03–08 approved conceptual scope (18 November 2026):** [Events](../events/capability-record.md) consumes effective/versioned event policies for disclosure, invite/RSVP handling, recurrence restrictions, provider selection, retention and approvals; applies own invariants under server authorisation. Configuration owns declaration/value/precedence and change history, not Event records or policy bypass. Attendee register/check-in specifics remain open as EVT-15. [Public contract](../../../reviews/events-contract-attendance-and-handover.md).

## Federation — reciprocal conceptual note (18 November 2026)

**Status:** Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69), not a published implementation contract or completed independent review. See [Federation conceptual contract](../federation/capability-record.md).

Configuration supplies scoped, versioned enabled-role and operator preference values; Federation owns active peer/subscription/acknowledgement state. Configuration selections never authorise publication or grant remote access; source-owner visibility, Authorisation and law govern effective disclosure. Public directional ports, explicit absence modes and acyclic package dependencies apply.


## Infrastructure reciprocal interface — 18 November 2026

**Proposed reciprocal review — 18 November 2026:** Infrastructure [conceptual control boundary](../../../reviews/infrastructure-conceptual-architecture.md) consumes allowed versioned deployment settings but retains the exclusive privileged authority to select, apply and verify approved NTP/NTS sources (previously owner-approved CFG-07). A Configuration value never grants operational privilege or overrides source trust, hard security floors or recovery constraints. `OperationalChangeResult` reports applied versus requested revision; contract pending INF-01/03/05.


## Infrastructure INF-05 approval — 18 November 2026

The [Infrastructure owner-approved clarification](../../../reviews/infrastructure-approved-contract-standards-gui.md) confirms previously agreed CFG-07: privileged NTP/NTS source selection, OS application, trust checking and recovery belong to Infrastructure/host, not Configuration tenant/user settings. Infrastructure may use Clock's public temporal operations for timestamp interpretation/presentation; Clock does not select upstream sources. No Configuration-owned NTP policy is created by this conceptual sign-off.

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Configuration retains authority for declared effective provider-selection references, scoped approvals, staged revisions and rollback (CFG-08); Integrations independently validates actual connection, provider scopes, readiness, mapping compatibility and reconciliation. A selected provider is not a verified active connection; provider cutover cannot be activated by settings alone. Read the [Integrations proposed conceptual public contract](../integrations/capability-record.md#idealised-public-inbound-contract); status INT-01–06 proposed in draft PR #76. Preserve existing Configuration approvals and use host-supplied public ports without mutual package imports.


## Legal Compliance reciprocal conceptual contract — 19 November 2026 (draft PR #85)

**Status: proposed, pending owner approval; not an implemented or published interface.** [Legal Compliance dedicated conceptual contract](../legal_compliance/capability-record.md#legal-compliance--dedicated-conceptual-review-19-november-2026) proposes scoped, time/version/source-qualified legal applicability, mandatory restrictions, holds, deadlines and uncertainty. **configuration** supplies only authoritative, minimally necessary resource/service/activity/tenant context and completion/refusal evidence through documented public contracts; Legal Compliance does not take ownership of configuration's records, business decisions or enforcement. Statutory interpretation is not personal Authorisation, Privacy's specialist consent/rights rules, or proof of regulator acceptance. Missing or conflicting mandatory legal qualification holds only the affected unsafe action; authorised source owners report applied decision version and partial/failed enforcement. Cross-capability cooperation is host-composed, not an implicit direct package dependency. Existing neighbouring decisions and active PR proposals retain their own status.
