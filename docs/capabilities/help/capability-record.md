# Help — Capability Conceptual Record

**Status:** Proposed architectural classification and conceptual contract; **owner approval outstanding** (18 November 2026). No dedicated implementation, runtime, root `CONTRACT.md` or acceptance test is verified. This record is **not** a Publisher contract amendment or accepted governing decision.

**Exact directory:** `help`. **Review:** [opening baseline](../../../reviews/help-review-baseline.md), [draft PR #72](https://github.com/nuxt-layers/architecture-blueprint-review/pull/72). Governing `architecture-rules/master` opening SHA `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint opening SHA `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.

## Purpose and classification

Offer a consistent, accessible, version-aware Help Centre and optional contextual assistance on fields, actions, errors, pages and workflows of composed applications. **Proposed classification: Presentation plus an optional, narrowly scoped platform mapping/resolution service, not a second publishing domain.** A distinct package/service is justified only if the reusable governed help-context registry, compatibility rules and version resolution have independent cross-application lifecycle needs; otherwise a host composition with Publisher and Search is sufficient. This classification remains an owner decision (HELP-01).

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
- **HELP-01 — owner decision OPEN:** Adopt **presentation/composition by default**; allow a narrowly scoped, independently owned platform context-mapping service only when a governed reusable mapping lifecycle is demonstrated. Do not create a `nuxt-layers/help` repository or duplicate Publisher based solely on the name.
- **HELP-02 — owner decision OPEN:** Use explicit versioned context descriptors and stable keys in each owning capability's public documentation, not guessed implementation internals. Select governed mapping registry versus host-declared mappings at actual deployment/design time.
- **HELP-03 — owner decision OPEN:** Publisher owns Help documents; Content Editor generic authoring; Search discovery; Help only context resolution/UI, with optional reference registry.
- **HELP-04 — owner decision OPEN:** Adopt security/failure semantics, optional accessible contextual controls and headless-first contract described above, subject to owner approval.
- **Technical investigations:** whether any current host manifests expose usable versioned context descriptors; Publisher document-type `help-article` schema, published search contract, stable deep-link/version semantics, source metadata compatibility, minimum composition under ADR-0012 and cache invalidation details.
- **Implementation alignment:** No verified Help implementation/root `CONTRACT.md` (`nuxt-layers/help` fetch 404); Search root `CONTRACT.md` not retrievable in this review; Publisher contract reviewed from `master`, without claiming tested operation. Published capability contracts, packages, screens and CI must be independently proven later.
- **Acceptance/sign-off:** Proposed, not conceptually accepted. This draft PR requires user decision and pre-merge technical plus architectural consistency check against latest `master`, CI/branch protection and explicit merge approval.
