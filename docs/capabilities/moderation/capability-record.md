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


## Dedicated conceptual review — 19 November 2026 (PR #96)

**Status and provenance:** Proposed detailed design, **pending owner conceptual approval**; earlier owner-approved cross-cutting online-safety direction remains distinct. Opening governing `master@b920ce0d8b361de000a6739a16123dbdc56df7a7`, blueprint `master@6dac83a03da8704f7945ee1bc894f2248300445a`. No standalone `nuxt-layers/moderation` repository was returned by repository discovery; no implemented root `CONTRACT.md`, actual interfaces, runtime, test or regulatory certification is asserted. The `moderation` directory is the actual blueprint directory. This extends, rather than supersedes, MOD-01–MOD-10 in the existing [report](capability-report.md).

### Classification, authority and native operation

**Proposed classification: Platform.** Reports and cases are reusable across unrelated resource-owning domains and retain independent evidence, appeal and disposition lifecycles. This supports an independently owned bounded capability, but **not** a mandatory separate service, Nuxt Layer or database server: a modular monolith with a headless core is the default. Moderation is optional to applications with no case-management needs, and absence cannot disable source-owned emergency holds and their own legal/security controls.

**Authoritative case facts:** case ID/tenant/initiator, classified report source and safe reporter follow-up, joined source references and revisions, triage/severity, policy/jurisdiction snapshots, qualified investigation and decision with reasons, conflict-of-interest assignments, appeal submission and independent outcome, action-intent ledger, per-target enforcement receipts and reconciliation, deadlines, lawful disclosure/referral approvals, case closure/reopening, retention/holds and case-owned durable outbox. Evidence bytes and original publication remain with their owners or explicitly approved restricted evidence custodian. Audit owns evidential custody of accepted events, not Moderation's case truth.

**Native lifecycle:** received/validated → triaged (or declined with safe rationale) → investigating → decision pending → decided → action requested → per-target confirmed, refused, failed or unknown → notifications/appeal/reconsideration → closed or reopened. Investigation, enforcement, appeal and statutory handoff are **orthogonal state tracks**, not one lossy global enum. Protect urgent cases with due dates and manual escalation; do not conflate a report, scanner flag, moderation finding, criminal conviction or completed takedown. On reversal, preserve prior historical outcomes and initiate separately reauthorised owner-state restoration; appeal does not guarantee reinstatement if other holds apply.

**Native without optional providers:** accept safe reports, conduct authorised human triage/investigation, record decisions, coordinate direct owner ports where configured, admit appeals and reconcile acknowledgements. No automatic trusted detection or statutory filing is invented. Mandatory IAM checks, qualified legal rules or persistence, if required by the selected operation, fail closed; unavailable scanning/Workflow/Scheduler/Notifications cannot be silently treated as success. Local source protection continues if Moderation is down.

### Idealised public inbound contract

These are business-level boundaries; not endpoints, TypeScript types or an imposed universal request envelope. Classification `R` = required for the operation, `C` = conditional on the governed use case, `O` = optional enhancement.

| Surface / supplier | Facts and intent supplied | Owner, validation and absence / uncertainty | Need |
|---|---|---|---|
| **MOD-01 reports** — person, authorised guest or host | Reported source owner/type/ID/revision, conduct category, statement, evidence references, reporter-safe contact token, consent and correlation | Moderation validates abuse/rate limits and source scope without trusting claimed actor or unbounded text. Non-disclosable target yields opaque receipt, not source details; repeated report joins may be safe but does not automatically close cases | R |
| **MOD-02 detection referral** — Content Security | Detector/rule/version, verdict, confidence/limitations, inspected resource revision, evidence location, time and incomplete state | Content Security owns detection. Unknown/stale result remains unknown, never guilty/cleared; case intake can proceed without automatic scan where permitted | O/C |
| **MOD-03 triage** — qualified operator, case policy | Priority, safeguarding category, target scope, case assignment, urgency and deadline, emergency request | Moderation authorises reviewer and separation of duties, validates policy effective version and escalation; conflicting priorities require recorded resolution | R |
| **MOD-04 decision** — authorised adjudicator and source-owner read port | Bounded current source status, versioned case evidence, reasons, effective policy, requested disposition | Source owns actual resource state; Moderation owns qualified case decision. Stale source revision blocks irreversible enforcement; missing mandatory evidence yields unresolved/escalation | R |
| **MOD-05 enforcement receipts** — Publisher, Media, Comments Engine, Marketplace, Gaming, Hub/source owners | Request acceptance/refusal, completed state, exact target/revision, action ID, owner decision, effect time and exception | Owner exclusively executes and checks rules. Acceptance ≠ completion; missing/late/contradictory receipt → pending/unknown and reconciliation, never success by timeout | C |
| **MOD-06 challenge/appeal** — affected authorised party or safeguarded representative | Case-specific challenge, evidence reference, challenge authority, procedural deadline | Caller rights verified without disclosure of other parties; independent reviewer/conflict handling. Late or unverifiable submissions receive qualified rejection/extension decision | R when appeals apply |
| **MOD-07 legal and disclosure** — Legal Compliance, Privacy, authorised disclosure officer | Jurisdiction/service/audience, dated applicable duties, hold/retention, filing threshold, disclosure scope, approval and uncertainty | Legal Compliance qualifies duty; Privacy qualifies processing; disclosure authority independently approves. Unknown mandatory rule → escalate/hold, never assert compliance or send data | C |
| **MOD-08 evidence** — authoritative source owner and Audit receipt | Purpose-bound evidence access, provenance, immutable source reference, preservation/acceptance receipt, completeness | Original remains with source; Audit owns accepted custody. Missing/expired/conflicting evidence is surfaced explicitly and limits findings | C |
| **MOD-09 Hub signals** — Federation/Hub composition | Peer/collection/index item, local service scope, remote provenance and revocation signals | Remote signals are untrusted leads, not global findings; source Node owns original, Search owns index, Federation owns exchange and peer actions | O |
| **MOD-10 administration and policy** — host/Configuration, IAM, Clock | Approved case policy and source, protected caller/tenant/assurance, effective time, retention and deadlines | Server-side Authorisation required; immutable legal/security floors cannot be configured away; unknown authenticated tenant/assurance denies sensitive actions | R |
| **MOD-11 operations** — Workflow, Scheduler, Notifications and Integrations ports | Assigned human steps, timed escalation/delayed work, delivery/transport receipts | Each specialist owns execution facts; unavailable optional adapter produces visible degraded/queued/failed status, not a case decision | O/C |

### Idealised public outbound contract

| Surface / permitted consumer | Authoritative meaning and limitations |
|---|---|
| **MOD-O1 report receipt** — reporter/host | Opaque case reference or safe tracking token, accepted/duplicate/rejected status and allowed next action; does not reveal target visibility, other reporters or investigation |
| **MOD-O2 case query/queue** — authorised moderator, supervisor, operator | Tenant/role-filtered case summary, subject-safe evidence references, assignments, deadlines, policy/evidence version, completeness/freshness and redacted view; denies cross-case fishing |
| **MOD-O3 adjudication result** — affected parties and authorised source owners | Reason-coded, policy-versioned decision, exact scope/target revision, deciding authority, time, reviewability and disclosure-approved explanation. **Not proof of executed restriction** |
| **MOD-O4 action intent** — selected source owner via public port | Scoped request ID and idempotency, exact tenant/target/revision, action, urgency, expiry, reason category, authority and case correlation; recipient must independently reauthorise, may reject |
| **MOD-O5 enforcement reconciliation** — operator, affected owner, case reporting | Per-target requested/accepted/completed/refused/failed/unknown status, receipt provenance and effective time, outstanding retries/compensation; never silently aggregate partial completion to full success |
| **MOD-O6 appeal and correction** — eligible appellant, independent reviewer, source owner | Appeal acceptance and decision, changed evidence/decision revision, reasoned outcome and separately requested reversal, preserving original history and applicable competing holds |
| **MOD-O7 legal handoff** — explicitly designated filing/disclosure process | Approved, minimised case fact package, applicable duty/effective version, disclosure scope, authorised sign-off and handoff reference; transport acknowledgment and statutory acceptance separately tracked |
| **MOD-O8 evidence/audit event** — Audit and protected authorised evidence consumers | Attributable minimal case transitions, access, decisions, disclosures, holds and enforcement discrepancies with sensitivity classification; immutable Audit receipt remains Audit-owned |
| **MOD-O9 committed lifecycle events** — notifications, reporting, domain subscribers, Message Queue transport | CaseOpened, CaseTriaged, DecisionRecorded, ActionRequested, EnforcementReceiptRecorded, AppealResolved, CaseClosed/Reopened and DisclosureApproved (illustrative names). Committed facts only, with tenant scope, event ID, sequence/version, correlation, lawful disclosure classification |
| **MOD-O10 operator service state** — authorised host GUI/Observability | Queue/backlog, escalation, evidence-gap and receipt-lag indicators with denominators and freshness; health does not imply legal compliance; no raw sensitive evidence in telemetry |

**Command/query/event invariant:** Commands validate trusted caller, owner scope, policy and expected revision, return stable denial/conflict/unknown codes, and deduplicate by scoped intent key. Queries enforce purpose-based read privileges, redaction and freshness and do not leak the existence of restricted sources. Events follow committed case state through a **Moderation-owned durable outbox** where relevant; Message Queue only transports. Consumers tolerate duplication, reordering and gaps, reconcile by source/version and never infer exactly-once distributed effects. Source owners emit their own authoritative resource-change events. Keep direction through host-assembled public ports, not direct cyclic package imports.

**Shared context, scoped per surface:** tenant and actor/service principal with authentication assurance, resource owner/type/opaque ID and expected revision, case and action IDs, effective policy/constraint version and jurisdiction, Clock-based event/effective/deadline time, evidence provenance/classification/expiry, correlation/idempotency, result status, and explicit `unknown` or `unsupported` outcomes. No universal shared DTO. Enforce stable contract versions and migration mappings; a changed policy must not retroactively rewrite the historical basis of a decided case.

### Cross-capability and provider matrix

| Relationship | Receives from other owner | Supplies to other owner | Absence / dependency boundary |
|---|---|---|---|
| Identity, Authentication, Authorisation, Profile/Verification | Scoped identity, assurance, rights and eligible representative claims, where lawful | Permission requests, minimised subject and case disposition notifications | Trusted caller/access boundary required for protected actions; no membership or identity proofing owned here |
| Configuration / Legal Compliance / Privacy / Clock | Valid effective policy, qualified service-specific duties, lawful basis/hold, deadlines | Policy-used provenance, restricted processing and correction/disclosure outcomes | Mandatory constraints fail closed; no implicit legality from configuration |
| Content Security | Revision-bound detection evidence and uncertainty | Report/case reference, scoped re-assessment request | Optional; scanner findings cannot decide cases |
| Publisher, Media, Comments Engine, Marketplace, Gaming, Course and other targets | Authoritative source status and independently executed restriction receipts | Targeted decision and action request | Conditional only when target type is supported; source emergency holds remain native |
| Federation, Search and Hub composition | Qualified peer/derived-index signals, withdrawal/index receipts | Scoped Hub-local case intent | Optional; no authority to delete origin or to demand remote universal enforcement |
| Audit / Logging / Observability / Reporting | Evidence custody receipt, technical health/aggregate consumption | Attributable audit facts, redacted diagnostics, scoped aggregate inputs | Audit custody distinct from technical logs; reporting never gets raw unrestricted case evidence |
| Workflow / Scheduler / Message Queue / Notifications / Integrations | Review coordination, due execution, delivery and adapter receipts | Pending task, committed event and safe notice/referral intent | Optional/conditional ports; no decision authority assigned to transport |
| Storage / host infrastructure | Capability-owned encrypted/restricted persistence and approved references | Storage register, retention and disposal requirements | Required case persistence fails closed; host supplies provider, Moderation owns store schema/lifecycle |

**Provider neutrality:** default native case management must not require a vendor AI moderation API. Providers are replaceable evidence producers, with declared identity, terms, versions, data-transfer location, charge/limits, outage, re-evaluation, migration, withdrawal and consent/retention controls. Import must preserve provenance and cannot falsely recast vendor verdicts as adjudications. Reconcile unknown asynchronous results; provider confidence is not a conviction. No global trusted peer reputation mechanism assumed.

### Security, compliance and adversarial challenge

- Apply OWASP ASVS 5 L2 with elevated applicable controls, segregated moderator duties, request-time Authorisation, high-assurance sensitive disclosure, audit of evidence viewing, protected reporter identity, careful notification wording, sanctions for abusive reporting, replay/race controls and tenant-scoped keys.
- Sensitive case records may implicate children, CSAM, NCII, harassment, domestic abuse or whistleblowing. Minimise payloads, use restricted evidence references rather than ordinary previews, avoid default downloading and raw telemetry, govern preservation, staff welfare, access reviews and deletion/hold exceptions. Do not promise that copying or viewing illegal material is inherently authorised.
- Qualified UK Online Safety Act obligations depend on **actual service type, jurisdiction, audience, risk category and operative duties**, supplied by Legal Compliance with qualified and dated source. Do not equate an installed module with compliance, content policy breach with an offence, a legal disclosure decision with a successful filing, or all private/E2EE communications with public searchable content.
- Private/E2EE reports require separately authorised user-submitted evidence and purpose-limited processing, not universal client-side scanning. False reports, compromise, brigading, spurious remote feeds and moderator conflict must support challenge and independent correction.
- Statutory submission ownership, designated qualified disclosure sign-off and legal holding authority remain **open decisions**. Until allocated, MOD-O7 is a preparation/handoff only, not a provider submission claim.
- Emergency holds are source-native and available if Moderation is unavailable. A stale case decision cannot override source-state revision, mandatory legal hold or newly revoked authorisation. Cases can close with explicitly unresolved downstream effects only under a documented escalation policy, never by concealing them.
- Persist minimal case/evidence references, action intents, receipts, deadline/disclosure and appeal trail, versioned policy basis and a durable outbox; record a future `STORAGE-REGISTER.md`. Use security classification, subject rights and lawful retention/erasure with qualified evidence preservation; no indefinite unrestricted case store.

### GUI, headless usage and conceptual acceptance

**Optional presentation:** Host sidebar → Moderation dashboard with scoped cases, prioritised triage queues, case detail and restricted evidence viewer, reasoned decision form, explicit target/revision and action-intent composer, acceptance/completion reconciliation, separate appeal review, statutory handoff approval, deadlines, incident/peer views and audit/provenance links. Reporter-facing safe receipt/status and appeals are separately permissioned; resource owner screens retain their own local holds and visibility controls. Show `pending`, `unknown`, `partial` and `failed` visibly, with no implied success from a spinner or delivered notification. The host owns routes/navigation, Theme Manager owns semantic styling; accessible WCAG 2.2 AA keyboard/focus/live status, localisation and responsive layouts are mandatory. Headless mode exposes all relevant public operations without any GUI dependency. Representative host: `nuxt-layers-test/application-test-template`; no tests run here.

| Conceptual scenario (input) | Expected result / output | Authority |
|---|---|---|
| Authenticated or permitted anonymous report of inaccessible resource | Safe opaque receipt; no unauthorised target disclosure | Moderation intake, owner visibility |
| Same idempotency key retried and brigaded duplicate reports | Same outcome or documented deduplication; rate/safety controls; no duplicate sanction | Moderation |
| Scanner flags an edited item and its verdict references an old revision | Quarantine/triage as warranted, stale evidence signalled; no automatic guilt or fresh-revision enforcement | Content Security verdict; Moderation decision; source owner execution |
| Urgent offending publication while case worker down | Source-native emergency hold succeeds independently; later case reconciliation | Source owner |
| Case spans a comment, media item and listing; one owner refuses action | Three separately scoped receipts, with overall partial/unknown instead of full takedown | Each source owner |
| Appeal overturns finding but another legal hold applies | Historical case remains, approved reversal requested, owner may still refuse release with explanation | Moderation appeal; Legal Compliance; source owner |
| Hub suppresses a peer index item | Hub-local Search receipt; origin Node record unchanged, remote withdrawal separately reconciled | Search/Federation/source |
| Mandatory qualified legal duty or tenant assurance absent | Protected action denied or suspended, logged and escalated; no default lawful filing | Legal Compliance/IAM + Moderation |
| Provider timeout and duplicate/reordered owner events | No fabricated completion, idempotent case receipt reconciliation, explicit evidence gap | Moderation action ledger + source owner |
| Rights/retention request for sensitive report | Scoped redaction/erasure or reasoned hold, audit-preserved receipt and known backup/provider limitations | Privacy/Legal Compliance and each data owner |
| Host without Moderation installed | Owner-native content checks and urgent holds still work; case-specific features explicitly unsupported | Host and resource owner |

### Decision and evidence register (19 November 2026)

- **Established governance:** accepted ADRs and normative standards govern capability ownership, protected actions, durable outboxes, security, provider-neutral contracts, acyclic dependency and host integration; accepted ADR-0017/0018 policies are not replaced by this proposal.
- **Previously agreed conceptual direction:** the Online Safety and Content Governance review's detection/case/source-enforcement separation, qualified legal applicability and no mandatory universal E2EE scanning. Preserve existing MOD-01–MOD-10 and reciprocal scope notes.
- **Proposed in PR #96, not owner-approved:** MOD-O1–O10 output distinction, MOD-11 operations, independent per-owner receipt ledger, versioned case policy basis and concrete GUI/acceptance model above.
- **Open decisions:** MOD-D1 scope and authority of statutory filing vs preparation; MOD-D2 appeal independence and delegated representative eligibility; MOD-D3 preservation custodian/retention for highly sensitive evidence; MOD-D4 cross-tenant and cross-node shared-abuse disclosures; MOD-D5 precisely supported source owner classes and emergency-hold policy minimum; MOD-D6 whether a standalone package adds value over implementation inside a broader trusted-services application.
- **Technical investigation:** current actual published owner `CONTRACT.md` ports and exact revisions; current legal operative duties and qualified counsel validation; existing target implementation discovery; provider/host acceptance evidence; potential concurrent PR conflicts. These are not owner decision proxies.
- **Deferred:** No implementation contract, runtime interfaces, package, regulatory attestation, migrations or test results are established. A separate architecture-rules PR and explicit approval would be necessary to make changed catalogue or standards normative.
