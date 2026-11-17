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
