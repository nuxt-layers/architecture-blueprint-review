# Capability Record — IAM Integration

## Capability Name
`iam_integration` (existing blueprint directory); governing name `iam-integration`.

## Status: Available, Installed, Configured, Operational, Enabled, Authorised and Proposed
**Established architectural responsibility; conceptual specification proposed in draft [PR #73](https://github.com/nuxt-layers/architecture-blueprint-review/pull/73), not owner-approved.** Implementation repository and root `CONTRACT.md` exist; implementation readiness and suite acceptance are **not** verified. Availability, installation, configuration, operation and authorisation are deployment-specific independent states, not established by the repository's existence.

## Purpose
Provide the single secure composition entry point and coordination interfaces for the IAM suite: Identity, Authentication, Authorisation and Profile. A host should be able to obtain trustworthy `resolveCaller`, `decide` and `tasks` through the documented one-call composition objective, and to coordinate safe, observable multi-member operations without writing suite-specific adapters. Maintain distinct authorities, independent ports and a minimal host.

## Classification
**Established: Foundation (IAM), suite integration/composition component, not a fifth domain-data owner.** A separately packaged suite integrator is expressly established by accepted ADR-0005 and ADR-0012; avoid reclassifying it as the general-purpose external `integrations` capability. Framework-independent core with optional Nuxt integration is a prospective implementation decision, not an assertion about current packaging.

## Dependencies
Essential operational **public contracts** of Identity (directory/membership/tenant lifecycle), Authentication (verified sessions/assurance/revocation), Authorisation (resource decisions/approvals), Profile (personal data/disclosure and data-subject rights); host-provided member persistence and migration capability, key management and mail where each member requires them. Essential absence: composition must refuse protected service or return explicit unavailable/denied result; do not invent synthetic principals, roles, identities or defaults. These are wiring/service relationships, not direct member-to-member package imports or a circular Nuxt extension graph.

## Optional integrations
Audit evidence custody, Logging diagnostics, Observability health, Notifications delivery, Privacy and Legal Compliance constraints, Configuration approved policy values, Clock time semantics, Message Queue outbox transport, Scheduler execution and Workflow external approval orchestration are conditional/optional where the relevant IAM operation uses them; each may become necessary for a particular deployment or regulated workflow. Each source retains its own authority. No mandatory direct import into foundational IAM members is implied.

## Version
Conceptual contract proposal 0 (not published). Production version/API compatibility must follow the independently published member contracts. The current `nuxt-layers/iam-integration/CONTRACT.md` includes `@nuxt4-layers` dependencies and says single-call `resolveCaller`/`decide`/`tasks` is **not built**. Do not confuse this proposed specification with an implemented contract.

## Availability
Host composition must report readiness by member and by operation: `ready`, `restricted`, `degraded`, `unavailable` or `unknown`, with checked time and provenance. A healthy process or accepted transport message alone does not prove effective revocation or IAM service readiness. Scope any capability-level status by tenant, permitted audience and operation; no sensitive cross-tenant inventory disclosures.

## Capabilities offered
- One suite composition operation that validates member ports/versions and publishes verified caller resolution, effective access decisions and collected member-owned scheduled tasks, without reimplementing member services.
- Public adapters translating Identity directory, governance and subject data into member-declared shapes; translating Authentication's authenticated principal and assurance into caller contexts; mapping Authorisation decisions to common `decide` without discarding step-up, risk, recency or phishing resistance.
- Cross-member orchestration of identity reservation/sign-up, consent-appropriate profile association, membership invitation/join/leave, account pause/resume/suspension/closure, scoped role synchronisation, session and derived-access revocation, recovery holds, controlled service identities, tenant bootstrap/closure, data-subject request coordination and break-glass follow-up, only where the appropriate member contracts support them.
- Explicit partial-completion/reconciliation receipts and operational status. Orchestration is not independent Identity, Authentication, Authorisation, Profile or Audit record ownership.

## Configuration
Host provides connections, pools, secrets and member ports under their public contracts; approved tenant/host policy choices come from Configuration or governing instruments; member owners validate all floors. Compose once using secure defaults where genuinely defined. Reject missing critical keys, invalid/contradictory tenant context, mismatched contracts or unsafe policy. No host-authored IAM adapters and no universal request object. Use authoritative Clock instants and declared bounded consistency limits. Never expose operator migration pools to request traffic.

## Ownership, state and lifecycle
**No independent identities, credential/session state, grants, profile records, decisions, approvals or personal details.** Identity owns opaque identifiers, tenants, groups, memberships, governance and its own pending changes. Authentication owns sign-in factors, sessions, assurance and their revocation. Authorisation owns permissions, roles, grants, pending access changes and access decisions. Profile owns personal data and requests/erasure actions. Each owner commits its own state and event outbox. Integration owns published adapter logic, process definitions, outcome aggregation and any necessary **ephemeral** coordination state.

**Architectural decision IAMINT-01 (open):** for multi-step operations lasting across restarts, decide whether the suite integrator should own only minimal durable *technical execution checkpoints* (not domain facts), or delegate durable execution state to Workflow/Temporal coordination behind a neutral port. Neither option may silently turn the integrator into an additional IAM authority. Pending stage and correlation are not proof of downstream completion. No distributed transaction, exactly-once guarantee or automatic rollback of irreversible actions is claimed.

Example transitions: `requested → validated → authorised → accepted → coordinating → completed`; alternative `pending-approval`, `partially-completed`, `failed-safe`, `reconciling`, `cancelled`, `unknown`. Owner-specific state is reflected, not invented. Retries use stable idempotency keys per member; remediation or compensating actions require independent authorisation and may be impossible for already-revoked sessions or issued notices. Unknown/revocation-critical states remain restricted.

## Idealised public inbound contract
| Source | Input and business purpose | Authority, validation and failure |
|---|---|---|
| Host composition / operator | Member public service handles, pools/keys/mail, tenant deployment settings, approved registration, clock and infrastructure ports | Host owns wiring/secrets; validate contract versions, service readiness and least privilege; missing mandatory member/critical key fails closed |
| Authentication | Verified principal, subject, assurance level, phishing resistance, authentication and step-up times, session revocation outcome, credential recovery signals | Authentication owns sessions/factors; no browser-asserted identity; expired, contradictory or unknown assurance cannot qualify privileged actions |
| Identity | Opaque principal/group/tenant references; direct membership status, group/tenant governance, directory freshness; change and recovery events | Identity owns records and owner constraints; strong reads for high-risk actions; unknown/paused/suspended/ended never silently treated as active |
| Authorisation | Permission definitions, resource-scoped decision, risk/assurance requirement, role/approval state and owner-referenced change outcomes | Authorisation owns grants and decisions; denial, unavailable or insufficient assurance cannot be converted to allow |
| Profile | Controlled disclosure, subject request, anonymisation/retention outcome and independent per-part receipts | Profile owns personal data and request lifecycle; withheld names remain withheld; legal holds prevent automatic erasure promises |
| Requesting person, authorised administrator or service | Provisioning, suspension, recovery, request coordination, status and reconciliation commands; target reference, purpose, revision and idempotency | Trusted server caller and scoped authority essential; resource belongs to correct tenant; high/critical independent approval and step-up per owner |
| Privacy / Legal Compliance / Configuration | Applicable qualified restrictions, consent/retention/hold, approved policy version and effective scope | Separate legal, policy and domain interpretation; missing mandatory applicable evidence blocks restricted action |
| Scheduler / Message Queue / Workflow / Audit | Delivery/execution receipts, retry triggers, approved external approvals and evidence acknowledgement | Acknowledgement establishes only what the provider actually completed; stale, failed or contradictory evidence remains pending/unknown |

## Idealised public outbound contract
| Consumer | Output and permissible conclusion | Guarantees/limits |
|---|---|---|
| Host and other capabilities | Trusted `resolveCaller(request)` with tenant, opaque subject/null and full relevant assurance/recency provenance | Server-verified; request identity not client supplied; null is anonymous, not authorised; stale/unknown fails appropriately |
| Host and other capabilities | `decide(caller, action, resource)` access result, explicit deny/unavailable, risk/step-up information in detailed companion result where required | Authorisation is sole access decision authority; no success based on Identity membership alone; compatibility with ADR-0012 shared shape must preserve detailed semantics |
| Host scheduler | `tasks` aggregated from member-published public descriptors | Source member owns handlers, retries and own outbox; no invented tasks or silent duplicate registrations |
| Authorised users/operators | Cross-member operation receipt, stage, involved owner statuses, revision, effective time, pending obligations, safe recovery guidance | Receipt distinguishes requested, accepted, applied and verified; no unsupported global atomicity |
| IAM member adapters | Verified subject, directory, policy and event delivery through their declared ports | Narrow scope, provenance, consistency bound, no copied private models; revocation events are at-least-once and idempotently handled |
| Audit / Logging / Observability | Minimised correlation, stage changes, outcome and error evidence; structured technical diagnostics and health measurements | Each consumer owns its separate record; logging is not evidence custody, Audit is not source of IAM decisions; no raw credential/profile payload |
| Reporting, Privacy and authorised requesters | Scoped reconciliation/disposition summaries and export-part statuses | Source-owned qualified facts, retention/hold and disclosure restrictions; no bulk unauthorised cross-tenant enumeration |

Published outputs should identify relevant owner, correlation/idempotency reference, source revision, source/effective time, observation time, freshness, completeness, operation status, tenant scope and authorised disclosure class when material. Stable codes rather than end-user wording; versioned contracts and explicit unsupported operations.

## Public interaction model
**Commands (conceptual, not claimed as implemented):** `composeSuite` (startup operation); `startCoordinatedOperation` for named supported workflows; `getOperationStatus`; `requestReconciliation`; `cancelPendingOperation` where the owner can still cancel. Explicit operation kinds (provision, pause/suspend, closure, recovery, revoke, tenant-governance maintenance, rights request) map to appropriate owner commands; no generic unbounded privileged dispatcher. Validate caller, tenant, policy, assurance, resource, expected revision and idempotency, and record per-owner acceptance versus completion.

**Queries:** `resolveCaller`, `decide`, `getSuiteReadiness`, `getOperationStatus`, `getRevocationProgress`, `getMemberIntegrationHealth`; separate privileged diagnostic and user-self views. Return unavailable/unknown rather than fabricate fresh completeness.

**Events:** only committed member-owned events originate in member durable outboxes. Integration may publish its own **technical coordination status** if durable checkpoints are explicitly approved; never masquerade as an Identity/Authentication/Authorisation/Profile lifecycle event. Message Queue transports, does not reown. Consumers deduplicate, tolerate reordering/replay, avoid cross-tenant leakage; transport success is not application success. The current Authentication best-effort event sink must be assessed for accepted durable-outbox compliance.

**Common context (not a universal payload):** tenant and group/owner resource reference; verified subject, authentication time and assurance; operation type, source revision, correlation and idempotency; applicable policy/evidence version; UTC/effective time and timezone meaning; per-member source and completion status. Missing and contradictory source inputs trigger refusal, restriction or qualified pending status.

## Full cross-capability interfaces and direction
| Capability | Needed by IAM Integration | Supplied by IAM Integration | Relationship |
|---|---|---|---|
| Identity | Directory, governance, tenant/membership states, owned lifecycle/events | Trustworthy subject and decision adapters, orchestration instructions, delivery/reconciliation outcome | Essential public contract |
| Authentication | Session principal, assurance/recency, recovery, revoke outcomes | Identity provisioning/service governance, verified directory and legal-hold adapters | Essential |
| Authorisation | Scoped decisions, grants and approval qualifications, directory freshness | Identity directory/governance adapters, verified session subject, permission registration and role-change reconciliation | Essential |
| Profile | Disclosure and rights lifecycle, names on permitted purpose, request-part status | Verified identity/disclosure adapter, coordinated exports and source status, member part handlers | Essential |
| Audit | Accepted evidence custody status and completeness | Minimised attributable stage/operation and source receipts | Conditional; avoid synchronous cycle |
| Logging / Observability | Technical diagnostics and platform health context | Structured safe errors, correlation and telemetry | Optional service ports |
| Privacy / Legal Compliance | Qualified scope, minimisation, holds/retention | Status and action evidence to owners; restrictions applied through source contracts | Conditional |
| Configuration / Clock | Approved policy settings and effective time semantics | Validated selected settings to member contracts, correlated timestamps | Conditional service context |
| Message Queue / Scheduler | Message transport acknowledgements; registered task execution | Member-owned outbox relay tasks and published handler contracts | Conditional operational infrastructure |
| Notifications / Workflow | Delivery status and independent approval completion where selected | Approved messages/approval requests via owner-owned commands | Optional, often required by deployment |
| Reporting | Authorised summarisation request | Minimised per-owner reconciliation/read-model references | Optional |

Dependencies are directional in **package/build** terms even when business information flows both ways: adapters accept host-injected member public ports. Never cause foundational members to depend on IAM Integration package code. Denial and revocation safety apply during transport outage; do not rely exclusively on eventually delivered notifications for immediate privileged decisions.

## Security, assurance, privacy and compliance
Apply OWASP ASVS 5 L2 baseline and L3 controls where security critical; WCAG 2.2 AA for screens. Enforce server-side authorisation, no impersonation, no self-approval/self-grant, personal group sovereignty, founding and last-owner rules, high/critical dual control, trusted phishing-resistant step-up and recency. Account pause/closure/suspension must initiate Authentication session revocation and Authorisation restriction; enforce a safe restriction path during cross-member lag. Respect ADR-0017 tenant governance: parent tenant/group membership does not confer child access or legal entity authority. Require purpose-based Profile disclosure, data minimisation, secrets isolation, credential-safe logs, legally qualified holds, retention and subject rights handling. A profile erasure request cannot bypass lawful hold, and anonymisation by unlinking does not rewrite other capability records. Recovery/break-glass must be scoped, independently approved where required, time-bounded, attributable, reviewed and logged to Audit. Service identities must not act as approvers or receive prohibited critical grants.

**IAMINT-02 (open):** define and independently demonstrate the maximum *measured* window for cross-member revocation and the temporary deny/restrict mechanism during lag, including provider outage and message backlog. ADR-0005 requires revocation to reach Authentication sessions and membership changes to reach Authorisation within its directory bound; transport alone is insufficient proof.

**IAMINT-03 (technical investigation):** reconcile the current different member subject/assurance port shapes and `resolveCaller`/`decide` shared shape with preservation of recency, phishing resistance, service principals and step-up metadata.

## GUI and application host presentation
**Headless core essential; optional operator-facing suite dashboard justified, not duplicate member-owned screens.** In `nuxt-layers-test/application-test-template`-style host, a permission-gated sidebar item **IAM Operations** opens `/iam` suite dashboard (host-configurable). Show member integration health, pending/partial provisioning and revocations, workflow stage/reconciliation queue, audit linkage, owner-specific remediation and privileged diagnostics. Context actions link to existing member-owned pages: Authentication security, Identity group/tenant lifecycle, Authorisation roles/grants and Profile rights requests. A person's account overview can aggregate *authorised* source views, not copy personal or credential data. High-risk actions require contextual reauthentication/step-up, second-person approval and explicit confirmation; destructive operations must not be available solely because someone can see the dashboard. Support pages/components off (`presentation:false`), configurable route and sidebar placement, WCAG 2.2 AA, localisation, Theme Manager tokens, keyboard/screen-reader status updates, responsive layouts and privacy-safe redaction. Host owns navigation; independent member contracts remain callable without GUI.

**IAMINT-04 (open):** decide whether the suite integration package should ship an optional operator dashboard or provide only headless status contracts and host-composed navigation to existing member screens. No duplicate IAM edit screen is justified.

## Conceptual acceptance scenarios (input → expected behaviour → outcome → owner)
1. Valid suite ports and approved host settings → one-call composition, verified caller and decision and task descriptors; member-specific handles remain opaque → readiness and usable services; **IAM Integration/individual members**.
2. Missing Authentication resolver or ambiguous subject → protected action refused, no anonymous-to-admin promotion → denial/unavailable; **Authentication/Authorisation**.
3. High-risk role change with expired/non-phishing-resistant assurance or self-approval → step-up/independent approval required → pending/denied, never silently committed; **Authorisation/Identity**.
4. Account pause or suspension → Identity commits state and outbox; sessions revoked and Authorisation restricted → separately evidenced per-member states, retry on delay; **Identity/Authentication/Authorisation**.
5. Replayed delivered lifecycle event → no duplicate role assignment/revocation side effect → idempotent owner output; **receiving member**.
6. Outbox transport unavailable after Identity commit → coordination marked partial/reconciling and access restricted appropriately, never globally complete → pending/unknown plus recovery; **Identity/Integration**.
7. Cross-tenant operator tries to inspect or resume another tenant's account → deny and redact existence, no leakage → forbidden; **Authorisation/source owner**.
8. Recovery changes assurance/recovery hold → sessions and privileged approvals restricted pending independently owned decisions → stage receipt; **Authentication/Identity/Authorisation**.
9. Profile export/erasure request with hold → per-part export/held disposition, never promise deletion of other owners' records → qualified status; **Profile and each part owner**.
10. Revoked session but stale directory cache → privileged access denied pending fresh verification → safe restriction not allow; **Authentication/Authorisation**.
11. Unsupported impersonation or automatic irreversible rollback → explicit unsupported/refused result → no operation; **suite contract**.
12. Operator dashboard disabled → headless operations and source member screens still function where composed → no mandatory GUI dependency; **host**.

## Findings and decision register (18 November 2026)
| ID | Status | Finding / decision |
|---|---|---|
| IAMINT-01 | **Open owner decision** | Technical checkpoint ownership vs external durable workflow for long-running cross-member work |
| IAMINT-02 | **Open owner decision + acceptance measurement** | Explicit revocation consistency/deny window and outage semantics |
| IAMINT-03 | **Technical investigation** | Verified ADR-0012 shape adapters preserving each member's full assurance and caller semantics |
| IAMINT-04 | **Open owner decision** | Optional suite operator GUI vs headless suite status plus existing member screens |
| IAMINT-05 | **Implementation alignment** | Current published `CONTRACT.md` uses legacy `nuxt4-layers` naming, outdated references and host-authored multi-call wiring; accepted ADR-0012 single composition not built |
| IAMINT-06 | **Implementation alignment** | Current Authentication sink/other event delivery semantics require durable source-owned event and bounded revocation reconciliation evidence |
| IAMINT-07 | **Proposed** | Adapter/public orchestration surface, stage receipts, per-owner outcome provenance, tenant-safe health and reconciliation |
| IAMINT-08 | **Acceptance** | Prove one-call documented consumption and ≤50 Nuxt host lines by CI/user, plus isolation, replay, fail-closed recovery, approvals, accessibility and headless operation |

## Governing evidence and limits
- Accepted [ADR-0005 IAM suite](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/decisions/ADR-0005-iam-suite.md); [ADR-0012 composition](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/decisions/ADR-0012-trivial-composition.md); [ADR-0017 tenant governance](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/decisions/ADR-0017-tenant-hierarchy-and-accountable-digital-control.md), accepted [ADR-0018 policy governance](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/decisions/ADR-0018-policy-governance-and-commercial-entitlements.md), and normative Capability Standard. Opening governing SHA `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
- Current target [implementation root consumer contract](https://github.com/nuxt-layers/iam-integration/blob/master/CONTRACT.md) was read, **not executed**. Individual [Identity](https://github.com/nuxt-layers/identity/blob/master/CONTRACT.md), [Authentication](https://github.com/nuxt-layers/authentication/blob/master/CONTRACT.md), [Authorisation](https://github.com/nuxt-layers/authorisation/blob/master/CONTRACT.md) and [Profile](https://github.com/nuxt-layers/profile/blob/master/CONTRACT.md) contracts are independent implementation evidence, not proof of suite acceptance.
- **Not conceptually signed off**; no implementation edits or local tests; open owner decisions and future acceptance work persist. No merge without approval.


---

## Approved IAM suite façade and presentation decision — 18 November 2026

**Owner-approved conceptual direction (PR #73):** `iam-integration` is the IAM **composition, façade and coordination layer** between the host and four distinct IAM members: Identity, Authentication, Authorisation and Profile. `configuration` is a cooperating source of approved host/tenant settings, **not a fifth data-owning IAM member**. The integration publishes one documented host entry point and shared IAM service ports, member adapters and cross-member orchestration, but is **not** an obligatory network API gateway through which every operation must pass. Hosts and peers may use individual members' authorised public contracts directly; no bypass of server-side security or member policy is implied. IAM Integration must not duplicate the members' state, roles, credentials, profiles, or decisions.

### Approved presentation split
Two **separate optional presentation contributions** are conceptually approved:

1. **IAM Suite Dashboard:** the primary `/iam` overview reachable from a single host-owned **Identity & Access Management** (or **IAM**) sidebar entry. It provides an authorised orientation and coherent navigation to **Identity** (people/groups/tenants/memberships), **Authentication** (sign-in/MFA/sessions), **Authorisation** (roles/grants/permissions), **Profile** (personal information/disclosure/rights) and contextual **Configuration** settings. Each member retains its own screens, actions and authoritative service/data. IAM Integration should only offer public composition/view contracts and reusable overview/navigation components: **no duplicate group editors, permission engines, credential screens or personal-data forms**. The host's overview must distinguish personal/self-service and privileged administration paths; navigation visibility is not access permission.
2. **IAM System Health:** a distinct, privileged area for integration and reconciliation operators, linked from the dashboard only when authorised; expose member connection/contract readiness, partial provisioning, delayed revocation, failed outbox delivery, pending recovery/approvals, source-linked audit evidence, idempotent reconciliation and diagnostics. **Do not make technical health the default IAM dashboard**. Show accurate `complete`, `pending`, `partial`, `restricted`, `unknown` status based on source confirmations rather than inventing global atomic success. Reconciliation actions are server-authorised, with risk-specific step-up and independent approval.

### Host presentation contract and routes
Use [`nuxt-layers-test/application-test-template`](https://github.com/nuxt-layers-test/application-test-template/blob/master/README.md) as the representative shell: homepage `/`, host test dashboard `/admin`, responsive collapsible sidebar, top bar, Theme Manager entry `/theme-manager`. A derived IAM test application can add one **IAM** sidebar entry, optional `/admin` card and configured `/iam` overview; member-owned pages remain linked via public routes. Optional host-configurable `/iam/system-health`, `/iam/operations`, `/iam/operations/:id`, `/iam/reconciliation` consume IAM Integration public status/recovery services. These are **proposed illustrative paths**, not published implemented routes. The host owns actual routes, naming, navigation and branding, and may disable/relocate components. A composable package may contribute presentation only through documented optional public exports, not private package imports.

**Headless parity:** `presentation:false` means no suite pages/components, without disabling APIs, orchestration, lifecycle or member screens; `pages.enabled:false` permits host-placed reusable components. All privileged screens recheck trusted actor/tenant/resource and necessary assurance server-side. Privacy-scoped disclosure, redaction/no-existence leakage, keyboard accessibility, WCAG 2.2 AA, responsive/mobile, locale/i18n and Theme Manager semantic tokens apply. Do not expose health diagnostics, credentials, raw tokens or cross-tenant directories through the normal dashboard.

### Consequences and acceptance
**IAMINT-04 is now RESOLVED / owner-approved:** ship an optional reusable suite dashboard *and* separate optional privileged system-health presentation, with host-owned navigation and member-owned detailed screens. Whether the implementation uses one package export or separately loadable presentation modules remains an implementation detail under the ADR-0012 host composition budget. Acceptance must verify both presentation-disabled/headless mode and member screens, user versus operator access, route overrides, configuration contextual links, no duplicated records, real operation-status provenance, accessible sidebar/mobile interactions and use of Theme Manager. No current implementation or tested UI is asserted.


## Preserved pre-existing reciprocal notes (15 November 2026)

## Cross-capability note — Authentication suite choreography (15 November 2026)

**Established:** The IAM suite composes the separate public contracts of [Authentication](../authentication/capability-record.md), Identity, Authorisation and Profile; it does not take ownership of their records. **Agreed conceptual direction:** coordinate account provisioning, suspension/closure and revocation, recovery, service-identity governance, data-subject operations and emergency account lifecycle without private imports. Preserve assurance, recency, session revocation, fail-closed behaviour and ADR-0012's single-call composition objective. **Open:** bounded revocation consistency and verified integration contracts. IAM integration's individual conceptual review remains incomplete.

## Cross-capability note — Multi-step IAM accountability (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** IAM Integration coordinates distinct Authentication/Identity/Authorisation/Profile operations without reowning their facts. **Proposed:** approved multi-step provisioning, suspension, step-up, delegation, recovery and account closure retain source identifiers/correlation and independently qualified receipt status in [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026). The suite must not create a synchronous circular Audit dependency or substitute Audit evidence for originating IAM decisions. Its conceptual review remains incomplete.

## Cross-capability note — Authorisation composition and revocation (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns policy evaluation, role/grant records and access decisions; IAM Integration coordinates trusted Identity and Authentication inputs without taking ownership. **Proposed:** harmonise single-call ADR-0012 composition, role synchronisation, approval choreography, assurance/freshness, emergency restrictions, revocation and retryable cross-capability delivery. **Open:** measured consistency, direct privileged operation trust and no-cycle event choreography. IAM Integration's review remains incomplete.


## Owner-approved review elaboration — published contracts, standards, libraries and presentation (18 November 2026)

**Status:** Owner approved the recommended conceptual direction in conversation, including documenting these concerns; named API signatures, library adoption and undecided IAMINT-01/02/04 alternatives remain proposals or acceptance tasks. Do not confuse this review with a published implementation contract. Current governing master checked: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint master advanced to `02b2302e90e94680928abb9ac5553e81c9e67a53` after branch opening. Reconcile all concurrent master changes before merge.

### Main design issues, stated plainly
The suite must connect verified sign-in, directory, access decisions and personally controlled profile disclosure without owning any of their records. An account pause, suspension or closure is not complete merely because an event was sent: members must enforce safe restrictions, revoke sessions, reconcile downstream role access and publish verifiable per-owner progress. Require independent high-risk approval, tenant isolation, anti-impersonation, freshness/step-up and privacy even while another service is unavailable. Operations lasting across restarts need reliable, idempotent checkpoint/recovery coordination. One-call host composition is mandatory under accepted ADR-0012, but not yet delivered by the current published implementation contract.

### Existing published versus idealised public contract
**Documented but unverified implementation:** [`iam-integration/CONTRACT.md`](https://github.com/nuxt-layers/iam-integration/blob/master/CONTRACT.md) currently describes public adapters including `identitySubjectResolverFromAuthentication`, `identityAccessDecisionFromAuthorisation`, `identityApprovalPolicyFromAuthorisation`, `authorisationDirectoryFromIdentity`, `authorisationGovernanceFromIdentity`, `authenticationIdentityFromIdentity`, `authenticationServiceGovernanceFromIdentity`, `profileAccessDecisionFromAuthorisation`, `profileRequestCoordinatorFromMembers`, `tenantExportFromMembers`, legal-hold and event-handler adapters. The host must currently wire member-specific providers, permissions, database and migrations manually. That contract retains legacy `@nuxt4-layers/*` references and says its required one-call `resolveCaller`, `decide`, `tasks` is not yet implemented. Existing `CONTRACT.md` is evidence of *documentation*, not proof of running behaviour or a reliable version of all four current member contracts.

**Approved idealised conceptual interfaces:** **inbound** trusted host-provided member service ports, credentials/secrets and approved config; verified Authentication principal/assurance/recency and session status; Identity directory/governance and committed lifecycle events; Authorisation resource-specific decisions/approval outcomes; Profile disclosure and rights-request statuses; qualified legal/policy restrictions and execution receipts. **Outbound** one-call composition result; verified `resolveCaller`, fail-closed `decide`, source-owned `tasks`; explicit multi-step operation command outcomes and restricted status/reconciliation queries; minimum necessary operation evidence, diagnostics and authorised reporting views. Each output must state whose record it reflects, source revision, effective/observed times, tenant/subject disclosure scope and whether it was *requested, accepted, completed, denied, incomplete or unknown*; none may invent cross-member atomicity. Detailed command names remain illustrative until public contract ratification and implementation alignment.

### Logging, Audit and Reporting — reciprocal public information boundaries
| Cooperating capability | Input IAM Integration would publish | Output to IAM Integration / authorised host | Ownership, safeguards |
|---|---|---|---|
| Logging | Sanitised technical diagnostic events with severity, operation stage, correlation, controlled error codes, component/tenant-safe context, latency and retry classification | Diagnostic reference, sink/transport status and scoped troubleshooting query if actually exposed by its contract | Logging owns diagnostic records/sinks; never credentials, raw tokens, Profile payloads or authoritative approval evidence |
| Audit | Source-linked security/governance evidence, requested/approved/applied/failed transitions, attributable actor and independent approval, replay/correction references, privacy-safe correlation | Evidence accepted/pending/rejected/unknown, custody reference, integrity/completeness check where supported | Audit owns evidential custody; source IAM members own source decisions, Integration owns coordination semantics only; transport acknowledgement is not Audit receipt; high-risk evidence failure needs policy-backed safe handling |
| Reporting | Authorised source-reference or derived, minimised operation-status/freshness/revocation/backlog/approval-stage summaries | Tenant-scoped report definitions, aggregates, exceptions and report provenance through its own public contract | Reporting owns reports, not IAM source records; reauthorise each query and export; suppress identities/small cohorts where disclosure risk requires; no grant from mere group ancestry |

Avoid a synchronous hard Audit/Logging/Reporting package cycle. Logging and Audit should consume only defined public event/evidence types, and Reporting consumes authorised query/read models, never private IAM databases. The conceptual capabilities' own pending reviews cannot be assumed implemented.

### Established standards to reuse
| Standard | Appropriate scope / limit |
|---|---|
| [NIST SP 800-63-4](https://csrc.nist.gov/pubs/sp/800/63/4/final), especially [63B-4](https://csrc.nist.gov/pubs/sp/800/63/B/4/final) and [63C-4](https://csrc.nist.gov/pubs/sp/800/63/C/4/final) | Authentication assurance, recency, federation and assertion handling; baseline for preserving assurance across adapters, not permission policy ownership |
| [OWASP ASVS 5.0](https://github.com/OWASP/ASVS/tree/master/5.0) | Verification of authentication, authorisation, security logs, safe failure, session security; platform L2, L3 when high risk |
| [SCIM RFC 7643](https://www.rfc-editor.org/rfc/rfc7643) / [RFC 7644](https://www.rfc-editor.org/rfc/rfc7644) | Where provisioning/discovery synchronises accounts/groups with outside directories; Identity retains canonical records; not a reason to expose personal data or make SCIM mandatory |
| [OAuth Security BCP RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html), OpenID Connect and WebAuthn/FIDO2 | Secure protocols in Authentication / external federation; IAM Integration should consume member assertions, **not reimplement** tokens, passkeys or sign-in |
| [CloudEvents 1.0](https://cloudevents.io/) / W3C Trace Context | Optional standard envelopes for cross-capability events and distributed correlation; events remain source-owned, trace IDs do not establish permissions |
| [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457.html) | Portable machine-readable errors where an HTTP boundary is exposed; do not introduce it as a forced internal TypeScript shape |
| [WCAG 2.2 AA](https://www.w3.org/TR/WCAG22/) and BCP 47 | Inclusive keyboard/screen-reader design and localised screen messages |
| UK GDPR / ISO 27001 controls / NIST 800-53 AU/AC/IA | Minimise disclosure, retain audit evidence and document controls; legal applicability must be qualified by Legal Compliance rather than asserted by a library |

### Permissively licensed maintained libraries — selective, not a new mandatory stack
| Library | Confirmed licence and use | Boundary/decision |
|---|---|---|
| [Zod](https://github.com/colinhacks/zod) | MIT; validate public adapter input/output and configuration at trust boundaries | Preferred for existing TypeScript contracts; reject bad shapes rather than trust casts |
| [OpenTelemetry JS](https://github.com/open-telemetry/opentelemetry-js) | Apache-2.0; contextual tracing/metrics for partial work, latency and cross-service correlation | Prefer platform Observability/Logging integration; no sensitive baggage or authentication facts in tracing attributes |
| [Temporal TypeScript SDK](https://github.com/temporalio/sdk-typescript) | MIT; durable long-running steps, replay/retry and cancellation via existing provider-neutral `temporal-gateway` if chosen | Conditional on IAMINT-01; preserve provider-neutral orchestration port and independently verify server/SDK/worker licensing and hosting; no hard direct dependency on cloud service |
| [p-retry](https://github.com/sindresorhus/p-retry) | MIT; bounded transient retry for explicitly safe idempotent calls | Optional; don't retry denied privileged changes, unknown provider outcomes or irreversible operations blindly |
| [Pino](https://github.com/pinojs/pino) | MIT; structured technical logging with redaction | Ideally supplied by Logging capability, not installed as an independent IAM-owned log subsystem |
| [openid-client](https://github.com/panva/openid-client) / [jose](https://github.com/panva/jose) | MIT; mature OIDC client and JOSE/JWT crypto primitives | Use inside Authentication/federation owner only when needed; IAM Integration must not duplicate token verification/authenticator ownership |
| [pg / node-postgres](https://github.com/brianc/node-postgres) | MIT; PostgreSQL client and pool where the host supplies member database connections | Only when needed by host/owning members; IAM Integration must not query another member's tables |

**Selection gate:** verify release activity, licence of *the exact version and transitive dependencies*, security maintenance, Node/TypeScript compatibility and absence of mandatory cloud/control-plane features before implementation. Avoid source-available, delayed-open, commercial-tier-dependent or externally controlled managed services. An optional support contract does not itself make a permissive upstream library non-open-source; distinguish the code's licence from the service's commercial terms.

### GUI and test-host integration — concrete conceptual design
The [application-test-template](https://github.com/nuxt-layers-test/application-test-template/blob/master/README.md) establishes a home page `/`, shared `/admin` test dashboard, responsive collapsible sidebar, top-bar branding/authentication placeholder and Theme Manager link `/theme-manager`. It is explicitly **local test mode** and must not be deployed publicly with Theme Manager's unauthenticated test endpoints.

**Recommended host pattern:** permission-visible (but server-rechecked) sidebar entry **IAM Operations** → host-configurable suite dashboard `/iam`, with an admin card under `/admin` in a derived `iam-integration-test` application. Existing authentication, identity, authorisation and profile pages stay owned by those members. IAM Integration provides only read-only status and cross-member *coordination* views or headless contracts, not duplicate credential/role/profile editing.

| Route (illustrative) | Screen / data source | Permissions and behaviour |
|---|---|---|
| `/iam` | Suite dashboard: member health, restricted/degraded operations, pending revocations, recovery queues, links to source screens | Admin/operator visibility, tenant-scoped status, accessible states; no unauthorised information leakage |
| `/iam/operations` and `/iam/operations/:id` | Coordinated-work list and detail: source-owned stages, pending/partial/unknown, correlation and remedy; each stage links to owner record | Role-limited read, always verify data on server; redacted source links |
| `/iam/reconciliation` | Failed or delayed propagation, review and retry; explicit owner-specific action approval | Privileged access; step-up and independent approval as applicable, idempotency and safe retry |
| `/iam/health` | Configuration/readiness by member and contract, safe diagnostics, non-secret dependency status | Operator-only; no raw keys, tokens, protected subject data or private internals |

**Presentation choice IAMINT-04 remains open:** The *screens and navigation patterns* are approved review recommendations; whether the suite ships its optional dashboard component or the host presents the headless public status contract remains a packaging decision. Preferred low-coupling path is a reusable optional presentation contribution with `presentation:false`, `pages.enabled:false`, route/message overrides, Theme Manager semantic tokens, responsive sidebar and WCAG 2.2 AA. Only host owns final navigation. User-self account links should route to member-owned screens, not disclose operational health.

### Approval, acceptance and outstanding alignment
**Agreed conceptual direction:** keep owner separation; expose consistent public operation/caller/decision/status surfaces; minimise diagnostic/evidence/report data; use standards and commercially permissive libraries where needed; follow application-test-template's sidebar-to-dashboard pattern without duplicating member UI. **Still open:** IAMINT-01 technical checkpoint owner, IAMINT-02 enforceable measured revocation window/restrictions, IAMINT-04 GUI packaging. **Implementation alignment:** update the target root `CONTRACT.md` in its own separate implementation PR later, not here. Future acceptance must prove disclosure, status consistency, failure modes, recovery, event replay, 50-line composition budget, routes, translation/accessibility and test-mode isolation by user/CI.
