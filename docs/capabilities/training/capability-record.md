# Capability Record — Training

**Capability Name:** `training` — learner participation, learning evidence, achieved competencies and programme completion.
**Classification:** **Domain capability candidate** (governing catalogue: “Verified training participation, competencies and completion records”).
**Status:** **Owner-approved conceptual decisions TRAIN-01–08; PR integration and final consistency review pending**. Existing Course COURSE-08–12 boundaries are also owner-agreed. Available, Installed, Configured, Operational, Enabled and Authorised **not evidenced**. No implementation API, compliance or acceptance is claimed.
**Opening baseline:** governing `architecture-rules/master` `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint `architecture-blueprint-review/master` `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9` (18 November 2026). [Review protocol](../../review-protocol.md); [opening evidence](../../../reviews/training-review-baseline.md).
**Evidence:** governing `docs/catalogue.md`, `docs/architecture.md`, `docs/capability-standard.md`, accepted ADR-0001/0002/0008/0009/0012/0016; owner-approved Course COURSE-08–12 in [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Qualification](../qualification/capability-record.md). These links indicate conceptual sources, not live published APIs.

## Purpose and independent justification

Provide independent, reliable evidence of **what learning a person actually undertook, what competencies were demonstrated and which learning programme requirements were completed**, including blended, supervised, self-directed, offline and externally delivered training. Preserve learner progress and history after enrolment/course revisions or external-provider changes. Training's own evidence verification, review/correction, recognition and completion lifecycles are distinct from Course design, Enrolment admission, Assessment marking and Qualification awarding. Headless operation must work with no optional learning management provider or GUI.

## Authoritative ownership and exclusions

Training owns tenant/learner-scoped learning evidence records, learning-participation observations and verified attendance for learning activities, attributable instructor/supervisor attestations, training activity progress, evidence-to-learning-outcome mapping, competency-achievement determinations within the **training programme scope**, and independently authorised programme-completion decisions, revisions, disputes, correction and lawful provenance/history. Distinguish submitted/unverified claims from validated observations and finally accepted achievements. Training preserves source references, source-effective versions, basis, verification status, decision maker and time.

Training **does not own** Course curricula, learning outcomes or completion-rule definitions; Enrolment applications, cohort allocation or standing; Assessment instruments, attempted answers, assessment grades, moderation or assessment appeals; Qualification scheme rules, qualification eligibility adjudication or authorised awards; Credentials issuance/verification/revocation; Identity/Profile information; timetables, room/event bookings, workplace working time/payable hours (Time & Attendance), original content/file bytes, safety checks, financial charges or legal authority. It may refer to each through its public contract.

**Boundary caution:** a course-completion decision is neither evidence of a formal qualification award nor permission to issue an externally recognised certificate. A competency within training scope is not a professional licence. Conversely training evidence can legitimately inform Qualification without compulsory course enrolment where recognised-prior-learning rules permit.

## Information model, native services and lifecycle

- **Training record:** learner opaque identity, tenant and authorised resource owner, optional enrolment/cohort reference, fixed course/programme revision and rule set, effective range, current status/revision and source identifiers. No course snapshot may silently replace Course authority.
- **Activity observation:** particular learning activity/session, participation interval, actual attendance/engagement assertion, provider/device/instructor provenance and evidence reference; `submitted → under-review → verified / rejected / disputed → corrected / superseded`. Record a missing observation as **unknown**, not as non-attendance.
- **Evidence item:** referenced source, permissioned evidence attributes, claimed competencies/outcomes, verification method, source time, receipt time, validity and restrictions; evidence may be revoked, disputed or superseded without deleting the historical reference.
- **Achieved learning outcome/competency:** explicit mapping to relevant Course revision/standard, accepted supporting evidence, evaluator and rule revision; `not-evaluated → pending → achieved / not-demonstrated / inconclusive → reviewed / superseded`. Do not infer achieved from enrolment or mere attendance if criteria require demonstration.
- **Programme completion:** assessment of all applicable frozen criteria with supporting outcome/evidence references, exemptions, explicit reviewer or approved rule engine, reason and effective date; `in-progress → evidence-pending → eligible-for-decision → completed / incomplete / disputed → corrected / withdrawn / superseded`. **Completion is a Training decision, not an assessment mark or qualification award.**
- **Operational services:** register training activity, ingest/verify participation, accept evidence, review/attest achievements, calculate a non-authoritative progress projection, make/approve completion decision, dispute/correct findings, read/export authorised history, reconcile external evidence. Explicit negative/unknown states avoid false certainty.
- No blanket retroactive edit: preserve original facts, correction reason, immutable references and previously communicated decision; affected downstream owners get a changed-evidence notification and independently decide their own status. Training must not revoke a Qualification award or issued Credential.
- On unavailable mandatory evidence, rules, access decision or required verification: fail closed for **new authoritative achievements/completions** while allowing permitted historical reads and pending ingestion; distinguish provider unavailable, unverifiable, disputed and stale. Never relabel provisional evidence as verified.

## Dependencies and public information received — idealised inbound interfaces

All surfaces below are **proposed business contracts**, not implementation signatures. The host wires public ports without cycles; requiredness varies by operation.

| Source / authority | Facts or command received and purpose | Requiredness, validation and absence semantics |
|---|---|---|
| Course (curriculum authority) | Immutable course/programme revision, learning outcomes, prerequisite/completion conditions, attendance minima and assessment references | **Required for course-defined completion**; match exact revision, validity and effective period; withdrawn/unavailable or conflicting revision → pending/unknown, never substitute newest revision |
| Enrolment (admission/participation authority) | Learner standing, eligible cohort allocation, authorised participation scope and effective course revision | **Conditional** for enrolment-governed training; not required for independently authorised prior-learning evidence; suspended/withdrawn/ineligible → block applicable activity/decision and preserve existing history |
| Assessment (assessment authority) | Final or appropriately provisional result, rubric/outcome links, appeal/moderation status, result revision, effective dates and provenance | **Required when completion requires assessment**; provisional, disputed, stale or withdrawn grades cannot become final marks inside Training; reassessment triggers fresh training evaluation |
| Instructor, supervisor or learner | Signed/attributable participation observation, learning work evidence, attestation or correction request | **Conditional** to activity; trusted caller, permitted role, time overlap, evidence integrity, source confirmation and conflict checks; self-attestation not automatically verified |
| Integrations / external LMS, skills provider | Provider-scoped events/evidence and evidence status, original references, webhook provenance and sync watermark | **Optional/conditional**; verify trusted binding, agreement, source authority, signatures, freshness and replay; missing external verification → pending/unknown |
| Identity, Authentication, Authorisation | Opaque subject and owner identifiers, caller/assurance and resource-scoped permission decision | **Required on protected actions**; missing or invalid subject, expired session or unknown permission → deny |
| Privacy / Legal Compliance / Configuration / Clock | Applicable consent/disclosure/retention/legal-hold constraints, authorised organisation policy and effective temporal interpretation | **Required where applicable**; legal/security floors not weakened by preferences; missing required policy → deny or defer |
| Authorised human/automated decision request | Activity/evidence submission, verify/reject, map achievement, decide completion, review/correct/dispute with expected revision and reason | **Required for mutations**; validate source authority, domain scope, idempotency, consistency, references and decision permissions |

Other optional public cooperation: Event/Booking for learning-session schedule and allocated place (not proof of attendance); Publisher/Media/Storage for course materials and evidential file references; Verification for trusted attestations; Workflow for configured multi-stage review; Scheduler for due evaluations; Notifications for delivery only; Audit for accountable custody; Search/Reporting for derived views. No blanket mandatory dependency is implied by listing a neighbour.

## Idealised public outputs and consumer guarantees

| Output (authoritative owner) | Authorised consumers and precise permitted conclusion |
|---|---|
| Training record / activity-progress query (**Training**) | Learner, instructor, programme administrator and permitted reporting/Enrolment consumers: **as-of** status and verified versus asserted participation; progress is explicitly a projection, **not** a completion or enrolment decision |
| Verified participation/attendance finding (**Training**) | Enrolment, Course delivery reporting, qualification evidence intake where relevant: source-bound verified actual learning activity for one subject, not work hours, session reservation or an assessment pass |
| Outcome/competency achievement finding (**Training**) | Learner, authorised Qualification and development records: mapping, verified evidence set, evaluation authority, relevant course/standard revision and effective time; no universal occupational licence implied |
| Programme completion decision (**Training**) | Enrolment, Qualification, Credentials (only for permitted non-qualification claims), Reporting: completed/incomplete/pending/withdrawn with explicit criteria and evidence revisions; **not** award, certificate or credential issuance authority |
| Correction, dispute and history (**Training**) | Subject, reviewers, Compliance/Audit, Qualification: initial and successor findings, reasons, supersession, lawful retention and effective versus recorded time; historical query never rewritten silently |
| Authorised evidence reference / export (**Training**, source still external where applicable) | Qualification, learner portability/reporting: minimum needed claims, integrity, freshness, access limits and source provenance, not an unrestricted transfer of sensitive materials |
| Domain event from committed Training change (**Training**) | Message Queue/qualified subscribers: `TrainingEvidenceRecorded`, `TrainingParticipationVerified`, `TrainingAchievementDetermined`, `TrainingCompletionDetermined`, `TrainingFindingDisputed`, `TrainingFindingCorrected` / `TrainingCompletionWithdrawn`; events notify **changed source facts** only and never instruct downstream to confer awards |

Every output carries tenant/owner scope, opaque learner and resource references, domain revision, governing criteria/source versions, effective and recorded/as-of timestamps, authority and evidence provenance, verification/finality state, limited disclosure classifications and explicit unknown/stale/completeness indicators. No unauthorised historical or cross-tenant disclosure. Source guarantee: Training attests its own verification/decisions, not the continuing accuracy of unverified external evidence or outcomes belonging to other owners.

## Commands, queries, events and shared invariants

**Commands** (conceptual): `recordParticipation`, `submitEvidence`, `verifyEvidence`, `determineAchievement`, `determineCompletion`, `disputeFinding`, `correctFinding`, `withdrawCompletion`, `reconcileProviderEvidence`. Each validates caller authority, resource context, course/criteria revision, expected record revision, duplicate request key, source/evidence provenance and scope. Return accepted/pending/completed/rejected/indeterminate with stable domain reasons and authoritative record revision; acceptance of a command is not evidence of a successful completion. A retry with matching idempotency key and identical meaning returns the original result; conflicting reuse is rejected.

**Queries:** subject progress, verified observations, evidence/achievement matrix, completion certificate **status (not the credential document)**, history and restricted evidence export; enforce learner/assessor/employer/issuer/tenant scopes separately, paginate and declare completeness, effective/as-of time, freshness and provenance. Bulk and analytic reads never bypass policy.

**Events:** produce only after committed authorised state transitions through Training-owned durable outbox when persistence is required under accepted ADR-0012; transport via Message Queue or configured port at-least-once with ordering/replay/duplicate tolerance, safe schemas and idempotent subscribers. An inbound event is neither a command nor an authorisation. No exactly-once distributed delivery guarantee.

**Cross-cutting invariants:** immutable course/assessment source revision pointers, recorded-versus-effective time through Clock, origin/correlation and idempotency, subject/tenant isolation, least-privilege role and assurance, explicit adjudicator/provenance, legally constrained retention and deletion, status reversibility via auditable correction not mutation of history. Do not require a universal request object. Host supplies persistence/provider ports; Training owns its state/schema/migrations, never another capability's private table. Any direct Nuxt extension and contract edges must remain explicit and acyclic; host composition stays within accepted ADR-0012 budget.

## Optional integrations, configuration, privacy and security

**Native baseline:** manual instructor/supervisor verification and authorised programme-completion processing, without a third-party LMS, qualification service or credential issuer. Enrolment and Assessment are conditional by programme criteria; a free-standing training achievement is permissible if organisation policy authorises it and its claims are narrowly scoped. No optional provider may become a hidden requirement.

**External providers:** provider-neutral LMS/attendance/skills evidence port, binding/tenant approval, permissions and assurance, data-flow agreement, provenance/signature, revision mapping, duplicate handling, loss-of-service status, import/export, repair/reconciliation and source withdrawal. Import alone does not confer verified status. Explicit source of truth, conflict resolution, version and revocation precedence required before production adoption.

**Configuration:** accepted evidence types, attestor roles, competence thresholds only insofar as allowed by frozen Course requirements, permitted verification methods, review steps and appeals, provider trust, attendance policy, sensitive-data retention, notifications, locale and disclosure. Configuration cannot waive mandatory law/security, override a Course revision retroactively, grant awarding authority or conceal an appeal.

**Security/privacy/compliance:** OWASP ASVS 5 Level 2 minimum; heightened controls for sensitive outcomes/privileged corrections as indicated by threat model; WCAG 2.2 AA; BCP 47/CLDR locale and Theme Manager vocabulary. Protect children/vulnerable learners, disability/accommodation and sensitive evaluation data with purpose-specific minimisation; instructor privacy and subject access/rectification requests; configurable lawful retention, legal holds and secure deletion. Classify original evidence and scans through Content Security before trusted use; quarantine/blocked uploads never count as verified. Separate server-side Authorisation from training decision competence. Audit significant decisions with minimised provenance; Logging/Observability contain technical diagnostics not learner transcripts. Applicability of education, employment, safeguarding and UK GDPR duties requires Legal Compliance assessment by jurisdiction and effective date, not a claimed blanket certification.

## Cross-capability interface directions and reciprocal notes

| Neighbour | Needed by Training → supplied back | Authority / dependency |
|---|---|---|
| [Course](../course/capability-record.md) | Frozen outcomes/rules → achievement and completion evidence | Course definitions; Training learner facts; conceptual contract edge Training → Course |
| [Enrolment](../enrolment/capability-record.md) | Eligibility/cohort/standing → progress, presence, completion notice | Enrolment admission; Training evidence; conditional read port, no direct reciprocal package dependency |
| [Assessment](../assessment/capability-record.md) | Final versioned assessment results → derived outcome/competence and completion status | Assessment marks; Training achievement; conditional read/event port; avoid direct reverse import |
| [Qualification](../qualification/capability-record.md) | Qualification may read permitted Training evidence → Qualification separately adjudicates awards | Qualification is consumer; never Training dependency for normal learning lifecycle |
| [Credentials](../credentials/capability-record.md) | May read completed training facts for authorised claim type → issues/manages credentials only on appropriate issuer authority | Credentials consumer; Training never issues or revokes |
| [Audit](../audit/capability-record.md) | Training offers minimised committed evidence → Audit protects evidential custody | Audit never changes completion decision |
| [Time & Attendance](../time-attendance/capability-record.md) | Independent workplace working-time evidence (only when separately permitted) ↔ learning evidence with explicit activity mapping | Time & Attendance owns worked hours; Training owns learning participation; no automatic inference in either direction |

**Graph policy:** these arrows express business information flows, not necessarily compile-time imports. Use host-supplied provider ports or event subscriptions where a reciprocal consumption would otherwise create a cycle. No direct implementation dependency from Qualification/Credentials/Assessment back to Training may silently acquire Training private storage.

## Presentation / GUI and headless integration

Optional separable Nuxt presentation: sidebar **Training** → permission-sensitive dashboard (my learning, instructor queue, administrator reports); learner progress/attendance and evidence submission; instructor participation capture/verification, outcome mapping and completion review; administrator correction/dispute workflow, provider reconciliation and scoped exports; history/source provenance, outstanding verification and stale-source indicators. Qualifications and issued credentials are **linked status views** served by their own contracts, never editable under Training. The host owns menu placement, routes, branding and selected capability wiring. No Training GUI is required for the headless public contract. Semantic form controls, keyboard review, screen-reader descriptions of verification status, responsive layouts, accessible correction mechanisms, internationalisation, Theme Manager semantic tokens and accessible status independent of colour are required.

## Conceptual acceptance scenarios (not executable tests)

| Input / situation | Expected behaviour and output | Authority |
|---|---|---|
| Legitimate supervised learning, fixed Course revision and authorised instructor | Verified learning observation and attributable outcome evidence; separate completion decision only if criteria met | Training; Course defines criteria |
| Course required graded examination, Assessment result pending appeal | Completion is pending/indeterminate, never inferred from attendance or an unfinalised mark | Assessment grade; Training completion |
| Valid final Assessment evidence plus full learning requirement satisfaction | Evidence mapped to frozen outcomes; authorised `completed` decision with provenance/version | Training completion |
| Eligible learner transferred to new Course revision | Explicit authorised mapping/gap review; original source revision retained, no silent progress carry-over | Enrolment transfer; Course rules; Training mapped achievement |
| Recognition of prior learning without Enrolment | Accept narrowly scoped evidence where policy permits; Training may determine competencies; no Qualification award or credential automatically | Training findings; Qualification award |
| Valid training completion sent to Qualification | Only evidence is offered; Qualification separately checks pathway, issuer authority, appeal and award status | Qualification |
| Learner attempts to certify their own competency without permitted verification | Unverified claim remains pending/rejected; cannot become achieved | Training |
| Caller requests other tenant's private transcript | Denied; no data leakage through list, export, event or error | Authorisation and Training isolation |
| Same external participation event delivered repeatedly | One logical source observation, idempotent result, no double-counted attendance | Training |
| External LMS is unavailable, signature invalid or late contradictory data arrives | Pending/unknown or dispute; original fact preserved, no false completed assertion; recovery reconciliation with audit trail | Training / provider |
| Assessment mark corrected after Training completion | Mark remains Assessment-owned; Training reviews dependent completion with superseding decision, downstream Qualification/Credentials notified but not automatically altered | Assessment, Training, downstream owners |
| Course withdrawn or provider trust expired after historically valid completion | Preserve lawful history and original versions; reassess only under explicit applicable policy, no silent retroactive cancellation | Course, Training |
| Request to issue accredited qualification or employment timesheet | Return unsupported/forward to proper capability, without pretending Training has the power | Qualification / Time & Attendance |

## Findings and owner decision register

- **Established (governing):** Domain responsibility named in governing catalogue; accepted public contract, acyclic dependencies, independent state, host composition, server authorisation and presentation/security/privacy standards.
- **Owner-agreed (carried):** COURSE-08 Assessment marks distinct from Training verified outcomes; COURSE-09 Enrolment admissions distinct from actual learning participation; COURSE-10 training completion distinct from formal awards/credentials; COURSE-11 historical evidence/migration integrity; COURSE-12 Qualification independently owns authoritative awards.
- **TRAIN-01 — Owner-approved (18 November 2026):** training evidence and verified learning attendance have one Training lifecycle; workplace hours remain Time & Attendance.
- **TRAIN-02 — Owner-approved (18 November 2026):** competency and programme-completion decisions are distinct, attributable, revision-bound and correctable without overwriting assessment marks.
- **TRAIN-03 — Owner-approved (18 November 2026):** accept external/self-supplied evidence as provisional until required verification; outages mean unknown/pending, not success.
- **TRAIN-04 — Owner-approved (18 November 2026):** support native headless learning evidence without mandatory Enrolment, Assessment or third-party LMS when programme policy allows.
- **TRAIN-05 — Owner-approved (18 November 2026):** source-event and completion revision changes trigger downstream reassessment, not automatic credential/qualification mutation.
- **TRAIN-06 — Owner-approved (18 November 2026):** optional learner/instructor/admin GUI and scoped disclosure.
- **TRAIN-07 — Owner-approved (18 November 2026):** Training also verifies competencies demonstrated outside formal courses, including workplace and independent learning, where a defined/versioned competency standard, sufficient evidence and an authorised evaluator exist. This does not grant professional licensure or a Qualification award.
- **TRAIN-08 — Owner-approved (18 November 2026):** Approved, narrowly scoped automation may make auditable corrections only for objectively verifiable errors under deterministic evidence/policy rules. Disputed, judgement-dependent or consequential competency and completion decisions require authorised human adjudication. Original and successor evidence remain traceable.
- **Implementation alignment:** publication of root `CONTRACT.md`, exact commands/queries/events, provider and schema obligations, access matrix, datastore/outbox, minimal host integration, threat model, revisions and migrations await separate implementation work.
- **Acceptance:** no implementation runtime or CI acceptance verified; the scenarios above are design acceptance criteria only.
- **Conceptual sign-off:** TRAIN-01–08 are all owner-approved on 18 November 2026. Full conceptual review closure remains subject to latest-master architectural and technical consistency validation and explicit merge approval.

## Original Course reciprocal findings retained

### Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)
**Status: Proposed at inception, Course review PR #56.** Course defines versioned intended learning outcomes, completion criteria and assessment requirement references; Training owns verified learner attendance, competency evidence, achievement and completion records. A course revision or external provider assertion is never itself proof of individual achievement. Training must evaluate against the applicable immutable course revision and preserve provenance even when later course versions differ.

### Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)
**Owner-agreed:** COURSE-08 Assessment owns instruments/attempts/marks/results/appeals; Training owns verified learner achievement. COURSE-09 Training owns actual participation/attendance, not session reservations. COURSE-10 programme completion does not automatically confer formal award or verifiable credential. COURSE-11 Training retains lawful history and course-version migration evidence.

### COURSE-12 — Qualification authority reciprocal note (18 November 2026)
**Owner-approved:** Qualification adjudicates qualification eligibility and awards; Training owns learning participation, verified competencies and programme completion, supplied as provenance-rich evidence. An award need not involve Training; neither party silently reowns the other's lifecycle.


## TRAIN-07/08 approval and explicit Audit/Logging public-contract boundary (18 November 2026)

**Owner-approved conceptual decisions:** TRAIN-07 permits verified competencies outside formal courses when a defined, versioned competency standard, sufficient evidence and authorised evaluator exist; no qualification or professional licence follows automatically. TRAIN-08 permits narrowly scoped and auditable *deterministic* corrections with approved rules; human adjudication remains mandatory for disputed, judgement-dependent or consequential competency/completion decisions. These are approved conceptual choices, not implemented operations.

### Public inputs to Training from Audit and Logging

| Source/public surface | Input meaning | Validation and absence behaviour |
|---|---|---|
| **Audit — Evidence Intake response** | Evidence receipt ID, accepted/pending/rejected/uncertain, validation reason and proof/reference; associated Training event and source revision | Match tenant, event identity, correlation and expected status. Audit acceptance acknowledges custody only, **not** the correctness or completion of a Training decision. For mandatory evidence, ensure durable producer-owned outbox/capture and explicit delivery/reconciliation assurance; if mandatory capture cannot be secured, high-risk finalisation fails closed or follows an expressly approved recoverable pending arrangement. |
| **Audit — Evidence Query and Integrity/Completeness response** | Authorised timeline or evidence reference, integrity verified/failed/incomplete/unknown, coverage gap, verified-as-of and disclosure limits | Training may link a permitted review to accepted Audit evidence. Incomplete or unknown proof is never silently labelled verified; Audit evidence cannot override Training's source record. |
| **Logging — Diagnostic Write response/Health** | Accepted/dropped/rejected/unknown or sink-unavailable status, correlation reference and scoped health signal where supported | Operational feedback only. Optional Logging failure must not independently invalidate or confirm committed Training state; record degradation through separate observability/operator alerting. Logging acknowledgement is not Audit receipt. |

### Public outputs from Training to Audit and Logging

| Training output → consumer public intake | Minimum meaning and guarantees |
|---|---|
| **Training → Audit: defined evidence event** | Versioned event family and retention/sensitivity category for attendance verification, evidence approval/rejection, competency determination, programme completion, automated or manual correction, dispute/review, privileged export and material access/security decisions. Include opaque tenant/resource/learner references, actor/service and decision authority, result, original/corrected revision, source/evidence IDs, effective/recorded times, reason category, correlation and idempotent source-event identity. Classify attempts versus committed outcomes; omit raw educational submissions, medical/accommodation details, secrets and unrestricted identifiers. Produce committed-state evidence from Training-owned durable outbox; relevant denied attempts require separate safe security-event capture. Audit owns receipt, custody, integrity, review and disclosure, not Training's result. |
| **Training → Logging: bounded structured diagnostic** | Event code, severity, operation, outcome category, safe dependency/provider label, retry/latency/error class, queue/outbox lag and permitted opaque tenant/correlation reference. Exclude full learner transcripts, grades, raw training evidence, access tokens, private evaluator notes and sensitive free-text. Logging owns sink delivery/redaction/retention and technical access; source Training owns what happened and domain state. |

**Failure separation:** Training business outcome, Audit custody/completeness and Logging diagnostic delivery are three **different statuses**. Test Audit available/Logging down, Logging available/Audit down, both down, replay, evidence correction after completion, forbidden cross-tenant query, and revoked authorisation. No direct bidirectional package import or private datastore access; compose ports and subscribe to events via the host. The full Audit contract is proposed and Logging's independent full review is still incomplete, so precise implemented API shapes remain unverified.

### Training's idealised published contract — service catalogue

**Inbound commands (caller → Training):** register training activity/context; record learning participation; submit learning/competency evidence; verify or reject evidence; determine competency against named criteria/version; determine programme completion; challenge/dispute, correct or supersede findings; reconcile provider observations; request authorised export. Each returns status, reason, record/reference revision, correlation/idempotency, permissions failure or pending/unknown outcome as appropriate. The caller needs verified identity and authority; commands never authorise themselves.

**Inbound factual/evidence ports (source → Training):** Course frozen outcomes/criteria, Enrolment standing when applicable, Assessment final versioned results when required, competent evaluator/instructor attestation, authorised external provider or Verification trust evidence, and applicable Configuration/Clock/Privacy/Legal Compliance/IAM constraints. Unavailable mandatory data yields denied/pending/unknown, not invented verified results.

**Outbound queries (Training → permitted consumer):** participation and evidence status; achieved competencies with standard/version and decision provenance; programme progress (labelled non-final); programme completion decision; historical corrections/disputes; restricted evidence reference/export; freshness, source authority, completeness and as-of-time in every view.

**Outbound committed events (Training → qualified subscriber):** EvidenceRecorded, ParticipationVerified, AchievementDetermined, CompletionDetermined, FindingDisputed, FindingCorrected and CompletionWithdrawn with source-event identity, version and privacy scope. Consumers may re-evaluate their own authoritative decisions; the event itself cannot award a Qualification or issue/revoke a Credential. Audit evidence and Logging diagnostics remain separate public interfaces, above.

**Implementation/publishing gap:** these are agreed/proposed **logical business surfaces**, not a verified root `CONTRACT.md`, TypeScript exports, endpoint names, package availability or CI-tested behaviour. Exact typed schemas, delivery/acknowledgement methods, access matrix, producer outbox guarantees and minimal-host acceptance require implementation alignment.


## Owner approval confirmation — TRAIN-01–06 (18 November 2026)

All six proposed definitions were explicitly approved by the owner on 18 November 2026 without alteration. TRAIN-01 learning participation versus work-time ownership; TRAIN-02 distinct evidence-backed competency/completion decisions; TRAIN-03 verify external and self-supplied evidence; TRAIN-04 conditional independence and native headless operation; TRAIN-05 downstream re-evaluation without automatic qualification/credential mutation; TRAIN-06 optional GUI. TRAIN-07–08 were already owner-approved. This approval does not assert publication of implementation contracts or discharge mandatory PR technical/architectural merge checks.

## Qualification independent conceptual review — reciprocal interface (18 November 2026)

**Status: proposed detailed contract under [Qualification review](../qualification/capability-record.md), PR #65; COURSE-12 ownership remains owner-agreed.** Training owns actual participation, verified achieved competencies and programme completion. Qualification maps source-attributed Training evidence to a qualification rule revision and makes separate eligibility/formal award decisions only where empowered. Completion is not a qualification; direct assessment or prior learning can qualify without Training where scheme permits. Training may display authoritative Qualification award status but cannot mutate it. This note does not complete this adjacent capability's independent review or assert an implemented contract.

## Current governing alignment — accepted ADR-0017 and ADR-0018 (18 November 2026)

Training uses explicitly authorised tenant/resource contexts; tenant hierarchy and organisation membership alone confer no learner-record access (ADR-0017). Competency, evidence and completion policies declare responsible authority, scope, version/effective period, permitted overrides, independent legal constraints and unknown/failure behaviour (ADR-0018). Configurable preferences cannot weaken security floors, manufacture evaluator mandates or erase historical Training decisions. Qualification's newer reciprocal note is retained above.

## Reciprocal Assessment conceptual interface — 18 November 2026 (draft PR #64)

**Status: Assessment's reciprocal relationship recorded; Training TRAIN-01–08 are owner-approved.** [Assessment conceptual review](../assessment/capability-record.md): Assessment supplies attributable result revisions, finality/release status and assessment-level appeal, correction and invalidation notifications. Training independently owns verified competence and completion; it must re-evaluate downstream claims on material assessment changes without modifying Assessment grades. A grade alone is not completed training. Training PR #63 has reconciled this reciprocal relationship. Conceptual cooperation does not require cyclic package imports; all protected reads and commands require public contracts, purpose/tenant permission and explicit unknown/failure handling. Preserve the training owner's existing decisions.



## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)); COURSE-12 retained.** Training owns attendance, participation, competency and completion facts. Qualification decides formal qualification awards; Credentials consumes only recognised authoritative award decisions or an independently authorised non-qualification achievement decision. Completion certificates may represent permitted Training achievements but cannot silently claim qualification recognition. Source corrections and subsequent credential status changes remain separate attributable transitions.

## Cross-capability review note — Enrolment (owner-accepted conceptual)

**Enrolment reciprocal interface (owner-accepted; 18 November 2026; [Enrolment review PR #60](https://github.com/nuxt-layers/architecture-blueprint-review/pull/60)).** Training owns independently verified attendance, competencies, completion, qualifications and evidence; Enrolment owns admission and participation status. Training may consume effective enrolment as prerequisite context and supply verified prior-learning/completion facts to Enrolment. Neither event automatically reassigns the other's domain status absent explicit course/programme rules. This is not Training review approval or a verified implementation.

## Attendance capability candidate — evidence boundary (18 November 2026)

**Status: pending explicit reconciliation; existing TRAIN-01–08 remain owner-approved.** [Attendance](../attendance/capability-record.md) is proposed as a generic source of activity presence observations and verification, independent of educational context. Training's earlier owner-accepted responsibility for verified *learning participation and attendance* cannot be transferred silently: Training remains authority for whether evidence satisfies educational standards, learning engagement, competence and completion. A future approved public interface might consume Attendance's verified presence source with revision, provenance, corrections and unknown/absence semantics; Training independently judges its relevance and may retain its own specialist verified educational evidence. No duplicate general presence ledger, no mandated Attendance dependency and no assumed approved modification to Training.
