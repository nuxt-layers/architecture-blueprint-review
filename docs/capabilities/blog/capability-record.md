# Capability Record — Blog

**Status:** Proposed Publisher-backed composition and optional presentation; classification awaiting project-owner approval. No independent Blog implementation or runtime service is asserted.  
**Review date:** 15 November 2026.  
**Governing baseline:** `nuxt-layers/architecture-rules` `master` `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.  
**Blueprint baseline:** `nuxt-layers/architecture-blueprint-review` `master` `a3320121cc897fb706efb99a7b52c922385df55e`.  
**Test-template baseline:** `nuxt-layers-test/application-test-template` `master` `8b7b142b84b5ec2379d4e2e727914fe344187d64`.  
**Primary evidence:** Governing [catalogue](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/catalogue.md) explicitly calls `blog` a Publisher document type and presentation unless separate domain state is shown; its working [catalogue](../../capability-catalogue.md) and [register](../../capability-register.md) retain candidate status. Verified `nuxt-layers/publisher` root `CONTRACT.md` on `master` provides the canonical content lifecycle and read/write operations. Direct `nuxt-layers/blog` repository lookup returned 404; absence of a standalone public contract is not evidence of hidden implementation. Other candidate implementation contracts are unverified.

## Capability Name

**Blog** — a reusable, site-scoped editorial and public-reading experience assembled from published capabilities; not a second publication authority.

## Status: Available, Installed, Configured, Operational, Enabled, Authorised and Proposed

**Proposed** conceptual contribution. Independent repository, installation, configured deployment, operational behaviour and authorisation evidence: **unverified**. Publisher's existing published contract is verified evidence of available *Publisher* operations, not of an implemented Blog composition.

## Purpose

Enable site owners, editors, contributors and readers to create and discover blog articles through an accessible, configurable site experience while relying on Publisher for canonical documents, versions, addresses, approvals, publication, public listings and feeds. Blog-specific ordering, editorial landing-page composition and reader navigation are presentation or application choices unless an additional independently authoritative rule is demonstrated.

## Classification

### Architectural classification and ownership gate

| Gate | Finding |
|---|---|
| Distinct responsibility | A reusable article-focused authoring and reading journey, not independent content management |
| Authoritative records | **None owned by Blog** in the recommended design: Publisher owns documents, revisions and publication status; Metadata owns reusable taxonomies when present; media owns image metadata; source capabilities own any social or commerce facts |
| Independent rules/lifecycle | None justified beyond host-registered Publisher article-type validation and site/presentation rules; no Blog state machine |
| Presentation alternative | **Preferred**: publisher document-type specialisation plus optional Blog presentation and host composition |
| Domain-service alternative | Rejected provisionally: duplicates Publisher unless a later substantiated business invariant cannot live in Publisher or a cooperating owner |
| Implementation kind | Application composition / reusable presentation contribution. **No independent repository or Nuxt capability layer approved**; a reusable package is optional and requires a demonstrated second consumer |
| Persistence | **None by default.** Host configuration/presentation preferences remain with their established owners. Optional caches are derived and must be justified, scoped and invalidated |
| Contract dependencies | Publisher essential for article state; Authorisation essential for protected operations via Publisher; other relationships optional or conditional through published contracts |
| GUI | Principal deliverable: reader-facing and editorial views, separable by audience; host owns routes, sidebar, navigation and branding |
| Disposition | **Proposed reclassification:** retain Blog as Publisher-backed document type and presentation/composition, not an independent Domain owner |
| Approval/implementation | Classification and contract are proposed, not approved; Publisher root contract is verified, Blog implementation is not |

The governing catalogue already favours this outcome. The working register's `Domain candidate` label describes an unreviewed candidate, not authority to duplicate records. No accepted ADR contradiction is identified, but a separate Domain implementation would conflict with existing ownership without new evidence.

## Dependencies

**Essential:** Publisher's approved type registration, article and public read/list/feed contracts; host-resolved site and caller context; Publisher's required Authorisation and persistence providers. Blog does **not** directly own those providers or replicate their decisions.

**Conditional:** Workflow for article approval when type policy requires it; Scheduler for scheduled publication through Publisher; Message Queue for distributing Publisher's committed outbox facts; Configuration for site editorial settings; Legal Compliance and Privacy for applicable constraints; SEO and Search for discoverability; Metadata for governed taxonomy; Media/Storage for approved article images; Profile for permitted author display; Clock for temporal formatting; Integrations for authorised syndication.

**Optional:** Content Editor and `ui` for standard editing/rendering; Comments Engine for comments/moderation; Notifications for contributor alerts; Translate for translations; Reporting for cross-site performance; Audit for accountable evidence; Logging/Observability for operational diagnostics.

Dependencies are conceptual interface relationships, not automatically package dependencies; host composition must retain a jointly acyclic graph and respect ADR-0012's budget.

## Optional integrations

External blogging platforms, social syndication, email campaigns and analytics are optional. Integrations owns connection credentials, provider discovery, delivery/retry and external mappings. In the recommended mode Publisher remains authoritative for platform-hosted articles; provider acknowledgements do not prove publication unless confirmed. A provider-authoritative or bidirectional-authority mode would require an **explicit separate decision**, ownership mapping, import reconciliation, conflict handling and reversal plan. No implicit fallback, mirror-as-master or automatic cross-site publication.

## Version

No independent Blog package, manifest, schema or contract version verified. The proposal is a conceptual review revision; existing Publisher contract versions and host type definitions continue to govern real consumers.

## Availability

Publisher contract is published; Blog feature delivery is not independently established. Missing Publisher means article management and publishing unavailable; public UI may show a controlled unavailable state but cannot claim content was published. Optional absent integrations degrade only their own features. Protected operations fail closed for absent or failed authoritative access, site or policy resolution.

## Capabilities offered

**Proposed presentation/composition duties:** site-specific Blog home and latest articles; chronological, taxonomy and author-scoped listings (subject to actual published query capabilities); article detail; linked previews for authorised editors; editorial dashboard; create/edit/review/publish via Publisher public actions; status/history; link-impact warnings; optional accessible searching, categories, subscriptions, comments and sharing as supplied by their respective owners. Support empty, withheld, stale, partial and provider-unavailable states. No independent Blog-owned commands, data events or CRUD API are justified.

### Conceptual information and lifecycle

An article is a **Publisher document of a host-registered type**, for example `post`, not a Blog record. Article content fields may include plain title, summary, publication settings, body in the governed safe rich-text Document profile, editorial metadata and authorised media references. Exact field schema is host-registered and must pass Publisher's field/type contract. Publisher owns `draft → submitted/approved (where configured) → published/scheduled → unpublished/archived/deleted` transitions and revisions; Blog renders the available states without defining replacements. External taxonomy, person, image and engagement references remain owned by their source. Slug/address, feed and redirect ownership remain Publisher/SEO as their contracts define.

## Configuration

Site chooses enabled Blog views, article type, content collections, listing options, featured-item policy, visual presentation, locales and optional modules within published extension points. Publisher document types are **code registered by the host** in its verified current contract, not arbitrary runtime configuration; new runtime type registration needs a separately approved Publisher contract change. Configuration owns approved site settings; host owns routes, branding and navigation; Theme Manager alone determines effective visual tokens. User preferences cannot relax editorial permissions or lawful disclosure controls.

## Idealised conceptual public input interfaces

These are **proposed Blog composition/presentation inputs**, not newly implemented Blog APIs. Each requires tenant/site, authenticated or anonymous viewer, source version and appropriate permissions where material.

| Source / type | Information or command; purpose | Authority and validation | Requirement; failure |
|---|---|---|---|
| Host / configuration and commands | Site selection, article-type mapping, nav/layout choices, list/preview/edit intents | Host owns routing; Configuration owns settings. Validate allowed type, site and approved settings; intent is not permission | Essential host context; reject unknown site/type and fail safely |
| Publisher / source facts and queries | Published article, listing, addresses, feed, history, backlinks, editable schema, permitted actions; editorial and reader content | Publisher owns versions, state and URL. Preserve scoped queries, version and public/private distinction; do not infer publication from local view | Essential; unavailable/hidden must not expose drafts or pretend success |
| Publisher / commands | Create, save, submit, publish/schedule, unpublish, archive, restore, delete with expected revision and approved link acknowledgement | Publisher alone validates transitions, type and authorisation; UI forwards intents, never mutates authoritative state | Conditional on editorial UI; conflict reload, not silent overwrite |
| Identity/Authentication/Authorisation / context | Trusted caller, group/site membership, assurance and resource decision via host/Publisher | Source capabilities retain authority; display controls are not access control | Essential to protected actions; fail closed |
| Workflow / evidence | Approved version/digest and decision state when article type mandates approval | Workflow owns approval path; Publisher validates exact revision and controls publication | Conditional; remain pending if unavailable |
| Metadata / source facts | Approved category, tag or taxonomy identities and display labels | Metadata owns taxonomy; validate tenant, active scope and public disclosure | Optional; hide/filter unavailable taxonomy without relabelling articles |
| Media/Storage / source facts | Allowed image identity/variant, safe address, alt metadata and access | Media owns image metadata; Storage owns bytes; Publisher validates asset references, alt and safety | Conditional on images; refuse unsupported assets; no broken privileged URLs |
| Profile / source facts | Approved author attribution/display name | Profile owns personal data and visibility; never derive display name from opaque ID | Optional; use safe byline fallback or omit |
| SEO/Search / facts | Public search/discovery/redirect metadata and derived indexing status | Publisher remains source of publication; SEO/Search own derived artefacts | Optional; stale or unavailable search cannot override access |
| Comments Engine / commands and reads | Public comments, submit/moderate intent and statuses | Comments Engine owns posts, moderation and abuse controls | Optional; explicitly disabled/unavailable |
| Privacy, Legal Compliance / policy | Retention, consent, disclosure, legal holds, jurisdiction rules | Their policy authority remains independent; enforce before display/action where applicable | Conditional mandatory constraints; fail closed on material uncertainty |
| Integrations / external evidence | Provider discovery, authenticated sync/receipt, mapped external resource and reconciliation | Provider facts require verified origin and freshness; no assumed publication | Optional; queued/unknown/confirmed remain distinct |
| Clock / fact | Authoritative effective instant, time zone and locale formatting | Clock controls semantics, Publisher controls scheduled state | Conditional; never turn formatted time into confirmation |

## Idealised conceptual public output interfaces

| Output and consumer | Legitimate meaning and authority | Lifecycle/provenance/disclosure |
|---|---|---|
| Public Blog homepage/article/list view → reader/application | Authorised **presentation** of Publisher-confirmed public content, not a separate canonical article | Source document ID/type/version/site, publication visibility, freshness; no private drafts |
| Article-focused editorial dashboard → editor | Aggregated Publisher-owned state plus permitted actions, pending approvals and link warnings | Authorised per document and site; unavailable and partial labels; no false permission grants |
| Editor interaction result → editor/host | Publisher's accepted/rejected/version-conflict outcome relayed faithfully | Distinguish command submitted, accepted and definitively committed; preserve correlation and error |
| Optional taxonomy, author and media facets → reader | Joined presentation only; no new ownership of person, image or classification | Each source's permission and data-freshness rules; suppress forbidden joins |
| Navigation and screen definitions → host | Proposed Blog entry and public/editor routes, messages, component surfaces and access hints | Host accepts/overrides/omits; server authorisation independently mandatory |
| Presentation exports / feed links → reader, SEO, integrations | Links to **Publisher** published feed/listing and canonical address outputs | Source revision and site, not a Blog-created export or new content master |
| Operational diagnostics → Logging/Observability | UI/render/adapter failures and correlation; not evidence of business publication | Minimal structured signals, no personal content or secrets |
| Accountable action attribution → Audit | **Publisher** and source capabilities produce authoritative event/evidence; Blog may report UI attempt/correlation only | Audit owns custody; never claim a UI click proves a committed transition |
| Reporting-ready display aggregates → Reporting | Derived counts/engagement presentation only, with source IDs/coverage | Reporting owns defined reports, Publisher owns content; unknown source status stays unknown |

### Commands, queries and events

**Commands:** Blog introduces no new authoritative domain command. Its authoring screens forward authorised Publisher create/transition/delete operations with the verified contract's `expectedVersion` and `acknowledgedLinks` requirements; optionally route comment/moderation commands to Comments Engine. Replayed user intents require owner-enforced version and idempotency semantics; a response must not imply distributed exactly-once handling.

**Queries:** Blog composes Publisher `getPublishedDocument`, `listPublishedDocuments`, `getPublisherFeed`, `listPublisherSitemapEntries`, public path resolution and privileged document/history/backlink/type reads, and conditional owner-provided taxonomy, image and comment reads. Existing Publisher listing supports documented equality filters and limits; richer full-text queries and aggregation require Search or a **published contract extension**, not assumptions about Publisher.

**Events:** **No Blog-owned business events** in this disposition. Publisher owns events for its committed document changes and its transactional outbox. Consumers of publication events use source ID, revision, tenant/site and idempotent processing; redelivery or out-of-order arrival cannot create an alternative article authority. UI telemetry, where justified, is diagnostics rather than a document event.

### Shared context and invariants

Host supplies trusted tenant/site, viewer identity/assurance, source owner and resource identifiers, correlation/operation identity, document version, state, effective time and applicable policy. No universal request object is proposed.

- Never create a second source of article truth or a Blog-owned publishing lifecycle.
- Public reads expose only Publisher-authorised published material; hidden and missing must be indistinguishable where mandated by Publisher's contract.
- Every protected command is validated and authorised again by the owning server capability; client-side controls are advisory.
- Do not expose an unauthorised person's identity, media or metadata through joined facets, preview caches, search indexes, snippets or feed output.
- Keep tenant/site isolation and provenance across source joins, caches and exports.
- Reject unsupported type fields, invalid rich text, inaccessible assets, stale revisions and illegal lifecycle transitions using the source owner's stable outcomes.
- Degraded state, pending external receipt and completed publication are distinct.
- Respect legal holds, retention, consent, data rights and any configured approval gates.
- Use the shared safe rich-text tree; never treat article content as raw HTML; no independent Markdown dialect.
- Do not claim exactly-once distributed delivery or infer policy permission from an event.
- Public contracts and host-controlled presentation must remain compatible with ADR-0009/0011/0012/0016.

## Cross-capability relationships and reciprocal ownership

| Capability | Blog consumes / supplies | Ownership; absence |
|---|---|---|
| [Publisher](../publisher/capability-record.md) | Article type registration and public/admin document reads/actions; Blog supplies optional user journey only | Publisher authoritative; **essential** |
| [Content Editor](../content_editor/capability-record.md), [UI](../ui/capability-record.md), [Theme Manager](../theme_manager/capability-record.md) | Safe form/editor, rendering and semantic tokens; Blog supplies article context/view composition | Presentation-only; optional, host may substitute |
| [Configuration](../configuration/capability-record.md), [Site Hosting](../site_hosting/capability-record.md) | Site policy/settings and host-resolved site address; Blog supplies consumption/navigation requests | Site ownership/configuration stay at source; site selection essential |
| [Authentication](../authentication/capability-record.md), [Authorisation](../authorisation/capability-record.md), [Identity](../identity/capability-record.md), [Profile](../profile/capability-record.md) | Caller, permission, person-reference and permitted byline; Blog contributes no identity data | Protected paths fail closed; byline optional |
| [Media](../media/capability-record.md), [Storage](../storage/capability-record.md) | Media variants and authorised addresses; Blog supplies content references only | Conditional on image content |
| [Metadata](../metadata/capability-record.md), [Search](../search/capability-record.md), [SEO](../seo/capability-record.md) | Taxonomy/search/redirect/sitemap outputs derived from published material | Optional discovery; Publisher state stays canonical |
| [Workflow](../workflow/capability-record.md), [Scheduler](../scheduler/capability-record.md), [Message Queue](../message_queue/capability-record.md) | Publisher-owned approval, due tasks and event transport; Blog displays status | Conditional, via owning contracts; Blog does not orchestrate |
| [Comments Engine](../comments_engine/capability-record.md), [Notifications](../notifications/capability-record.md), [Translate](../translate/capability-record.md) | Discussion, alerts and translation projections | Optional; no duplicated records |
| [Integrations](../integrations/capability-record.md) | External syndication and verified receipts | Optional; reconcile provider ambiguity |
| [Legal Compliance](../legal_compliance/capability-record.md), [Privacy](../privacy/capability-record.md) | Binding compliance and privacy constraints | Mandatory where applicable; cannot be overridden by Blog settings |
| [Audit](../audit/capability-record.md), [Logging](../logging/capability-record.md), [Observability](../observability/capability-record.md) | Publisher/source accountable events vs Blog diagnostic signals | Audit owns evidence, Logging diagnostics, Blog neither |
| [Reporting](../reporting/capability-record.md) | Public source references and permitted derived displays | Reporting owns report definitions; Blog owns no source metrics |
| [Clock](../clock/capability-record.md) | Site-sensitive date/time formatting | Canonical time remains source-owned |

All are conceptual relationships, not mandatory direct imports. Providers must not import Blog, preventing cycles; the application composes sources.

## Security, privacy, compliance and external boundary

**Established:** OWASP ASVS 5 Level 2 minimum, relevant Level 3 for privileged security operations, server-side Authorisation, scoped site/tenant access, WCAG 2.2 AA, i18n, privacy-by-design and consent classification. Publisher's published headless-surface rules require a server-resolved site/caller, safe-tree rendering, redacted hidden content, no-store/non-frameable admin views, origin checks and explicit version/link acknowledgements. Author attribution must come from authorised Profile information, not a guessed identity.

**Proposed:** Editorial roles/views (contributor, editor, approver, site administrator) are UI audiences, not newly granted privileges. Publisher's existing per-type permissions remain authoritative. Blog public embeds, comments, third-party tracking and external syndication are disabled until separately configured and legally permitted; neither cookie consent nor an external service's terms should be inferred. Conditional applicable copyright, image rights, accessibility, advertising, privacy, defamation and online-content moderation obligations require Legal Compliance assessment, not blanket certification claims. If a future Blog contribution creates storage, its owner must document the storage register, retention and erasure path.

## Likely GUI and navigation presentation

**Reader audience:** Blog landing/latest, article detail with author/date/byline when permitted, category/tag listing where supported, accessible search, feed subscription link, related articles and pagination; optional comments. All public routes and SEO/head tags are host owned and based on authoritative published content.

**Editorial audience:** Blog dashboard (draft, awaiting approval, scheduled, published, archived and failures); searchable/filterable article list; create/edit with Content Editor over Publisher's public type schema; preview; revision comparison/history; publication/withdrawal/scheduling actions; backlink warnings; optional moderation/translation/syndication status; site-level Blog settings. Approver view appears only when the host's approved workflow and permissions allow it. Each action shows owner-confirmed success, revision conflict, pending, denied and unavailable states.

**Representative host pattern:** The verified `nuxt-layers-test/application-test-template` has a host-owned responsive Capabilities sidebar and `/admin` dashboard, with Theme Manager as an example. A Blog-enabled derived test application could offer **Capabilities → Blog → Blog dashboard**, plus public reader routes. This is an **illustrative integration pattern**, not a proven automatic navigation-registration interface. The host controls route placement, menu visibility and branding; a separate administration card may link to the dashboard. The base template is local test-only and does not demonstrate production authentication.

**Separation:** Blog's optional standard presentation, if later packaged, must be removable/overridable without affecting Publisher. The core/sources remain headless. Editorial and public audiences must not be mixed in a privileged page. Theme Manager alone defines semantic styling; `ui` draws safe rich-text trees. WCAG 2.2 AA, keyboard support, meaningful status announcements, semantic landmarks, contrast and localisation apply. Public page cache must never leak previews, unpublished content or permission-specific fragments. Empty, partial, offline, conflict, withheld and unsupported feature states are distinct.

## Conceptual contract acceptance scenarios

| Scenario and input | Expected output/behaviour; authoritative owner |
|---|---|
| Native article create/edit/publish | Host registers article type, editor sends Publisher command; Publisher validates, versions and publishes; Blog reflects committed state only |
| Public reading/list/feed | Anonymous scoped read returns only Publisher-confirmed published items and safe tree; Blog displays without new canonical record |
| Cross-capability author/image/taxonomy | Correct authorised references join into an article view; missing optional sources produce safe omissions, never fabricated values |
| Unauthorised site or draft access | Source rejects or hides; Blog does not leak existence, body, snippet, author or image |
| Invalid field/unsafe media | Publisher rejects validation failure; editor displays stable error and preserves safe unsaved work |
| Two edits from stale revision | Publisher rejects stale `expectedVersion`; Blog reloads/asks for conflict resolution, never overwrites silently |
| Publication pending approval or schedule | UI shows pending/scheduled; only Publisher's confirmed published state becomes publicly visible |
| Event duplication/out-of-order | Search/SEO/reporting projections deduplicate by authoritative version; Blog creates no domain event |
| External syndication timeout | Local article remains Publisher-owned; provider status unknown until verified read-back; retry/reconciliation explicit |
| Withdrawal or erasure with backlinks/hold | Source enforces link acknowledgement and legal hold, with correct 404/redirect and removal of derived public projections |
| Optional comments or taxonomy absent | Article remains readable; feature is clearly absent/unavailable without inventing records |
| Unsupported full-text query or provider mode | Host rejects/degrades clearly rather than calling a nonexistent Publisher operation |
| GUI disabled | Publisher works headlessly, host can draw alternatives; no Blog-specific route/style remains |
| Audit versus Logging | Publisher committed event flows to Audit evidence under its contract; Blog failure diagnostics to Logging; a UI attempt never implies committed publication |

## Findings, open decisions and engineering follow-up

**Established requirements:** GOV-BLOG-01 governing catalogue prefers Publisher document type and presentation; GOV-BLOG-02 Publisher publishes content types, safe rendering, access decisions, revisions, editorial transitions, feeds and outbox; GOV-BLOG-03 ADR-0009/0011/0012/0016 and security/privacy baseline govern separable views and contract-only, acyclic integration.

**Proposed conceptual direction:** BLOG-01 Blog is a Publisher-backed composition/presentation, no authoritative domain persistence, independent Blog lifecycle or business event stream. BLOG-02 The idealised inbound/outbound surfaces and failure modes above form Blog's review contract. BLOG-03 A two-audience screen inventory with host-owned sidebar/dashboard and public routes is appropriate. **These await project-owner sign-off.**

**Open architectural decisions requiring approval:**
- **BLOG-04 — Classification:** confirm Blog as composition/presentation and remove its *Domain candidate* implication in the working register/catalogue, or supply evidence for a distinct independent domain invariant. **Recommendation:** composition/presentation.
- **BLOG-05 — Packaging:** keep Blog as a documented host-registered Publisher type and app-owned views initially, or authorise a reusable presentation package only after demonstrated multi-application use. **Recommendation:** no new repository yet.
- **BLOG-06 — Editorial scope:** choose whether article type, featured/curated content, author pages and category/taxonomy assumptions form a reusable standard Blog profile versus host-specific configuration. **Recommendation:** minimal article type/list/detail first; optional advanced modules through source contracts.
- **BLOG-07 — External authority:** decide whether externally authoritative articles/imports are in scope. **Recommendation:** native Publisher authority only pending explicit authority-transfer design.

**Technical investigation (no policy decision required yet):** verify actual Publisher type schema constraints and read/list/feed feature coverage for Blog consumption; inspect other owners' `CONTRACT.md` when implemented; design performant paginated reads and SEO metadata/structured data without content leakage; verify latest provider behaviour at delivery; explore localisation and author attribution before engineering. These are not inferred completed features.

**Implementation alignment:** a future Blog consumer must implement only owner-published interfaces, describe host composition, prove optional screens and absence mode, and add missing Publisher/Search/Metadata contract extensions through those owners' normal PRs rather than private integration. No implementation repository is modified here.

**Acceptance/verification:** root consumer contract if packaged; independent test host within 50-line budget if a Nuxt capability; presentation-off and source-unavailable cases; identity/site negative isolation; content safety, safe-byline, accessibility/light-dark/i18n, feeds, robots/canonicals, redelivery, conflict handling, reconciliation and relevant source-compatibility checks.

## Architectural consequences and reciprocal documentation

The [working register](../../capability-register.md) currently lists Blog as a Domain candidate but describes it as Publisher document type and presentation. The recommended classification reconciles this without making a normative change. Any formal reclassification of the governing catalogue requires separately approved governing change where its wording is altered. No ADR amendment is presently proposed.

Reciprocal notes belong with Publisher (article type/presentation use and ownership), Content Editor (article editor slot), SEO/Search (published content discovery) and optional other owners only where a genuinely new reciprocal requirement is established. Do not prematurely complete their alphabetical conceptual reviews or claim their interfaces are implemented.

## Conceptual sign-off

**Awaiting owner approval** of BLOG-01 through BLOG-07 as applicable; technical contract evidence beyond Publisher is incomplete. Suitable for review as a non-normative proposal, **not** approved architecture, implementation acceptance or a claim of regulatory compliance.

**Next alphabetical capability directory:** [`booking`](../booking/capability-record.md).
