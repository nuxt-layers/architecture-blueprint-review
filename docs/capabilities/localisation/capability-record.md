# Capability Record — Localisation

**Capability:** `localisation` — **Platform candidate**, conceptually replacing the empty `translate` candidate.  
**Status:** Proposed conceptual record; no implemented capability, package, independently verified `CONTRACT.md` or acceptance evidence is asserted.  
**Recorded:** 17 November 2026.  
**Governing authority:** Current accepted `nuxt-layers/architecture-rules` architecture and capability standard; governing catalogue rename requires its own accepted PR. This working blueprint is non-normative.  
**Source:** Owner-approved rename and scope expansion from `translate` to `localisation`; preserve source/domain authority, provider neutrality and existing i18n/accessibility rules.

## Purpose, classification and definitions

**Localisation (l10n)** coordinates **language and locale adaptation of content and application text**, including human/machine-assisted translation, terminology, translation workflow, quality review, variant availability and provenance. The scope is broader than translation alone.

- **Internationalisation (i18n):** the established cross-cutting requirement to design interfaces and content contracts that support multiple locales. It is **not** another independent capability.
- **Translation:** transfer of meaning between languages; a function performed within Localisation's remit, not an additional `translate` capability.
- **Localisation:** adaptation of linguistic resources for language, region, cultural and audience context, subject to applicable domain/legal constraints.
- **Locale formatting:** must respect existing owners (Clock for date/time/timezone semantics, domain financial owners for currency and amounts, platform presentation for accessibility/RTL layout). Do not duplicate them in a universal formatter.

**Classification gate:** a reusable, provider-neutral translation workflow, terminology registry, quality status and coordination lifecycle can justify an independent Platform candidate. Localisation does not automatically own every translated document or product, nor does it require a Nuxt-specific implementation. A repo/Layer and runtime form remain for later approval.

## Authoritative ownership and exclusions

| Localisation owns (conceptually) | Explicitly owned elsewhere |
|---|---|
| Translation jobs/requests, source-to-target mapping references, locale-target intent, review and quality workflow states | Publisher owns authoritative documents, revisions, publication/withdrawal, canonical addresses and its approved language variants |
| Terminology/glossary, style guidance, translation memory and provenance where independently maintained | Source domain owns business meaning and source text; Product/Marketplace owns authoritative listings/catalogue facts and domain approvals |
| Translation provider selection policy, request orchestration and qualified output metadata | Integrations owns external provider connection lifecycle/adapters where applicable; host owns secrets, credentials and infrastructure |
| Locale-specific resource bundles and controlled application-text adaptation when explicitly delegated | Application UI owns navigation/layout and accessibility; Configuration/Profile own user or host language preferences under their contracts |
| Translation review/acceptance outcome and language-variant readiness signal | Domain owner alone may commit or reject publication and legal/safety-sensitive content; Content Security/Moderation supply safety evidence/case decisions |
| Localisation-specific case provenance, quality and missing variant reports | Audit owns accepted evidential custody; Logging owns diagnostics; Reporting owns authorised cross-capability metrics |

**Invariant:** Localisation never unilaterally publishes, edits or removes Publisher documents, Product details, contractual text, regulated warnings or private messages. The authoritative source owner must validate/approve changes and retain the canonical revisions. A translation is not automatically faithful, legally effective or safe merely because a machine produced it.

## Conceptual native lifecycle

1. **Register locale resources or request adaptation** from an authorised source capability/application, with stable owner record ID, source revision, source/target BCP 47 language tags and policy/quality expectations.
2. **Plan translation**: check existing approved variants, glossary/translation memory and required specialist review; select native human workflow or one or more configured providers.
3. **Produce candidate translation**: preserve semantic structure, placeholders, directionality, safety labels and provenance; explicitly classify machine/LLM/human output and provider/model/version where known.
4. **Review and approve**: qualified translator/reviewer validates accuracy, completeness, terminology, accessible wording and sensitive/legal phrasing as required.
5. **Handoff**: return a reviewed candidate, target-locale status and source-version binding to the original owning capability; owner decides whether/how to persist and publish.
6. **Maintain**: source updates invalidate or mark downstream variants stale; withdrawn sources require controlled downstream visibility/withdrawal; version/expiry and retranslation remain attributable.
7. **Fallback**: missing/unknown translation resolves to a documented fallback with clear locale indication where needed; do not silently claim source or translated content is authoritative in the wrong locale.

**Proposed states:** requested, queued, translating, candidate, in-review, approved-for-handoff, refused, cancelled, obsolete/source-changed, delivered, failed/unknown. Distinguish *translation approved by Localisation* from *document published by Publisher*. Source revision changes must invalidate review assumptions and handle race conditions.

## Conceptual public contract — inputs and outputs

| Surface | Trusted input | Output and boundary |
|---|---|---|
| LOC-01 Locale capability/resolution | Requested language/region, permitted user/host preference, product support, fallback policy | Effective locale and fallback provenance; no parallel Profile or Configuration preference storage |
| LOC-02 Translation request | Qualified source owner/reference/revision, source/target language, structured fields, constraints and caller | Idempotent translation job reference, validation and refusal/unknown status |
| LOC-03 Terminology and style | Scoped glossary, prohibited terms, tone, market/jurisdiction context, reviewer authority | Versioned terminology resources, conflicts and approved usage |
| LOC-04 Translation provider port | Authorised request, protected content subset, locale pair, provider limits and trust policy | Candidate output, provider/model/version, quota/price, latency, confidence/limitations or failure |
| LOC-05 Review and quality | Candidate, source, quality policy, reviewer identity/assurance, findings | Accepted/rework/refused quality decision with reasons and source revision binding |
| LOC-06 Owner handoff | Approved translation candidate, exact canonical record/revision and target locale | Authorised owner delivery request/receipt; Localisation does **not** mutate private owner records |
| LOC-07 Variant availability | Qualified variant refs, locale and source freshness/version | Published/readable availability *as reported by owner*, stale/unsupported/unknown states, fallback advice |
| LOC-08 Source change and withdrawal | Origin capability committed revision or withdrawal event, version and correlation | Idempotent retranslation/review-invalidated signal, downstream reconciliation status |
| LOC-09 Evidence and operations | Job/provider/reviewer activity, data protection and cost scope | Safe typed events, quality/coverage metrics, retention/disposal and observable unknowns; Audit retains evidence |
| LOC-10 Optional administration GUI | Authorised editor, reviewer, translator and operator context | Queue, glossary, review comparison, coverage, provider/cost/quality dashboard with accessible headless alternative |

These are idealised contract surfaces, **not asserted endpoints or API exports**. Required and optional ports, no-provider behaviour, privacy classification and one-call composition under ADR-0012 remain for a later detailed review.

## Cross-capability relationships

| Cooperating capability | Localisation receives | Localisation supplies |
|---|---|---|
| Publisher | Approved source documents/revisions and desired locale variants; explicit owner validation/publication port | Reviewed translated candidate and source-freshness information; Publisher alone commits published versions and feeds |
| Content Editor | Authorised editor requests, review actions and display locale | Translation workflow/status, preview, terminology and quality warnings; UI owns no authoritative document |
| Product / Marketplace / Commerce | Authorised public text, product terminology, permitted target market and source revision | Candidate translations; source owner retains product facts, pricing and legal offer |
| Configuration / Profile | Locale preferences, precedence and approved host configuration | Supported locale metadata and fallback; never reowns preferences |
| Clock / finance domains | Date/time/currency formatting information through existing owner contracts | Linguistic/context guidance, not competing monetary/date business values |
| Integrations / host | Provider connectors, credentials through safe references, rate/cost constraints | Translation job intent and qualified provider feedback |
| Content Security / Moderation / Legal Compliance | Sensitive-content flags, case restrictions, legally mandated wording and publication constraints | Reviewed translations and provenance; no bypass of source content moderation, statutory notices or required review |
| Audit / Logging / Reporting | Evidence/telemetry contract and reporting configuration | Minimised requests, approvals, failures and coverage/quality data |
| Federation / Search | Approved public locale variants from source owner through published feeds/index port | Locale-related metadata for discovery; no independent publication/dissemination of private translations |

## Provider neutrality, quality and security

Support native human translation and configurable external machine translation/LLM providers; local-only modes when appropriate. Sending content to external services requires an authorised purpose, confidentiality and lawful data transfer, provider terms, retention controls, protected placeholders and secrets, clear input/output provenance, cost/retry limits and failure semantics. Never automatically upload private or regulated content to an external model. Assess translation of legal agreements, age/safety warnings, financial terms and medical/safety instructions with higher review requirements and version-specific specialist approval; machine translation is not a substitute for legal validation.

Use well-established locale conventions (BCP 47 language tags, Unicode, CLDR/ICU as applicable, accessible RTL/bidirectional text and pluralisation). Avoid assuming one national locale maps to a single language. i18n remains mandatory for presentation even when Localisation is absent or disabled. Unknown translation quality and unavailable providers require explicit status, not silent approval.

## Conceptual GUI / navigation and acceptance

Host-owned sidebar may expose a Localisation dashboard with language coverage, source-version divergence, translation queue, side-by-side source and target, glossary, reviewer history, provider configuration/cost and access-controlled quality checks. Publisher's generic Content Editor remains the authoring/publishing UI; Localisation supplies workflow and optional panels, not duplicate Publisher lifecycle screens. WCAG 2.2 AA, internationalisation, accessible RTL and low-bandwidth/headless modes apply.

Suggested acceptance scenarios: standalone one-locale Node with capability absent; translation of Publisher article that cannot go live before Publisher's own authorisation; edited source invalidating a prior approved target; plural/placeholder preservation; untranslated fallback clearly signalled; provider downtime with human alternative; no external transfer of confidential content; legal warning reviewed by qualified human; multiple Nodes/Hubs displaying independently approved locale variants without losing canonical provenance.

## Open decisions

- Is terminology and translation memory independent durable state sufficient for a separate Platform capability, or should parts be packaged as a library?
- Are interface resource bundles centrally controlled or application-owned with Localisation supplying review/tooling only?
- Which content types and review standards require mandatory qualified human approval?
- Which public owner interfaces preserve exact source revision, target locale and approval status without cyclic dependencies?
- How do we avoid stale translated legal notices, misleading prices and unauthorised translated marketplace claims?
- Which specific locale library, translation providers and open formats (e.g. ICU MessageFormat) meet licensing/portability requirements?
- What does the source owner actually publish to Federation/Hubs for multilingual discovery?

## Disposition

Canonical **candidate name is `localisation`**. The empty `translate` candidate is removed instead of retained as a directory or compatibility alias. Catalogue notes document the replacement for historical traceability; use the new name in all active references. No implementation/repository creation or normative ADR change follows from this working conceptual review alone.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not implemented or approved. [Conceptual interface](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

The editor requires translated message keys, accessible bidirectional forms and locale-sensitive presentation; Localisation owns translation process, source domain retains content authority.


## Dedicated conceptual review — 19 November 2026 (draft PR #86)

**Status and evidence:** This supplement is a **proposed** contract refinement under [the review protocol](../../review-protocol.md), not owner sign-off, a published implementation \`CONTRACT.md\`, a governing amendment or runtime acceptance. Initial governing baseline: \`architecture-rules/master\` \`b920ce0d8b361de000a6739a16123dbdc56df7a7\`; blueprint baseline: \`architecture-blueprint-review/master\` \`6dac83a03da8704f7945ee1bc894f2248300445a\`. The owner-approved 17 November rename/scope is retained. No separate \`nuxt-layers/localisation\` implementation repository was found through repository search; no actual target root contract has been verified.

### Classification, implementation choice and minimum state

**Recommended: retain the Platform candidate as a framework-independent, headless workflow/terminology capability with optional Nuxt presentation.** A pure locale parser/formatter is a library, not the justification: the distinct platform lifecycle comprises multi-actor requests, revisions, review qualifications, approval evidence, provider coordination, and translation memory/glossary governance. It is not a general document master, presentation framework, legal interpreter, preference store or new translation provider SDK.

Minimum justified **operational** persistence: translation request/attempts and idempotency keys; owner/source revision and field identifiers; target locale and status; constrained candidate/review metadata; scoped versioned glossaries and optional translation-memory entries; provenance/retention/withdrawal tombstones and owned outbox. Content bodies should be minimised, encrypted where retained, subject to owner-supplied retention and privacy restrictions; record references or approved limited snapshots instead of duplicating complete Publisher/Product documents. Optional derived coverage projections are rebuildable. No separate database, independently deployed runtime, Nuxt Layer or universal locale-preference database is mandated by this conceptual choice.

**Required independent mode:** a single-language host does not require Localisation; an enabled Localisation instance supports manual translation and review with no external provider, including purely host-owned application resource catalogues and source-authorised work. Provider-assisted translation is optional. If no qualified review is available for a policy-restricted category, the request remains pending/refused, not implicitly approved. If required owned persistence or trusted access determination is unavailable, protected mutations fail closed.

### Contract envelope and state model

Use BCP 47 tags (canonicalised without confusing script, region and language), Unicode-safe text, explicit source/target variants and ICU/CLDR semantics when applicable. Source identity is an opaque **owner namespace + tenant/resource ID + revision + field or resource key**, never a pointer to another capability's private table. Protected operations carry resolved trusted tenant/caller/assurance, authorised owner scope, purpose, policy revision, correlation/idempotency reference and Clock-derived timestamps where required. Relevant source metadata includes content type, confidentiality, restrictions, immutable revision token, text safety constraints, placeholders/plural categories, source direction and permitted transformations. No universal request object or mandatory provider-specific DTO is implied.

**Lifecycle:** requested → validated/queued → translating or assigned-human → candidate → in-review → approved-for-handoff / rework / refused → delivered (owner receipt) or failed/cancelled; any stage may be marked **obsolete** when source/policy revision changes. A delivered translation is **not** published. Provider attempts can be pending, completed, refused, timed out or **unknown**; an ambiguous remote outcome is not evidence of completion, and retries must not expose the same protected content to a different provider contrary to policy. An owner may subsequently accept, reject or publish a candidate through its **own** contract and lifecycle. Review signatures bind source revision, target locale, candidate digest, glossary and policy versions, reviewer authority and effective time. An older sign-off cannot be silently reused after material source changes.

### Idealised published inbound contract (proposed)

| Public surface | Authoritative source; input | Requirement and validation / absence behaviour |
|---|---|---|
| **I-01 Resolve supported locales and fallback** | Host's supported locale declarations, Configuration effective site/tenant preference, authorised Profile preference and requested BCP 47 tag | Optional preference sources; distinguish no preference, unsupported locale and invalid tag. Return chosen locale + deterministic fallback path and precedence provenance. Never change preference owners' records. A host with no Localisation still supplies its own i18n defaults. |
| **I-02 Register source and request adaptation** | Publisher, Product/Marketplace or another source owner supplies authorised resource reference, exact revision/field, text or safe structured form, source and requested target locales, sensitivity, intended channel and quality requirements | Essential owner authority, stable revision, tenant and data classification; reject untrusted/unauthorised or changed source, unsuitable target, forbidden transfer or malformed placeholders. Deduplicate scoped idempotency keys; return accepted job or stable refusal rather than falsely completed translation. |
| **I-03 Manage terminology and translation memory** | Authorised language manager supplies tenant/project/source-domain-scoped glossary terms, forbidden equivalents, context, version, approved contributors and reuse restrictions | Optional resources; validate conflicts, revision, permitted reuse and cross-tenant isolation. Absent glossary is explicit, not fabricated guidance; confidential memories are never globally reusable by default. |
| **I-04 Supply provider transport** | Host/Integrations-approved connector port receives minimally disclosed source subset, language pair, policy, limits and protected correlation; returns candidate/provenance or error | Optional and conditional on provider approval, confidentiality, cost, residency and credentials. Provider absence selects permitted human work; unavailable required provider causes pending/refusal. Provider assertion is never quality approval. |
| **I-05 Review or correct candidate** | Authorised reviewer/translating operator supplies candidate revision, source/review snapshot, quality checklist, qualified sign-off, rework/refusal reasons | Essential for policy-gated approvals. Server checks role, reviewer separation where required, assurance, version freshness and structured-text invariants. Unknown qualification fails closed for restricted text; stale review is refused. |
| **I-06 Hand off to owner** | Owner-supplied documented public delivery/validation port accepts approved candidate, exact source revision and target locale; owner returns receipt/denial | Conditional on owner support. No direct writes to Publisher, Product or private records. Missing receipt => delivery unknown; do not claim owner acceptance/publication or automatically retry a non-idempotent owner operation. |
| **I-07 Reconcile changes and withdrawal** | Source owner supplies committed revision, delete/withdrawal, variant acceptance and availability facts by query or event | Required for ongoing freshness when source is versioned. Handle duplicates, order and gaps; missing/late source status is **unknown**, never fresh or published. Apply retention/hold rules; no unauthorised resurrection. |
| **I-08 Effective policy, permissions and time** | Host via trusted caller/Authorisation, Legal Compliance, Privacy, Configuration, Clock and source-owner restrictions supplies effective constraints | Mandatory applicable server permissions and legal/security floors; policy conflicts resolve to the stricter applicable constraint, or fail closed pending qualified resolution. Source data and translated text are untrusted content. |
| **I-09 Task and observability ports** | Host-approved Scheduler/Workflow/Message Queue transport and Audit/Logging/Reporting public intake where configured | Optional delivery mechanisms; essential state transition remains owned by Localisation. A missing optional relay must not forge evidence or lose committed state; persistent outbox required where it emits business events. |

**Validation semantics:** distinguish **invalid** (cannot parse/schema/unsupported), **unauthorised** (deny), **stale** (source/policy/candidate version no longer current), **absent** (no configured resource), **temporarily unavailable**, **unknown** (indeterminate provider/owner result) and **contradictory** (conflicting revisions/authorities). Errors expose stable codes and \`messageKey\`, never sensitive provider payloads. Do not turn a failed dependency into an implicit grant, successful translation or available public variant.

### Idealised published outbound contract (proposed)

| Public surface | Authorised consumer and guarantee | Limits, provenance and disclosure |
|---|---|---|
| **O-01 Locale resolution** | Host UI and eligible services obtain supported locales, effective chosen locale, fallback chain, script/direction hints, resource availability and reasons | Preference source and policy version noted; not a guarantee that target-language content exists or has been published. |
| **O-02 Job result/read model** | Requester, authorised translator, reviewer, owner receive job ID, requested scope, current state, retries/attempt summary, progress, stale/unknown flags and completion receipt | Scoped by tenant/source/role; no cross-tenant leakage, no credential/provider raw trace; version and observed-at timestamps. |
| **O-03 Candidate translation** | Source owner and authorised reviewers obtain structured, source-bound candidate, placeholder/plural verification results, candidate digest, source/target locale, provider/method and limitations | Candidate is **not** verified domain truth, owner approval or public text. Restricted text remains restricted; machine confidence alone cannot authorise publication. |
| **O-04 Quality/terminology result** | Owner, reviewer, editor receive review disposition, qualified sign-off or refusal/rework, glossary versions, terminology conflict and accessibility checks | Binds exact source/candidate/policy revisions, provenance and reviewer qualification; do not disclose protected reviewer identity outside permitted roles. |
| **O-05 Owner delivery outcome** | Originating owner receives approved candidate handoff and idempotent correlation; requester receives accepted/rejected/pending/unknown delivery acknowledgement | Owner controls authoritative variant records and publication. Do not reinterpret a transport ACK as publication. |
| **O-06 Version/availability advice** | Host, Publisher editor, Search/Federation adapters obtain locale coverage and stale/fallback advice | Explicitly label **owner-verified published availability** versus Localisation's own \`candidate ready\`; public consumers see only owner-authorised metadata, with freshness and checked-at. |
| **O-07 Committed events** | Authorised source owners, Audit intake, reporting projections and work coordination receive \`TranslationRequested\`, \`CandidateProduced\`, \`ReviewDecided\`, \`SourceBecameStale\`, \`HandoffRecorded\`, \`GlossaryChanged\` as appropriate | Localisation-owned durable outbox, stable event ID, tenant/owner refs, version, time and minimal payload. At-least-once relay, duplicate/replay tolerant; no claim of distributed exactly-once or owner publication. |
| **O-08 Reporting/export and operations** | Authorised Reporting, administrator and Privacy/export rights workflows obtain bounded coverage, throughput, cost, quality/exception and scoped provenance/export with retention constraints | Missing inputs remain unknown, not zero; aggregate permission/disclosure checks still apply; Audit owns accepted evidence, Logging diagnostic logs, Reporting report definitions and distribution. |

**Commands** request/revise/cancel work, submit/review candidate, manage terminology, issue authorised handoff and acknowledge reconciliation; each validates trusted context, revision preconditions and idempotency. **Queries** return scoped supported locales, resource status, jobs, candidate/review metadata, coverage and provenance with known freshness, redaction and completeness. **Events** report committed Localisation facts only and do not replace synchronous owner validation. Application message catalogues remain owned by their providing layer/host under ADR-0009; Localisation may supply translation assistance and a versioned reviewed resource **export**, without taking ownership of the consuming layer's public \`messageKey\` contract.

### Directional cross-capability contracts and failure modes

| Relationship | Needed from partner → supplied by Localisation | Direction and degradation |
|---|---|---|
| **Publisher / domain source owners** | Authorised text, exact revision, restrictions and owner validation/variant/withdrawal evidence → approved *candidate*, stale notices, provenance and handoff | Localisation consumes owner contract; owner may consume Localisation's service through host composition, **not** mutual package imports. Owner absent: refuse source-specific requests; keep existing jobs unverified. |
| **Content Editor and UI** | Editor submits authorised translation/review actions, renders owner content via its own contract → queue, side-by-side safe candidate, terminology and actionable status | Optional presentation consumer; UI absence means headless commands/queries remain available. |
| **Configuration / Profile** | Effective host/group and personal language preference and permitted scope → supported locale/fallback diagnostics | Preference owners retain values/precedence; missing preference uses declared default, never silent profile writes. |
| **Clock / financial domains** | Trusted instants/time zones or money/tax meanings when needed → text linguistic guidance only | Localisation does not format canonical amounts, calculate exchange rates or select time zones. Unknown monetary/legal context forbids misleading replacements. |
| **Integrations / provider adapters** | Approved connector, scopes, limits, authenticated transport and remote outcome → translation request context, result correlation and safe status | Optional provider port; native human flow available; ambiguous remote response stays unknown and reconciled. |
| **Legal Compliance / Privacy / Verification / Authorisation** | Applicable statutory warnings, disclosure/transfer/retention restrictions, qualified reviewer evidence and server access decision → scoped case/evidence and constraints observed | Decisions remain with their owners. If required clearance or jurisdictional interpretation is unresolved, restricted work fails closed. |
| **Moderation / Content Security** | Safety classification, restrictions and cases → candidate-risk metadata and review traces | Neither machine translation nor Localisation clearance overrides source moderation or public release gates. |
| **Audit / Logging / Reporting / Observability** | Accepted evidence, telemetry and report contracts → minimised committed audit-grade events, diagnostic codes, aggregate-quality/coverage metrics | Delivery is distinct from evidence intake; no logs of secrets/full sensitive source text. |
| **Workflow / Scheduler / Message Queue** | Host-supplied orchestration/timer/relay services → owned task registration, checkpoints and outbox events | Execution mechanism does not own translation decision/outbox; degraded optional queue still leaves durable state and explicit delayed work. |
| **Search / Federation** | Source-owner-approved public variant/visibility/index status → locale mapping hints where authorised | Localisation must not syndicate unpublished content or present its private drafts as available variants. |

### GUI, navigation and accessibility

**Headless core is primary; optional, separable, audience-specific presentation** may provide: (1) translator work queue and assigned tasks; (2) accessible source–target compare/editor with structural/placeholder checks, conflict warning and rework; (3) qualified reviewer evidence/decision screen, independent of source publication; (4) language manager's glossary, variant coverage, locale support and fallback settings; (5) administrator's approved provider scopes, budget/quota, incident/unknown delivery/reconciliation view, privacy retention/export controls. Ordinary content authors should see only contextual translation status and request actions inside Content Editor, not privileged provider or reviewer administration. Tenant administrators must not gain platform-global secrets. Platform operators see restricted operational metadata by explicit authorisation.

Host owns the sidebar's capability entry, routes, integration, branding and per-audience visibility; a capabilities dashboard link is a **representative test application pattern**, not an automatic registration contract. Each page and **each server operation** requires independent resource-aware authorisation, purpose/tenant checks and appropriate assurance. Hidden UI is not security. Presentation-off mode exposes no Localisation pages/components/styles, while all permitted headless services continue. Use Theme Manager's semantic tokens, stable message keys, WCAG 2.2 AA, keyboard/screen-reader accessible bilingual comparison, logical reading order, Unicode bidi isolation, RTL support, plural/gender/context messages and narrow/mobile layouts. The UI must visibly distinguish machine candidates, reviewed candidates, owner-delivered and owner-published variants; empty, stale, permission-denied and provider-unknown states require accessible explanations. Do not introduce a second Publisher authoring/publishing screen.

### Representative contract acceptance scenarios (conceptual only)

| Input/scenario | Required outcome | Authority |
|---|---|---|
| One-locale host, no Localisation | Core host i18n and source content operate without translation runtime | Host/source owner |
| Owner-authorised Publisher revision A translated to Welsh | Scoped job then reviewed candidate; Publisher may separately accept and publish | Localisation review; Publisher release |
| Revision B arrives during review of A | A's review/delivery becomes stale and cannot silently be published against B | Source owner revision; Localisation freshness |
| Machine provider times out after request | Status unknown, bounded reconciliation and no unapproved failover/disclosure | Localisation attempt ledger; provider evidence |
| Confidential content submitted to unapproved processor | Deny before transfer; no private source in logs or metrics | Privacy/Legal policy; server authorisation |
| Unqualified reviewer signs regulated warning | Refuse approval, retain attributable failed decision; specialist clearance remains pending | Legal source owner / qualified review policy |
| Reviewer attempts cross-tenant glossary or job read | Deny at public server contract; avoid metadata leakage | Authorisation, Localisation |
| Identical command replay | Same logical job/outcome or explicit reconciled result; no duplicate paid dispatch by default | Localisation idempotency |
| Invalid BCP 47 tag or changed plural placeholders | Stable invalid/incompatible result and safe diagnostic; no handoff | Localisation validation |
| Source withdrawn or publicly delisted | Mark candidate stale/restricted, notify owning consumer; never republish by translation pipeline | Source owner |
| Search asks for published variant | Return only source-owner-verified public availability, else unknown/fallback advice | Publisher/Product, not Localisation |
| Provider disabled, permitted manual translator available | Continue native review flow without external transfer | Localisation |
| Presentation disabled | No routes/styles; identical protected headless contract | Host composition / Localisation |
| Audit/Reporting consume events | Duplicate-safe typed facts and scoped metrics without assuming authorisation, proof of publication or personal-data transfer | Localisation outbox; Audit/Reporting respective authorities |

### Standards, risks and genuinely open architectural decisions

**Established technical references to evaluate, not adopted library selections:** IETF BCP 47 / RFC 5646 and language-tag matching RFC 4647; Unicode CLDR/ICU for locale-sensitive messages, segmentation, plural categories and numbering; W3C internationalisation and bidirectional text guidance; WCAG 2.2 AA; XLIFF 2.x for portable localisation interchange and compatible message schemas; OWASP ASVS 5 Level 2 and risk-sensitive Level 3. Translation memory exchange formats and MessageFormat 2 may be evaluated for portability and ecosystem maturity. Versioned format migration/round-trip checks, rights over training/reuse and rendering safety are necessary. Cross-border data transfer and jurisdictional wording need specialist Legal Compliance review; a language tag is **not** a legal jurisdiction.

**Decision proposals, not yet owner approved:**
- **LOC-D01 — Retain independent workflow owner:** recommended Platform candidate; separate pure formatting/i18n helpers as libraries, not a second Platform authority.
- **LOC-D02 — Application strings:** host/layer retains source message-key catalogue and version; Localisation offers optional translation/review/export, not central control of every runtime string.
- **LOC-D03 — Human review policy:** mandatory qualified approval for legally binding, regulated, safety-critical and other owner-labelled high-risk resources; normal UI copy may use policy-authorised automation with visible provenance.
- **LOC-D04 — Owner handoff:** immutable source-revision-bound candidate + explicit owner validation/receipt; no unilateral publication and no mutual implementation dependency.
- **LOC-D05 — Provider boundary:** manual native baseline; external processing only through approved provider-neutral ports with scoped confidentiality, transfer/cost policy and ambiguous-result reconciliation.
- **LOC-D06 — Public discovery:** Search/Federation receive only source-owner-verified published language variants; Localisation provides review/coverage hints, never publication authority.
- **LOC-D07 — Durable memory:** tenant/source-scoped, consent/policy-governed translation memory with expiry, correction and erasure; do not default to global re-use.
- **LOC-D08 — Runtime form / standards:** choose concrete library, message schema, import/export formats, versioning and optional Nuxt presentation after portability, maturity, licensing and acceptance evidence.
- **LOC-D09 — Locale precedence:** host declares precedence between permitted application/organisation/individual settings; Localisation resolves against effective supplied settings but never overrides Configuration/Profile ownership.
- **LOC-D10 — Cross-capability verification:** obtain actual public owner contracts, qualified-review policies, events and extension graph before implementation; conceptual compatibility alone is not verified interoperation.

**Remaining work:** owner review of D01–D10; root \`CONTRACT.md\` verification for any subsequently created target repository; external-provider/legal-jurisdiction research; schema/API design and export/version acceptance; tests by CI/user; governing catalogue reconciliation in a separately approved normative PR. This draft is **not conceptually signed off or merge authorised**.
