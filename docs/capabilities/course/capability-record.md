# Capability Record — Course

**Capability:** `course` (actual directory `docs/capabilities/course`).  
**Classification:** **Domain candidate** — proposed independent owner of structured learning offerings, curricula and intended learning outcomes; distinct from Enrolment and Training.  
**Review status:** **Proposed conceptual design; owner approval outstanding.** No implementation, live public contract, legal compliance or acceptance evidence is claimed.  
**Reviewed:** 17 November 2026.  
**Opening authority:** `nuxt-layers/architecture-rules/master` `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint `master` `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`.  
**Evidence:** Governing `docs/catalogue.md` defines Course as “Structured learning offering and outcomes”; separately defines Enrolment as “Course/learner participation and allocation” and Training as “Verified training participation, competencies and completion records”. Normative `docs/architecture.md` and `docs/capability-standard.md` establish ownership, explicit acyclic public interfaces, server authorisation, provider-neutral composition and optional presentation. The target record was an empty pro-forma; `nuxt-layers/course` was not found at review time. All service names below are **conceptual**, not an asserted implemented API.

## Capability Name

`course` — Structured learning offering and curriculum authority.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed)

**Proposed** domain candidate only. Available, Installed, Configured, Operational, Enabled and Authorised are **not established**. No release or package version is verified.

## Purpose

Define reusable, versioned **learning offerings**: what is taught, why, to whom, under which prerequisites, in which ordered/optional learning units, with what intended outcomes, teaching/assessment specifications, delivery modes and published revisions. Offer safe, independently useful catalogues and course definitions to learning providers, applications, Enrolment, Training and other authorised consumers.

A Course is not a learner's admission, progress, attendance, performance, qualification or credential. A course can be maintained and published without any learners; that independent lifecycle justifies the candidate boundary.

## Classification

**Domain candidate**, independent of Nuxt implementation/deployment. Native headless public business contract, with optional separable presentation. The host composes capabilities and owns routes/branding. No separate service or repository is mandated by classification.

## Authoritative ownership, exclusions and invariants

Course owns:
- Tenant-scoped course identifiers and versioned learning-offering definitions: name, descriptions, audience, objectives, structured outcomes, units/modules, ordering, dependencies, estimated learning effort, delivery-mode eligibility, expected capacity *constraints* and prerequisite **definitions**.
- Course definition lifecycle, draft revision, review/approval reference, publication, replacement, retirement, tombstone/withdrawal reason and immutable historical version references needed to interpret enrolments/completions.
- The course-defined requirements for successful completion (rubrics, outcome mappings, assessment requirements, minimum participation or other declared criteria), **not individual evaluation or certification decisions**.
- Course-owned catalogue/discovery metadata and permitted reference mappings to reusable Publisher content, Media, external learning resources, classification taxonomies and externally recognised standards; source bytes and external standards are not reowned.
- Course-version provenance, approval/effective dates and safe authoritative domain change events.

Course does **not** own:
- Learner identities, group membership, consent, authentication or authorisation (Identity/Profile/Privacy/Authentication/Authorisation).
- Applications, offers to named learners, waitlists, seats allocated to named persons, admissions and enrolment states (**Enrolment**).
- Attendance, learning activity evidence, achievement, competency evidence, individual completion, transcript or certificates (**Training**, and any future independently justified assessment/credential authority). An outcome *definition* is not a verified achieved outcome.
- Event sessions, venues, calendars, bookings and attendance. Scheduled workshops may compose Course and an event capability; “workshop” is not assumed to be a new authority.
- Published content versions, rich-text storage, images/videos and file bytes (Publisher, Media, Storage).
- Payments, orders, billing or prices actually charged (respective commerce/accounting owners); Course may reference an offering's commercial terms, not assert a transaction.
- Final statutory legality, individual eligibility or institutional accreditation. Policy and compliance evidence remain with their authorities.
- Workflow orchestration, delivery, search index, analytic aggregates, notifications or provider-specific LMS connectors.

**Invariants:** Course version references are never silently reinterpreted; the applicability of requirements is explicit; publication does not establish capacity, an admitted learner or earned competence; loss of external sources cannot silently change an already-published curriculum; course access is tenant/resource scoped; withdrawal never silently erases existing enrolment/training evidence.

## Dependencies

**Required conceptual contracts:** server access-decision/caller context from Authorisation with Identity ownership references, the capability's own persistence when stateful, and trusted Clock semantics for effective times. Host composition supplies documented shared infrastructure, not private stores or business adapters. Actual package imports are not decided. Access/standing unavailability fails closed on protected operations.

**Conditional:** Publisher for referenced versioned learning materials and optional formal editorial publication; Media/Storage for course assets; Enrolment for learners; Training for achieved learning; Workflow for configured approvals; Configuration for approved organisational preferences; Legal Compliance/Privacy for effective restrictions; Content Security/Moderation for applicable submission and exposure gates; integrations for an external LMS or catalogue. Their absence must not prevent native *definition* and controlled internal management where law, security and the chosen configuration permit it. An unavailable mandatory publication/safety gate fails closed.

**Optional integrations:** Metadata, Localisation, Search, Reporting, Notifications, Scheduler, Message Queue and Audit/Logging/Observability via independently owned published boundaries. Optional external LMS imports/exports use Integrations adapters; not a required SaaS provider.

## Version

Course entity has a stable identifier plus immutable published revision ID, schema/contract version, effective interval, provenance and supersedes link. Document/asset references identify their own owner and revision. No implementation or release version is asserted.

## Availability

Per tenant/site, per user/role, per offered revision and its publication status. Separate visible catalogue availability from permission to edit, permission to enrol and verified learning outcomes. Missing or stale eligibility/enrolment information must be represented as **unknown**, never “eligible”.

## Capabilities offered — native lifecycle and service behaviour

1. **Author and revise:** create a draft; attach structured outcomes/units/prerequisites, instructional/assessment specification and authorised external references. Validate identifiers, dependency graph, duplicate units, cross-tenant references, minimum content and declared delivery modes.
2. **Validate and compare:** detect incomplete outcomes, broken prerequisites, missing/withdrawn content and changes that affect existing consumer obligations; produce actionable validation findings, never fabricated accreditation.
3. **Review and publish:** record permitted approval/authorisation provenance; publish a frozen revision and its effective time, subject to configured gates; emit committed facts through an owned durable outbox.
4. **Maintain:** publish successor revision, retire future discovery, withdraw access to unsafe or unlawful content and preserve lawful historical references. An existing enrolment's applicable requirements do not change merely because the public catalogue changed.
5. **Discover and read:** list/filter visible offerings; return a public or authorised course outline, requirement definitions, dependency/prerequisite graph, version history, validity and associated sources with clear stale/unknown status.
6. **Import/export:** accept schema-validated authored definitions and references with explicit conflict resolution/provenance; emit portable definitions with redaction, licence and transfer constraints. No provider import auto-publishes.
7. **Recover:** idempotently retry failed writes/publication projections, reconcile external reference drift and expose blocked/degraded states. A failed validation or gate produces a stable error without partial publication.

**Lifecycle:** Draft → Pending review (optional) → Approved (where required) → Published → Superseded / Retired / Withdrawn. Rejected returns to revision or is closed. Published revisions are immutable; modifications create a successor. Deletion obeys legal/retention holds, protected consumer references and history; hard deletion is not a default user action.

## Idealised public inbound contract

Every row states source → input meaning → authoritative owner → validation and absence semantics. These are *not fixed endpoints*.

| Surface | Source, facts/commands or context | Authority and validation; absent/stale/invalid behaviour |
|---|---|---|
| `courseDefinitionCommand` | Author/editor: create/revise/archive; title, outcomes, modules, prerequisites, delivery settings, expected effort, reference IDs, draft revision, idempotency key | Course owns resulting definition; schema + semantic/prerequisite DAG checks, resource permission, tenant and revision preconditions. Invalid rejects; duplicate same-key returns same prior result; conflicting payload/revision returns conflict. |
| `coursePublicationCommand` | Authorised publisher or approved Workflow: request review, approve/reject, publish, supersede, retire, withdraw | Course owns transition; Authorisation supplies caller decision, Workflow only process evidence; verify effective policy, safety/content gates and approval evidence. Missing required gate blocks; queued ≠ published. |
| `materialReference` | Publisher/Media and permitted external provider: opaque content ID, source owner, version, licence, availability/access and review status | Source owns content, bytes and access. Course validates permissible version reference and health before release; stale/withdrawn source blocks unsafe exposure, but does not overwrite original revision. |
| `participationConstraint` | Enrolment/host consumer requests published course/version, prerequisites and capacity **constraints** | Course supplies rules, not learner standing or seat decisions. Unknown student eligibility is an explicit unresolved decision for Enrolment. |
| `completionSpecification` | Training requests versioned requirements, outcome mapping and effective criteria | Course supplies criteria only; Training determines individual evidence and completion. Unknown version fails without inventing a qualification. |
| `effectivePolicyContext` | Configuration, Privacy, Legal Compliance, Authorisation, Clock: validated settings, mandatory restrictions, retention/age/access applicability, effective time | Each source owns its own decision. Course enforces applicable constraints; invalid or unavailable mandatory context fails closed. Settings never override statutory floors. |
| `providerImportEvidence` | Integrations: external course ID, mapping, licence, provenance, revision, validity and conflict evidence | External provider owns its remote facts. Course accepts draft proposals only after validation; untrusted provider assertions do not prove enrolment, completion, accreditation or approval. |

## Idealised public outbound contract

| Surface | Authorised consumers; meaning and guarantee |
|---|---|
| `courseDefinition` / `courseVersion` | Enrolment, Training, Publisher/editor, learner catalogue: Course-authoritative canonical ID, tenant, revision, title, outcome/prerequisite definitions, module graph, effective status, provenance and publication/withdrawal state; **no claim of individual success**. |
| `courseCatalogue` / `courseOutline` | Public/authorised discovery: only permitted metadata and content references, visibility status, locale and partial/staleness indicators; not proof a learner may enrol or has purchased a place. |
| `courseRequirements` | Enrolment/Training: immutable versioned prerequisites, eligibility *rules*, learning outcome mapping and completion criteria; Enrolment owns learner eligibility decision and Training owns verification. |
| `courseCommandResult` | Authenticated caller: accepted/rejected/committed transition, resource+revision reference, validation failures, idempotency/correlation and unknown/blocked status; accepted asynchronous action is not completed publication. |
| `courseChangeEvent` | Approved internal subscribers: committed Created/RevisionPublished/Superseded/Retired/Withdrawn/RequirementsChanged and optional ReferenceBlocked; stable event ID, tenant, version, effective time, safe references and correlation. Outbox-backed at-least-once delivery; replay and duplicates expected. |
| `courseExport` / `sourceHealth` | Authorised export, audit and integrations: portable course definition/version with permission-based disclosure, licence and source provenance; provider status is reported, not guaranteed by Course. |
| `courseActivityEvidence` | Audit/Reporting: domain decision, actor/context references, version, effective event and safely minimised reason; Audit owns evidence acceptance, Reporting owns derivations. No secret/raw learner information in event payload. |

**Commands:** enforce server authorisation, tenant isolation, expected revision, idempotency and domain invariants; return stable coded failures; no implicit auto-enrolment. **Queries:** scoped by audience/tenant/version, disclose revision, freshness, source completeness and permitted fields. **Events:** only after committed authoritative state transitions, via Course-owned durable outbox; consumers must deduplicate, handle replay and obtain authoritative state as needed; no exactly-once claim. **Unsupported:** record a grade, certify a person, grant course access, book a seat, send a notification, create a payment or make an accreditation decision.

### Shared context and consumer guarantees

Per operation carry only relevant resource/tenant owner, trusted caller and assurance, permission decision context, expected course version, effective date/Clock zone where needed, policy revision, idempotency/correlation and provenance. **No compulsory universal request envelope.** Public errors are stable codes/message keys, safe for localisation. A course's authoritative source is clear; dependent facts retain their source authority. Consumers cannot assume eventual delivery time, perpetual public accessibility, complete externally hosted content or valid learner standing. Preserve immutable references or explicit withdrawal tombstones while applying lawful erasure. Authorisation and disclosure apply equally to exports, search projections and cached summaries.

## Cross-capability relationship and reciprocal interface register

| Partner | Course receives / supplies | Authority, dependency and degradation |
|---|---|---|
| **Enrolment** | Supplies published course version, entry requirements, offering eligibility constraints; receives enrolment counts/availability only if separately needed | Enrolment owns applications, admissions, allocations and learner participation; candidate collaboration, no hidden bidirectional package import. Unknown capacity/eligibility → pending/unavailable, not admitted. |
| **Training** | Supplies immutable outcome/assessment criteria and version references; receives aggregate feedback only when authorised | Training owns attendance, competency evidence, completion/credentials. Training unavailable → Course authoring still works; no completion assertion. |
| **Publisher / Content Editor** | References approved, versioned learning resources and editor presentation; provides course-owned structured fields/action descriptors for optional host editor integration | Publisher owns document lifecycle; Course owns curriculum and rule revisions. A generic document editor cannot infer a course's outcomes from arbitrary rich text. Concurrent Content Editor PR #54 is provisional. |
| **Identity / Authentication / Authorisation / Profile** | Trusted tenant, group, caller and standing; authentication assurance and access decisions; limited profile display/contact context | IAM owns people, sessions and access. Deny/unknown → no protected operation. No duplicate class/learner membership hierarchy. |
| **Configuration / Clock** | Effective approved preferences/rules and time-zone semantics; returns effective course revision/time | Configuration owns setting precedence, Clock owns time calculations; Course owns meaning of its effective state. Concurrent Configuration PR #53 provisional. |
| **Privacy / Legal Compliance** | Retention, lawful basis, hold, child-safeguarding/disclosure and jurisdiction constraints | Policy sources own restrictions; Course enforces its part, including vulnerable learners and lawful history. No unapproved cross-border provider transfer. |
| **Content Security / Moderation** | Receives source safety decisions, quarantine and withdrawal/appeal references for submitted materials | Each retains its content/safety authority; fail closed on mandatory gating; Content Security PR #55 provisional. |
| **Metadata / Localisation / Search / SEO** | Sends permitted course labels/revisions/publication facts; receives controlled taxonomies, approved translations and derived discovery projections | Course owns core source; search index and translations must not override it. Unavailable search does not block direct authorised reads. |
| **Media / Storage** | Receives stable safe media references/access; supplies course-context permissions | Media owns metadata and asset lifecycle; Storage owns bytes. Never expose an unsafe signed address from course metadata. |
| **Workflow / Scheduler / Notifications / Message Queue** | Supplies decision requests and time-triggered commands/recipient-safe facts; receives approval outcomes, delivery/queue status | Workflow owns choreography, Scheduler timing, Notifications delivery, Queue transport. No scheduler job or message by itself authorises publication. |
| **Audit / Logging / Observability / Reporting** | Supplies material domain actions/failed security operations and minimised correlation; receives acceptance/diagnostics/derived aggregates | Audit owns accountable evidence; Logging technical telemetry; Reporting analysis. Course does not reown any of these records. |
| **Integrations / Federation** | Supplies controlled versioned export/import/syndication references and origin/provenance | External LMS/federated copies retain source attribution and local access restrictions; remote claims not automatically authoritative. Provider outage cannot silently advance course state. |
| **Events, bookings and commerce domains** | Supplies delivery/session specification and versioned pricing references; consumes capacity/booking/sales evidence where explicitly composed | Event, Booking, Order, Pricing and Accounting each own their records. No automatic service dependence or package cycle. |

**Dependency rule:** Consumer calls to Course are not Course imports of all consumers. Domain cooperation may use host-supplied ports, subscriptions or public contracts. Any necessary two-way coordination must preserve one-way build/runtime dependencies and independent authority.

## Configuration

Proposed tenant-/organisation-scoped, approval-controlled settings: course authoring permissions and visibility; review gates; supported languages and delivery modes; entry/completion requirement schemas; external source/provider policy; archival and export defaults; applicable privacy and retention constraints. Course validates **domain** settings; Configuration owns selection/precedence/provenance. Personal reading preferences are not course completion criteria. Security and statutory minima are non-overridable.

## Security, assurance, privacy and compliance

Use OWASP ASVS 5.0 L2 minimum and L3 where sensitive; server-side resource authorisation; separate author/reviewer/publisher/learner capabilities; step-up and separation of duties where policy requires. Prevent cross-tenant references, unauthorised preview of unpublished modules, malicious resource links, unsafe content uploads, dependency-graph resource exhaustion, forged completion claims and replay/confused-deputy publish operations. Enforce provenance on remote materials and media, quarantine upon required safety decision failure, and invalidate projections/signed access after withdrawal. Do not expose grades, learner rosters or sensitive profile data in public outlines, logs, events or exports.

Apply UK GDPR/GDPR where relevant, children's/educational data safeguards, retention and legal holds through authoritative policy sources, with jurisdiction and effective-date review; no claim of legal compliance is made by this document. Accessible disclosure of prerequisites, language and learning outcomes is required. External LMS terms, licences, international transfers and accreditation require documented review; provider neutrality is the default.

## Conceptual GUI and headless operation

**Course management dashboard** in host capability sidebar: authorised catalogue and status counters, draft/review/published/withdrawn queues, warnings about unpublished/unsafe references and recently changed revisions. **Create/edit wizard:** audience, titles, outcome builder, structured module order, prerequisite dependency visualisation plus accessible equivalent, linked Publisher/Media picker, assessment requirement definitions, languages, delivery settings, validation and preview. **Review/publish workspace:** version comparison, approvals, scheduled effectiveness, publication/withdrawal confirmation, provenance, failure/recovery. **Learner-facing catalogue/outline:** only authorised/published descriptions, prerequisites, outcomes, delivery mode, clear “enrol” handoff to Enrolment (never Course granting participation). **Operator:** external source health, import conflicts, retry/degradation, retention/withdrawal impact and controlled export. A learner transcript, grades and certification UI belongs with Training, not Course.

Optional separable Nuxt presentation consuming only Course public contracts; host owns sidebar/routes; Theme Manager semantic vocabulary, WCAG 2.2 AA, BCP 47/CLDR/Intl, keyboard and screen reader support, accessible mobile layout, plain-language uncertainty and status messages. Headless Course must remain fully capable of authorised management/consumption without any of these screens.

## Conceptual acceptance scenarios (input → behaviour → output → owner)

| Scenario | Expected behaviour, result and authority |
|---|---|
| Native creation | Valid authorised draft definition → validate module graph, persist draft → revision and validation report (**Course**). |
| Publication | Approved draft with source refs and required gates → freeze and publish revision → committed version + outbox event (**Course**); approval process evidence remains **Workflow**. |
| Enrolment consumer | Enrolment requests course/version prerequisites → return published criteria, not learner eligibility → learner decision remains **Enrolment**. |
| Training consumer | Training requests frozen outcome criteria for historical enrolment → return original version even after successor publication → achieved competence remains **Training**. |
| Permission / tenant | Caller requests another tenant's private draft → deny without disclosing existence → **Authorisation** decision applied by Course. |
| Invalid input | Circular prerequisites or mismatched content owner → reject with stable code, no changed revision → **Course**. |
| Retry / replay | Repeated identical publish command/event → same committed result, deduplicable event → **Course** outbox; consumer handles duplicate. |
| Provider failure | Referenced remote material unavailable or unverified → show degraded/blocked and prevent unsafe new release; no false completed operation → **Course** state, provider evidence **Integrations**. |
| Withdrawal / history | Published course becomes unsafe or retired → stop public discovery/access as required, emit withdrawal, preserve lawful version references → **Course**; learner records remain **Enrolment/Training**. |
| Reporting/export | Authorised aggregate request → permitted versioned definition without learner records → **Course**; report derivation/disclosure remains **Reporting**. |
| Unsupported action | Caller requests marking named learner complete → explicit unsupported operation; no state mutation → **Training** retains individual outcome authority. |

## Decision register

- **Established (governing):** Capability separation, normative access/security/contract, provider-neutral composition, acyclic dependencies, Course/Enrolment/Training catalogue division, optional headless presentation and owner-retained persistence.
- **Proposed COURSE-01:** Course is an independent domain capability owning versioned offering/curriculum/outcome **definitions**, not learner outcomes.
- **Proposed COURSE-02:** Published revisions are immutable, and consumer participation/completion refers to the effective frozen revision.
- **Proposed COURSE-03:** Course stores structured learning units and outcome criteria while Publisher owns reusable editorial material; Content Editor can present a Course-specific editing surface only through an authorised published Course contract.
- **Proposed COURSE-04:** Enrolment manages admission, allocation and learner participation; Training manages evidenced achievement; no Course completion or seat assignment.
- **Proposed COURSE-05:** Provider-neutral native authoring/discovery must remain functional without an LMS; external import remains controlled drafts pending review.
- **Proposed COURSE-06:** Publication/withdrawal obeys explicit safety, legal, access and approved workflow gates; versions never silently overwrite history.
- **Proposed COURSE-07:** Course offers native headless operations and an optional management/catalogue GUI, without owning host navigation.
- **Agreed COURSE-08 (17 November 2026):** Course defines outcomes and assessment requirements; newly created Assessment candidate owns instruments, individual attempts, marking/moderation, appeals and authoritative assessment results; Training verifies learning achievement and course completion. See [Assessment candidate](../assessment/capability-record.md).
- **Agreed COURSE-09 (17 November 2026):** Course owns versioned curriculum and delivery constraints; Enrolment owns cohorts, admission, waitlists and learner allocation; Events/scheduling owns teaching sessions, venues and timetables; Training owns attendance. Physical venue limits, instructional limits and enrolment allocations remain distinguishable; effective capacity computation is deferred to Enrolment/Events/Booking review. Self-paced learning need not use cohorts.
- **Agreed principle COURSE-10 (17 November 2026):** Course recognition and learner results and formal qualification awards are distinct authorities. An external accreditor owns actual recognition, subject to verification; an authorised awarding body or demonstrably delegated organisation owns its award decision. Assessment does not own credentials. **Open:** placement and detailed operating contract for award administration, credential issuing/verifying/revoking; separate candidate boundary recommended, not approved.
- **Agreed COURSE-11 (17 November 2026):** Distinct approval, safeguarding, retention and migration safeguards: Workflow can coordinate reviews, Authorisation decides access, Course commits publication; Legal Compliance/Privacy supply mandatory restrictions; historical course revisions remain traceable; transfer between versions requires explicit outcome/assessment mapping, review and approval where relevant. Exact legal periods, policies and procedures are jurisdiction/organisation-dependent and remain open for later specification.

No COURSE IDs are approved solely by inclusion here; adjacent unmerged PRs are provisional.

## Deferred implementation and acceptance

Confirm classification/decisions with owner; then independently specify actual `CONTRACT.md` ports, permissions, data model, outbox semantics and migrations; compose through documented minimal consumer/ADR-0012 host budget; ensure failure and release compatibility tests, isolated persistence, storage register, threat model, accessibility/i18n and external provider contracts. Only CI/user can conduct local/CI builds and tests; none were run as part of this conceptual review.

**Conceptual sign-off:** Pending owner review. **Implementation readiness:** Not established. **Pre-merge:** Mandatory fresh master, governing and PR consistency checks recorded separately.


## Owner-approved clarifications — COURSE-08 to COURSE-11 (17 November 2026)

**Status:** Owner-agreed conceptual boundaries; no published API, package or compliance evidence. Original Course review remains draft PR #56. These clarifications override earlier **Open** wording in this record; unresolved technical and new capability decisions remain open.

### COURSE-08 — Separate assessment responsibility

The owner agreed distinct responsibility for Course (outcomes and required assessment criteria), **Assessment** (reusable assessment definitions/instruments and individual execution/marking/results/appeals) and Training (verified learner achievements/completion). The owner explicitly requested creation of [`assessment`](../assessment/capability-record.md) as a new Domain candidate with the standard pro-forma and notes for **later full review**. A learner's mark is not a course completion, qualification or credential. Integrate by published versioned reference, not shared persistence or mutual package imports.

### COURSE-09 — Course, cohort, session and capacity

- Course owns structured curriculum/version, delivery-mode eligibility, recommended group size and learning constraints, not actual scheduled runs or person-level seats.
- Enrolment owns cohort participation/allocation, admissions and waiting lists, referencing frozen Course revision. A cohort is a particular organised offering; learners cannot be allocated by Course. Whether a cohort's own operational record belongs wholly to Enrolment or a distinct offering/run entity remains a detailed Enrolment decision, without transferring curricula.
- **Events** (not background Scheduler) owns the dates/times/venues and session lifecycle for actual teaching events. Scheduler may trigger timed jobs but is not the class timetable or an event booking authority. Bookings manages applicable bookable resource reservations.
- The **effective seat limit** may combine venue safety/physical capacity, instructor/staff constraints, course recommended limits and Enrolment's organisation-approved seats. Source each constraint from its owner and compute the resulting availability at the enrolment/booking decision boundary; never store multiple competing authoritative “places left” values. Availability is unknown/pending if mandatory constraints are missing or stale.
- Training/Time & Attendance as appropriate own their own actual participation/time evidence. A course can be self-paced with neither cohort nor scheduled sessions. No assumed direct runtime dependency or cycle.

### COURSE-10 — Recognition, awarding authority and credentials

**External accrediting organisation:** A third-party regulator, awarding organisation, educational institution or professional body is authoritative only for the scope of recognition it actually controls. Model a provider/organisation identifier, recognised programme/qualification code, issuer jurisdiction, recognition scope, course/revision applicability, effective and expiry dates, evidence/last-verified time, authoritative source, withdrawal/suspension state, conditions, and ambiguity. **Integrations** owns provider-specific discovery, secure connections, sync and webhooks; **Verification** may validate relevant issuer/representation claims within its approved remit; **Legal Compliance** qualifies applicable law. Course holds a provenance-marked reference/status projection, not an invented accreditation decision. Unknown, expired, disputed or stale recognition must not be publicly presented as current verified accreditation.

**Authorised awarding body:** The actual issuer/awarding institution holds the right to decide a qualification award. The platform must check entity standing, the issuer's recognised award scope, the delegated agent's identity and **explicit, time-bounded, revocable authority** to award a particular qualification/cohort/context, and individual eligibility/evidence. Identity/Authorisation covers platform principals and access; it **does not create external statutory/accreditor powers**. Record an externally evidenced delegated mandate, issuer, delegate, scope, effective interval, restrictions, status, provenance and any requirement for final issuer countersignature. A local workflow approval never substitutes for awarding authority.

**Award vs credential:** Assessment supplies authoritative results; Training supplies verified achievements/requirements satisfied. An **award decision** is made by the accredited awarding authority (or verified delegate under allowed scope) and may require an external authoritative response. A **credential** is the verifiable representation of that award, with distinct issue, replacement, correction, suspension, expiry, revocation and status verification. Neither belongs to Assessment by default; a separately reviewed qualification/credential authority boundary is **proposed, not yet approved or created**. Publisher/Storage may store a rendered certificate but cannot establish an award. An internal course participation certificate must be labelled accurately and not presented as an externally recognised qualification.

**Failure rule:** If issuer verification/mandate status cannot be established when mandatory, do not create or claim a verified recognised award. Preserve signed/sourced historical evidence and appropriately distinguish formerly valid awards from current accreditation. External provider outages do not silently revoke or re-authorise qualifications; return verified-as-of and unknown status. Corrections and revocations require source-authoritative events, secure provenance, status propagation and appeal/reconciliation.

### COURSE-11 — Four independent policy areas

1. **Approval:** Course validates/publishes its revisions; Workflow owns approval process state, IAM enforces role, permitted assurance and separation-of-duties. Organisation policy may permit a simple process, but required safeguarding, legal and security gates cannot be disabled. Revision author/reviewer/publisher attribution, change reasoning, rejection and withdrawal must be traceable.
2. **Safeguarding:** Course applies relevant minors/vulnerable-learner controls on catalogue content, age eligibility, restricted learning materials and permitted contact. Identity/Profile/Verification/Authorisation/Privacy/Legal Compliance and domain-specific safeguarding operations retain their respective authorities. A content moderation case or safeguarding allegation is not an assessment result. Fail closed for required checks without unnecessary collection of sensitive learner data.
3. **Retention:** Retain only lawful, necessary course versions and approval provenance; protect personal assessment, enrolment and achievement records under their owning capabilities' own schedules. Erasure, hold, archival, withdrawn discovery and historical certification evidence have distinct semantics. No hard-coded universal retention period; policy depends on jurisdiction, purpose and approved schedule.
4. **Migration:** Active enrolments/attempts reference the frozen applicable Course revision. A newer curriculum does not rewrite previous obligations. Moving learners requires versioned outcome/credit/rubric equivalence mappings, gap identification, competent review/approval, learner notification where necessary, and provenance. Unknown or conflicting mappings block automatic transfer. Preserve original Course, Assessment and Training evidence and explicit migration decision history.

**Future technical investigation:** credential/qualification ownership and public contracts; cohort/run identity and effective capacity adjudication; legally required evidence and safeguarding case handling; recognised-provider evidence freshness/reconciliation; jurisdiction-specific approvals, appeals and retention. No assumption that these are already implemented.


### Credentials candidate created (17 November 2026)

The owner explicitly requested creation of [`credentials`](../credentials/capability-record.md) with the standard capability pro-forma and the conclusions of this discussion; it is a **Domain candidate**, not yet an approved independent conceptual review or implemented capability. Credentials' proposed authority is the lifecycle of evidence-backed credential representations (issuance, verification, replacement, correction, suspension, expiry, revocation). It does **not** own Course curricula, Assessment marks, Training achievements or the underlying externally governed qualification award. The award/qualification decision's ultimate authority remains the recognised awarding body or explicitly empowered delegate. A dedicated Credentials review must decide whether an additional platform-controlled awards domain is justified. A document rendered by Publisher is not independently verifiable award evidence.

## COURSE-12 — Qualification authority reciprocal note (18 November 2026)

**Status: Owner-approved conceptual responsibility; detailed Qualification review and implementation pending.** [Qualification candidate](../qualification/capability-record.md): **COURSE-12 owner-approved:** Qualification independently owns versioned qualification schemes/recognition requirements and multi-pathway eligibility, including evidence from several Courses or none; Course retains individual teaching curricula, delivery modes and learning outcome definitions. Course publication, passing or completion does not itself award a Qualification. Use immutable course versions/references and public interfaces, not shared course records. No change to previously approved course ownership.


## COURSE-12 — approved creation of Qualification domain (18 November 2026)

**Owner-approved:** The five essential requirements justify creating [`qualification`](../qualification/capability-record.md) as a distinct Domain candidate: independent qualification specifications, multi-source/multi-pathway eligibility, awarding body/centre/delegation scope and status, authoritative individual award decisions, and qualification withdrawal/teach-out/version transitions/award appeals. Formal awarding is native to Qualification; do **not** create another generic `awarding` domain. The claimant's course, assessment and training records remain with their original owners, as does credential issuance/status with Credentials. The actual accreditor or external awarding organisation retains its own legal source authority. 

**Approval scope:** Approves architectural ownership and a candidate pro-forma, **not** complete Qualification conceptual sign-off, API/package, independent repository, implementation or regulatory compliance. All shared contracts remain conceptual pending dedicated review. This resolves the earlier qualification-domain deferral; COURSE-10's authority provenance and credential separation continue to apply.

## Reciprocal Assessment conceptual interface — 18 November 2026 (draft PR #64)

**Status: Proposed, not an independently approved course contract.** [Assessment conceptual review](../assessment/capability-record.md): Course supplies immutable course requirements and outcomes, including required assessment conditions; Assessment owns reusable assessment definitions, rubric versions and individual attempts/grades. Course must never interpret a raw mark as course completion and must preserve revision matching. An unavailable Course revision blocks claims of course alignment, but not an independently authorised standalone assessment. Conceptual cooperation does not require cyclic package imports; all protected reads and commands require public contracts, purpose/tenant permission and explicit unknown/failure handling. Preserve the course owner's existing decisions.


## Qualification independent conceptual review — reciprocal interface (18 November 2026)

**Status: proposed detailed contract under [Qualification review](../qualification/capability-record.md), PR #65; COURSE-12 ownership remains owner-agreed.** Course retains curriculum and immutable learning-outcome/course-revision authority; Qualification independently owns qualification scheme requirements, approved course-to-credit equivalence and cross-pathway award eligibility. Course's catalogue/accreditation reference is not external recognition or an individual award. Qualification may reference a frozen Course revision without importing its internals; Course need not depend on Qualification for native teaching definitions. Source mismatch/retired revisions remain explicit and historic records intact. This note does not complete this adjacent capability's independent review or assert an implemented contract.

## Training TRAIN-01–08 reciprocal proposal (18 November 2026)

**Status: TRAIN-01–08 owner-approved in [Training conceptual review](../training/capability-record.md), PR #63; proposed public contract, not an implemented interface or completed course review.** Training consumes immutable curriculum/criteria versions and returns independently verified learner achievement/completion; cannot change Course learning outcomes. Course revision/withdrawal needs explicit version-specific migration impact, never silent rewriting. All exchanges are public-contract scoped, tenant-authorised and provenance/version aware; avoid directed dependency cycles and treat unknown/stale external assertions explicitly.

## Cross-capability review note — Enrolment (owner-accepted conceptual)

**Enrolment reciprocal interface (owner-accepted; 18 November 2026; [Enrolment review PR #60](https://github.com/nuxt-layers/architecture-blueprint-review/pull/60)).** Course owns published offering/cohort identity, admission parameters, revisions, learning outcomes and any Course-owned seat supply. Enrolment consumes these as versioned facts and owns individual application/admission/withdrawal status, supplying authorised roster/participation evidence back. When Booking or Course owns seats, Enrolment must use its checked capacity contract and cannot create a competing pool. This note is not Course review approval or an implemented contract.
