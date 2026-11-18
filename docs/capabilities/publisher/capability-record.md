# **Capability Record**

## Capability Name:

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

## Purpose

## Classification

## Dependencies

## Optional integrations

## Version

## Availability

## Capabilities offered

## Configuration

## Cross-capability note — Publication and evidential version references (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** Publisher owns its versioned documents, approvals, addresses, publication and withdrawal; Audit owns evidential acceptance, custody and verification. **Proposed:** Publisher publishes confirmed version/approval/withdrawal actions with safe provenance and permitted content-version references for [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026). Audit must not republish, keep a competing master document or presume retained source bytes after lawful deletion. Publisher's conceptual review remains incomplete.

## Reciprocal note — Generic Content Editor workspace (15 November 2026)

**Agreed conceptual direction:** [Content Editor](../content_editor/capability-record.md#approved-conceptual-direction--complete-generic-editorial-gui-15-november-2026) owns the complete generic **presentation** for Publisher-registered document types, including lists, creation/editing, preview, review/approval status, lifecycle actions and history. Publisher remains fully headless and exclusively authoritative for document records, validation, permissions checks, lifecycle, addresses, outbox and confirmations. The approved allocation does **not** change Publisher's published root `CONTRACT.md`, claim Content Editor implementation is delivered, or create a direct private dependency. Public article and archive pages are application-owned presentation over Publisher's published document, listing, feed and address outputs; they do not establish an independent publishing capability.


## Article and application-generated content — publisher responsibility (15 November 2026)

**Agreed conceptual allocation:** Articles, posts, news, announcements, pages and other published documents are **host-registered Publisher document types**, not separate domain capabilities solely because their presentation differs. Publisher owns content validation, revisions, lifecycle, approvals, scheduled publication, addresses, listings, feeds, transactional outbox, server-side authorisation enforcement and historical traceability. This confirms the accepted governing catalogue's default Publisher ownership; any independent domain candidate needs distinct owned facts or invariants before recognition. No additional article/blog service, document master, domain event stream or persistence is justified.

**Conceptual inbound public contract:** authorised host or generating capability registers a valid document type and submits/create-imports content, revisions or requested lifecycle transitions through Publisher's public services, accompanied by trusted site/tenant/caller context, correlation/provenance, revision preconditions, applicable approval and policies. Host-registered types are presently code declarations in the published `CONTRACT.md`, not dynamically registered end-user types. A generated announcement or report must be attributed to its true originating capability and requires an independently authorised create/publish path; an observed event does not itself authorise publication. User-edited and application-generated documents use the same Publisher lifecycle and safeguards.

**Conceptual outbound public contract:** authoritative document/revision and lifecycle read/command results, published safe content trees, authorised lists, previews, canonical addresses, feeds, redirects and source-owned committed domain events. Content-specific public displays such as chronological article lists, public detail pages, archives, bylines and taxonomy facets are application-owned presentation using Publisher plus the appropriate Profile, Metadata, Media, Search and SEO public contracts; none becomes Publisher's mandatory GUI. Optional external syndication through Integrations preserves a single declared source of authority with explicit uncertainty and reconciliation.

**Editorial presentation:** [Content Editor](../content_editor/capability-record.md) supplies the generic reusable dashboard, document lists, create/edit/preview, approval-status/history and publication/lifecycle controls. Publisher remains headless. The host may expose an **Articles** document-type filter or a **Manage articles** link to that same workspace; no separate article-specific administrative GUI is needed. Check source contract coverage before proposing expansions; this note does not assert that additional client/UI features are implemented.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Own versions, approval, publication and history of policy documents including modern slavery, privacy, cookie and safety notices; publication does not assert legal compliance or activate executable rules. The content-editor supplies generic GUI.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Publication safety:** Publisher owns document creation/versioning, approval, publishing, addresses/feeds and actual withdrawal/reinstatement. Risk-based content gates must distinguish pending assessment, unknown/unavailable detection, held, approved and removed states without treating automated flags as guilt. Content Security supplies verdicts; proposed Moderation supplies case conclusions/restriction requests; Publisher independently enforces server-side authorised transitions and returns actual outcome receipts. Its confirmed changes must reconcile Search, Federation Hub indexes and caches; published policy notices are not enforcement proof.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Publisher retains document publication eligibility and enforcement; may need a locally validated, threshold-scoped age-assurance decision for regulated content creation/viewing rather than collecting ID documents. An age-provider approval or user-supplied declaration cannot bypass domain publication holds, legal constraints or Authorisation.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Publisher and other registered target owners retain eligibility/visibility, owner revision and publication decisions. Comments Engine owns reply/thread records and comment-local enforcement. A host-wired target eligibility/withdrawal contract should supply trusted tenant/target/revision and change signals; Comments Engine checks them before posting, restricts inaccessible targets and returns withdrawal/reconciliation receipts. No mutual package imports, source database reads or assumption that a deleted document automatically erases lawfully retained comment evidence.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed contract alignment in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not a completed publisher review, normative rule or implementation change. See [Content Editor conceptual boundary](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Content Editor consumes Publisher's published type/schema, authorised admin reads, previews, history, backlinks and revision-conditioned commands. Publisher remains fully headless and exclusively owns document/version/approval/publication/retention decisions and committed outbox events; the editor is optional, not a Publisher runtime requirement. Network uncertainty is reconciled against Publisher's authoritative state, not UI optimism.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Publisher requests revision-bound technical checks for registered documents before the exposure decisions its policy requires; Content Security returns scoped detection evidence, coverage and unknown/stale states. Publisher owns actual publish/hold/unpublish and reconciles address/feed/cache exposure; Content Editor presents status through Publisher/public contracts, not detector tables.

## Reciprocal decision — redundant Document capability retired (17 November 2026)

**Owner-approved resolution, 17 November 2026:** the separate `document` capability candidate is retired. Publisher remains authoritative for its registered document types, revisions, approvals, publication, addresses, feed and withdrawal lifecycle. Source-specific business records remain with their domain owners; Publisher does not automatically acquire invoice, employment or other domain master records. No second document master, service or event stream is required. Historical analysis: [Document](../../../reviews/document-directory-removal-2026-11-17.md).

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed publisher review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Course owns course curriculum structure, prerequisite and learning outcome definitions and versioned reference mappings; Publisher owns authored document versions, approval/publication and source materials. Course may reference Publisher material by immutable source/revision; a Publisher publication is not by itself Course publication, and source withdrawal must be propagated safely without rewriting historical Course meaning.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-10/11 agreed:** a course syllabus or certificate PDF is a Publisher document, not proof that a qualification award was authorised. Course owns curriculum, Assessment owns marks, Training owns achievement, Credentials owns credential status, and the qualified awarding authority owns formal award decisions. Curriculum migration and withdrawal preserve lawful historical references. This note does not complete the separate publisher review.


## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)).** Publisher may produce versioned certificate documents or presentation using a permitted Credentials public view model, but owns only its own rendered document lifecycle. It cannot issue the underlying credential, award a qualification, revoke a credential or certify live proof status. Corrections/revocations trigger controlled rendering/withdrawal or status updates through explicit public contract and reconciliation; a cached PDF remains an artifact, not a status authority.

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** Publisher keeps authoritative approved revisions, publication/withdrawal, visibility and document lifecycle. The Export Library renders a permitted revision's safe rich-text tree into file bytes/stream; Publisher or the calling host owns any stored downloadable copy, source disclosure recheck, retention and invalidation. There is no restored generic Document capability and no Export-owned Publisher master. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.

## Federation — reciprocal conceptual contract (18 November 2026)

**Status: Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69); not an approved implementation API, and does not complete this capability's independent review.** [Federation public contract](../federation/capability-record.md#independent-review-contract-completeness-and-authority-18-november-2026).

Publisher may provide explicitly approved, versioned, public collection projections and durable publication/update/withdrawal facts to Federation. Publisher remains the publication and visibility authority; Federation owns peer subscriptions, deliveries, remote acknowledgements and reconciliation, without editing source documents. No implicit publication to a Hub and no private-state replication. All cooperation is via public, directional host-composed contracts with scoped failure/absence semantics; preserve existing approvals and avoid package dependency cycles.

## Gallery reciprocal interface — 18 November 2026 (proposed; PR #70)

[Gallery's conceptual public surfaces](../gallery/capability-record.md#dedicated-conceptual-review--gallery-18-november-2026) remain **presentation only**. Publisher owns host-registered `album`, `members-album` and `featured-photo` document type records, order/captions/credits, revisions, audience constraints, publishing/scheduling, addresses and source outbox. Gallery consumes only authorised public published/admin reads and version-conditioned commands through host composition; Media remains authoritative for asset eligibility. **Contract gap:** current root `CONTRACT.md` documents `view-draft/edit/publish/delete` but not the historical Gallery `moderate` action, nor a proven member-submission workflow. Do not infer these from the earlier design; source-authorised intake/review and private-document access require contract verification/reconciliation. This note is not approval of a Publisher implementation change.


## Reciprocal conceptual note — Help review (18 November 2026)

**Status:** Proposed in [Help draft PR #72](https://github.com/nuxt-layers/architecture-blueprint-review/pull/72); not approved, implemented or an amendment to published `CONTRACT.md`. See [Help conceptual contract](../help/capability-record.md).

Publisher remains the sole owner of Help article/document content, revision, approval, publication, withdrawal, canonical addresses and authoritative safe renderings. Proposed Help contextual resolution consumes only authorised public Publisher references and reconciles withdrawn or stale material; it never publishes or holds a second content master. The host may register a Help document type and use generic Content Editor. No dependency from Publisher back to Help is required.
