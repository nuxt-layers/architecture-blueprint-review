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


## Reciprocal conceptual note — Metadata review (19 November 2026)

**Status: Proposed in [Metadata draft PR #95](https://github.com/nuxt-layers/architecture-blueprint-review/pull/95), not an approved implementation contract or completed review of this adjacent capability.** [Metadata conceptual contract](../metadata/capability-record.md#dedicated-conceptual-review--metadata-19-november-2026).

Metadata owns stable term identifiers, reference labels and classification relationships; Localisation may supply translated term labels and review status via public interfaces. A translated display string is not a new term or an authorised assignment; absent translation uses a declared source-locale fallback without cross-tenant leakage. Conceptual cooperation is optional and host-wired through public contracts; avoid circular required package dependencies.
