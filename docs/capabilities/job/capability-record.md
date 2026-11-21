# Capability Record — Job

**Capability Name:** `job` — employment **position definitions**, not execution jobs, approved vacancies or recruitment.  
**Status:** JOB-01–JOB-09 **owner-approved conceptual direction, 20 November 2026**, refined by owner's preference for a separate Recruitment Domain and proposed vacancy ownership there. Non-normative blueprint; no published contract, installed/operational implementation, security/compliance acceptance or permission implied.  
**Classification:** Domain candidate; independent packaging remains subject to capability classification and published contract.  
**Version / Availability:** Conceptual version unspecified; no accessible `nuxt-layers/job/CONTRACT.md` verified.  
**Opening evidence:** Governing `architecture-rules@b920ce0d8b361de000a6739a16123dbdc56df7a7`, blueprint `architecture-blueprint-review@6dac83a03da8704f7945ee1bc894f2248300445a`; [review PR #84](https://github.com/nuxt-layers/architecture-blueprint-review/pull/84), [baseline](../../../reviews/job-review-baseline.md). The governing catalogue still labels job ambiguous until separate governance adoption.


**Companion plain-English review:** [Published interface expectations, cooperating capabilities, Logging/Audit/Reporting, standards, permissive libraries and representative GUI](../../../reviews/job-public-contract-standards-and-gui.md). It is conceptual, not a verified implementation `CONTRACT.md`.

## Purpose, ownership and exclusions

Job owns a trustworthy, organisation-controlled, versioned **catalogue of position/post definitions**: stable position reference, owner/tenant, title and code, purpose/duties, job family, grade/classification and validated compensation-band *reference* where applicable, skills, essential/desirable qualification criteria and alternatives, work-mode/location references, validity, approvals, corrections and lifecycle provenance. Position records describe a type of work and its conditions; they do not themselves authorise staffing, recruitment or expenditure. An organisation may reuse one position definition for many openings or engagements.

**Explicit exclusions:** Recruitment owns **proposed** vacancy/requisition lifecycle, approved seat/capacity request, recruiting budget/authority evidence reference, advertising intent and listing states, applications, interviews, evaluation/selection and recruitment-stage offer recommendations (precise approval/offer ownership to review). Employment owns actual employer/worker engagement, accepted contractual terms, effective assignment/occupancy and termination. Publisher owns publication documents; Integrations owns provider transport; Qualification owns qualification schemes/awards and qualified comparisons; Verification owns purpose-limited attestations; Payroll owns wages; Accounting/finance owns ledger and relevant funding decisions; Scheduler owns background execution; Task owns assigned work; Process owns process definitions and Workflow execution, neither automatically owns applicant decisions.

**Boundary invariant:** a position may be approved with no vacancy, candidate or employee. A position revision cannot independently create/close a vacancy, fund a post, publish an advertisement, select a candidate, issue an offer, amend a contract or end an engagement. Conversely, an Employment engagement can legitimately exist without a Job reference where its own domain rules permit.

## Status, capabilities offered and native lifecycle

**Position lifecycle only:** draft → under review → approved/active → suspended/retired, plus rejected/withdrawn and attributable corrections/effective revisions. Historical editions remain traceable, with effective-time interpretation via Clock. Reject stale expected revisions and duplicated operations; perform server-side policy and tenancy checks. Preserve committed change evidence via a capability-owned durable outbox, and distinguish accepted requests from committed results.

Native services: create, validate, amend, review, approve, activate, suspend and retire a position; query current/as-of position and revision history; obtain authorised, frozen position requirements/alternatives; restricted exports; publish position-owned committed changes. **No Job-owned vacancies, openings, seat counts, occupancy projections, advertisements, application dossiers, interview pipelines or recruitment/Employment approval operations.**

## Idealised public inbound contract

| Source / provided information | Nature and invalid, absent or contradictory semantics |
|---|---|
| Authorised position administrator: create/revise/approve/suspend/retire position | Essential scoped command, actor/assurance/tenant, expected revision and idempotency key. Authorisation must decide server-side per action and resource; deny missing privilege, invalid scope and stale revision. |
| Identity, Authentication, Authorisation | Essential subject/group/tenant, session assurance and access decisions. Group membership does not prove legal employer, employment or permission to recruit. |
| Configuration, Clock and applicable Legal Compliance | Scoped taxonomy, authorised definition workflow, effective-time and legally constrained occupation terminology. Invalid essential controls hold the action; preferences do not override legal floors. |
| Qualification / professional registers | Conditional canonical scheme/award-type and recognition-reference information to express **position requirements**. Job does not import an applicant's verified qualification dossier or decide individual eligibility. |
| Employment / Recruitment consumers | Versioned position-reference queries, not commands granting those domains' rights; neither domain's assignment or applicant state becomes Job input or owned state. |
| Optional external HR position catalogue through Integrations | Provider-attributed position data/updates; explicit source authority, freshness, reconciliation, conflicting versions, withdrawal and unknown completion. Unconfirmed remote changes remain pending/unknown. |

## Idealised public outbound contract

| Surface / consumer | Authority and guarantee |
|---|---|
| `getPosition`, `listPositions`, `getPositionRevision` → authorised Employment, Recruitment, reporting and operators | Authoritative Job-owned definition and effective status, frozen revision and provenance. **No vacancy approval/quantity, publication, headcount, worker or candidate status.** |
| `getPositionRequirements` → Qualification/Recruitment authorised use | Versioned essential/desirable educational, professional and skill criteria, accepted alternatives and effective version. Does not assert an award, right to practise or hiring suitability. |
| `createOrRevisePosition`, `approvePosition`, `suspendPosition`, `retirePosition` → authorised caller | Result accepted/committed/held/conflict/rejected, resulting revision, reason code and correlation, not approval of recruitment or employment. |
| `position.created`, `position.revised`, `position.statusChanged` → authorised subscribers | Domain-owned committed facts from durable outbox with tenant/owner, event ID, revision, effective/recorded time and provenance; duplicates/out-of-order delivery expected. |
| Restricted position export → Reporting/Audit/management | Purpose- and scope-limited historic definitions, approvals and evidence references; no applicant or employee dossier. |

**Not exported:** `requestOpening`, `approveOpening`, `getOpening`, `listOpenings`, `changeOpeningState`, listing publish/withdraw/status commands, `opening.changed`, `listing.statusChanged`, recruitment decisions or Employment assignment updates. The earlier PR draft suggested these as Job surfaces; they are **superseded** by JOB-02/03 approval and Recruitment ownership direction.

Commands enforce revision and idempotency; queries label as-of time and completeness; events convey committed Job changes only and cannot grant authorisation. Use public contract values, not persistence/private/provider SDK types; do not impose one universal request object. Errors are stable codes/message keys. Every consumer independently checks tenant, scope, version and effective position standing rather than treating a received event as authorisation.

## Dependencies, optional integrations and reciprocal public interfaces

- **Essential:** host-composed server-side Identity/Authentication/Authorisation decisions, independent tenant ownership, Clock time semantics and capability-owned persistence/outbox. Provider-neutral interfaces, acyclic dependency graph, minimal host composition under accepted ADR-0012.
- **Recruitment (separate owner-approved Domain direction, proforma only):** consumes Job's versioned position definitions and criteria. **Proposed Recruitment authority:** approved requisitions/openings and capacity, vacancy state and adverts, applications, candidates' recruitment-specific evidence, interviews and selection case outcomes. Financial approval remains with its true decision owner; Recruitment records evidence and decision status. See [Recruitment proforma](../recruitment/capability-record.md). Recruitment may use Process/Workflow/Task/Scheduler to operate stages without delegating records or decisions to execution engines.
- **Employment:** consumes optional Job ID and effective position revision; independently owns actual engagements, individual contracted salary, assignments, start/end and headcount. It may serve authorised recruitment vacancy reconciliation but **does not update Job's records**. No Job↔Employment cyclic import.
- **Qualification / Verification:** supply authoritative schemes, recognition and attestations to qualified consumers; Job defines position requirements only. An application comparison and recruiting decision belong to Recruitment, with provenance and unknown semantics.
- **Publisher / Search / Integrations / Notifications:** Recruitment-owned listing intent is passed to Publisher for document publication and to Integrations for board/API transport; Search has derived indexes, Notifications communications. Job does not claim any channel is published/withdrawn.
- **Accounting/finance, Legal Compliance, Audit/Logging/Observability/Reporting:** Job only references relevant approved position grades; Recruitment seeks financing/advertising decisions and records source evidence; other capabilities retain their own authority, privacy and qualified legal obligations.

## Configuration, assurance, privacy, legal and GUI

Configuration owns scoped position taxonomies/templates/default approval settings; Job enforces valid revisions and decisions. Server authorisation applies to read/list/count/history/export and mutation; OWASP ASVS 5 L2 minimum, relevant L3 security-sensitive controls, tenant isolation, purpose limitation, protection of salary-grade metadata and attributable Audit events. Job does **not** collect CVs, protected-characteristic applicant data, interviews, medical information, employee confidential contractual facts or right-to-work evidence. Qualified local rules for professional role descriptions and pay-band references are conditional; no legal-compliance claim.

**Optional Job GUI:** host-sidebar **Positions** dashboard with role catalogue, revision/approval/status editor, classification and qualification requirement editor, restricted history/export. **No** opening approval/seat occupancy, vacancy posting, application, interview or offer management screens in Job. Those belong to the separate Recruitment GUI; Employment controls assignments/contracts. Headless first; host owns navigation and Theme Manager integration; WCAG 2.2 AA, BCP 47 and CLDR/ECMA-402 localisation apply.

## Conceptual acceptance scenarios (not executable tests)

| Input | Expected output and authoritative owner |
|---|---|
| Manager approves Software Engineer position | Job returns versioned approved role; **zero new vacancies or employees** |
| Recruitment requests frozen position revision for new requisition | Job supplies approved revision; Recruitment separately authorises/owns vacancy |
| Recruitment opening approved for three seats | Job remains unchanged; Recruitment owns openings/capacity and approval evidence |
| One selected applicant becomes engaged | Employment owns accepted agreement/assignment; Recruitment owns selection/handover; Job definition unchanged |
| Employee ends an assignment | Employment updates its facts; Recruitment reconciles any vacancy as independently authorised; Job unchanged |
| Qualification evidence missing for candidate | Job returns role requirement only; Recruitment/Qualification handles unknown comparison; no Job hiring judgement |
| Candidate application, advert publish, vacancy expiry or offer command submitted to Job | Explicit unsupported operation; no hidden delegation |
| Expired role revision or replayed update | Job rejects invalid reference/update or returns idempotent prior result |
| Cross-tenant position export | Denied without information disclosure |
| Recruitment, Employment, ATS and Workflow absent | Job still operates as a native, headless position catalogue |

## JOB-01–JOB-09 — owner-approved conceptual decisions (20 November 2026)

- **JOB-01 — Approved:** `job` is the employment **position-definition** Domain candidate; infrastructure background jobs belong to Scheduler. Separate implementation/package not yet approved.
- **JOB-02 — Approved:** `job` owns **positions only**. Vacancy/opening ownership is separate; following owner's preference, **Recruitment is the proposed owner**, to be validated in its dedicated conceptual review. This does **not** approve vacancy contracts or a new implementation.
- **JOB-03 — Approved, updated by latest owner direction:** Recruitment and candidate selection remain outside Job. Owner favours **Option A — an independent Recruitment Domain**, which may itself compose Process/Workflow/Task; workflow orchestration does not acquire applicant records or selection authority.
- **JOB-04 — Approved:** Employment remains sole authority for actual engagement, assignment and occupancy. Job publishes position definitions only; derived vacancy counts, if needed, belong to authorised Recruitment/Reporting projections and must qualify Employment evidence freshness.
- **JOB-05 — Approved:** Job owns versioned position qualification requirements; Qualification/Verification owns authoritative evidence/recognition; Recruitment owns applicant-specific assessment and hiring determination subject to legal and human controls.
- **JOB-06 — Approved, clarified:** Job position approval is not recruitment/vacancy funding or public advertising authorisation. Recruitment will define those approvals, independently evidenced by finance/governance owners; Job remains native without external ATS/Workflow/Scheduler.
- **JOB-07 — Approved, clarified:** Job may reference approved role grade/band definitions but not advertise pay or determine contract terms. Recruitment owns approved vacancy advertising information, Employment individual contractual terms, finance/Legal Compliance applicable constraints.
- **JOB-08 — Approved, clarified:** Job enforces revision/idempotency/tenant/provenance on position operations. Recruitment's future contract must distinguish requested/accepted/published/unknown/withdrawn listing status; remote acknowledgement is not confirmed publication.
- **JOB-09 — Approved, clarified:** Job has optional authorised **position-only** manager GUI and complete headless contract; Recruitment/Employment own their own screens, linked by the host; WCAG/i18n baselines apply.

**Historical refinement:** The original 19 November PR draft allocated vacancies, staffing approval, advertising and occupancy projections to Job. The owner subsequently chose position-only Job, and on 20 November preferred an independent Recruitment Domain for the remainder. This supersedes the earlier **proposed** Employment and Qualification reciprocal allocations where they implied Job vacancy authority; no existing approved Employment/Qualification source ownership is changed.

## Remaining substantive questions for Recruitment's dedicated review

1. Define requisition/opening/vacancy identity and whether seats/capacity are one per opening or many; distinguish standing workforce establishment versus authority to recruit and funding approval. Job owns neither.
2. Define internal/external/talent-pool hiring, speculative candidates, applicant dossiers, consent, evaluations, disagreements, appeals, offer and conditional-offer custody and protection.
3. Clarify offer authority and handover: Recruitment owns **pre-engagement selection and offer tracking provisionally**, Employment must own accepted contractual terms and final engagement activation. Acceptance does not prove commencement or right-to-work.
4. Reconcile recruitment capacity with Employment's source-owned, dated appointments; unknown or incomplete evidence must never become zero occupancy or automatic reopening.
5. Define Publisher/Integrations listing approval and remote status, jurisdictional equal-opportunity/pay transparency duties, accessible application process, data retention and audit.
6. Formalise provider-neutral independent public input/output contracts, configuration, permissions, event/outbox and GUI before any Recruitment implementation.

**Sign-off:** JOB-01–JOB-09 conceptual directions approved by owner; the conceptual **Recruitment** classification direction is favoured but its detailed vacancy/recruitment design and package/implementation acceptance are pending. Conceptual review approved for merge by the owner on 20 November 2026, subject to the required current-master architectural/Git and branch-policy checks. Implementation, Recruitment's independent contract and runtime acceptance remain deferred.


## Recruitment reciprocal contract proposal — 20 November 2026

**Status: Proposed in [Recruitment draft PR #99](https://github.com/nuxt-layers/architecture-blueprint-review/pull/99), not owner-approved or implemented.** Job owns permitted frozen position revisions; Recruitment owns requisitions, openings, adverts, applications and selection, with explicit review on Job changes. Neither depends on the other for native operation. Cooperation uses published contracts/host ports, without private state or mandatory cyclic imports. [Recruitment record](../recruitment/capability-record.md).


## Legal Compliance reciprocal conceptual contract — 19 November 2026 (draft PR #85)

**Status: Legal Compliance LC-01–LC-13 and boundary decisions owner-approved; implementation not verified.** [Legal Compliance dedicated conceptual contract](../legal_compliance/capability-record.md) proposes scoped, time/version/source-qualified legal applicability, mandatory restrictions, holds, deadlines and uncertainty. **job** supplies only authoritative, minimally necessary resource/service/activity/tenant context and completion/refusal evidence through documented public contracts; Legal Compliance does not take ownership of job's records, business decisions or enforcement. Statutory interpretation is not personal Authorisation, Privacy's specialist consent/rights rules, or proof of regulator acceptance. Missing or conflicting mandatory legal qualification holds only the affected unsafe action; authorised source owners report applied decision version and partial/failed enforcement. Cross-capability cooperation is host-composed, not an implicit direct package dependency. Existing neighbouring decisions and active PR proposals retain their own status.
