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


## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)); COURSE-12 owner-approved ownership unchanged.** Qualification supplies versioned authoritative individual qualification-award decisions, award/appeal/withdrawal state and verified issuer/delegation scope through a public provenance-rich contract. Credentials owns issued representation, issuance transaction, proof and credential-specific suspend/revoke/replace/status, consumes source changes with idempotent reconciliation, and returns bounded receipt/status where required. Qualification must not import Credentials internals or infer that successful award implies delivered credential. A stale external source does not confer award authority; a later credential correction does not change Qualification's underlying award.
