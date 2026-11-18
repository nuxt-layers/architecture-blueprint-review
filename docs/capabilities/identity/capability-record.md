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


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Identity retains tenant, group, membership and digital group-owner source facts. Approved ORG-01–ORG-08 require secure self-service host-mediated provisioning and multi-context membership without exposing privileged tenant/bootstrap functions. Proposed TEN-03–TEN-08/OWN-01–05 add separately governed *tenant* parentage (not the existing single-parent group tree), active human tenant-owner floor, joint digital ownership, protected transfer/succession, evidence-based disputed recovery and creator provenance. Parentage must never automatically grant child-data access. Exact invariants require an accepted governing amendment; current implementation contract does not expose tenant hierarchy.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.


## Classification reconciliation — Tenancy is an Identity responsibility (17 November 2026)

**Established governing boundary:** Tenant identifiers, tenant isolation/governance, parent–child tenancy (ADR-0017), Identity groups and membership facts belong to Identity; there is no independent `tenancy` capability authority. This preserves the legacy Tenancy reciprocal Billing finding before that redundant candidate directory is eligible for removal.

**Proposed reciprocal input/output boundary:** Billing consumes a trustworthy tenant reference, tenant/entity association and relevant scoped authority where needed, but a tenant or Identity group identifier alone never proves a legal charge issuer, debtor, payer, bill-to party or customer/supplier counterparty. Identity supplies only its authoritative tenant, group and digital-governance references; verified legal-party/contract records require a separately designated owner, not Identity. Billing returns its own charge status and commercial references without modifying tenant or group lifecycle. Cross-tenant commercial queries, charges or exports require independent Authorisation and lawful disclosure checks. Missing or contradictory legal-party evidence holds the affected operation. No direct package dependency or implemented new port is asserted.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Identity owns local opaque principals, standing, tenants and memberships, not civil-identity/KYB verification or assurance that a person is adult, a company officer or authorised seller. Proofing and legal representation evidence owners remain open. If links to verified external identities are kept, require scoped issuer, status, retention and verified subject-binding; do not equate email/domain/group with company authority. Consult the cross-capability review before changing any IAM contract.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Verification is now an owner-approved *candidate* for claims and issuer-status lifecycle. Identity continues to own opaque local principals, tenant/group memberships and standing; a civil identity, age or company verification claim does not create, merge or alter these automatically. Verify local subject bindings through public contracts and minimise third-party evidence.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); not an accepted public contract. See [conceptual record](../comments_engine/capability-record.md).

Comments Engine uses stable Identity subject/tenant/group references and status-change signals but never duplicates identities, personal data, group membership or representation. Source-owned author attribution must honour revocation, erasure and tenant isolation. Guest and remote identities require separately defined trust/provenance, not fabricated local identity records.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Identity owns trusted tenant/group/account IDs, memberships, ancestry and closing state; Configuration consumes those facts to scope its own settings and history. A setting never grants membership or authorisation, and unknown/closing scopes block protected changes. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-05/06 (Options B/C):** Identity remains authoritative for account and resource-associated tenant/group identities, membership, group lifecycle and any registered group ancestry; Configuration does not create an alternative user profile or generic resource hierarchy. Resource-specific settings require their *own domain's* stable resource identifier and lifecycle/authority checks.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.

## Employment reciprocal conceptual interface — 17 November 2026

**Status: Proposed in [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59), not an Identity API amendment.** Identity owns principals, tenant/group structures, membership and digital governance, none of which proves employment or legal employer-of-record. Employment consumes scoped standing and identifier facts and provides dated worker-engagement status signals; departures must coordinate revocation and access reviews through published IAM contracts rather than silently deleting memberships or sessions. Tenant/group identifiers do not establish the employing legal entity. Access to remuneration/personnel records requires separate Authorisation and Privacy checks. See [Employment public contract](../employment/capability-record.md).

## Cross-capability review note — Enrolment (owner-accepted conceptual)

**Enrolment reciprocal interface (owner-accepted; 18 November 2026; [Enrolment review PR #60](https://github.com/nuxt-layers/architecture-blueprint-review/pull/60)).** Identity supplies stable learner/guardian/representative identity references and independently verified authority where supported; Enrolment owns educational admission state, not Identity group membership, tenant hierarchy, guardian relationship or permission. Host-composed scoped authorised lookups must avoid student-data duplication or implied cross-tenant access. Guardian proof and eligibility remain conditional, provenance-bearing. This note is non-normative and cannot claim new Identity published APIs.


## Attendance ATT-09 — optional guest identity and later account linkage (18 November 2026)

**Owner-approved Attendance accountless-access requirement, conceptual reciprocity only:** [Attendance](../attendance/capability-record.md#att-09--owner-approved-secure-accountless-participant-access-18-november-2026) must permit activity-scoped pseudonymous participants without requiring a permanent Identity user, personal group or membership. Identity remains authoritative for **actual** digital principals, account standing and verified principal associations if a guest subsequently registers and explicitly claims earlier activity records. A verified account link is an attributed, revocable referential association with provenance, not a destructive merge or an assertion that shared email addresses identify the same person. No automatic cross-tenant linking/disclosure; no implied implemented Identity guest API. **ATT-10** cross-capability historical link ownership is owner-approved (18 November 2026); source participation remains Attendance-owned.

## Attendance ATT-11 — standards reference for optional identity proof and account linking (18 November 2026)

**Status:** Standards applicability note proposed in Attendance PR #79 (18 November 2026); ATT-09/ATT-10 are owner-approved, but ATT-11 standards mapping is not separately approved. References are design guidance unless an accepted governing rule or applicable law already makes a control mandatory. No implementation, certification or new dependency implied.

**Apply:** [NIST SP 800-63A-4](https://csrc.nist.gov/pubs/sp/800/63/A/4/final) when real-world identity proofing is justified; [NIST SP 800-63C-4](https://csrc.nist.gov/pubs/sp/800/63/C/4/final) when federated identity is used. No-account attendance does not automatically require proofing, Identity membership or a personal group. Later linking must use qualified, purpose-limited evidence of both claims, not an email match; Identity owns principal association history, Attendance retains immutable source participation history under ATT-10. Protect cross-tenant privacy and revocation; no universal guest identity master is created.

## Federation — reciprocal conceptual contract (18 November 2026)

**Status: Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69); not an approved implementation API, and does not complete this capability's independent review.** [Federation public contract](../federation/capability-record.md#independent-review-contract-completeness-and-authority-18-november-2026).

Federation may refer to Identity-owned local tenant, group, principal or service identity references for peer administration, but remote network identities are evidence and do not create Identity principals, group memberships or cross-tenant rights. Trust/endpoint status belongs to Federation; request-time permissions belong to Authorisation. Cross-node identity mapping requires separately governed proof and consent. All cooperation is via public, directional host-composed contracts with scoped failure/absence semantics; preserve existing approvals and avoid package dependency cycles.

## Cross-capability note — Gaming conceptual review (18 November 2026)

**Gaming (18 November 2026; proposed reciprocal note):** [Gaming](../gaming/capability-record.md) consumes Identity-owned principal, tenant/group and membership references through authorised public contracts; Gaming owns only game-specific participant entries and result state. Identity's tenant/group hierarchy is not a gaming bracket, and parent tenants gain no automatic visibility or administrative access to child games (ADR-0017). Game registration must not create or rewrite an Identity membership.

### Gaming portal scope correction — 18 November 2026

**Gaming scope clarification (18 November 2026, owner-provided; detailed decisions proposed):** [Gaming](../gaming/capability-record.md) is a shared game catalogue, launch portal and accepted-score/leaderboard owner, **not** a generic game engine. Independently composed game layers own their own gameplay, session/move/physics state, game rules and original results. Earlier gaming reciprocal wording implying that Gaming owns gameplay, game rounds, adjudication of moves or original raw results is superseded. This owner-supplied distinction takes precedence within this working review; no implementation or published game contract is asserted.



## Reciprocal conceptual note — IAM Integration (18 November 2026)

**Status: Proposed under [IAM Integration draft PR #73](https://github.com/nuxt-layers/architecture-blueprint-review/pull/73); not a new published implementation contract or owner approval.** Identity remains authoritative for opaque identifiers, group/tenant/membership lifecycle, owner governance, pending changes and source outbox. IAM Integration consumes only its public directory, lifecycle, governance and outbox surfaces; it supplies verified Authentication-subject and Authorisation-decision adapters, status/reconciliation and coordinated calls. Revocation and tenant restriction must remain safe under delivery delay; this note does not introduce an Identity dependency on the integration package. See [IAM Integration conceptual public contract](../iam_integration/capability-record.md).


---

# Identity — dedicated conceptual review (18 November 2026)

**Status:** Proposed conceptual specification for owner review in [draft PR #74](https://github.com/nuxt-layers/architecture-blueprint-review/pull/74). Existing owner-approved decisions above remain intact. This chapter is not a replacement for the implementation `CONTRACT.md`, approval of new interfaces, or verification of runtime conformance.

**Baselines:** governing `architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `architecture-blueprint-review/master@a4e40a5cd82a2f79e8edd872af55c22d472b61cb`; published implementation `identity/master@7cfb0d0bc6ebb824575827798e5507f4a511db57` (root `CONTRACT.md`; documented behaviour, not independently tested). Classification: **Foundation / IAM, authoritative state-owning capability**, with headless server contracts and optional Nuxt presentation. A separate Tenancy capability is neither required nor justified.

## Purpose and ownership

Identity supplies durable, opaque, local digital principal and context references, their standing, tenant isolation boundaries and independently governed tenant and group structures, membership associations, and digital governance ownership. It allows one human to participate in many independently isolated tenant/group contexts without multiplying that person's underlying local principal.

**Identity owns:** principal identifiers, kind and standing; atomic human personal-group linkage; tenant identities, separate parentage, isolation/lifecycle and verified human *digital* owner state; group identifiers, names, one-parent tree and lifecycle; direct membership and dates/status; invitations and join requests; Identity governance/change requests, approved transitions, emergency-recovery constraints, creator attribution of its own records, and durable facts/events about its state. Retain versions, actor/correlation and evidence references sufficient to explain privileged changes. A third party's evidence remains owned by its producer.

**Identity does not own:** credentials/sign-in identifiers/sessions or proof of authentication (Authentication); permissions, resource access, roles/grants or delegation decisions (Authorisation); personal profile/contact data (Profile); real-world civil identity, verified corporate control, age, legal entity and representation adjudication (Verification/qualified legal authority, ownership of legal evidence still under design); subscription, payer and debtor (commercial domains); domain resources and data-ownership decisions; tenant configuration policy (Configuration); privacy consents/legal obligations (Privacy/Legal Compliance); infrastructure scheduling, transport, audit-log custody or generic workflow design. A principal, tenant, owner, group or membership reference alone is never proof of lawful authority, commercial status, age, eligibility or cross-tenant disclosure permission.

**Governing invariants:** normative `docs/identity.md`, ADR-0003/0005 and **accepted ADR-0017**: each human has exactly one permanent, nontransferable personal group, created atomically; group forest has zero/one parent per group and no cycles; separately, tenant tree has at most one parent and no cycles; neither tree confers access or membership. Many explicit direct group memberships are possible. Active operational tenants require at least one real, currently verified, active human digital governance owner; multiple and joint owners supported. Owner removal cannot remove the last qualified human. An owner-loss case enters restricted, reviewable recovery, never a fabricated human owner. Platform operators, domain creators, commercial payers and legal controllers are not synonymous. Sensitive operations require independent policy checks and protections against self-approval or policy weakening followed by exploitation.

## Native capability services and lifecycle

1. **Principal registration and standing:** reserve → validate and idempotently confirm → active; pause/suspend → requalify/resume; closure request → protected pending period → dispose or retain on hold. Reject identity activation when atomic personal-group establishment fails. Non-human/service principals have an expressly governed kind, custody, credential-management audience and restrictions, and never count as verified human tenant owners.
2. **Tenant isolation and digital governance:** proposed protected create/request, bootstrap, describe, parent/reparent, scoped owner appointment/transfer, multi-owner approval, exceptional recovery, closure and export. Explicit pending/active/restricted-recovery/closing/closed states; state changes and cross-tenant moves must preserve separate group/data lifecycles and lawful export. Current privileged provisioning is **not** a safe browser-facing create interface.
3. **Group directory:** create, describe, rename, protected archive/delete/reparent; a single parent, cycle rejection, no inferred membership or resource authority. Group creator/founding ownership is separately guarded.
4. **Membership and admission:** invite/request/approve/accept, effective start/end, suspend/resume/leave/remove; record independent direct membership, actor, applicable approval and revision; an ended relation does not alter unrelated memberships.
5. **Governed change and exception:** privileged approvals, safety holds, last-owner checks, objection, break-glass with retrospective independent review and narrow expiry; recovery must not turn a source-evidence claim into verified legal control. Approval does not by itself override Authorisation or Privacy.
6. **Directory, disclosure and records:** strong reads for standing/access-sensitive use; bounded reads only where safe and explicitly qualified; minimal, scoped disclosure; native data-subject export/disposal/hold coordination; source-owned versioned event/outbox and idempotent maintenance.

**Failure rule:** do not create, grant, confirm or disclose on unknown caller, stale authoritative standing, missing required provider, uncertain proof, contradictory owner evidence, broken isolation, incomplete atomic transition, unavailable authorisation or unresolved dispute. Return safe, typed refusal or pending/review states, not success by inference. Replay must not duplicate tenants, groups, memberships, appointments or effects. Record accepted/pending/completed distinctly.

## Actual published surface versus proposed alignment

**Documented implementation (not execution-verified):** `nuxt-layers/identity/CONTRACT.md` publishes `composeIdentity` and provider ports, `getIdentityProvisioning`, `getIdentityDirectory`, `getIdentityAccessGovernance`, `getIdentityDisclosureContext`, `getIdentityGovernance`, `getIdentityApprovals`, `getIdentityJoining`, `getIdentityLifecycle`, `getIdentityBreakGlass`, `getIdentityQueries`, `getIdentityScimStructure`, `getIdentityServiceIdentities`, retention/disposal/export, `getIdentityTasks`, `relayIdentityOutbox`, typed client `useIdentity()`, and `/api/identity/*` routes. The published contract documents strong-versus-bounded reads, checked server subjects, approval digests, exported `IDENTITY_PERMISSIONS`, fail-closed provider errors, and scheduler-neutral outbox descriptors.

**Documented implementation gaps / verification required:** ADR-0017 tenant ancestry, human digital tenant-owner verification/transfer, restricted exceptional recovery and guarded self-service orchestration are not exposed as a completed public tenant-tree contract. Published operator-only `provisionIdentityTenant` and `bootstrapIdentityRootGroup` are insufficient for customer self-service or verified owner governance. The implemented set of caller/decision providers still differs from ADR-0012's simplified `resolveCaller`/`decide` composition shape. Claim neither conformance nor guaranteed revocation timing without independently evidenced integration acceptance.

## Idealised public inbound interfaces

All inbound operations validate server-side source, tenant, scope, authority, caller/assurance/recency, revision, correlation/idempotency, evidence provenance, policy and effective time as relevant. Missing essential information refuses or holds the operation; an event never authorises a command.

| Input / source | Business meaning and authoritative owner | Requirement and invalid/unknown handling |
|---|---|---|
| Verified caller, session assurance and recovery status — Authentication through IAM composition | Current authenticated local principal, authentication time, strength/phishing resistance, session continuity; Authentication owns authentication | Required for protected interactive changes; unknown, expired, stale or insufficient assurance refuses or requires explicit step-up. Never accept browser-produced subject assertions |
| Resource/action/tenant decision, scoped delegation and risk — Authorisation | Independent access decision and any qualified approval constraints; Authorisation owns grants/policy decisions | Required for protected access/mutation; deny, unavailable or indeterminate fails closed. Membership or parentage never substitutes |
| Principal, group and tenant commands — verified self, authorised managers and trusted host/orchestration | Reserve/confirm/suspend/close principal; create/reparent/close group or tenant; admission; owner appointment/transfer/recovery; dispute and review actions | Required for intended action; validate revision, unique references, cross-tenant bounds and invariants; privileged provisioning stays operator-only |
| Trusted change approval / decision evidence — authorised approvers and Workflow where configured | Proposal digest, immutable reviewed version, independence, time, reason, objection and approval outcome | Conditional on risk; self-approval, stale digest or weakened policy invalidates outcome; high-risk without independent approval holds/refuses |
| Effective bounded settings — Configuration plus mandatory security floor | Allowed names, admission options, governance time windows, display choices, notification choices; Configuration owns settings | Optional unless particular policy requires; missing optional selection uses secure documented default; cannot disable mandatory protection |
| Verified human/organisation/relationship claims — Verification and qualified legal evidence authority | Issuer, claims, scope, subject link, issuer status, evidence age, challenge/dispute record; Identity owns *resulting digital governance decision*, not underlying legal truth | Conditional for verified ownership and recovery; unverifiable, expired, contested or incompatible evidence enters hold/review, never automatically appoints an owner |
| Legal restrictions, subject rights and privacy constraints — Legal Compliance / Privacy | Applicable jurisdiction/version, lawful restrictions, holds, permitted disclosure, minimisation and disposal | Required when applicable; uncertain legal basis blocks irreversible destruction, transfer or disclosure pending lawful review |
| Clock, persistence, scheduler execution, durable transport — host/Clock, owned database and outbox, Scheduler/Message Queue | Reliable effective times and ordering, atomic Identity transactions, periodic maintenance, asynchronous delivery | Required according to operation; invalid time, absent store or failed outbox relay cannot silently complete. Publish at least once with downstream de-duplication |
| Domain resource associations and departure/transfer intents — domain owners / IAM integration | Domain-owned stable resource references, creator versus owner facts, offboarding and revocation coordination | Conditional; verify source, tenant and operation. Never let a domain event create identity standing/rights by implication |

## Idealised public outbound interfaces

| Output / consumers | Identity's authoritative guarantee and limits |
|---|---|
| **Principal reference and standing** → Authentication, Authorisation, IAM integration, Profile and authorised domains | Opaque stable principal ID/kind and active/paused/closing state, version/effective time, source and freshness. **Not** name, email, credential, proof of age or sign-in success |
| **Tenant descriptor and ancestry** → Authorisation, Configuration, Billing, domain owners and secure hosts | Isolation-boundary ID, state, separate parent reference, revision/effective time; permitted queries scoped to caller. **Not** implicit child access, company control, payment liability or customer disclosure |
| **Tenant digital ownership / recovery state** → IAM integration, Authorisation, verified recovery and Audit consumers | Qualified human owner references, source decisions, joint-approval constraints, restricted/recovery status and recorded evidence references under disclosure rules. **Not** independent legal-title adjudication |
| **Group and direct membership facts** → Authorisation, Authentication sign-in gating, domain owners, Profile and Configuration | Group hierarchy, direct member reference, status, effective range and revision; strong freshness for access decisions. **Not** inherited access, domain employment, guardianship or organisational office |
| **Admission and governance results** → authorised participants, Workflow, Notifications and Audit | Pending/reviewed/committed outcomes, digest, version, reason code and safe status; avoid leaking existence or private member details to unauthorised viewers |
| **Authorised directory/disclosure queries** → approved consumers and optional UI | Strong or explicitly bounded consistency and scoped minimal projection; absent/not-disclosable distinguished only to trusted consumers, without enumeration |
| **Source-owned committed events/outbox** → IAM integration, Message Queue transport, Authentication, Authorisation invalidators, Audit and domain subscribers | Principal standing, tenant/group/membership/governance, owner/recovery, closure and disposal transition events with stable ID, aggregate version, timestamp and correlation; may deliver more than once/out of order; consumers deduplicate and reconcile. Do not publish unsupported future event names as existing |
| **Export/disposal/exception evidence** → Privacy, Legal Compliance, Audit, authorised export/reporting coordinators | Scoped Identity-owned records, legal-hold/retention and completion/refusal, safe provenance. Does not export other domains' data or imply all processing ceased |

**Common semantics:** stable public IDs; tenant and resource scope; server-verified actor and step-up; effective time through Clock; optimistic revision and idempotency key for risky mutation; immutable change digest; source version/evidence reference; accepted/pending/applied/rejected states. These are per-operation fields, **not** a mandated universal request envelope. Commands return an authoritative applied state only after Identity commits its transaction and outbox; asynchronous downstream effects are reported separately. Queries carry consistency/freshness qualifiers and source revision. Events are change facts, not commands or permission grants. Preserve compatibility/version policies when published interfaces evolve; never expose private tables.

## Cross-capability direction and dependency boundaries

| Cooperating owner | Identity needs from it | Identity supplies / consequence |
|---|---|---|
| Authentication | Trusted principal binding, assurance/recency and credential recovery status | Standing, sign-in eligibility and revocation facts; Authentication invalidates sessions/claims under a measurable guarantee |
| Authorisation | Resource/action decision, delegation and policy enforcement; no direct assumed role | Fresh principal, tenant, group and direct membership facts; changes invalidate derived access without disturbing independent grants |
| IAM Integration | Composition and cross-capability orchestration | Source-authoritative transitions and verified references; integration must not duplicate Identity records |
| Profile | Purpose-limited presentation labels if authorised | Opaque principal refs and lifecycle, never Profile-owned personal data |
| Verification / qualified legal control owner | Verified claims, linkage, authority evidence and dispute disposition | Identity's scoped digital ownership and recovery decisions, not independent assertions of legal entitlement |
| Configuration | Approved settings and change options | Authoritative tenant/group/reference standing and closure invalidation; config never creates membership |
| Privacy / Legal Compliance | Subject-rights/hold/disclosure constraints and applicable lawful control | Scoped Identity records, retention/disposal dispositions and governance evidence |
| Audit / Logging / Observability | Independent evidence receipt, protected operational diagnostics | Sensitive transition and refusal provenance with minimised subject data; logging is not the authoritative audit record |
| Scheduler / Message Queue / Clock | Execution and delivery adapters; validated effective time | Source-owned maintenance tasks, durable outbox change facts, temporal state transitions |
| Workflow / Notifications | Independent review coordination and safe delivery | Governed requests/statuses and authorised recipient references, without moving approval authority into messaging |
| Billing / commercial onboarding | Legitimate onboarding request and independently evidenced payer/legal party relationship | Tenant and digital governance refs; no money/liability or subscription status reownership |
| Employment / Enrolment / other domains | Their own asserted engagement/admission/representation statuses when relevant | Scoped identity refs and facts; no automatic staffing, learning, guardianship or finance eligibility |
| Federation / Integrations | Verified external trust bindings and provider evidence, when actually enabled | Scoped local principal linkage and lifecycle; no automatic local account merging, implicit peer trust or cross-tenant grant |

**Composition:** directed ports/contracts and versioned notifications, not mutual runtime imports. Required core: Identity-owned durable state/persistence, server-side decisions for protected operations, and strong authenticated caller for interactive changes. Optional presentation, provider connections, external verification and notifications degrade explicitly. Bootstrap and emergency operator operations are separate tightly restricted trusted boundaries. No provider-neutrality claim should hide a hard dependency on the published PostgreSQL implementation.

## Conceptual GUI and host navigation

**Host sidebar entry:** “Identity” (or “People and groups” by app context) opens a scoped capability dashboard, using the representative `nuxt-layers-test/application-test-template` sidebar-to-dashboard composition. Host owns menu, navigation, app shell and tenant selection; Identity's optional presentation owns authorised screen flows, never a second identity store.

- **My identity:** standing, linked personal group, direct memberships, pause/resume, pending closure, protected export and recovery guidance; profile display names come from Profile.
- **Groups:** scoped group tree (no inheritance badges implying rights), member directory, invitations, join requests, pending approvals and lifecycle actions; group-member actions require resource-specific server decisions.
- **Tenant governance:** tenant hierarchy and isolation/status, verified human digital owners and joint governance, protected ownership transfer and restricted recovery case queue. Separate digital control from legal representation, payer and group membership; flag future-only screens until supported by public contracts.
- **Service identities:** group-scoped list, custody, standing and secure handoff to Authentication-managed credential controls, never raw secrets.
- **Governed decisions / emergency:** proposal digest, approver independence and risk, evidence references, objections, safety holds, irreversible-action confirmations, break-glass retrospective review and protected operator bootstrap interface (not normal user navigation).
- **Administration / monitoring:** scoped lifecycle and delivery failures, stalled revocation/reconciliation and authorised evidence/export; prevent cross-tenant enumeration and avoid operational secrets.

Direct routes and headless/custom hosts remain supported via published contract; existing documented screen paths include `/account/groups`, `/groups/:groupId`, `/invitations/accept`, `/changes/:changeId`. New dashboard routes are **conceptual**, not claimed implemented. Progressive disclosure, status/pending/unknown labels, meaningful empty/error states, non-cacheable sensitive views, non-frameable administration, no-referrer/token-safe invitation handling, responsive keyboard interaction, accessible confirmation/step-up dialogs, WCAG 2.2 AA, BCP 47/CLDR, host semantic Theme Manager tokens and screen-reader status updates are required. The UI never makes an access decision.

## Security, privacy, failures and provider constraints

Follow ASVS 5 L2 minimum and risk-appropriate L3; treat high-risk tenant owner/recovery flows as privileged. Avoid enumeration, inference through timing or error distinctions, confused-deputy cross-tenant effects, forged subjects/claims, stale cache grants, owner-floor race conditions, self-approval and compromised operator bypass. Enforce transactional invariant checks with appropriate concurrency control. Preserve lawful retention, transparent storage register, tenant isolation and independently governed erasure/export; privacy restrictions apply even if access is authorised. Native-only mode retains local principal/group/tenant ownership; external IAM, SCIM, federation or verification providers supply qualified evidence/adapters, never silently replace local authority. Provider reconnection, duplicate events, failed delivery, partial migration, appeal, credential rotation and recovery require versioned reconciliation; external APIs and their costs/terms are optional, not baseline prerequisites.

## Conceptual acceptance scenarios (not executed)

| Input/scenario | Expected result, source of authority |
|---|---|
| New human reservation/confirmation, retry | One active opaque principal plus exactly one atomic permanent personal group; duplicate retry returns same result; Identity |
| Explicit membership in two tenants/groups | Two separate direct memberships, no cross-tenant or parent-derived permissions; Identity facts, Authorisation decisions |
| Attempt group reparent cycle / second parent | Conflict and no mutation or emitted committed-change event; Identity |
| Attempt tenant reparent cycle / parent reads child private resources | Reparent refused; parenthood never grants read; Identity and Authorisation |
| Activate new tenant with no genuinely verified human owner | Refused or held; claim without verified provenance insufficient; Identity with evidence provider |
| Last tenant owner becomes unavailable / disputed transfer | Restricted recovery with independent evidence, approval, hold and appeal, not manufactured verified owner; Identity and qualified adjudicator |
| Self-approve governance change / stale digest / weaken-then-transfer | Refuse or hold; Identity checks invariant and Authorisation/approval ports enforce independence |
| Membership ends during active session / cached decision | Source state changes and durable event committed, relevant permissions invalidated within independently evidenced bound; Identity, Authentication and Authorisation |
| Replay duplicate transfer or out-of-order membership event | No duplicate owners/memberships; consumer reconciles aggregate revision; Identity/outbox and subscriber |
| Database unavailable or event transport fails | Protected mutation refuses unless atomic commit/outbox succeeded; committed outbox is retried without claiming downstream completion |
| Contractor leaves but organisation legitimately owns domain report | Contractor's derived access ceases; report stays domain-owned, lawful authorised export remains possible; domain owner/Authorisation |
| Profile/verification unavailable | Core local opaque directory still works where independent; display/verified control operations safely degrade or hold, no guessed personal/legal claim |
| Disallowed cross-tenant lookup / closure with legal hold | No disclosure; retention/hold enforced with auditable refusal and permitted export only; Identity, Privacy/Legal Compliance |
| Unsupported customer tenant tree endpoint in current runtime | Explicit unavailable/not-supported, never call operator-only privileged provisioning from browser |

## Review decisions, technical investigation and handover

- **IDN-01 — Established:** preserve Identity/Authentication/Authorisation/Profile split, opaque local references and strong source-of-truth boundaries.
- **IDN-02 — Established:** group forest/personal-group rules and no inherited authority; distinguish direct membership from access.
- **IDN-03 — Established (accepted ADR-0017):** separate tenant tree, verified human owner floor, protected joint ownership and exceptional recovery; do not claim implementation.
- **IDN-04 — Proposed alignment:** standardise source-owned strong/bounded directory, revisioned principal/tenant/group/member facts and safe disclosure projections for IAM consumers.
- **IDN-05 — Proposed alignment:** bind source-owned standing changes to independently measured Authentication/Authorisation revocation, durable events, retries and no cyclic imports.
- **IDN-06 — Proposed alignment:** secure self-service tenant request/orchestration and protected human-owner appointment/recovery public contracts; never expose privileged provisioning pool.
- **IDN-07 — Open owner decision:** designate qualified legal/organisational evidence verification and dispute/adjudication authority, appeal process and permissible custody/retention; Identity records only digital outcome.
- **IDN-08 — Open owner decision:** precise tenant-parent change consent, suspension/recovery and tenant closure/migration rules across jurisdictions and resource domains.
- **IDN-09 — Technical investigation:** compare target `CONTRACT.md` against ADR-0012 caller/decision semantics, existing approval/assurance ports and controlled migration path, maintaining minimal host composition.
- **IDN-10 — Technical investigation:** quantify feasible revocation/freshness guarantees for sensitive operations, delayed subscriber/partition cases, strong lookup fallback and reconciliation telemetry.
- **IDN-11 — Proposed GUI:** host sidebar dashboard and public-contract screens; future tenant/recovery workflows must remain marked unsupported until published and verified.
- **IDN-12 — Acceptance pending:** evidence for migration, tenant ownership reconciliation, invariant stress/concurrency, security, accessibility, legal/privacy, interface compatibility and end-to-end integration is not present in this review.

**Conceptual sign-off:** not yet owner-approved. Technical/architectural pre-merge verification against latest `master`, mergeability/checks, and explicit owner consent still required. This record does not modify implementation repositories.


## Extended review — published interfaces, observability, standards, library suitability and GUI (18 November 2026)

**Decision status:** Owner approved the prior review's recommendations and requested deeper investigation on 18 November 2026. The details below are **recommended conceptual elaboration**, not separate owner approval of new technical choices, evidence of implementation, or an amendment to the implementation root contract.

### Concise issued contract mapping

The actual published `nuxt-layers/identity/CONTRACT.md` (implementation `master@7cfb0d0bc6ebb824575827798e5507f4a511db57`, read-only) exposes:

- **Inbound composition ports:** `composeIdentity({ database, accessDecision, approvalPolicy, subjectResolver, eventPublisher, policy?, clock? })`; compatibility `provideIdentity*` exports. Validated, secure denial-only fallback for missing privileged authority, rather than operational IAM by omission.
- **Inbound server commands:** principal reserve/confirm and standing/closure; group/membership creation and change; invitation/join; approvals/objections; break-glass; service identity; legal hold/disposal/export; operator-only tenant/bootstrap functions. Server-verified subjects and decisions remain mandatory. The operator-only pool is not a public self-service endpoint.
- **Outbound queries:** `getIdentityDirectory`, `getIdentityAccessGovernance`, `getIdentityDisclosureContext`, `getIdentityQueries`, `getIdentityScimStructure`, `getIdentityServiceIdentities`; return only scoped, permitted facts and strong consistency for security decisions.
- **Outbound lifecycle/events:** `getIdentityTasks()`, `relayIdentityOutbox()`, outbox events with at-least-once delivery semantics; no assertion that optional transport was successful until acknowledged. Typed client `useIdentity()`, supported `/api/identity/*` HTTP operations, optional screens and `./contracts` schema/error/permission exports.
- **Gaps relative to accepted ADR-0017:** full public tenant tree, verified human digital tenant-owner lifecycle, disputed transfers and recovery, safely composed self-service. Reconcile ADR-0012 simplified caller/decision shapes without removing current assurance, approval and recency checks.

### Special relationships: Logging, Audit and Reporting

**Logging (optional diagnostic sink):** Identity *sends* bounded, structured operational signals for validation/refusal categories, database/clock/provider failure, slow directory calls, repeated retries, failed maintenance/outbox relay, reconciliation backlog and correlation IDs. Logging *returns* technical sink/delivery or availability status where exposed; it owns log storage, routing and technical retention. Identity owns the actual lifecycle outcome and must not treat a successful log as an Identity commit or an Audit receipt. Exclude raw invitation tokens, session/bearer material, credentials, legal evidence and unnecessary personal data. Logging outage alone must not grant access or destroy source-owned evidence.

**Audit (evidential custody):** Identity *supplies* provenance-qualified source events for risk-selected principal/tenant/group/membership, owner appointment/transfer, privilege, governance approval, emergency/recovery, export/disposal and significant denied-attempt outcomes. Include source event ID/aggregate version, actor type, permitted tenant/target references, assurance provenance, decision and applied outcome, event/effective times and correlation; minimise identifiers. Audit *returns* separately verifiable accepted/rejected/quarantined/uncertain evidence receipts, integrity/completeness status and review/hold findings through its proposed contract. Audit owns evidential custody, integrity and review, not Identity's original membership or tenant facts. **Committed identity changes must not be reported as Audit-captured merely because an outbox event exists.** If mandatory evidence intake fails, preserve the source outbox, expose backlog and follow risk-defined fail-closed/hold or safely retry; do not fabricate audit completion. Audit may be only conceptual today; do not assert a working receipt API.

**Reporting (optional derived analysis):** Identity *supplies* authorised, purpose-limited principal/tenant/group/membership and governance status queries, revisions/effective periods, source freshness/coverage and versioned invalidation events, suitable for scoped membership movement, tenant counts, admission/recovery backlog, churn and governance completion reports. Reporting *returns* report definitions, requests, run status, lineage, effective-date/cutoff/freshness, derived metrics, snapshot/export references and delivery outcomes. Reporting never owns Identity facts or decides access. Protect against cross-tenant correlation, tiny-cohort re-identification, historic snapshot leakage and saved-export access after membership revocation. If Reporting is absent, Identity's native directory and lifecycle continue; do not assert a Reporting published adapter exists.

**Direction/acyclicity:** Identity produces source-owned events or permits host-mediated authorised queries; Logging/Audit/Reporting consume without importing private Identity tables. Diagnostic or evidence acknowledgement flows via host-composed ports/events; no mandatory bi-directional package edge. Classification and event eligibility remain aligned with each neighbour's conceptual review, not silently settled here.

### Established standards to apply at appropriate boundaries

| Standard | Reuse without confusing authority |
|---|---|
| NIST SP 800-63-4 / 63A-4 / 63B-4 / 63C-4 | Proofing, assurance, authentication and federation terminology; Identity consumes verified assertions but does not own credential verification or proofing |
| IETF SCIM RFC 7643 / RFC 7644, and relevant later updates | Standard structural user/group provisioning and synchronisation; mapping does not turn foreign SCIM users into verified local human owners |
| RFC 8417 Security Event Tokens and CloudEvents | Portable security/lifecycle event vocabulary/envelope; retain source ownership, idempotency and capability outbox guarantees |
| OAuth 2.0 step-up RFC 9470, OIDC where applicable | Authentication/IAM interface, not a new Identity password/session engine |
| OWASP ASVS 5.0 (L2 minimum, risk-suitable L3) | Security/invariant assurance, authorisation, lifecycle, isolation, anti-enumeration, abuse resistance |
| W3C WCAG 2.2 AA, BCP 47, Unicode CLDR / ECMA-402 | Accessible, internationalised optional Identity presentation |
| OpenAPI and JSON Schema | Versioned externally callable HTTP and validation descriptions; retain actual published TypeScript/Zod contract as implementation authority |
| OpenTelemetry semantic conventions | Cross-service diagnostic correlation and metrics without making telemetry evidentially authoritative |
| UK GDPR/GDPR and applicable jurisdictional requirements | Lawful minimisation, retention, access, disclosure and erasure; qualified legal advice, not presumed certification |

Do not impose SCIM, event envelopes or OAuth on all internal requests where a simpler public domain contract is already sufficient.

### Mature and commercially permissive open-source tools — evaluated candidates, not mandates

| Candidate | License | Suitability and boundary |
|---|---|---|
| PostgreSQL | PostgreSQL License (permissive) | Existing Identity persistence provider; ACID atomic personal group/owner constraints, transactions and owned outbox; no vendor-hosted dependency |
| `pg` / node-postgres | MIT | Current public pool shape; self-hosted PostgreSQL interoperability |
| Zod | MIT | Already published runtime input/output schemas and `./contracts`; avoid duplication |
| Kysely | MIT | Optional typed SQL builder if it simplifies isolated schema queries; no reason to replace working persistence solely for fashion |
| OpenTelemetry JS | Apache-2.0 | Trace/metric correlation to Logging/Observability; not Audit evidence |
| Pino | MIT | Optional structured diagnostic logger behind Logging's provider-neutral port, not a second Identity logging authority |
| fast-check | MIT | Future CI property/state-machine invariant tests for single parent, owner floor, idempotency, replay and concurrent membership changes |

Licenses checked against publisher/repository/npm pages in November 2026; audit the **exact selected version, transitive packages, trademarks and non-code dependencies** before adoption. Permissive licenses alone do not guarantee maintainability, safe supply chain or absence of operational lock-in. Avoid all-in-one hosted identity platforms and proprietary enterprise feature gates where they would duplicate established Authentication/Authorisation boundaries or hold tenant governance hostage. Reuse the existing Clock capability for effective date and time, rather than adding a separate time library simply for Identity.

### Concrete optional presentation on representative test host

The published `nuxt-layers-test/application-test-template/README.md` documents `/` public homepage, `/admin` test dashboard, responsive collapsible sidebar, overlay mobile menu, test-mode Theme Manager under `/theme-manager`, and a top bar with Appearance menu and an explicit **Not signed in** placeholder. It is a local-only unauthenticated test fixture, **not safe for public deployment**. Derived test applications own sidebar entries and integration fixtures, using published capability exports.

**Proposed sidebar:** `Administration → Identity` links to an Identity dashboard (proposed route `/admin/identity` in the test application; host owns route and nav). Render status, permitted principal and group counts, pending invitations/approvals, membership transitions, recovery/owner alerts and delivery backlog **only when the respective published interface exists and authorises the viewer**. No fabricated live metrics.

**Dashboard sub-navigation:** `My identity` (personal group and standing); `Groups & members` (directory, membership lifecycle, admission queue); `Invitations`; `Governance approvals`; `Service identities`; `Tenants & digital owners` (future governed tree/transfer/recovery screens), `History & evidence` (Audit-backed only if integrated), `Reports` (Reporting-linked only if integrated). Show context selection, pending/unknown states and authorisation-based actions. Operator-only privileged bootstrap has **no ordinary sidebar link**. Profile handles name/avatar editing; Authentication handles password/MFA/sessions; Authorisation handles role/grant administration.

**Screen interaction:** dashboard tiles link to permitted scope; master/detail lists and forms show tenant, owner, lifecycle revision, effective time and status; high-risk transfers use inspectable proposal digest, independently qualified approver, reauthentication, safety delay, and explicit committed-vs-pending result; last-human-owner removal blocked server-side regardless of UI. Group tree never displays parenthood as permission. Sign-in fixture cannot spoof verified production caller.

**Accessibility and integration:** semantic Theme Manager tokens, WCAG 2.2 AA, BCP 47 localisation, keyboard and screen-reader announcements, desktop/mobile reflow, denial-safe errors, non-cacheable management pages and no leaked invitation fragments/referrers. Existing documented Identity default routes (`/account/groups`, `/groups/:groupId`, `/invitations/accept`, `/changes/:changeId`) remain supported; proposed `/admin/identity` is a composition route, **not** claimed implemented.

**Additional conceptual acceptance:** source committed vs delivered vs Audit accepted; Logging failure without event loss; Reporting stale/small-cohort scope denial; test host navigation with anonymous refusal and authenticated permitted dashboard; independently authorised owner transfer with MFA/approval; absent tenant-tree API shows unavailable rather than invoking operator-only bootstrap.

### Extended status and follow-up

Proposed elaboration above is ready for review in this draft PR; it does not settle open legal-control adjudication, cross-tenant consent, precise revocation latency or deployment-specific screens. No implementation edits or tests. Before merging, reconcile the branch with the *latest* governing and blueprint `master`, including concurrent IAM Integration and other reciprocal updates, inspect checks/mergeability and seek explicit approval.
