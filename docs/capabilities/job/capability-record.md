# Capability Record — Job

**Name:** `job` (employment positions and vacancies, not background execution jobs).  
**Status:** Proposed conceptual Domain capability; not owner-signed-off, installed, configured, operational, enabled or generally authorised. Access is always per actor/action/resource.  
**Baseline:** Governing `architecture-rules@b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint `architecture-blueprint-review@6dac83a03da8704f7945ee1bc894f2248300445a`.  
**Review:** [draft PR #84](https://github.com/nuxt-layers/architecture-blueprint-review/pull/84); [opening baseline](../../../reviews/job-review-baseline.md). This record proposes a conceptual contract, not a published implementation API.  
**Evidence:** Governing [catalogue](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/catalogue.md) explicitly treats `job` as ambiguous: employment role/post may warrant a Domain; background execution belongs to Scheduler. The existing Job record contained proposed Employment and Qualification reciprocal notes, retained below. A direct `nuxt-layers/job/CONTRACT.md` fetch returned 404 and organisation repository search yielded no matching accessible repository. No published Job contract, runtime, GUI or test was verified.

## Purpose and classification

Provide an organisation-owned, revisioned catalogue of **employment positions/posts** and their **vacancy/opening authorisations**, including requirements, headcount/capacity and vacancy publication status. Distinguish a reusable position definition, a specifically authorised opening and an externally advertised job posting. A position may exist without a vacancy; several openings may refer to a single position; one incumbent may cover more than one assignment, and one position can have multiple authorised seats. The boundary has independent change and approval history, but standalone packaging remains conditional on demonstrating reuse beyond a host/Employment module.

**Do not confuse:** Scheduler owns background job triggers/attempts; Task owns assigned units of work; Project owns project delivery; Employment owns a person's engagement, terms and appointment/assignment; Qualification owns qualification scheme/award authority; recruiting/application pipeline and selection decisions require a separately justified owner (potential Process/Workflow host composition). Job does not own job seekers, applications, interviews, offers, employment contracts, CVs, actual headcount from Employment, work rosters, pay slips, professional licences, legal organisation records, or access decisions.

## Dependencies, availability, version and optional integrations

**Essential conceptual inputs per protected operation:** host-provided scoped caller and server-side Authorisation decision; Identity-owned tenant/group and resource owner references; Clock-consistent effective dates. A valid organising/employing party may require separately evidenced legal entity authority, rather than inferring employer from group/tenant. Dependency means a public contract or host-supplied port, not an import cycle.

**Conditional:** Employment occupancy/assignment evidence; Qualification and Verification evidence for stated requirements; Configuration for organisation policy, template and disclosure preferences; Profile for a subject's permitted display attributes only; Legal Compliance for jurisdiction-specific advertising, equal-opportunity and regulated-role duties; Publisher for public advertisements; Search for derived discovery; Integrations for external ATS/HRIS/job boards; Workflow/Process for approvals; Scheduler for time-triggered expiry/reminders; Notifications for permitted alerts; Audit/Logging/Observability/Reporting for their distinct responsibilities.

**No required external provider.** Native positions and openings work offline from provider business authority (subject to host infrastructure). External integrations use explicit per-organisation/source-of-truth mode, scopes, provenance, freshness, retries, conflicts, import/export, reconciliation, revocation and withdrawal. A remote acknowledgement is not proof of publication or appointment. Conceptual schema/API version unassigned; future commands/events need explicit compatibility and versioning.

## Authoritative information, native services and lifecycle

Job owns: immutable position identifier, owning organisation/tenant, position title/code, duties, level/category, location/work-mode references, working conditions *as a vacancy description*, required/desirable qualification and skill criteria with versioned alternatives, restricted compensation **advertising ranges** where permitted, approval limits, approved opening count, open/fill/cancel disposition, effective dates, listing visibility/consent, revisions, attribution and publication evidence references. Employer-approved ranges are not Employment's individual contractual salary or Payroll's wage entitlement. Legal obligations are qualified by Legal Compliance, not made true by locally selecting a checkbox.

**Position lifecycle:** draft → submitted/under review → approved → active → suspended/retired, with rejected/cancelled correction routes and historical effective revisions. **Opening lifecycle:** requested → approved/held → open → filled/closed/cancelled; partial occupancy and reopening are explicit, authorised revisions. **Advertisement lifecycle:** prepared → submitted → confirmed published → corrected/withdrawn/expired; provider-unknown is distinct from published. Position approval alone does not create a budget, recruitment approval, employee or public advert. Historical revisions survive cancellation and retirement subject to lawful retention.

Native services: create/revise/approve/suspend/retire positions; request/approve/update/close openings and authorised seats; validate criteria and dates; manage permitted advertisement metadata and withdrawal intents; read scoped positions/openings; reconcile occupancy from Employment without taking ownership of engagements; produce exports and committed events; preserve evidence and correction history. Approval of a new seat is subject to the employer's independently authorised finance/workforce policy, not implicit because a user can edit a job.

**Failure rules:** insufficient authority or tenant mismatch: deny without disclosure. Missing mandatory legal/approval evidence: hold sensitive action; stale/contradictory occupancy: report uncertain, do not fabricate vacancies. Missing optional Qualification comparison: show unassessed; not automatically unsuitable. Provider timeout/unknown outcome: pending reconciliation; never report publication confirmed. Retries are idempotent; expected revisions reject stale writers. An expiry scheduler outage cannot convert an expired opening into a valid opening; read/command path re-evaluates effective time.

## Idealised public input contracts

| Source / incoming facts or commands | Requirement, ownership and validation / failure semantics |
|---|---|
| Authorised hiring manager / administrator: create position, revise duties, request opening, approve seats, open/close/retire, publish/withdraw | Per-operation essential scoped caller, assurance and server-side Authorisation; permissions for vacancy approvals distinct from job editing and advertising; deny on missing decision or mismatched owner, stale revision or unsupported action |
| Identity and organisation/legal-party evidence: tenant, group ownership, acting role and evidenced employer/advertiser | Essential to protected scope; Identity authoritative for subject/group but not employer legal standing; unknown legally required advertiser identity blocks regulated publication |
| Configuration and policy owners: position taxonomy, default approvals, permitted listing/retention and remuneration disclosure rules | Conditional; versioned settings are interpreted/validated by Job and qualified law; invalid or missing mandatory policy holds changes, never defaults to unrestricted publication |
| Employment: active/delayed/ended position assignment references and dated occupancy changes | Conditional, source-owned employee/engagement facts; Job reconciles capacity projections, detects duplicates/unknowns; must never fabricate contractual assignment, termination or seat filling from job metadata |
| Qualification, Verification and regulated authority sources: scheme requirements and purpose-limited checked award/licence/eligibility signals | Conditional to role and legal risk; Job owns requirement wording/accepted alternatives but not award, credential or right-to-work verdict; missing evidence is unknown, not automatically ineligible |
| Publisher / external job board via Integrations: publication acceptance, listing identifier, status, correction and withdrawal evidence | Conditional; distinguish submitted, acknowledged, confirmed, rejected, delayed and unknown; provenance, time and external authority determine what can be asserted |
| Clock / Scheduler / Workflow: effective-time interpretation and proposed due/approval prompts | Conditional; triggers and process execution cannot approve, publish or close without fresh Job state and authorisation |

## Idealised public output contracts

| Public surface | Authorised consumer and meaning / limits |
|---|---|
| `getPosition`, `listPositions`, `getOpening`, `listOpenings` (conceptual queries) | Scoped Employment, workforce planners, authorised managers, optional recruitment consumers; versioned position/opening, effective and publication state, approved/open/filled capacity with **source-qualified** occupancy status; no personnel dossier |
| `createOrRevisePosition`, `approvePosition`, `requestOpening`, `approveOpening`, `changeOpeningState` | Server-authorised command results: accepted/rejected/held/conflict with resulting revision; acceptance does not imply candidate hired, budget committed or external advert completed |
| `requestListing`, `correctListing`, `withdrawListing`, `getListingStatus` | Publisher/Integrations/host consumers; Job's intent and local reconciliation plus externally proven state, not falsely claimed provider confirmation |
| `evaluatePositionRequirements` or `getPositionRequirements` | Restricted recruitment/Qualification consumer gets required/desirable criteria and accepted alternatives at a frozen revision; any comparison is source-attributed and non-binding for final hiring or regulated practice |
| `position.changed`, `opening.changed`, `listing.statusChanged` | After committed Job-owned changes via capability outbox; event IDs, tenant/resource, revision, effective/recorded times, limited payload and provenance; duplicate/out-of-order delivery normal, consumer deduplicates; no exactly-once guarantee |
| Restricted export and reporting projection | Authorised managers/Reporting/Audit get attributable history, approval decisions, counts with completeness/freshness flags and retention-safe disclosures; Audit owns preserved audit evidence, Reporting owns report assembly |

For every input/output expose only necessary tenant/owner references, actor/decision context, expected revision, idempotency/correlation ID, effective time/zone with Clock rules, evidence provenance/status, policy/version and stable error codes/message keys. No mandatory universal request object and no private DB or provider SDK types. Publication and public discovery require distinct permissions and approved disclosure settings; applicant personal information is never embedded in Job public output.

## Cross-capability ownership and reciprocal obligations

| Cooperating capability | Job receives / Job supplies; boundary and outage |
|---|---|
| **Employment** | Receives position-linked engagement and effective occupancy signals; supplies stable position/opening refs, title, criteria and current revision. Employment alone owns persons, agreement and appointments. Missing Job may permit independently valid engagements; missing Employment marks occupancy unknown, not zero. No mutual package imports. |
| **Qualification / Verification** | Receives source-qualified awards, status, accepted equivalences and purpose-limited assurance; supplies dated required/desirable criteria and alternatives. Job cannot decide award authenticity, statutory licence or hiring outcome; unresolved source status remains unknown. |
| **Identity / Authentication / Authorisation** | Receives scoped identity/group/tenant, session assurance, action/resource decision; supplies resource ownership/operation context for decisions. Access enforced on server; group membership alone does not establish employment or recruitment rights. |
| **Configuration / Clock / Legal Compliance** | Receives versioned preferences and statutory constraints/time interpretation; supplies references to effective rules and revisions. Legal uncertainty holds regulated publication; formatting does not determine legal deadlines. |
| **Publisher / Search / Integrations** | Supplies approved advert content/metadata and withdrawal intent; receives publication evidence, statuses and derived search visibility. Publisher owns publishable documents; Search only owns derived indexes; external boards keep their remote records. |
| **Process / Workflow / Scheduler / Message Queue / Notifications** | Supplies authoritative domain commands/outbox events and due hints; consumes execution/attempt/transport/notification acknowledgement. None becomes vacancy approval or ownership authority. |
| **Audit / Logging / Observability / Reporting** | Supplies attributable sensitive-action facts to Audit under its contract, structured diagnostics to Logging, telemetry to Observability, authorised projections to Reporting; none takes Job's record or derives unrestricted HR visibility. |

**One-way graph:** host composes ports/contracts; Job queries Employment-owned occupancy via a host-supplied public read port, Employment can consume Job positions via its own public port, but neither implementation imports the other or subscribes to a private schema. Consider an integration/orchestration read model where directional contract dependencies otherwise cycle. Domain authoritative evidence is never changed merely by delivery of an event.

## Configuration, security, privacy, legal and assurance

- OWASP ASVS 5 Level 2 baseline (Level 3 controls as risk warrants); deny by default at server including list/filter/count/export and public/private listing separation; owner/tenant and restricted hiring-manager scopes checked on every access.
- Approval segregation for opening authorisation, salary band changes, sensitive publication and withdrawal; step-up/dual control where risk requires. An organisation owner does not automatically obtain protected applicant/employee personal information.
- Personal details/CVs, protected characteristics, diversity monitoring and medical information are outside Job's core model. Recruitment/Employment/Verification must manage their own purpose-restricted evidence and confidentiality; subject access, retention, correction, lawful basis and cross-border disclosure require jurisdiction-specific qualification.
- Employment advertising, equal-opportunity rules, transparent pay requirements, work rights, protected occupations, age eligibility and record-keeping vary by country, region and effective date. Legal Compliance qualifies applicability; this document makes no legal compliance claim.
- Use configuration for controlled templates, taxonomy, approvals, geography, vacancy limits and provider modes, not to waive statutory floors. Record administrator actions, attempted prohibited changes and publication/outbox outcomes with minimal sensitive identifiers.
- Preserve lawful history and hold/recovery paths without over-retaining applicant data. Mutating historic meaning requires attributable corrected revisions, not silent overwrite.

## GUI and headless composition

**Job dashboard**, reachable via host sidebar for authorised organisation managers: positions catalogue with filters/status/version; position editor (duties, work mode, requirements, pay-band visibility); opening/headcount approval queue; opening occupancy reconciliation with Employment source/freshness; listing preview and publish/withdraw/status with channel attribution; timeline/audit history; permission-aware exports and reporting. Simple manager/operator surfaces hide irrelevant privileged choices but never grant permission through visibility alone. Public candidate-facing discovery (if enabled) consumes only approved listing projections through Publisher/Search; recruitment application UI belongs to its separately justified owner.

Host owns routing, organisation selector and menu placement; Job owns its domain state and consumes authorised public ports. Presentation is optional; headless operations remain complete. Theme Manager tokens and accessible components, WCAG 2.2 AA (keyboard, focus, error summaries, contrast/reflow), BCP 47, CLDR/ECMA-402, responsive mobile and clearly distinguishable pending/unknown states apply. Prefer semantic JobPosting structured data on actually confirmed public advertisements only, with truthful provenance.

## Conceptual acceptance scenarios (not executed tests)

| Input / situation | Expected output and authority |
|---|---|
| Authorised manager drafts position and independently approves three seats | Job returns position/opening revisions, three authorised seats, zero **verified** occupied seats only if Employment evidence confirms none |
| Employment reports one dated engagement assigned to valid position | Job reports attributable occupancy signal and revised freshness; Employment remains engagement authority |
| Position requires regulated qualification; Qualification signal unavailable | Requirement and comparison status remain unknown/needs review; no invented licence or exclusion decision |
| Unauthorised cross-tenant manager requests list/export | No protected records or revealing counts; Authorisation/Job enforce server-side denial |
| Two edits use same expected revision or repeat idempotency key | Conflict for stale writer; duplicate operation returns prior outcome without double-creating opening |
| Job board confirms submission but publication status unavailable | Pending/unknown, not published; reconcile using external identifier and provenance |
| An opening expires while Scheduler is down | Job refuses a stale publish/open action using Clock-effective state; later maintenance reconciles |
| Employee terminates engagement and related opening remains authorised | Employment owns termination; Job re-evaluates seat/vacancy state but never terminates or changes employment |
| Position retired after public listing | Job holds or closes openings per rules, requests withdrawal, distinguishes remote withdrawal pending from confirmed |
| Employment not integrated or job posting disabled | Headless native position catalogue remains usable with occupancy unknown and no fabricated external vacancy state |

## Decision register and challenge

- **JOB-01 — Proposed:** Separate employment Job (position/opening) from background Scheduler jobs. Governing catalogue already establishes execution-job ownership; independent Domain packaging awaits owner decision.
- **JOB-02 — Open owner decision:** Does Job own both reusable positions and **approved openings/vacancies**, with adverts as provider/status projections (recommended), or only position definitions with vacancies owned elsewhere?
- **JOB-03 — Open owner decision:** Applicant tracking, screening, interviews and hiring decision remain outside Job (recommended); choose eventual independent Recruiting domain versus host-composed Process/Workflow after a bounded lifecycle assessment.
- **JOB-04 — Proposed:** Individual employment and position assignment/occupancy facts remain in Employment; Job derives source-qualified seat state and fails safely on missing evidence.
- **JOB-05 — Proposed:** Qualification requirements and alternatives are Job-owned; recognition, awards, regulated eligibility and hiring suitability remain with their respective authorities.
- **JOB-06 — Proposed:** Opening approval and advertising are separately authorised; native operations must work without job boards, ATS, Workflow or Scheduler.
- **JOB-07 — Proposed:** Employer-approved position/pay-band advertising metadata is not Employment contractual remuneration; jurisdictional publication duties and effective rules are independently verified.
- **JOB-08 — Proposed:** Public listing requires positive confirmed publication state; external unknown/failure never becomes confirmed; all operations carry revisions, idempotency, tenancy and source provenance.
- **JOB-09 — Proposed:** Optional role-scoped manager dashboard plus public approved listings, complete headless interfaces and minimum WCAG/i18n baselines.

**Architectural challenge:** Seats may represent funded workforce capacity while budgets belong to Accounting/finance approval authority; do not imply a capacity approval spends money. Candidate selection and applicant PII must have an explicit future owner; neither Job nor Process/Workflow automatically takes that authority. Two-way information exchange with Employment must use contract/host orchestration instead of cyclic imports. Decide whether vacancy state is sufficiently independent for Job before repository creation. Public advertising must not disclose internal salary, personnel or draft vacancy information without a separate disclosure approval.

**Deferred:** Owner decision on JOB-01–09; actual root `CONTRACT.md` and provider-neutral composition entry point; authority mapping, precise schemas/events, tenancy/security threat model, legal assessment by jurisdiction, accessibility/manual acceptance, CI and independent consumer verification. No new governing ADR, implemented API, tests, integration or merge implied.

## Retained preceding reciprocal findings

**Employment reciprocal conceptual interface — 17 November 2026:** From [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59): Job should own positions/vacancies; Employment owns engagements and assignment; position reference is not employment evidence. This initial statement was proposed pending this review; JOB-02 and JOB-04 refine it, not retroactively approve it.

**Qualification trust and employment interoperability — 18 November 2026:** QUAL-06–08 owner-agreed; QUAL-09 accepted in principle. Job owns versioned requirements/alternatives; Qualification supplies qualified award/recognition comparisons; no automatic hiring, right-to-practise or eligibility assertion. See [Qualification](../qualification/capability-record.md). Exact interfaces in this document remain conceptual pending owner approval.
