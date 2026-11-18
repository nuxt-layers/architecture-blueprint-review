# **Capability Record**

## Capability Name:

`qualification` — Independent qualification schemes, recognised awarding scope, multi-pathway eligibility and authoritative individual award decisions.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

**Proposed — owner-approved creation and conceptual boundary (18 November 2026; COURSE-12).** This is the standard capability pro-forma supplemented by the agreed findings for a **later independent conceptual review**. No package, operational availability, live contract, implementation, CI acceptance or legal compliance is asserted.

## Purpose

Manage qualifications independently of individual courses: their definitions and versions, requirements across multiple pathways, issuer/centre recognition and delegation evidence, individual award cases and authoritative decisions, and qualification withdrawal, teach-out, correction and appeal. Support both legitimately locally decided awards and externally decided awards while preserving the actual awarding organisation's authority.

This domain is justified by five project-owner-confirmed essential needs:
1. Own qualification specifications independently of Course.
2. Evaluate multi-course, multi-assessment and recognition-of-prior-learning evidence.
3. Manage the lifecycle of awarding-body/approved-centre scope, delegated authority and restrictions.
4. Maintain authoritative qualification-award decisions independently of issued credentials.
5. Manage qualification withdrawal, teach-out, version transitions and award appeals independently of training completion.

**Boundary invariant:** A platform record of recognition or external award is not a unilateral grant of statutory, academic or professional authority. External awarding/accrediting organisations remain authoritative within their legitimate remit. Local award decisions are authoritative only within independently evidenced and currently effective issuing powers.

## Classification

**Domain candidate — creation and principle approved under COURSE-12**, not an automatically independent repository/service/deployment. Framework-neutral business contract with optional Nuxt presentation; detailed classification/public contract acceptance remains for Qualification's own review. Default deployment may be modular monolith, and shared contracts must not force a runtime dependency cycle.

## Dependencies

**Potential public contract relationships (not approved code/package imports):**
- [Course](../course/capability-record.md) supplies course identifiers, versioned curriculum/outcome requirements and course publication state. Qualification independently owns multi-pathway qualification requirements; no competing curriculum master.
- [Assessment](../assessment/capability-record.md) owns individual attempts, marking, moderation and assessment-level appeals; supplies versioned admissible result evidence.
- [Training](../training/capability-record.md) owns verified participation, competencies and programme completion; supplies attributable achievement evidence, without itself conferring formal qualifications.
- [Credentials](../credentials/capability-record.md) receives an authoritative qualification award decision and manages credential issuance, representation, verification, expiry, correction, replacement and revocation. Qualification retains the **underlying award record**, status and decision provenance.
- [Enrolment](../enrolment/capability-record.md) supplies approved learner context and applicable course versions where needed, not qualification-award eligibility as such.
- Identity/Authentication/Authorisation supply identity references, trusted caller, assurance and platform resource permissions. An IAM role does not confer external awarding powers.
- Legal Compliance, Privacy, Verification and Integrations supply effective legal restrictions, data rights, claim/issuer verification when within agreed remit, and provider-specific accreditation/registry/award evidence with provenance and uncertainty.
- Workflow coordinates approval and appeal processes; Qualification determines domain outcome. Audit accepts accountability evidence; Logging/Observability diagnostics; Clock effective time; Reporting approved facts; Notifications delivery.
- Publisher/Storage may produce certificates/documents; they do not own award decisions or independently establish credential validity.

All dependency edges must remain explicit, directed and acyclic; event subscribers are not implicit code dependencies.

## Optional integrations

Accreditation/qualification registers, external awarding bodies, government/professional regulators, recognised training/assessment centres, digital award registries and qualification frameworks through provider-neutral Integrations ports. External authority is verified by source, scheme, jurisdiction, scope, effective dates, current status and delegation chain. Do not infer power to award from technical access, an imported claim or organisational membership.

## Version

**No implementation/release version.** Conceptual immutable qualification-definition revision; awarding rule/recognition version and effective interval; stable award-case ID, individual award decision revision, authority/delegation evidence reference, applicable version, evidence IDs, decision time, appeal/correction chain and provenance.

## Availability

Distinct from local platform availability: qualifications may be draft, submitted for recognition, recognised, suspended, withdrawn, in teach-out or archived. Individual cases may be pending, incomplete, under review, approved/rejected, appealed, awarded, corrected, suspended, withdrawn or reinstated. Unknown/stale external recognition or delegated status must be shown explicitly and fail closed for new regulated award decisions requiring current verification. Historical validity and current authority are not equivalent.

## Capabilities offered

### Native qualification management

1. Create, revise, validate and govern qualification schemes, titles, levels, frameworks, award types, outcomes, modules, required credits, equivalence/transfer and recognition-of-prior-learning rules independently of any Course.
2. Model permitted achievement pathways: multiple course revisions, assessment results, Training achievements, directly assessed candidates, prior learning and externally verified evidence. Retain source references and versions; never duplicate source grades or learner activity histories.
3. Model scheme issuer and centre authorisation: awarding organisation, recognised scope, approved providers/centres, delegated powers, source proofs, start/end times, local restrictions, withdrawal and suspension. Distinguish external facts from locally governed decisions.
4. Open and evaluate individual qualification award cases, including prior-learning equivalence, completeness/validity, appeals/review, separation of duties, rule version and evidence integrity. Accept/reject/award only where the decision actor has actual authority.
5. For external-only awards, submit an application/evidence and consume the authoritative external award decision; distinguish received, verified, pending, rejected, unknown and disputed, without self-awarding.
6. Own authoritative *local* qualification awards and provenance, and verified references to *external* awards; manage corrections, appeals, review, withdrawal, reinstatement, source-specific status, and lawful history.
7. Handle qualification scheme retirement and teach-out: affected learners, eligibility deadlines, transition/equivalence, historical award preservation and safely blocked new awards where recognition is absent.
8. Publish safe committed changes through domain-owned durable outbox, expose scoped queries/exports, and reconcile duplicate/replayed provider events and uncertain statuses.

### Exclusions

No teaching/curriculum, enrolment, teaching attendance, exam delivery/marks, generic IAM/organisation registry, universal accreditation-law interpretation, credential signing/rendering/technical status service, provider SDK, generic workflow engine or ownership of unrelated licensing/membership decisions. Credentials may attest to those other domains via their own authoritative decisions; Qualification should not become universal award infrastructure for every claim type.

### Initial idealised public input/output notes

| Inbound source/surface | Purpose and failure semantics |
|---|---|
| Qualification author/policy authority: scheme draft, version, awarding rules, recognition or teach-out commands | Qualification validates scope, domain invariants, permitted governing authority, effective dates, expected revision and current policy; invalid/unauthorised requests reject atomically. |
| Course: frozen course/outcome reference | Check pathway matching against versioned Qualification rules; no learner membership inference. |
| Assessment and Training: source-attested results, achievements, completion and correction evidence | Validate source owner, original revision, authenticity, credit equivalence and finality; missing or disputed facts remain unresolved. |
| Learner/assessor/awarding officer: application, prior-learning evidence, credit transfer and appeal | Check assurance, applicant identity, evidence integrity, moderation, legal and segregation-of-duties policy. An application is not an award. |
| External accredited/awarding authority via Integrations/Verification: recognition, mandates, delegated approvals and actual external award decisions | Require source/provenance, effective intervals, scope and freshness; unknown or revoked authority blocks new award action; provider outage is not revocation. |
| Authorisation/Privacy/Legal Compliance/Clock/Workflow: effective policy, identity, rights, time, review outcome | Mandatory permission/policy uncertainty fails closed; process approvals alone are not awarding powers. |

| Outbound authority/surface | Authorised consumers and meaning |
|---|---|
| Versioned qualification definition, requirements, equivalence and recognition state | Course, Assessment, Training, prospect/catalogue, controlled external providers; qualification-source authoritative, but third-party recognition remains externally authoritative. |
| Award-case status and evidence-gaps/decision record | Subject, authorised awarding officers, Training/Assessment and legally permitted reviewers; distinguish pending, internally recommended, externally submitted, formally awarded and disputed. |
| Formal award record or verified external award-decision reference | Credentials and authorised subject/institution: unique award ID, issuer/delegation, actual decision source, qualification version, person reference, evidence/provenance, effective date and status; *not* a certificate or raw result. |
| Qualification/award change events and auditable exports | Credentials, Audit, Reporting, Notifications, relevant domain consumers: committed published/recognised/withdrawn/teach-out, award granted/corrected/appealed/revoked/reinstated with limited identifiers, versions and effective times. Subscriber replay/dedup expected; no exactly-once claim. |

**Interaction invariants:** Server-side authorisation; tenant/issuer scope; applicable versions, evidence/provenance, policy, correlation and idempotency; consistent historical records. A missing essential authority check cannot be replaced by a user's access grant. External connected source facts are never silently promoted into locally issued awards. Authoritative award change may require a separately committed Credentials status transition; monitor/reconcile the hand-off, never assume same-transaction atomicity.

## Configuration

Possible jurisdiction/scheme selection, issuer/centre roles and approval routing, acceptable pathway/rubric rules, equivalent credits, prior-learning evidence, transition/teach-out policy, external provider and authority freshness thresholds, privacy, retention and notifications. Configuration resolves declared settings; Qualification applies qualification-specific rules; external recognition and statutory floors cannot be changed by ordinary preferences.

## COURSE-12 — approved conceptual decision and deferred questions (18 November 2026)

**Owner approval:** Establish `qualification` as an independent **Domain candidate** because all five substantive native responsibilities above are essential. It owns qualification definitions and their independent lifecycle, cross-course/pathway award eligibility, issuer/centre/delegation governance, formal individual award decisions, qualification-specific appeals/withdrawal/teach-out. A separate generic `awarding` capability is **not** justified: awarding is native to Qualification. Maintain separation from [Credentials](../credentials/capability-record.md), whose purpose is evidence-backed issuance and credential status.

**Source-authority rule:** External accreditor owns accreditation; external awarding body owns actual external award; an evidenced, valid delegate may decide only within the permitted mandate. Local Qualification is authoritative for its *own authorised* decisions and for faithfully qualified references to external awards. Organisation/subject identity, authority provenance and provider status must be independently verified; IAM access and configuration do not create accreditation.

**Challenges/open for separate full conceptual review:**
- Legal qualifications and recognised levels vary by jurisdiction and issuer: authoritative registries and assurance/freshness requirements.
- Exact qualification and award states; teach-out transfers, historic amendments, retrospective revocation, provider insolvency, appeals and lawful retention.
- Multi-pathway credit/recognition-of-prior-learning equivalence and dispute review; qualifications with no Course or Training.
- Centre recognition/delegation scope, time-limits and withdrawal; safety and vulnerable learners.
- External-only, locally authorised, mixed and delegated awarding modes and reconciliation.
- Public input/output contract, provider-neutral integration, independent minimal consumer, GUI and acceptance criteria require the dedicated Qualification review, not this initial pro-forma.

**Initial conceptual presentation:** Qualification scheme catalogue/editor; recognition/centre/delegation dashboard and status history; awarding case queue; evidence review/equivalence matrix; authorised decision and appeal workspace; teach-out/withdrawal/transition view; issuer/learner status portal. Headless operations remain first class; host owns navigation. WCAG 2.2 AA, UK English/localisation/i18n, privacy and Theme Manager apply.

**Acceptance sketches (conceptual only):** Multi-course valid evidence + live authorised issuer → one attributable formal award; raw Assessment mark → no automatic qualification; invalid/expired delegate → block award; external award pending → no local award asserted; corrected Assessment evidence → pending award re-evaluation, not automatic revocation; expired course recognition → preserve historically valid award where applicable; withdrawn scheme → block new awards as required while retaining lawful teach-out/history; duplicate/late external callback → idempotent state/reconciliation; cross-tenant learner record → deny.

**Sign-off:** Creation and ownership direction approved as COURSE-12; **the independent Qualification capability review, detailed public contract and implementation acceptance remain pending**. No implementation repository change or local tests are authorised.

## Independent conceptual review — Qualification (18 November 2026)

**Status:** Proposed conceptual specification for owner review, grounded in owner-agreed COURSE-12; not an implemented API, accepted contract or verification of external awarding powers. Opening governing SHA `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`, blueprint SHA `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9`. [Review baseline](../../../reviews/qualification-review-baseline.md). Related draft PRs #60, #62, #63 and #64 are provisional.

### Authoritative domain objects and permissible decision modes

Qualification owns independently versioned **scheme definitions**, requirements and equivalence mappings; qualification revisions and their effective recognition/teach-out intervals; **award cases** and evidence references, admissibility judgements, requirement evaluations, formal **locally authorised** award decisions, appeal/reconsideration outcomes and immutable historical correction chains; and **verified assertions** about externally owned mandates/awards with source attribution. It does **not** own the legal entity, person identity, original marks, enrolment, training record, credential, or accreditor's register.

Distinguish four routes:
1. **Local issuer:** qualification-owner institution has independently evidenced, current authority in the applicable jurisdiction, qualification, award kind, subject cohort and effective period; only a separately authorised decision actor may award.
2. **Delegated centre:** the awarding body owns the scope and terms of delegation; an approved centre may make only the decisions delegated, subject to review, restrictions, expiry and any final awarding-body ratification. Recommendation/endorsement is not a formal award.
3. **External awarding body:** the platform submits an application/evidence; pending submission and an internal eligibility recommendation do not establish an award. The authoritative external decision is verified and referenced without inventing a local award.
4. **Direct assessment / recognition of prior learning / mixed pathway:** a qualification case may rely on authenticated external evidence, multiple courses or assessments, prior learning, credit transfer and direct tests; no Course, Training or Enrolment record is intrinsically mandatory if scheme rules permit an alternative.

Never conflate **scheme recognition** (authority to offer/award), **issuer mandate**, **centre authorisation**, **individual eligibility**, **formal individual decision**, **credential issuance** and **third-party verification**. Unknown mandate, disputed issuer identity, suspension or missing positive authority blocks *new* regulated formal decisions; provider downtime is represented as unknown, not as mandate revocation. Historical awards are re-evaluated under the legally applicable effective-time rules, not today's scheme status alone.

Scheme lifecycle: draft → submitted/under review → published or recognised (only where independently substantiated) → amended/suspended/teach-out/withdrawn/archived; published revisions remain immutable. A local catalogue listing is never itself recognition. Award case lifecycle: opened → evidence gathering → eligible/ineligible/needs review → recommendation → approved/rejected by proven empowered actor → awarded (or external decision pending/verified) → corrected/appealed/suspended/withdrawn/reinstated as warranted. Appeals must not overwrite the original decision and do not automatically reverse an award. Eligibility is recalculated against frozen rules and attributable source revisions; conflicting or overturned source evidence triggers review rather than an unqualified automatic rescission.

### Idealised public inbound interface

| Source and necessity | Information/command provided; owner and verification | Missing, stale, invalid or contradictory behaviour |
|---|---|---|
| Authorised scheme/issuer governors (required for native scheme changes) | Create/revise/publish/retire scheme; issuer, framework, levels, outcomes, credit thresholds, pathways, equivalence rules, scope, effective time, expected revision, accountable approval | Validate actor, invariants, policy and revision; reject unauthorised or conflicting publication atomically; do not mark recognition verified from self-entry |
| Identity/Authentication/Authorisation and legal/privacy context (required where applicable) | Trustworthy caller/subject/tenant, assurance, resource decision; applicable statutory conditions, disclosure/retention and decision-maker restrictions. Identity owns identity, Authorisation owns platform permission, external source owns awarding mandate | Missing/ambiguous required access, assurance, lawful basis or awarding mandate fails closed; no inherited tenant/group permission |
| Course (conditional per pathway) | Published immutable course/outcome version references and course-authoritative mapping facts; Course owns curriculum | Missing, withdrawn or incompatible revision = unresolved pathway; no invented pass/completion |
| Assessment (conditional per pathway) | Final/versioned moderated assessment result and status, issuer, rubric reference, appeal/correction status, provenance; Assessment owns marks | Provisional/disputed/retracted result cannot be treated as final eligible credit |
| Training (conditional per pathway) | Verified learner participation/competency/programme-completion facts and revisions; Training owns achievement | Absent only blocks pathways that require it; never infer accredited award from completion |
| Enrolment (conditional per scheme) | Attributable learner/cohort/admission and immutable course-version reference; Enrolment owns eligibility to participate, not qualification eligibility | Missing enrolment does not invalidate permitted external/direct pathways |
| Applicant/assessor/credit reviewer (conditional per pathway) | Identified application, prior-learning evidence, credit-transfer requests, consent/disclosure scope, case appeal, evidence references | Check provenance, consent, malware safety where relevant, duplicate claims, assurance and conflicts of interest; incomplete case remains pending |
| External accreditor, awarding body, registry or verified delegate via Integrations/Verification (required for externally controlled authority or decisions) | Signed/attributable recognition/delegation scope and restrictions, effective intervals, external case ID, decision, source status, observed-at freshness, revocation/correction | Source outage or stale proof = unknown; contradictory authoritative evidence = held for reconciliation; fail closed for new awards; do not fabricate status |
| Workflow, Configuration, Clock and responsible review authority (conditionally required) | Approved routing results, configured scheme choices, clock time and qualified domain approvals | Generic Workflow approval or tenant setting is not awarding power; required review unavailable = pending, not approved |

Each inbound surface is a **conceptual service port or externally validated command**, not a direct package dependency claim. No universal mandatory request DTO or coupling to provider SDKs.

### Idealised public outbound interface

| Output and consumer | Meaning, authority, status and disclosure |
|---|---|
| `getQualificationRevision` / `listQualifications`: Course, Training, Assessment, permitted catalogue | Immutable scheme ID/revision, permitted pathways, outcomes, credit/equivalence rules, recognition source/freshness, effective interval, teach-out/withdrawal state; Qualification owns local scheme content, *not* external accreditation |
| `getAuthorityScope` / `checkIssuingAuthority`: authorised operators, decision service and Credentials | Specific issuer/delegate, qualification revision, jurisdiction, permitted action, scope, expiry, verified source and result `valid / invalid / unknown / disputed`; not permission to infer unrelated authority |
| `evaluateEligibility`: award case actor/authorised learner | Rule revision, candidate reference, admissible evidence IDs and source revisions, satisfied/unsatisfied requirements, contradictions and `eligible / ineligible / incomplete / disputed`; **not** a formal award |
| `getAwardCase` / `getAwardDecision`: subject, mandated centre/issuer, reviewer, approved consumer | Case ID, privacy-scoped evidence summary, actor authority, provenance, decision source, revision/effective time, approval/finality, appeal/correction chain, external pending/verified status. Qualification owns local decisions; remote issuer retains external decisions |
| `getAuthoritativeAwardReference`: Credentials | Subject/award/scheme revision, actual issuing entity, validated mandate/delegation and source, formal decision ID/status/effective time, qualifications-specific restrictions and correction/withdrawal chain; may be **verified external reference** rather than locally issued award. A certificate has separate state |
| Committed events/outbox: Credentials, Audit, Reporting, Notifications, reconciler | `qualification.revisionPublished`, `qualification.recognitionChanged`, `qualification.teachOutChanged`, `qualification.awardDecisionRecorded`, `qualification.awardCorrected`, `qualification.awardStatusChanged`, `qualification.appealResolved`; scoped identifiers, revision, source, effective/observed times, correlation. Events describe committed owner facts, not delegated commands or guaranteed credential completion |
| Export/read models: entitled institution/subject, controlled external registries | Purpose- and jurisdiction-scoped history with revision, provenance, retention/disclosure policy and explicit completeness/freshness. No raw learner evidence in broadcast events |

**Commands:** `draftScheme`, `reviseScheme`, `publishScheme`, `changeRecognitionAssertion`, `changeTeachOut`, `openAwardCase`, `attachEvidenceReference`, `evaluateEligibility`, `recordRecommendation`, `submitExternalAwardApplication`, `decideLocalAward`, `recordVerifiedExternalDecision`, `requestAppeal`, `resolveAppeal`, `correctDecision`, `changeAwardStatus`. These names describe business capabilities only. Risky decisions require server-side authorisation, positive mandate and segregation of duties as applicable. Expected revisions prevent lost updates; replay of the same idempotency key/semantics returns the original result; conflicting replay rejects. Accepted, pending, completed and failed outcomes must be distinct; external submissions may remain uncertain and require status reconciliation before retry.

**Queries:** Scheme/version, mandate, case/eligibility, award/appeal and provenance-aware status with explicit permission, completeness, source freshness, as-of time and effective-time meaning. Query outputs cannot imply an external body has granted a decision when it has not.

**Events:** Publish *after* owned transaction commits using Qualification's durable outbox; relay through host-composed Message Queue; consumers independently deduplicate, tolerate replay/reordering, retrieve authoritative revisions as needed and reconcile independently. Credential issuance and award status must not claim atomic transactions across capabilities. An external callback is an untrusted input until verified and committed by Qualification; it is not automatically a Qualification event.

**Common conceptual context:** trustworthy tenant and issuing organisation, learner identity reference, actor/assurance, action and resource authorisation, qualification/award/case IDs with expected revisions, jurisdiction and effective/observed times from Clock, recognised authority source and delegation chain, applicable rule/policy revision, source evidence IDs/status, correlation/idempotency and scoped disclosure. No global DTO is mandated. Reject cross-tenant references and identifiers from unrelated identity or issuer scopes; legal holds and correction/erasure requests preserve necessary accountable history lawfully.

### Cross-capability direction and recovery

- [Course](../course/capability-record.md) **supplies** immutable curricula and outcomes; Qualification **supplies** scheme requirements and accepted course/equivalence mappings. Mapping decisions belong to Qualification, curriculum revisions to Course. Cooperation through host ports/event-derived views avoids circular import.
- [Assessment](../assessment/capability-record.md) **supplies** source-final moderated grades/results and corrections; Qualification **supplies** qualification-specific assessment requirement references and downstream evidence decisions. Assessment never awards a qualification; revised grades force controlled re-evaluation.
- [Training](../training/capability-record.md) **supplies** participation, achieved competencies and course completion; Qualification **supplies** versioned eligibility requirements and formal award status only to authorised consumers; independent completion remains authoritative in Training.
- [Enrolment](../enrolment/capability-record.md) **supplies** authorised participation/course revision references when a pathway requires them; Qualification may provide course-pathway restrictions but not admissions decisions.
- [Credentials](../credentials/capability-record.md) **consumes** formal authoritative award references and status changes; Credentials **supplies** credential issuance/status/reconciliation acknowledgement when requested; it cannot make or rescind the underlying qualification decision. A pending credential response does not undo the formal award.
- Verification/Integrations provide externally evidenced scope, authoritative awards and callbacks behind provider-neutral ports; Qualifications validates/qualifies these. Publisher and Storage produce/store representations, never confer awards. Audit is accountable independent evidence; Logging/Observability diagnostics; Reporting derived authorised views; Notifications delivery; Workflow approval choreography; Scheduler retry; Privacy/Legal Compliance qualified constraints. Do not infer a direct code edge from a reciprocal fact flow.

**Failure/recovery:** External network unavailable: preserve pending external submission and safely retry/reconcile via correlation; unknown cannot become rejected or approved without evidence. Source grade appealed: reopen eligibility review, retain immutable award decision and route appropriate correction/withdrawal through legally competent decision maker. Lost credential message: replay Qualification outbox, query current award and reconcile; no duplicate issuer assertion. Expired delegation: prohibit newly authorised actions while preserve historic evidence and route impacted pending cases for reassessment. Conflicting external sources: quarantine *claims* in review state, not silently overwrite; no fresh award. Qualifications cannot promise third-party registry uptime, perpetual recognition or universally valid awards.

### Security, governance, configuration and provider boundaries

Baseline OWASP ASVS 5.0 L2 with risk-based L3 controls for formal awards, delegated authority and high-value evidence; server decisions/step-up, two-person approval or separation of duties for suitably sensitive decisions, immutable actor and evidence provenance, request replay protection, scoped signing/credential handling, encrypted and minimised sensitive learner evidence, safe file-content screening, audit trails and controlled retention. Protect special-category or children's records by applicable consent/lawful basis, policy, safeguarding and purpose limitation; verify jurisdiction-specific qualification rules with competent authorities before claiming legal recognition.

Configuration may supply permitted scheme preferences, workflow routing, thresholds, acceptance policies, retention rules within legal floors, language/locale, provider endpoints/freshness requirements and time-zone presentation. It **cannot** create accreditation/awarding powers or bypass issuer restrictions; domain rules remain with Qualification. Distinguish legal duties (Legal Compliance), executable qualification policy (Qualification), general approved settings (Configuration), published documents (Publisher) and third-party contract limits. Provider-connected, native and mixed pathways remain possible without forcing proprietary provider identity or universal external connectivity; imported records carry source, revision, rights and reconciliation status.

### GUI and headless acceptance

Optional separable Nuxt presentation, or host screens over the headless contract. Host sidebar entry **Qualifications** → capability dashboard; authorised scheme catalogue and revision editor; authority/recognition/centre-delegation status board (with last-verified and unknown warnings); candidate case queue; evidence coverage and equivalence matrix; formal decision workspace with step-up/approval boundaries; external submission/reconciliation queue; appeals/corrections; withdrawal/teach-out and transition planner; learner's own status; tightly scoped credential hand-off status. Host owns route/menu composition and Theme Manager vocabulary; no private Qualification tables accessed by presentation. Support keyboard and screen reader flow, meaningful status, no solely colour-coded recognition, WCAG 2.2 AA, light/dark mode, responsive layouts, BCP 47/i18n and locale-aware Clock date/time. Hide restricted evidence and enforce permissions on the server even when controls are not rendered. Presentation can be disabled without disabling native APIs or rule checks. Conceptual minimal-consumer acceptance: independently compose business contract, and, if a Nuxt adapter is provided, one installation/one call/at most 50 lines capability-specific host integration under ADR-0012.

### Conceptual acceptance matrix

| Input | Expected behaviour and output | Deciding authority |
|---|---|---|
| Approved local issuer + valid scheme revision + verified evidence across two courses | Eligibility computed; independent, empowered decision creates one formal award reference, event and historical provenance; credential not presumed issued | Qualification, within verified issuer mandate |
| Direct assessment or prior-learning evidence without Course/Enrolment | Evaluate only if versioned pathway explicitly permits; accept case, no fabricated course completion | Qualification rules; Assessment/external sources for original evidence |
| Raw provisional mark, pending external decision or unverified accreditation assertion | Pending/incomplete/unknown, **no formal award** | Assessment/external body owns source; Qualification owns case |
| Revoked, expired or unknown centre delegation; privileged IAM role | Reject formal decision even for an otherwise permitted platform actor | External delegator and Qualification enforcement |
| Cross-tenant subject/evidence, unsupported award type, unsafe upload | Deny/reject with stable error code; no record leak and no issued award | Identity/Authorisation/Privacy and Qualification |
| Duplicate award request or replayed external decision notification | Same idempotent result or explicit conflict; reconcile rather than duplicate award | Qualification |
| Grade corrected or appealed after award | Flag impact, re-evaluate, retain history, authorised review determines corrective action; credential status reconciled separately | Assessment result authority; Qualification award authority; Credentials status |
| External awarding-body outage after submission | Report pending/unknown with source and last verification; no success claim; retry/status inquiry with correlation | External body owns decision; Qualification records process |
| Recognition withdrawn; legitimate teach-out allowed | Block outside-scope new awards; validate existing cases against effective deadlines, preserve historical decisions | Qualification under verified issuer/regulator conditions |
| Credentials delivery failure, delayed event or divergent status | Qualification award remains authoritative; replay committed event and reconcile independently | Qualification vs Credentials respectively |
| Public lookup or export | Only permitted scheme metadata or privacy-authorised redacted award facts with verified provenance/freshness | Qualification disclosure + Privacy policy |

### Decision register and review outcome

- **QUAL-01–05 — Agreed via COURSE-12:** Independent qualification specifications; multi-pathway equivalence and evidence; actual awarding-body and centre mandates; independent formal individual award decisions; qualification appeals, version retirement, withdrawal and teach-out.
- **QUAL-06 — Proposed refinement:** Separate scheme recognition, individual mandate, eligibility, decision, and credential state, with four authority modes and fail-closed uncertainty. Proposed for explicit owner sign-off.
- **QUAL-07 — Proposed refinement:** Preserve immutable decisions and conduct event-driven re-evaluation/correction rather than automatic revocation on upstream fact changes. Proposed for sign-off.
- **QUAL-08 — Proposed refinement:** Provider-neutral, independent headless operations and optional dashboard presentation; no universal awarding service. Proposed for sign-off.
- **QUAL-09 — Open decision:** Exact jurisdictional scheme taxonomy, formal appeal authority, delegation ratification thresholds, lawful retrospective effects and teach-out exception policy must be approved by scheme/legal owner before implementation.
- **QUAL-10 — Technical investigation:** Verify actual accreditor/register source APIs and evidentiary freshness, supported standards/formats, provider callback authenticity and effective-date rules per jurisdiction; no blanket regulatory compliance claim.
- **QUAL-11 — Implementation alignment/acceptance:** No `nuxt-layers/qualification` repository or root `CONTRACT.md` established at review opening. Future independent contract, published ports, threat model, immutable revisions, minimal consumer and CI/application evidence are outstanding.

**Conceptual judgement:** A dedicated Qualification *domain responsibility* is justified; this does not require a separate microservice, second universal Awarding capability or immediate implementation repository. Detailed contract refinements are proposed, **not owner-approved**, and merging this review requires latest-master consistency validation plus explicit approval.
