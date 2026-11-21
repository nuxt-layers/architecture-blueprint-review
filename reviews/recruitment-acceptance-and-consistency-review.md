# Recruitment — conceptual acceptance and architecture consistency review

**Review date:** 21 November 2026. **State:** Conceptual specification completeness review, not executable testing, formal legal interpretation, implementation verification, branch-policy clearance or merge authorisation. [Recruitment record](../docs/capabilities/recruitment/capability-record.md) · [Control traceability](recruitment-control-traceability.md) · [PR #99](https://github.com/nuxt-layers/architecture-blueprint-review/pull/99).

## Latest authoritative baseline and parallel work

- Governing `architecture-rules/master@b920ce0d8b361de000a6739a16123dbdc56df7a7`, accepted ADR/public-contract hierarchy governs. Blueprint `master@d39df23e087cd0510c82ba2cea78996c7624850f`; these remained unchanged at baseline recheck on 21 November.
- Accepted Job JOB-01–09 (merged #84), REC-01–15 and STD-A–F owner-approved; detailed external legal applicability and implementation remain unverified.
- Active provisional nearby PRs at the review include #85 Legal Compliance, #88 Logging, #90 Mailer, #94 Message Queue, #97 Notifications, #98 Location, and #100 review protocol; none is treated as accepted authority. PR #100 proposes canonical-document consolidation and must be reconciled on merge if it changes protocol.
- Provider-neutral, one-directional public contracts, capability-owned outbox, no implicit event-to-access authority, no shared internal persistence, modular-monolith default, headless plus optional GUI, OWASP ASVS and WCAG 2.2 AA remain unchanged. No implementation repository or published root Recruitment CONTRACT.md was verified; no local tests or builds were run.

## Conceptual acceptance matrix

**Each row:** test input/context → expected observable behaviour/output → authority. This is a design/acceptance obligation; real implementation test execution is deferred.

| ID | Input, attempted operation or situation | Expected result/public contract | Authoritative owner |
|---|---|---|---|
| S-01 Native | HR authorised, sourced funding permission, no Job, ATS or board | Creates approved recruitment opening; accepts direct application; returns employer-scoped IDs/revisions | Recruitment for opening/application; Finance for funding |
| S-02 Approval | Applicant or hiring manager acts without delegated financial/recruitment mandate | Reject/hold with safe reason and evidence request; never show approved vacancy; record actor/policy revision | Authorisation, Finance, Recruitment |
| S-03 Multiplicity | Two openings under one requisition; two adverts for one opening | Separate opening allocation, campaigns, channel states; position unchanged | Recruitment, Job retains position |
| S-04 Speculative | Applicant submits without known opening/Job | Only purposeful, time-bounded speculative/pool case if authorised; no implied vacancy | Recruitment/Privacy |
| S-05 Tenant isolation | User from employer A reads employer B candidate evaluation or guesses ID | Deny without case existence leakage; capture security evidence without dossier logging | Authorisation/Recruitment/Audit |
| S-06 Agency sharing | Agency tries to reuse dossier between employers without lawful permission | Deny; separated scopes and retention; sharing/withdrawal recorded only with valid mandate | Privacy/Legal Compliance/Recruitment |
| S-07 Offer | Candidate accepts conditional versioned offer; Employment down or rejects handover | Retain attributable offer accepted, handover pending/unknown/rejected; idempotent retry; never active engagement | Recruitment offer, Employment engagement |
| S-08 Publication | One board ACKs, other confirms remote listing; disclosure/pay policy changed | ACK alone remains unconfirmed; only valid channel confirmation shown, update/withdraw affected projection | Recruitment, Publisher, board, Legal Compliance |
| S-09 Events | Submit duplicate idempotency command; replay committed outbox delivery | Same-intent replay same receipt, conflict different intent; no duplicate domain decision/subscriber side effect | Recruitment, Message Queue, subscriber |
| S-10 Structured evaluation | Unsupported criterion, stale scoring method, evaluator with conflict | Block/require qualified review; retain method version and conflict/recusal evidence | Recruitment/Assessment/Legal Compliance |
| S-11 Cross-cutting | Selection reversed and reports recomputed; logging provider fails | Recruitment remains source; Audit has restricted evidence; Logging only safe diagnostics; Reporting corrected aggregate | Recruitment, Audit, Logging, Reporting |
| S-12 Accessibility | Screen-reader, keyboard-only, no CV parser, time-zone and timed assessment accommodation | Accessible application/interview alternate, recoverable errors, correct dates without exposing adjustments to ranking | Recruitment/host, Clock |
| S-13 ATS | External-primary configured, invalid webhook, stale external decision or provider outage | Validate signature and designated authority; reject forgery, leave stale/unknown as disputed; recover via reconciliation | Integrations remote transport; Recruitment local status |
| S-14 AI | Automated ranking/rejection requested with no legal or organisational approval | Default human-controlled decision; reject/hold automation; if approved enforce recorded model/rule, evaluation and appeal gates | Legal Compliance, Recruitment, Configuration |
| S-15 Legal policy | Requirement missing/unknown or rule changes after existing decision | Block affected consequential action, preserve historical version; re-evaluate pending work without retroactive rewrite | Legal Compliance/Privacy/Recruitment |
| S-16 Privilege | Received event or completed Workflow task demands approval/offer signing | Refuse without server-side access and native business guard, regardless of event receipt | Authorisation, Recruitment |
| S-17 Checks | Qualification/verification/right-to-work status revoked, expired or unknown | Status qualified by scope and freshness; no automatic hire clearance, review pending selection/offer | Qualification/Verification, Recruitment/Employment |
| S-18 Appeal | Candidate challenges decision, evidence corrected, panel member recused | Attributable new decision/reason/version with restricted historical record, appeal state and notices | Recruitment |
| S-19 Notifications | Message sender ACKs or delivery unknown while offer notice in flight | Delivery is not offer acceptance, Recruitment retains notice intent and qualified correlation | Notifications/Mailer, Recruitment |
| S-20 Rights | Candidate requests export, correction or withdrawal while agency shares references | Authorised scoped response with legal basis/recipients, rights status, no blanket immediate deletion claim | Privacy/Legal Compliance, Recruitment |
| S-21 Retention | Deletion deadline reached but valid legal hold exists; later hold expires | Restrict processing, defer deletion with evidence; reassess, dispose and propagate qualified outcomes after hold | Privacy/Legal Compliance, Recruitment/Storage |
| S-22 Upload security | Candidate uploads malicious file or provider sends forged payload | Quarantine/reject, least-privilege access, redact error logs and audit sensitive access | Content Security/Storage, Recruitment |
| S-23 Contract independence | Host composes native Recruitment; consumer uses only documented public interfaces | Operates without private database/schema/SDK, respects declared dependencies and budget, version compatibility specified | Recruitment + host |
| S-24 Reporting/performance | Funnel metric corrected; public search cache retains withdrawn listing | Correction-aware, restricted aggregate with provenance; index eventually retracts within declared freshness limit | Recruitment, Search, Reporting |
| S-25 Recovery | Scheduled interview reminder fails, board timeout, concurrent edit and repeated callback | Cases remain accurate, unknown/pending and retry/reconcile available; concurrency conflicts rather than lost updates | Recruitment, Scheduler/Integrations |

## Coverage and outcome

All **38** T-controls and **25** S-scenarios have at least one cross-reference; S-01…S-25 cover native use, scope/authorisation, invalid commands, replay, providers, recovery, historical lifecycle, external evidence, downstream consumers, no-implementation prerequisites and GUI. Each has an authoritative owner. No fixed endpoints or storage schema are mistakenly claimed as published interfaces.

**Conceptual design verdict:** On the documented assumptions, Recruitment is independently understandable and its approved ownership and public business contract are sufficiently specified for conceptual handover. The full set of conditional legal jurisdiction/sector profiles must be developed and validated when services and deployments are defined; that is not a claim of legal compliance.

## Architecture challenge and reconciliation

| Challenge | Assessment and disposition |
|---|---|
| Recruitment ↔ Job | Job position definition is optional, frozen referenced revision; Recruitment requisition/opening and application separate. No reciprocal private import or `filled` mutation. **Consistent** |
| Recruitment ↔ Employment | Offer/acceptance evidence and idempotent handover belong to Recruitment; definitive agreement/actual engagement to Employment. Handover unknown not completion. **Consistent** |
| Recruitment ↔ Finance/establishment | Recruitment permission to recruit constrained by independently issued funding/capacity approval; does not own budget or establishment ledger. **Consistent; source business delegation is tenant policy** |
| Recruitment ↔ Legal Compliance/Privacy | Legal applicability, privacy rules and holds source-owned; Recruitment enforces versioned policy. Active #85 proposal is **provisional**, no imported unpublished API. Reconcile signatures if merged. **No ownership collision** |
| Recruitment ↔ Verification/Qualification/Assessment | Source facts remain owned; Recruitment determines recruitment suitability and reacts to stale/disputed evidence. **Consistent** |
| Recruitment ↔ Integrations/ATS/Publisher/Search | Explicit configured source authority per case fact; remote listings and document versions not fabricated; search index derived. **Consistent** |
| Recruitment ↔ Notifications/Mailer | Intent, message delivery and offer acceptance are three independent facts. Active #97/#90 are provisional; no dependency on their unmerged signature. **Consistent** |
| Recruitment ↔ Message Queue/Workflow/Scheduler/Task | Recruitment domain state/outbox stay owned by Recruitment; MQ transport, Workflow routes, Scheduler times and Task assignments; no event provides authorisation. #94 is provisional. **Consistent** |
| Recruitment ↔ Audit/Logging/Observability/Reporting | Recruitment is only hiring outcome owner. Audit evidence, redacted Logging diagnostics, health signals and aggregate Reporting are separated. #88 is provisional. **Consistent** |
| Candidate identity/agency/federation | No globally authoritative candidate master or automatic cross-employer dossier; scoped subject linking and explicit mandates. **Consistent, regulatory controls vary** |
| Security, i18n, UI and resilience | ASVS L2/L3-sensitive cases, WCAG 2.2 AA, BCP47/CLDR, Clock, conditional providers and native manual fallback. **Consistent conceptually; implementation evidence deferred** |
| Contract direction and cycles | Published ports/host-mediated composition avoid forced circular package dependencies even where reciprocal information flows exist; no private database/schema. **Consistent** |
| Concurrent work | #85/#88/#90/#94/#97/#98/#100 and other open reviews were checked for overlapping conceptual themes; proposed notes remain marked, without overriding their reviews. **Recheck immediately pre-merge** |

## Completeness and residual work categorisation

**Owner-approved conceptual direction:** REC-01–15, STD-A–F; selection, agency and automated-decision policy gates. **Conceptual design complete subject to the currently accepted authority**; no new owner decision is presently required for core Recruitment ownership or interface shape.

**Deferred implementation/operational validation (not conceptual blockers):** separate implementation/CONTRACT.md and manifest, storage register/persistence/outbox, host composition/CI tests, live security/privacy threat model and DPIAs where required, local accessibility tests, measured latency and search-freshness SLOs, vendor contract evidence, jurisdiction-/sector-specific legal application, exact library/provider licence/security review and deployment.

**Future change triggers:** merge of governing standards, proposal #100's canonical-protocol wording, affected neighbouring draft contracts, new jurisdictions and external-ATS/AI modes, or unexpected source-of-truth conflict. Such changes require fresh architecture reconciliation, not silent global specification edits.

**Pre-merge gate:** Recheck latest governing and blueprint `master`, changed-file scope, link targets, branch conflict status, protected branch checks, CI and neighbour merges, and obtain explicit owner merge approval. No merge is authorised by this review.
