# Capability Register — Working Inventory

**Status:** Non-normative, catalogue-derived register. **Implementation and operational status have not been audited.**

**Source:** [Working Capability Catalogue](capability-catalogue.md), originally copied from the governing `nuxt-layers/architecture-rules/docs/catalogue.md` at commit `2eea557fa3acbf9412fea065d2a3cdda42a764fc`. Accepted governing rules remain authoritative.
**Design specification:** [Capability Register Design](../proposals/capability-register-design.md).
**Review records:** [Decisions](../records/decisions.md) · [Findings](../records/findings.md).

## Purpose

This document is the **populated working register**, distinct from its design specification. It indexes every entry in the working catalogue without claiming that a package exists or functions. "Established" means an established architectural responsibility, **not** an implemented or operational package.

## Catalogue-derived entries

### Established capabilities

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `theme-manager` | Foundation | Established | Theme definitions, the semantic token vocabulary, contrast checks, selection and preferences; the only authority for the effective theme |
| `clock` | Foundation | Established | Canonical date/time values, parsing, formatting, temporal arithmetic, time zones and clock services |
| `configuration` | Foundation | Established | The facts a site, tenant or group states about itself, changed through approvals |
| `identity` | Foundation (IAM) | Established | Identities, each person's personal group, groups, the single-parent hierarchy, tenants and memberships with their lifecycle; no personal data beyond opaque identifiers |
| `authentication` | Foundation (IAM) | Established | Credential verification, sign-in identifiers, sessions, rotation, revocation and reauthentication |
| `authorisation` | Foundation (IAM) | Established | Server-side, resource-aware access decisions, with no implicit inheritance through the group hierarchy |
| `profile` | Foundation (IAM) | Established | The personal data describing a person, keyed by an Identity identifier: what each context may see, under the person's control, and their access, correction, export and erasure requests |
| `iam-integration` | Foundation (IAM) | Established | The IAM suite's architecture, cross-capability processes and the adapters connecting its members ([ADR-0005](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/decisions/ADR-0005-iam-suite.md)); no data of its own |
| `rich-text` | Library | Established | The one safe formatted-text format, its profiles, checks and safe tree; never renders ([ADR-0011](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/decisions/ADR-0011-shared-rich-text-and-configurable-copy.md)) |
| `publisher` | Platform | Established | Documents of host-registered types: drafts, versions, approval, scheduling, addresses, listings and feeds |
| `media` | Platform | Established | Images: web-ready variants, metadata removal, alt text, group ownership and allowances; the files themselves through the Files shape ([ADR-0012](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/decisions/ADR-0012-trivial-composition.md)), which the host fills with `storage` |
| `storage` | Platform | Established | Files' bytes in an object store behind one provider-agnostic port: keys under tenant and group, signed addresses, lifecycle, backups and usage figures; no records of its own |
| `ui` | Presentation | Established | Generic, fully styled components on Theme Manager's vocabulary; knows no capability |
| `content-editor` | Presentation | Established | Complete generic editorial GUI for Publisher's registered document types through its public contract, without owning content or publication state; implementation not independently verified |
| `gallery` | Presentation | Established | Albums and photo of the week as Publisher types over media's images; no data of its own |
| `privacy` | Foundation | Established | Consent and retention policy, which capabilities receive and apply |
| `legal-compliance` | Foundation | Established | The legal duties that apply to each site by jurisdiction, such as UK GDPR and the Online Safety Act, and the constraints they impose beside Authorisation's decisions, such as legal holds that block deletion |
| `export` | Library | Established | Turning a `rich-text` safe tree into files such as PDF and .docx, extensible by format |
| `scheduler` | Platform | Established | Running every capability's `tasks` on time, like cron, for the host |
| `message-queue` | Platform | Established | Carrying messages that something happened, such as "password changed", from capabilities' outboxes to the capabilities that listen; not calendar events, which are the `event-service` candidate |
| `workflow` | Platform | Established | User-defined routes for review, sign-off and approval, per type and site; fills capabilities' approval ports |
| `content-security` | Platform | Established | Scanning what people submit for dangerous content, links and abuse, on top of each layer's own input checks |
| `notifications` | Platform | Established | Telling people something needs them, through their chosen channels; providers' keys come from the host's secret management |
| `comments-engine` | Platform | Established | Comments on content and their moderation |
| `metadata` | Platform | Established | Tags, categories, taxonomies and ontologies attached to content |
| `localisation` | Platform candidate | Proposed conceptual review | Language/locale adaptation, translation workflow, glossary, quality and provider-neutral translation; Publisher/domain owners retain their published data and business rules |
| `seo` | Platform | Established | Redirects, sitemaps and search-engine metadata, driven by Publisher's address events |
| `site-hosting` | Platform | Established | Where each site is served: custom domains, proving their ownership, and finding the site for a request's address; certificates and deployment stay with the host's proxy and provider (ADR-0014) |
| `integrations` | Platform | Established | Adapters to outside services such as Google Docs, Microsoft 365 and social feeds |

### Infrastructure integration libraries

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `temporal-gateway` | Infrastructure integration library | Established | Shared Temporal connection, schedule, execution and worker SDK integration; no business scheduling, workflows, message transport or capability-owned persistence |

### Additional architectural entries

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `architecture-rules` | Architecture governance (not a runtime layer) | Governance | Governs ADRs, normative standards and this catalogue; owns no application runtime data |
| `infrastructure` | Foundation candidate | Under consideration | Host/backend/deployment setup and operational configuration; infrastructure resources and domain data remain with the appropriate hosts/providers |
| `reviews` | Platform candidate | Under consideration | Customer ratings, testimonials, verified purchase/service evidence, moderation, merchant replies and trustworthy reputation aggregates; transaction and identity facts remain owned by source capabilities |
| `template-engine` | Library candidate | Under consideration | Secure deterministic template parsing, data binding and content rendering; no template persistence, document lifecycle, arbitrary code execution or business-data lookups |
| `organisation-model` | Domain / platform boundary to be decided | Retained pending classification review | Prove independent lifecycle for versioned archetypes/positions/relations/capability selection; otherwise use schemas, Configuration or composition; cannot reown IAM facts or legal authority |


### Federation and Node–Hub roles (conceptual review, 17 November 2026)

| Entry | Classification | Evidence and status | Scope |
|---|---|---|---|
| `node` | Deployment and network participant, **not a capability** | Conceptual role; no special implementation asserted | Independent installation; can be standalone, publisher, discoverer or Hub operator |
| `federation` | **Platform capability candidate** | [Candidate capability record](capabilities/federation/capability-record.md); no verified `CONTRACT.md`, runtime or repository | Optional peer participation, collection publication/subscription, exchange, synchronisation and withdrawal coordination; no authoritative domain data or search engine |
| `hub` | **Application composition / operator role** | [Architecture review](../reviews/node-hub-federation-architecture.md); not a standalone capability | Node that composes Federation, Search and applicable governance/safety/presentation to provide discovery/indexing |

**Current decision:** every Hub operates as a Node, while not every Node offers Hub services. A Node may become a Hub by composing the needed capabilities or operate multiple independently scoped Hubs. Record no claim of accepted governing status, package availability, tested protocol or deployed Hub. Implementation and conformance are unverified. The working catalogue has the same provisional entries.


### Moderation — new conceptual candidate (17 November 2026)

| Entry | Classification | Evidence/status | Responsibility |
|---|---|---|---|
| `moderation` | **Platform capability candidate** | [Pro-forma report](capabilities/moderation/capability-report.md), [conceptual capability record](capabilities/moderation/capability-record.md), [cross-capability review](../reviews/online-safety-content-governance.md); **proposed only**, no verified repository, root contract, deployed service or independent acceptance | User/system reports, cross-domain review cases, adjudication, appeals and authorised enforcement coordination. Originating domains retain their own content and actuation, Content Security owns scanning, Audit owns evidence |

This entry records review-approved conceptual documentation, not adopted governing classification or operational compliance with the UK OSA. Verify service applicability, provider options, source contract boundaries, persistence and tests at its later full capability review.

### Foundation, platform and library candidates

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `audit` | Platform | Candidate | Tamper-evident accountable business/security audit evidence and review; distinct from operational Logging and Observability |
| `caching` | Foundation | Candidate | Cache provider ports, expiration and invalidation; source capabilities remain authoritative |
| `logging` | Foundation | Candidate | Structured technical logs, correlation and sinks; not the authoritative business audit trail |
| `observability` | Platform | Candidate | Metrics, traces, system health and diagnostics; not logging or business auditing |
| `UUID-generator` | Library candidate | Candidate | Shared UUID generation, including UUIDv7; replaces retired `uuidv7_generator` / `uuidv7-generator` concept without owning entities or credentials, and does not automatically require a Nuxt Layer |
| `api-gateway` | Composition / platform to decide | Candidate | External API routing and exposure; not a replacement for capability APIs or server authorisation |
| `application-compositions` | Composition artefacts | Candidate | Reusable application templates and selected capability wiring; generally not independent stateful services |
| `organisation-console` | Presentation / application composition, not a business capability | Conceptual name accepted; independent packaging under review | Organisation-neutral dashboards, context selection and management screens consuming authoritative public contracts; no independent business records or grant authority |
| `user` | Presentation | Candidate | Group-scoped user administration screens via Identity/Profile/Authorisation; no user records |
| `search` | Platform | Candidate | Indexing, query and relevance over authorised source records; no source-of-truth storage |
| `location` | Platform | Candidate | Coordinates, geospatial and place references; not all postal addresses or site tenancy |
| `reporting` | Platform | Candidate | Authorised report definitions, aggregation and output; no source transaction records |
| `process` | Platform candidate | Candidate | Business process definitions and outcomes; execution uses Workflow/Scheduler without duplicating their responsibilities |
| `project` | Platform candidate | Candidate | Coordinated bodies of work, milestones, responsibilities and budgets; uses Task/Process contracts where applicable |
| `task` | Platform candidate | Candidate | Individual assigned work, goals, progress and due dates; not Temporal jobs or scheduler triggers |
| `booking` | Domain candidate | Candidate | Reservation lifecycle, availability and capacity for resources; neither a clock nor execution scheduler |

### Organisational archetypes and compositions

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `organisation` | Archetype / composition | Example, not standalone candidate | General organisational context and type; separate legal/governance records require a justified domain owner |
| `business` | Archetype / composition | Example, not standalone candidate | Organisation-oriented business application composition; commerce, accounting and other operations retain their own domain owners |
| `company` | Archetype / composition | Example, not standalone candidate | Organisation type with legal-entity references; statutory registration, officers or filings may warrant a separately reviewed domain |
| `club` | Archetype / composition | Example, not standalone candidate | Group type for a club with selected activity capabilities; paid scheme rights and subscriptions are not Identity membership |
| `committee` | Archetype / composition | Example, not standalone candidate | Group type and meeting composition; formal votes, resolutions and minutes may warrant their own independently governed lifecycle |
| `office` | Archetype / composition | Example, not standalone candidate | Organisational location/unit type; physical facilities, leases and managed assets belong to independently justified domain owners |
| `workshop` | Archetype / composition | Classification resolved — not a standalone candidate | Event/Course composition unless independently justified domain rules emerge; retain old directory until separate deletion PR |

### Activity domain candidates

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `membership` | Domain candidate | Retained pending classification review | Potential scheme/paid membership rights, terms, renewals and benefits; NOT Identity's existing group membership and not yet a verified independent capability |
| `events` | Domain candidate | Candidate | Planned participant activities and event lifecycle; not background scheduled tasks |
| `assessment` | Domain candidate | Candidate — owner-authorised pro-forma, independent review pending | Assessment instruments, individual attempts, marking, moderation, appeals and results; [record](capabilities/assessment/capability-record.md) |
| `credentials` | Domain candidate | Candidate — owner-authorised pro-forma, independent review pending | Authorised credential issuance, verification, correction, replacement and revocation; award decision remains with awarding authority; [record](capabilities/credentials/capability-record.md) |
| `qualification` | Domain candidate | Candidate — COURSE-12 owner-approved creation; full independent review pending | Qualification schemes, multi-pathway evidence and award decisions, issuer/centre authority, appeals and teach-out; [record](capabilities/qualification/capability-record.md) |
| `course` | Domain candidate | Candidate | Structured learning offering and outcomes |
| `enrolment` | Domain candidate | Candidate | Course/learner participation and allocation |
| `training` | Domain candidate | Candidate | Verified training participation, competencies and completion records |
| `gaming` | Domain candidate | Candidate | Game-specific state, rankings and participation; separate from generic Identity accounts |
| `job` | Domain candidate | Candidate | Ambiguous: employment role/post is possible domain; background execution job belongs to Scheduler |

### Commerce and operations domain candidates

| Name | Classification | Catalogue status | Responsibility / exclusion |
|---|---|---|---|
| `product` | Domain candidate | Candidate | Saleable products, families, bundles and variants; not stock quantities |
| `pricing` | Domain candidate | Candidate | Price rules, lists, promotions and calculations; not order records |
| `inventory` | Domain candidate | Candidate | Stock quantities, movements, reservations and stock ownership; not product definition or warehouse workflows |
| `asset` | Domain candidate | Candidate | Owned controlled assets, lifecycle, assignments and valuation references; not generic sale stock |
| `order` | Domain candidate | Candidate | Commercial orders, lines, states and fulfilment obligations; not payment settlement |
| `billing` | Domain candidate | Candidate | Billable charges and periods; not the owner of the entire ordering lifecycle |
| `invoice` | Domain candidate | Candidate | Invoice issuance, numbers, adjustments and settlement state; not payment provider execution |
| `payment-gateway` | Domain candidate | Candidate | Payment-provider initiation, status, capture and refund coordination; no accounting ledger |
| `accounting` | Domain candidate | Candidate | Ledger, journal, periods and reconciliations; not the originating sales or warehouse transactions |
| `subscription` | Domain candidate | Candidate | Recurring commercial agreements, plans, renewals and entitlements; not payment provider |
| `shop` | Domain candidate | Candidate | Retail/ecommerce composition and shop-specific operations; not replacement of Product/Order/Inventory |
| `marketplace` | Domain candidate | Candidate | Multi-seller participation, listings and marketplace-specific commercial operations |
| `warehouse` | Domain candidate | Candidate | Receiving, put-away, picking, packing and physical warehouse operations; Inventory owns stock facts |
| `logistics` | Domain candidate | Candidate | Shipment and delivery operations, dispatch, carrier coordination and tracking |

## Evidence and status fields

**For every entry above:** implementation evidence **not checked**; independent consumer tests **not checked**; application installation, composition and operational health **not assessed**. These are explicitly unknown, not absent or failed.

| Evidence to add | How it must be verified |
|---|---|
| Root public contract | Repository, path and exact revision of `CONTRACT.md`; or not retrievable |
| Implementation / package | Exact repository revision, public exports and relevant package metadata |
| Independent acceptance | Linked CI build, public-contract tests and minimal consumer evidence |
| Architectural decision | Reviewed decision ID, and governing ADR/catalogue adoption reference if accepted |
| Dependencies | Verified public `requires` and optional contracts; direct Nuxt `extends` separately |
| Application selection | Explicit deployment's installed, selected and composed packages, not platform-wide |
| Health / readiness | Owner-supported health observation with relevant time and scope |
| Action permission | Request-time Authorisation and owning domain decision, never a global register grant |
| Last verified | Date and exact source revision; use unknown where not examined |

## Rules for changes

1. Verify the current governing ADRs, Capability Standard, catalogue and owner root contracts before recording implementation or compatibility facts.
2. Treat catalogue classifications and proposed design changes as distinct from actual availability; maintain review evidence in [`reviews/`](../reviews/) and status/decisions in [`records/`](../records/).
3. An installed package is not necessarily configured, operational, enabled or authorised. An unknown status must not be shown as healthy.
4. Do not impose an undocumented universal manifest. Nuxt capability layers already publish `capability.json`; framework-independent packages use their public contracts and exports.
5. This register is neither a new runtime capability nor an authority for installing code, storing business data or deciding permissions.

**Next work:** assess each entry's root public contract and acceptance evidence, adding verified provenance without presuming implementation from its catalogue entry.


## Organisational tenancy and commercial onboarding review (16 November 2026)

**Classification:** `business` remains archetype/composition vocabulary only, without a standalone capability record or implementation assertion. The provisional Billing counterparty note is preserved in [Billing's record](capabilities/billing/capability-record.md). Commercial legal-party/contract evidence ownership remains open.

**References:** [tenancy/governance](../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../proposals/commercial-onboarding-and-entitlements.md), [policy boundary](../proposals/policy-and-governance-boundaries.md), [anti-lock-in recovery](../reviews/organisational-ownership-and-recovery.md). ORG-01–ORG-08 owner approved; TEN/COM/OWN and policy proposals are not independently accepted governing decisions or implemented functions. Preserve the separation of tenancy and organisation, real-world authority and digital control, commercial bill-to and service-consumer, mandatory invariants and adjustable policies, document publication and executable enforcement.


## Catalogue rationalisation — preservation before deletion (17 November 2026)

**Stage: preservation and classification only.** The previously proposed standalone entries `club`, `committee`, `company`, `group`, `image`, `tenancy`, `workshop` and `organisation` have **no independently justified capability authority** under the governing catalogue; `club`, `committee`, `company`, `workshop` and `organisation` remain valid archetype/composition terms, `group`/`tenancy` are Identity responsibilities, and `image` is Media's concern. The existing candidate directories deliberately **remain in place**, without being counted as proof of implemented capability. `business` was removed in the earlier approved consolidation.

**Preservation evidence:** legacy Tenancy's legal-entity/Billing note moved into [Identity](capabilities/identity/capability-record.md) and [Billing](capabilities/billing/capability-record.md); Company Console's navigation, governance, subscriptions, quota and policy dashboard requirements into [Application Compositions](capabilities/application_compositions/capability-record.md). [Membership](capabilities/membership/capability-record.md) and [Organisation Model](capabilities/organisation_model/capability-record.md) are retained candidates; neither has been prematurely promoted. [Organisation Console](capabilities/organisation_console/capability-record.md) is the accepted renamed presentation concept; its independently packaged status still requires a separate classification decision.

**Deferred action:** following review and merge of this preservation PR, create a second focused PR for directory removal only. Reconfirm that content is transferred, current governing references remain consistent, and all relative links have been repaired before deleting any of the eight directories. No governing amendment is needed solely to perform this classification: the current accepted catalogue and ADR-0017 already establish these boundaries.

## Identity, Age and Eligibility Assurance — working review index (17 November 2026)

| Topic | Classification | Status and source | Ownership disposition |
|---|---|---|---|
| Identity / age / eligibility assurance | **Cross-capability architectural review**, not an independent registered capability | Owner-approved direction, [dedicated review](../reviews/identity-age-eligibility-assurance.md), no verified new implementation | Identity owns local principals; Authentication sessions; Authorisation access; Marketplace merchant eligibility; Legal Compliance laws; external proofing and age evidence custody **open**, no mandatory additional package |

Do not equate an installed Identity or Authentication package with verified civil identity, adult age, organisation authority or seller trustworthiness. Federated assertions must not create local memberships or grants without independent policy decisions.

## Verification — candidate classification (17 November 2026)

| Candidate | Working class | Availability/evidence | Boundaries |
|---|---|---|---|
| `verification` | **Platform candidate; owner-approved conceptual creation** | [Capability record](capabilities/verification/capability-record.md), [cross-capability review](../reviews/identity-age-eligibility-assurance.md), [international comparison](../reviews/verification-international-jurisdictions.md). No verified root `CONTRACT.md`, package, CI, provider contract or deployment | Verified claim requests, purpose-scoped attestations, issuer trust/status, expiry/revocation and qualified evidence references; no civil-document master, IAM session/permission, merchant eligibility or legal applicability ownership |

Separate Verified/Installed/Configured/Operational/Enabled/Authorised status remains **unverified**, regardless of conceptual approval. Any future package needs independent classification, consumer contract, legal/privacy/security review, minimal-host acceptance and storage register.

### Localisation replaces the empty Translate candidate (17 November 2026)

The empty `docs/capabilities/translate/` directory has been removed in the working blueprint, not retained as a compatibility alias. The canonical active record is [Localisation](capabilities/localisation/capability-record.md). The old register's `Established` label denoted a catalogue entry, **not** an independently verified implementation; the new candidate has no verified root `CONTRACT.md`, package, installation or tests. The governing catalogue rename is a separate PR. Only the historical rename note uses the old name.


### Time & Attendance — proposed distinct Domain responsibility (17 November 2026)

| Entry | Classification | Decision/evidence | Boundary |
|---|---|---|---|
| `time-attendance` | **Domain candidate** | **Owner-approved conceptual separation** in [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59); detailed capability review and implementation unverified | Actual attendance, timesheets, breaks, approved time evidence and corrections; distinct from Employment contractual hours, planned Workforce Scheduling, Payroll pay calculation and platform Scheduler's timed triggers |

[Conceptual ownership note](../proposals/time-attendance-ownership.md) · [Capability pro-forma](capabilities/time-attendance/capability-record.md). No implementation/package/operational status is asserted. A dedicated future review must establish independently usable input/output contracts, privacy controls, GUI and package classification before creating a new implementation repository.

## Events — owner-approved conceptual boundary (18 November 2026)

| `events` | **Domain candidate** | **Conceptual EVT-01–10 and EVT-12–15 owner-approved**; [record](capabilities/events/capability-record.md), [PR #67](https://github.com/nuxt-layers/architecture-blueprint-review/pull/67). No verified implementation `CONTRACT.md`, CI, deployment or screens | Independent events, optional series/occurrences/programmes, schedule, restrictions, publication and lifecycle; does **not** own reservation ledger or attendance/people list |

**EVT-11 excluded.** Event attendee/RSVP/presence functions move under approved EVT-15 to separately reviewed [Attendance candidate PR #79](https://github.com/nuxt-layers/architecture-blueprint-review/pull/79), **not** an implied current implemented dependency. The independent owner-approved `time-attendance` boundary remains unchanged; Training/Booking/Enrolment own their existing specialist decisions. [Decisions](../reviews/events-refined-boundary-and-decisions.md) · [public contract and handovers](../reviews/events-contract-attendance-and-handover.md). `event_bus` is consolidated into Message Queue on master.

## Attendance generic participant and presence candidate — 18 November 2026

**New candidate `attendance`:** [conceptual record](capabilities/attendance/capability-record.md) — generic activity-scoped participant register, invitations/RSVP, check-in/out observations and validated attendance with corrections, provenance and owner outbox. Works without mandatory Events, Booking, Enrolment or Training. Explicitly **not** a universal Identity/Profile person master, admission authority or Booking capacity ledger. Previously owner-approved Booking/Enrolment/Training boundaries remain unchanged pending any later explicit transfer. Proposed one-roster/reference interfaces and pros/cons documented in the record; detailed ATT-01–08 not yet independently approved. Events EVT-15 is **owner-approved and merged in PR #67**; Attendance's detailed ATT-01–08 remain independently proposed. No runtime package or published `CONTRACT.md` asserted.

## Export evidence and boundary clarification (18 November 2026; draft PR #68)

The catalogue's `export` **Established** entry means the architectural library vocabulary/classification is established, **not** that a deployable API or runtime is verified. The `nuxt-layers/export` repository exists at `c75367e66c2d228a4d98193e7307335e6682a678` and contains only `.gitignore`, `LICENSE`, `README.md` (`# export`) on that baseline; no root `CONTRACT.md` or independent acceptance is available. The [Export conceptual review](capabilities/export/capability-record.md) proposes a stateless renderer boundary and flags durable bulk-export orchestration ownership as **open** (EXP-01/09). These proposals do not modify the governing catalogue or claim implemented functions.

## Export owner decision update (18 November 2026; draft PR #68)

The project owner approved the strict renderer Library boundary and commercially permissive, self-hostable, replaceable engines, while preserving optional-format and technical validation gates. EXP-01/09 are resolved conceptually; EXP-07 investigation and EXP-08 implementation alignment are still incomplete. No current root `CONTRACT.md`, delivered API, tested PDF/A/UA compliance, or independent consumer evidence is asserted. [Export record](capabilities/export/capability-record.md).

## Gaming — conceptual review evidence (18 November 2026; draft PR #71)

| Field | Recorded evidence |
|---|---|
| Classification | Proposed Domain candidate; independent gaming authority conditional on justified reusable lifecycle |
| Working record | [Gaming conceptual record](capabilities/gaming/capability-record.md) |
| Governing baseline | `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (ADR-0017/0018 accepted) |
| Blueprint opening baseline | `architecture-blueprint-review/master` `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` |
| Root implementation contract | Not retrievable; `nuxt-layers/gaming` returned 404 during access check; existence/availability not established |
| Public interfaces | Proposed commands for rules, instances, play, adjudication; queries for authorised game state and rankings; source-owned result/outbox events, subject to owner approval |
| Presentation | Proposed optional dashboard/play/organiser/referee interface and headless mode |
| Operational and acceptance evidence | Not verified; no implementation tests executed |
| Decision status | GAM-01–08 open owner decisions; GAM-09 technical investigation; GAM-10 implementation alignment; GAM-11 acceptance pending |
| Merge status | Draft PR only, explicit owner approval required |

This evidence supplement does **not** promote the existing candidate to Established, installed, operational, compliant or authorised status.

**Gaming correction — 18 November 2026 (draft PR #71):** The earlier entry in this register describing Gaming as a broad Domain game-engine/official-result authority is superseded. Current owner-described intention: portal for independently composed game layers with catalogue, launch routes and common score acceptance/leaderboards. **Proposed classification:** Platform with optional Presentation; each game owns its gameplay/rules/original scores. Detailed GAM-02–08 require approval, no implementation or root contract verified. See [Gaming record](capabilities/gaming/capability-record.md).



## IAM Integration conceptual review alignment — 18 November 2026

**Status: Proposed, non-normative; [draft PR #73](https://github.com/nuxt-layers/architecture-blueprint-review/pull/73), awaiting owner decisions.** The existing established `iam-integration` Foundation (IAM) entry remains a no-domain-data suite composition component under accepted ADR-0005/ADR-0012. The conceptual [IAM Integration record](capabilities/iam_integration/capability-record.md) proposes one-call public caller/decision/tasks composition, public member adapters, coordinated operation receipts, revocation safety, headless services and optional operator presentation. No implementation or operational status is asserted. Durable checkpoint ownership, measured revocation bound and suite GUI packaging remain open; the legacy published target `CONTRACT.md` requires alignment. Preserve independent Identity, Authentication, Authorisation and Profile authority.


### Infrastructure conceptual classification review (18 November 2026)

**Proposed, not approved or implemented.** The [infrastructure review](../reviews/infrastructure-conceptual-architecture.md) recommends retaining `infrastructure` as a **Foundation operational responsibility**, usually realised in trusted **host/deployment composition** rather than a mandatory separately installed Nuxt Layer or business-state-owning capability. Host/operator owns privileged resource/UTC-source application and recovery; provider evidence is qualified, not automatically verified. Clock, Configuration, Storage, Site Hosting, IAM, capability persistence, Temporal gateway and operational evidence owners retain their published responsibilities. An optional reusable headless control/status contract and operator-only dashboard require separate justification. The catalogue's prior *Foundation candidate / under consideration* status remains in force pending INF-01–05 owner decisions and separate normative adoption. Never infer an implemented public `CONTRACT.md` from this proposal.


**Owner-approved INF-01 refinement (18 November 2026):** `infrastructure` primarily defines the canonical hosting and deployment build standard, Docker/Compose configurations and server setup/upgrade/verification/recovery scripts. Optional headless operational status/control interfaces and operator screens complement—not replace—this responsibility. Retain Foundation responsibility with implementation kind **infrastructure blueprint / host-operated deployment composition**, not mandatory independent Nuxt Layer. The [conceptual review](../reviews/infrastructure-conceptual-architecture.md#owner-clarification--authoritative-hosting-environment-definition-18-november-2026-supersedes-narrower-wording-above) documents both. Working register remains non-normative; production acceptance is not claimed.


## Legal Compliance dedicated conceptual review — 19 November 2026

**Proposed, non-normative, pending owner approval (draft [PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85)).** Preserve established Foundation classification and governing ownership. The [dedicated `legal_compliance` record](capabilities/legal_compliance/capability-record.md#legal-compliance--dedicated-conceptual-review-19-november-2026) defines qualified jurisdiction/service/time-specific source and legal-obligation lifecycle; scoped legal holds; idealised applicability, hold, obligation and evidence input/output contracts; separate domain enforcement, Privacy, Authorisation and Audit authority; optional restricted GUI and headless operation. Implementation repository exists but root `CONTRACT.md` is absent on inspected `master`; none of these proposed interfaces is certified implemented. LC-01–LC-07 are recommendations, not approved architectural decisions. Changes to governing catalogue require separate authority.


## Legal Compliance conceptual specification coverage — 20 November 2026

**Draft [PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85); LC-01–LC-13 proposed.** The [consolidated `legal_compliance` capability record](capabilities/legal_compliance/capability-record.md) now documents purpose/classification, legal-source and interpretation ownership, canonical obligation/control/evidence schema, input/output contract, headless/GUI, event/scheduled/manual automation, sourced variables and restricted DMN 1.6-aligned evaluation, ISO 37301/37302-informed monitoring and effectiveness, ISO 31000 risk, PROV-O/ISO 15489 provenance/records, ISO 19011 audit guidance, security/Privacy references, twenty acceptance scenarios and open decisions. Actual `nuxt-layers/legal-compliance` root `CONTRACT.md` not verified. No legal conformity or standards certification claim. Draft branch requires newer-master Git reconciliation before merge.
