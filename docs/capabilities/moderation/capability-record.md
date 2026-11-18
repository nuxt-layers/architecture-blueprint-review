# Capability Record — Moderation

**Status:** Candidate Platform capability — non-normative conceptual review; no implementation, standalone repository or published root `CONTRACT.md` is asserted.  
**Review date:** 17 November 2026.  
**Authority:** Latest accepted `nuxt-layers/architecture-rules` ADRs, Architecture, Capability Standard, Security and Privacy.  
**Primary working materials:** [Moderation capability report](capability-report.md) and [Online Safety and Content Governance review](../../../reviews/online-safety-content-governance.md).

## Purpose and classification

Moderation is a **proposed independent case-management and adjudication capability** for user and system reports about content or conduct: intake, triage, investigation, decisions, appeals, coordinated restrictions and evidence. It is not a synonym for Content Security scanning and does not become the author of comments, images, documents, product listings or private messages.

**Classification gate:** case and appeal records have a potentially independent lifecycle spanning multiple domain owners. Candidate **Platform** classification merits examination; actual repo, Nuxt Layer, deployment or new database must be justified separately. Its optional presentation is separable. The pro-forma [report](capability-report.md) preserves the future detailed review questions.

## Ownership and exclusions

| Moderation owns (proposed) | Another capability retains authority |
|---|---|
| Reports, case references, triage, severity, review task state, decision, appeal and case outcome | Publisher owns drafts/revisions/publication; Media owns media metadata and asset visibility; Comments Engine owns comments and its moderation state |
| Authorised requests for holds, removals, restrictions and reinstatements, and acknowledgement reconciliation | Each domain capability enforces its own invariant and actually changes the source resource; Authorisation decides access rights |
| Scoped moderator and reporter case views, review queue and notices about case disposition | Content Editor/Gallery/Hub compositions render their own views; Notifications delivers messages |
| Case-linked assessments and qualified decision provenance | Content Security owns detection results; Legal Compliance owns dated applicability/obligations; Audit owns received tamper-evident evidential custody |
| Hub-local reports about peers/index entries | Federation owns peer/subscription state and Hub composition coordinates Search-derived index visibility; origin Node owns origin data |
| Statutory reporting case coordination where authorised | Legal Compliance establishes duty; designated owner of filing/submission and Integrations adapter must be reviewed |

No cross-tenant visibility by default. No criminal-guilt decisions, universal policy interpreter, duplicate source data, copy of private plaintext or technical incident detection engine.

## Logical input and output contracts

The **ten MOD-01–MOD-10 conceptual surfaces** in [capability-report.md](capability-report.md#conceptual-public-inputoutput-surfaces-not-implemented) describe report intake, automated referral, triage, adjudication, enforcement requests and independent receipts, appeal, statutory referral, evidence, federation moderation and GUI. They are not APIs.

Inputs must include trusted service/tenant/publisher context, subject/caller assurance, source owner/id/revision, permitted evidence and source policy/version when necessary; outputs distinguish decision, requested action, accepted receipt, completed enforcement and unavailable/unknown state. Authorisation is enforced by resource owners before acts. Required and optional ports and fail-safe absence behaviour need specification.

## Cross-capability relationships

**Content contributors:** Publisher, Media, Comments Engine, Marketplace, Product, Jobs, prospective Messaging and Federation.  
**Specialists:** Content Security (detection), Legal Compliance (obligations), Privacy (lawful processing), Identity/Authentication/Authorisation (actor assurance and permissions), Workflow (review coordination), Scheduler (timed escalations), Notifications (notices), Integrations (external adapters), Audit (evidence), Logging/Observability (technical health), Reporting (aggregate measures).

Dependencies must be explicit, one-way and acyclic under accepted ADRs. A workflow orchestration or event handoff is not authority to import another capability's private schema. Each originator retains its durable event/outbox responsibility.

## States, evidence and safety policy

Conceptual states and risk categories are preserved in the [report](capability-report.md). A reported item, scanner match, qualified moderation decision, legal determination and successful enforcement are **different facts**. Emergency pre-publication controls must work independently of the case-management service. An unavailable mandatory assessment cannot be silently converted into clearance.

Risk and obligation models must distinguish content harm, conduct harm, cyber abuse, fraud and illegal commercial offers; service type, audience, jurisdiction, effective dates and statutory reporting scope. Metrics need evidence of denominator, relevant coverage, response and exposure time, false-positive correction, backlog, appeal and external-provider failures. No claim of automatic OSA certification.

## Persistence and security boundaries

Proposed minimum state: cases, report metadata, source references, decision/appeal revisions, restricted evidence references, required action intents, enforcement receipts, status/expiry, disclosure approvals, legal-reporting correspondence references. Do not retain source bytes unless separately authorised and justified; protect extremely sensitive evidence and reporter identities under purpose/role restrictions, tenant isolation, immutable source references, retention/hold and explicit deletion rules. A future storage-owning package must publish its `STORAGE-REGISTER.md`.

Threats include abusive false reporting, brigading, moderator compromise, privilege escalation, regulatory disclosure errors, exposure of CSAM/NCII evidence, cross-tenant leakage, mistakes in automation, and stale Hub moderation feeds. Independent appeal/review authority and tamper-evident Audit intake are necessary, but Audit does not become domain truth.

## Conceptual GUI and acceptance

Optional host-navigated moderation dashboard, queues, case detail, restricted evidence viewer, decision/appeal workflow, action receipt reconciliation, regulatory escalation and reporting. Host retains navigation and server-side trusted context. WCAG 2.2 AA, accessible notices and internationalisation apply. A Hub composition may add index/peer case views; it cannot disclose originating private records without authorisation. The capability remains headless when presentation is disabled.

Acceptance scenarios, open questions, and more granular responsibility/contract notes are documented in [capability-report.md](capability-report.md), with cross-capability flow and risk coverage in [the safety review](../../../reviews/online-safety-content-governance.md).

## Disposition

Retain as **candidate** for future alphabetical conceptual review and classification approval. The owner's approval is approval to document the direction, **not** approval of a standalone implementation, API, normative ADR or legal compliance claim.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Moderation cases may rely on qualified age/identity/representation evidence for restricted actions, impersonation reports and fraud investigations but do not independently prove civil identity or authorise general access. Keep reporter/witness privacy and evidence provenance; adult/child misclassification and identity claims must admit safeguarded challenge. Separate case determination from proofing provider outcomes.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine remains source-of-truth for comment revisions, thread structure, local visibility, emergency holds and enforced receipts. Moderation candidate owns cross-domain reports, cases, appeals and case decisions. Exchange precise tenant/target/comment/revision and qualified evidence references; treat request acceptance, completed enforcement and remote withdrawal as different facts. Revisions, source policies and unknown/conflict outcomes must be explicit. No duplicate author text or automatic permission from a case decision.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Content Security owns qualified detection evidence, revisions and incomplete/unknown results; Moderation owns cross-domain reports, adjudication, appeal and case decisions. Moderation may request a scoped re-assessment or receive an indicator/evidence reference but cannot rewrite the historical verdict. Source owner alone performs and confirms holds/releases.

## Reciprocal conceptual note — Course (17 November 2026)

**Status: Proposed, pending owner approval.** [Course review](../course/capability-record.md), draft PR #56: Course may submit user-facing learning material reports for moderation. Moderation owns policy enforcement decisions and appeals where applicable; Course owns course withdrawal/access transitions and version history. Neither capability awards learner grades. This does not complete moderation's own review.

## Federation — reciprocal conceptual note (18 November 2026)

**Status:** Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69), not a published implementation contract or completed independent review. See [Federation conceptual contract](../federation/capability-record.md).

Federation submits locally admissible provenance and suspicious remote transmissions for review; Moderation owns cases, adjudication and appeal where installed. Federation controls local peer refusal/quarantine and transmission; Search controls index application; originating domains control source publication. A local defederation is not origin deletion. Public directional ports, explicit absence modes and acyclic package dependencies apply.

## Cross-capability note — Gaming conceptual review (18 November 2026)

**Gaming (18 November 2026; proposed, not owner-approved):** [Gaming](../gaming/capability-record.md) supplies game source references, permitted conduct/anti-cheat evidence and own restriction/enforcement receipts. Moderation retains cross-domain reports/cases/adjudication/appeal coordination; Gaming independently validates and executes match restrictions, disqualifications or scoring corrections under game rules and due process. Detection flags are not final guilt findings. No cross-tenant disclosure or verified adapter is implied.

### Gaming portal scope correction — 18 November 2026

**Gaming scope clarification (18 November 2026, owner-provided; detailed decisions proposed):** [Gaming](../gaming/capability-record.md) is a shared game catalogue, launch portal and accepted-score/leaderboard owner, **not** a generic game engine. Independently composed game layers own their own gameplay, session/move/physics state, game rules and original results. Earlier gaming reciprocal wording implying that Gaming owns gameplay, game rounds, adjudication of moves or original raw results is superseded. This owner-supplied distinction takes precedence within this working review; no implementation or published game contract is asserted.
