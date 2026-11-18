# Help — Capability Conceptual Record

**Status:** HELP-01–HELP-04 **owner-approved conceptual direction** (18 November 2026); detailed contract and options remain blueprint proposals, not verified implementation. No dedicated implementation, runtime, root `CONTRACT.md` or acceptance test is verified. This record is **not** a Publisher contract amendment or accepted governing decision.

**Exact directory:** `help`. **Review:** [opening baseline](../../../reviews/help-review-baseline.md), [draft PR #72](https://github.com/nuxt-layers/architecture-blueprint-review/pull/72). Governing `architecture-rules/master` opening SHA `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint opening SHA `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.

## Purpose and classification

Offer a consistent, accessible, version-aware Help Centre and optional contextual assistance on fields, actions, errors, pages and workflows of composed applications. **Proposed classification: Presentation plus an optional, narrowly scoped platform mapping/resolution service, not a second publishing domain.** A distinct package/service is justified only if the reusable governed help-context registry, compatibility rules and version resolution have independent cross-application lifecycle needs; otherwise a host composition with Publisher and Search is sufficient. This conditional classification is approved conceptually under HELP-01; the independent service/repository remains subject to evidence.

### Authority and exclusions

- **Publisher** exclusively owns article/document content, revisions, approval, publication, withdrawal, visibility and canonical addresses. Help may reference only authorised Publisher document identity/revision and confirmed publication status. Content Editor owns reusable generic authoring UI, not Help.
- **Help mapping registry (conditional)** owns stable documented context identifiers, mapping revisions, applicability ranges (capability/app/host version, tenant/site, feature, locale, audience), priority, approved fallback chains and deprecation metadata. This is *referential metadata*, not document content or an access-control policy. If this lifecycle is not required, the host owns declarative mappings and Help remains presentation.
- **Source capabilities** remain authoritative for operations, schema, user-visible errors, permissions, feature existence and documented context metadata. Metadata is explicit, reviewed, versioned and intentionally public; never inferred by scanning private code, route names or fields.
- **Search** owns indexing, query and relevance, while Publisher owns document visibility. Help does not build another generic index.
- **Host/application composition** owns navigation, installed capability/version inventory, active tenant/site/user context, route placement, contextual-help control enablement and dashboard integration.
- **Identity/Authentication/Authorisation** own identity, verified caller context and access decisions; Help must never grant rights or disclose a feature's existence where its visibility is protected.
- **Localisation** may coordinate translation; Publisher still owns authorised published language versions. Configuration/Profile own respective site/tenant and personal preferences; Help owns neither.
- **Audit** owns evidential records; Logging and Observability own operations telemetry; Reporting owns cross-capability analytics. Help may emit minimal safe signals and counts but must not store browsing histories by default.

## Native behaviour and lifecycle

1. Consume a host-supplied signed capability/application/version inventory and source-published context descriptors (stable namespace, identifier, meaning, supported version range, sensitivity and public documentation reference). Validate namespace collisions and provenance.
2. Register or update mappings only through authorised, version-checked changes. A mapping refers to Publisher document IDs/locale variants, not copied content or guessed URLs. Check permitted document type and publication/compatibility.
3. Resolve an authorised request by exact context and version then explicit ancestor/fallback topic; differentiate **exact**, **fallback**, **not documented**, **unsupported version**, **withdrawn** and **unavailable**. Never silently substitute an incompatible old guide.
4. Query authoritative Publisher publication and visibility at read time (or safely reconciled, time-bounded references); return a safe document/navigation reference or an unavailable/no-result response. Do not reveal whether a hidden topic exists.
5. On documented source version changes, mapping changes or Publisher withdrawal, invalidate stale resolutions, preserve revision history and repair broken links/route targets; use source-confirmed events as hints and reconcile against source reads.
6. If optional Search is unavailable, use bounded Publisher-backed topic navigation and exact context resolution; no false claim that comprehensive search is working. If Publisher or required access is unavailable, fail closed for protected topics; static openly licensed fallback help is only permitted through a separately declared, authorised host source.
7. Host may remove all Help UI; core source capabilities remain independently usable. No AI-generated answer, chatbot, external helpdesk or support-ticket lifecycle is presumed. Such integrations require separate security, provenance and owner approval.

**Potential mapping states:** proposed, validated, active, superseded, deprecated, withdrawn. Document draft/published/archived states remain Publisher's. Resolution results do not become authoritative statements about user entitlements or successful actions.

## Idealised public inbound contract

| Surface / origin | Input and required validation | Absence, staleness and authority |
|---|---|---|
| HELP-IN-01 — host context | Trusted tenant/site, caller and effective access context; installed application/capability version, requested locale and stable screen/field/action/error context ID | Required for restricted resolution; reject client-supplied forged tenant/version/permission; unknown context is explicitly unresolved |
| HELP-IN-02 — source descriptors | Versioned public context namespace, identifier, semantics, feature visibility, documentation references, supported version ranges and deprecations from individual capability's approved contract | Conditional by supported feature; reject collisions, unknown owners and stale descriptions; never infer from private source |
| HELP-IN-03 — mapping management | Authorised create/change/retire mapping requests with expected revision, source descriptor reference, Publisher document ID, version/locale/audience rules and idempotency key | Only if independent registry selected; permission and revision conflicts must fail safely; never publish a document |
| HELP-IN-04 — Publisher | Published document/revision, address, safe rendering payload, language variants and visibility/withdrawal results through public Publisher contract | Essential for Publisher-backed help; hidden/missing indistinguishable to unauthorised viewers; deny stale previews |
| HELP-IN-05 — optional discovery | Authorised Search query/results and indexing freshness; optional Metadata taxonomy | Search failure does not break exact topic resolution; results must be re-authorised at source |
| HELP-IN-06 — preferences and translations | Configuration/Profile locale/display choices and approved Localisation variant availability where integrated | Explicit fallback with actual language/version; do not invent translated or approved content |
| HELP-IN-07 — source changes and operations | Publisher committed revision/publication/withdrawal signals; source capability version/descriptor change, optional scheduler/invalidation notifications | At-least-once, duplicated/delayed/unknown possible; signals prompt reconciliation and never themselves grant access |

The host must supply permission decisions through public Authorisation interfaces. Context descriptors are metadata, not a replacement for an independently usable source `CONTRACT.md`.

## Idealised public outbound contract

| Surface and consumer | Output, provenance and guarantee |
|---|---|
| HELP-OUT-01 — contextual resolution (host UI and source GUIs) | Safe topic reference, declared match grade (exact/fallback), mapped source/context and compatibility version, locale, confirmed publisher revision/publication provenance, route/deep-link hint and freshness; or indistinguishable restricted/not-found outcome, incompatible/unknown/unavailable reason as authorised |
| HELP-OUT-02 — Help Centre model (host UI) | Authorised topics, sections, breadcrumbs, content references and available locale/version choices from Publisher and optional Metadata/Search; content ownership remains Publisher |
| HELP-OUT-03 — management queries | Authorised mapping version/history, unresolved contexts, broken/revoked references, coverage, review status and reconciliation issues; no private source schema |
| HELP-OUT-04 — command receipts (administrators) | Accepted/rejected/committed mapping changes, revision, conflict/idempotency status and recovery instructions; no claim that document publication succeeded |
| HELP-OUT-05 — committed mapping events (optional subscribers) | `help.mapping.changed/withdrawn` with scoped identifier, revision, correlation, timestamp and no sensitive content, emitted only after Help-owned mapping state changes via durable outbox where applicable; at-least-once and replay-safe |
| HELP-OUT-06 — operational/evidence projections | Minimal pseudonymised coverage/reconciliation metrics to Reporting, technical diagnostics to Logging/Observability and necessary accountable changes to Audit through its published intake; consumers must not infer individual reading behaviour or entitlement |

**Interaction model:** Commands are needed *only* for a governed mapping lifecycle. Queries are necessary for exact resolution, topic browsing and authorised mapping administration. Source change events and Help's own committed mapping events must be idempotent, replay-safe and eventually reconciled; no exactly-once distributed promise. If classified as presentation-only, **no Help-owned commands, durable state, outbox or domain events** exist: its outputs are derived UI/read responses from Publisher, Search and host-configured descriptors.

**Shared invariants:** authorised site/tenant scope; caller and assurance level; owner namespace/context ID; source/application/version and mapping/document revisions; requested/effective locale; purpose/audience; policy/version and Clock effective time where relevant; idempotency/correlation for changes; source provenance and freshness. Inputs are validated at runtime, tenant-isolated, least-privilege and version-compatible. Missing, withdrawn, ambiguous or contradictory data is not success. Public responses contain only permitted metadata. Do not impose a universal request shape.

## Cross-capability relationships and reciprocal contract boundaries

| Cooperating owner | Help receives | Help provides / relationship |
|---|---|---|
| Publisher (essential) | Authorised published content/revision/addresses and withdrawal confirmation | Scoped document references and access intents, never content publication; [reciprocal](../publisher/capability-record.md) |
| Content Editor (optional administration) | Generic Publisher document management presentation | Host-owned filtered Help article workspace and mapping links; [reciprocal](../content_editor/capability-record.md) |
| Search (optional) | Authorised index results, ranking, freshness | Search scope and safe Publisher references; never a second index; [reciprocal](../search/capability-record.md) |
| Application Compositions (essential host integration) | Current app/capability versions, contexts, routes, verified audience and enablement | Reusable Help Centre/sidebar entry and optional field-level contextual controls; [reciprocal](../application_compositions/capability-record.md) |
| Identity/Authentication/Authorisation (essential for protected help) | Server-verified site/tenant subject, assurance and access decisions | Scoped access requests and non-sensitive accountable activity; never grants |
| Individual domain capabilities (conditional) | Explicit source-owned stable help descriptors, user-facing error/operation semantics | Context resolution and approved documentation references; no hard source import |
| Localisation, Configuration, Profile (optional) | Translation-ready variants, scoped locale settings and preference | Coverage and missing/obsolete variant references; no replacement preference records |
| Metadata, Media, UI, Theme Manager (optional) | Taxonomy/assets/accessible rendering and semantic theme tokens | Presentation integration; existing owners retain their records |
| Audit, Logging, Observability, Reporting (conditional) | Published logging/evidence/aggregation intake contracts | Mapping change evidence (Audit), safe diagnostics (Logging/Observability), aggregated usage/coverage (Reporting); no raw sensitive browsing history |
| Scheduler, Message Queue (conditional) | Reconciliation scheduling and event delivery | Idempotent version/withdrawal repair; only when persistent mapping lifecycle chosen |
| Privacy, Legal Compliance, Content Security (conditional) | Retention/disclosure restrictions and safety findings applicable to documents | Enforce restrictions at Help boundary; Publisher retains original content action |

All relationships use public contracts and host-supplied ports, with explicit directed edges; referencing a capability does not require a package import. Avoid Publisher↔Help circular coupling: Publisher never calls Help as a required dependency, and Help consumes Publisher events/reads through host wiring.

## Presentation and GUI — application test-template pattern

The host owns a **Help** sidebar item or capability-dashboard card and routes to an accessible **Help Centre** (search input, version/locale filter, categories, results, article viewer, breadcrumbs and source version banner). Contextual **? / Help** controls appear beside documented screens, sections, fields, buttons, errors and workflows only where supported and permitted; use a lightweight side panel/dialog without loss of unsaved form state, and offer a full-page topic route. Provide keyboard access, focus restoration, descriptive text labels and screen-reader announcements; never rely on icon-only or hover-only hints.

An authorised administrator may have a **Help coverage dashboard** (unmapped/stale contexts, broken refs, compatibility matrix), **topic mapping editor** (select source descriptor and Publisher document/version with preview) and **review/history**. Actual article create/edit/publish tasks delegate to Content Editor and Publisher; do not build a duplicate rich text editor. Separate platform operator and tenant scopes. Support WCAG 2.2 AA, BCP 47/CLDR, RTL, responsive layout and Theme Manager tokens. The host controls UI opt-in; a headless resolution interface, if selected, remains consumable independently of screens. No work is authorised in the application test template.

## Security, privacy, external services and compliance

Server-side authorisation governs every restricted query/change and Publisher content view. Mask hidden topic existence; disable unsafe link previews and enumeration; treat metadata/provider text as untrusted; render only Publisher's safe structured trees. Cross-tenant leaks can arise through search indexes, URL titles, caches, coverage views, analytics and fallback chains: partition/recheck all. Respect UK GDPR/GDPR purpose minimisation, lawful retention, access/erasure and jurisdictional legal requirements as applicable; never collect user queries or fine-grained reading telemetry by default. Audit administrative mapping changes without logging protected content. Avoid provider lock-in: optional external search/translation/AI assistants require explicit contracts, permissions, export/withdrawal and disclosure controls. Security baseline: OWASP ASVS 5 L2 (L3 for critical contexts), WCAG 2.2 AA, host CSP and safe external-link handling.

## Conceptual acceptance examples

| Input | Expected behaviour and outward result | Owner |
|---|---|---|
| Known version/context + authorised published topic | Exact topic reference and safe content, supported locale/revision | Help maps; Publisher publishes |
| Valid context but older feature version | Only approved compatible article; otherwise explicit unsupported/fallback | Source metadata + Help |
| Unmapped documented control | Clear no-context-help outcome and administrator coverage warning | Help/host |
| Private tenant topic requested from another tenant | No existence disclosure, no cached/search leak | Authorisation/Publisher; Help enforces |
| Withdrawn Publisher article | Mapping stops resolving, index repaired; no stale preview | Publisher state; Help reconciles |
| Publisher offline | Fail closed for restricted help; explanatory unavailable state, preserve host task | Publisher + Help |
| Search offline | Exact context link and bounded topic browsing still work | Help/Publisher |
| Repeated mapping update with same key | One committed revision and replay-safe receipt; conflict on mismatched revision | Help registry if selected |
| Locale missing | Explicit approved fallback, not fabricated translation | Publisher/Localisation |
| User changes theme / keyboard navigates help panel | Accessible controls, preserved unsaved work and focus restoration | Host presentation |
| Unsupported external AI/helpdesk request | Unsupported; no unapproved provider invocation | Host/Help |

## Decisions and evidence register

- **Established:** Publisher `master` root `CONTRACT.md` publishes versioned document types, safe rendered documents, audience checks and headless access; Content Editor is its designated generic UI. Architecture Rules Capability Standard classifies presentation separately and requires one-way public contracts, runtime validation, separable UI and no duplicate ownership. Accepted ADR-0017/0018 status reconciled on governing `master`; no extra powers inferred.
- **Existing agreed blueprint direction:** Help aims for a version-aware Help Centre and contextual controls; this 16 November candidate record was not owner approval of a standalone service.
- **HELP-01 — OWNER APPROVED (18 November 2026):** Adopt **presentation/composition by default**; allow a narrowly scoped, independently owned platform context-mapping service only when a governed reusable mapping lifecycle is demonstrated. Do not create a `nuxt-layers/help` repository or duplicate Publisher based solely on the name.
- **HELP-02 — OWNER APPROVED (18 November 2026):** Use explicit versioned context descriptors and stable keys in each owning capability's public documentation, not guessed implementation internals. Select governed mapping registry versus host-declared mappings at actual deployment/design time.
- **HELP-03 — OWNER APPROVED (18 November 2026):** Publisher owns Help documents; Content Editor generic authoring; Search discovery; Help only context resolution/UI, with optional reference registry.
- **HELP-04 — OWNER APPROVED (18 November 2026):** Adopt security/failure semantics, optional accessible contextual controls and headless-first contract described above, subject to owner approval.
- **Technical investigations:** whether any current host manifests expose usable versioned context descriptors; Publisher document-type `help-article` schema, published search contract, stable deep-link/version semantics, source metadata compatibility, minimum composition under ADR-0012 and cache invalidation details.
- **Implementation alignment:** No verified Help implementation/root `CONTRACT.md` (`nuxt-layers/help` fetch 404); Search root `CONTRACT.md` not retrievable in this review; Publisher contract reviewed from `master`, without claiming tested operation. Published capability contracts, packages, screens and CI must be independently proven later.
- **Acceptance/sign-off:** HELP-01–04 conceptual direction approved; subsequent elaborations and package choices remain proposed. PR remains draft and requires final consistency checks, CI/branch protection and explicit merge approval.

## Approved-direction elaboration — published contracts, standards, libraries and GUI (18 November 2026)

**Approval:** Owner expressly approved HELP-01–HELP-04. The additional details in this section are **recommended for review**, not new automatic approvals or published implementation APIs. Baselines rechecked: governing `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master` `02b2302e90e94680928abb9ac5553e81c9e67a53`. This branch was six commits behind new `master` at inspection; reconciliation is mandatory before any merge.

### Human-readable consumer contract: who provides what

- **Ask Help for a topic:** Host submits a documented context key (for example `inventory.item.quantity`), installed source/version, locale and authenticated scope. Help resolves a compatible, authorised Publisher topic and returns its safe reference, match quality, effective version/locale and publication freshness, or an explicit unavailable/non-disclosing result. A context lookup is not an access grant.
- **Browse Help:** Host asks for permitted categories, article references, breadcrumbs, languages and versions. Help assembles a view from Publisher and optional Search/Metadata; it cannot create/approve content.
- **Maintain mappings (optional governed registry):** Authorised operator submits a source-owned stable descriptor, Publisher document reference, scope/version range, expected mapping revision and idempotency key. Help validates and returns committed mapping revision or a conflict/refusal; emits a source-owned mapping event only after persistence. Without a registry, equivalent mappings belong to host configuration and there is no Help-owned persistence/event.
- **Author help articles:** Authorised editor uses Publisher's registered document type and Content Editor's generic UI; the Publisher contract, not Help, returns article revision, preview, publication and lifecycle status.
- **Observe quality:** Help exposes aggregated mapping coverage, broken/stale references, unavailable languages and reconciliation status. Reporting may request scoped, minimised projections; neither Help nor Reporting should silently record individual help-reading trails.

**Dependency direction and degraded modes:** Publisher's published-content and access contracts are essential to Publisher-backed help; host caller/version and permitted context are essential for restricted help. Search, Metadata, Localisation, configuration-driven appearance and Reporting are optional for basic exact resolution. A disabled Search means no full-text results but direct topics still work. A disabled mapping registry means host-declared mapping only. If Publisher status/permissions are unknown, protected content is unavailable. Help must never reverse-call Publisher from a required Publisher dependency or read private stores.

### Logging / Audit / Reporting reciprocal public interfaces

| Partner owner | Help sends through partner's proposed public intake | Partner returns or makes available | Exclusions |
|---|---|---|---|
| [Logging](../logging/capability-record.md) | Severity-coded mapping resolution failure, stale reference, dependency outage, invalid descriptor and latency/correlation values; redacted tenant/subject and no raw query/article bodies | Accepted/dropped/failed diagnostic status and correlation for operational troubleshooting, where supported | Log delivery is not a business action, proof of publication or Audit evidence |
| [Audit](../audit/capability-record.md) | Classified producer-authenticated event for mapping create/change/withdrawal, privileged overrides or sensitive administrative actions with trusted actor, tenant, action/outcome, mapping revisions, source ID, event ID, occurrence time and correlation | Evidential intake accepted/pending/rejected/unknown reference, authorised verification/review result | Source owns mapping change; Audit owns custody and verification. No duplicate Publisher publication audit and no wholesale raw logs |
| [Reporting](../reporting/capability-record.md) | Authorised aggregate counts: documented/unmapped contexts, outdated/incompatible topics, broken links, missing locale variants, reconciliation health; scoped period and provenance/freshness | Authorised report definition/execution/result, aggregation/disclosure safeguards, status, freshness and lineage | Reporting is not the mapping source or a source-document owner; small-cohort disclosure and raw personal clickstream disallowed by default |

An operational logging outage must not alter a valid help lookup. Significant accepted mapping changes must have a reliable Audit evidence hand-off/reconciliation policy; a queued Audit submission is not an accepted evidential record. Reporting failure cannot stop core Help. For a presentation-only deployment, source owners and host own their own audited administrative changes, and there are no Help-owned domain events.

### Standards and established patterns to reuse

| Standard | Value to Help | Architectural qualification |
|---|---|---|
| [W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/) AA and [WAI-ARIA APG](https://www.w3.org/WAI/ARIA/apg/) | Keyboard, focus, labels, disclosure, popover/dialog semantics, screen reader support | Use appropriate dialog for interactive help; avoid an interactive tooltip antipattern |
| [IETF BCP 47 / RFC 5646](https://datatracker.ietf.org/doc/rfc5646/) with Unicode CLDR / ECMA-402 | Language tags, effective/fallback locale, RTL/layout and formatting | Keep preference and translation ownership with existing capabilities |
| [JSON Schema 2020-12](https://json-schema.org/draft/2020-12) | Versioned validation of public help-context descriptors and mapping declarations | Do not impose an undocumented universal ecosystem manifest |
| [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html) | Reuse compatibility ranges where source packages actually follow SemVer | Documentation/content revision and installed application version are separate dimensions |
| [OASIS DITA 1.3](https://www.oasis-open.org/2016/02/01/members-approve-dita-1-3-as-oasis-standard-for-authoring-and-publishing/) | Established topic modularity, reuse, indirect topic keys, navigation and conditional variants | Study as a design reference; do not require DITA XML or install a second content system |
| OWASP ASVS 5.0 + existing platform privacy and retention rules | Tenant isolation, authorisation, input validation, safe output and caches | No standards statement by itself proves deployment compliance |

Proposed help-content metadata should make context keys and audience visible without leaking sensitive configuration, and may link to schema.org `TechArticle` or `HowTo` only when the Publisher/SEO owners choose appropriate structured data. Do not reinvent route/URL ownership.

### Commercially permissive OSS selection, not a mandatory dependency list

Candidate packages with public permissive licence evidence (licence, maintainership, dependency tree and API must be checked/pinned at implementation selection):

| Candidate | Licence | Role and decision |
|---|---|---|
| [Ajv](https://github.com/ajv-validator/ajv) | MIT | JSON Schema validation for stable context metadata when JSON Schema is adopted; use existing platform runtime validation otherwise |
| [@floating-ui/vue](https://github.com/floating-ui/floating-ui) | MIT | Optional accessible placement of help popovers/side panels; does **not** supply dialog keyboard semantics by itself |
| [unified](https://github.com/unifiedjs/unified) / [remark](https://github.com/remarkjs/remark) | MIT | Documentation processing/checking tooling only if needed for metadata import; do not bypass Publisher safe-tree rendering |
| [MiniSearch](https://github.com/lucaong/minisearch) | MIT | Small local/offline authorised index **only when Search owner selects it**; maintenance cadence should be reassessed |
| [FlexSearch](https://github.com/nextapps-de/flexsearch) | Apache-2.0 | Alternative embedded search engine for Search owner, not a second Help index; check locale/tokenisation requirements |
| [ofetch](https://github.com/unjs/ofetch) | MIT | Optional request client if built-in Nuxt/Nitro facilities do not suffice |
| [Nuxt UI](https://github.com/nuxt/ui) | MIT | Optional presentation components only if interoperable with existing `ui` and Theme Manager; avoid parallel theming/component systems |

**Prefer existing Nuxt, shared UI, Publisher and Search functionality before any added package.** All packages are candidates, not dependencies or validated runtime versions. No closed-core, hosted-mandatory or freemium product is required. Recheck SPDX/NOTICE and transitive licences, provenance, vulnerability status and maintenance before adoption; permissive source licence alone does not ensure suitable maintenance or no operational lock-in.

### Specific host GUI layout and routes

The actual [application-test-template](https://github.com/nuxt-layers-test/application-test-template) currently exposes a shared shell: `/` home; `/admin` dashboard; `/theme-manager` for a capability; collapsible responsive sidebar, top bar Appearance control and authentication-status placeholder. Its `nuxt.config.ts` currently composes Theme Manager in `test` mode, explicitly **not** safe for public deployment. No new Help host route is claimed implemented.

Proposed host-owned navigation when Help is selected:

1. **Sidebar Help → `/help`**: Help dashboard with search, suggested topics, capability/category tiles, current version/language display, last-used context only if deliberately kept in non-sensitive session state; no behavioural tracking by default.
2. **Help Centre → `/help/topics` / `/help/topics/:topic`**: browse/search, results and safe Publisher article rendering with breadcrumbs, compatible version and locale/fallback banner; canonical Publisher address handling, not duplicate document ownership.
3. **Context controls on source screens**: labelled Help button adjacent to permitted inputs, operation/error guidance, optionally opens dismissible side panel with topic summary and link to full article. Restore focus and preserve unsaved forms. A text label must remain available; no hover-only functionality.
4. **Admin dashboard → `/admin/help`**: coverage by capability/version/locale and broken mapping alerts, with separate authorised mapping registry screens `/admin/help/mappings` and `/admin/help/mappings/:id` only if registry is deployed.
5. **Author help article**: `/admin/content-editor` (illustrative host route) filtered to Publisher's registered Help document type; no duplicate Help editor. History/publication action belongs to Publisher via Content Editor.
6. **Operations/reporting**: limited links from admin Help dashboard to owned Audit, Logging and Reporting screens; host navigation/access boundaries remain in force.

A small application can show only `/help` and contextual links; mappings may be static host declarations. An enterprise host may show the authorised coverage/mapping administration. Headless consumers may omit every screen, reading the public resolution contract only. All presentation remains reusable, themed, responsive, internationalised and WCAG 2.2 AA.

**GUI acceptance:** sidebar links only when Help is selected; 404/disabled state when not; user and administrator see different authorised navigation; keyboard/help panel focus and close operate properly; theme and locale changes do not invalidate document authority; offline Search preserves contextual access; Publisher/permission outages fail closed; wrong-tenant, wrong-version and withdrawn documentation never display; no deployment of unauthenticated Theme Manager test mode.
