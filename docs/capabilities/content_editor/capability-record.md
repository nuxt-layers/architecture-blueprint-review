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

## Approved conceptual direction — complete generic editorial GUI (15 November 2026)

**CED-01 — Agreed conceptual direction, explicitly approved by project owner:** Content Editor is the platform's **complete generic editorial user interface**, not merely a rich-text input. It presents authorised document-type selection, listing/filtering, generic dashboard/status queues, creation, editing of plain and formatted fields, preview, revision/history, approval/review state, scheduling/publishing/withdrawal, backlink warnings, archive/restore/deletion and clear errors/recovery. It uses the owning source's **public contract** and host-supplied composition, especially Publisher's editor slot (`types()` with schema, `richTextFields`, allowed actions; `create`, `act`, `documents`, `history` and `backlinks`); it may expose smaller reusable field/editor components and must support a presentation-off/headless host alternative. The host owns navigation, routes, branding and trusted site/identity context; Theme Manager owns semantic tokens. A derived test host may link **Capabilities → Content Editor → Documents**, with an Articles filter; the host may link directly to an Articles-filtered workspace rather than creating a separate editor or management dashboard.

**Explicit exclusion:** Content Editor is **Presentation**, with no article/document business record, publishing lifecycle, approval policy, permissions authority, durable domain event or duplicated persistence. Publisher continues to validate and authorise commands server-side, own versions, content, addresses and transitions, and publish its own authoritative events; other source owners retain their facts. Application-generated content is created/imported into Publisher through its authorised contracts and may subsequently be reviewed in Content Editor. Consent, legal holds, tenant isolation, safe rich text, expected-version conflicts, accessibility and i18n apply regardless of which UI sends an action.

**Conceptual public boundary (proposed elaboration of approved scope):** inputs: resolved site/caller/permissions, selected owner/type/schema, scoped document reads, revision and lifecycle state, optional approval/media/metadata context, user editing and management intents. Outputs: accessible lists/forms/editor/preview/workflow controls, filtered links/navigation proposals, validated command payloads sent to the owning capability and source-confirmed results/errors; no Content Editor-owned document business events. Absent optional sources disable only their features; absent Publisher or required access fails closed for the relevant operations. A generic `content-editor` implementation `CONTRACT.md` has **not** been verified, and this allocation neither establishes implementation completeness nor completes Content Editor's alphabetical review.
**Application presentation boundary:** Article pages, archives, chronological lists and other public layouts belong to the consuming application, using Publisher's published outputs and optional source capability contracts. The host may link **Manage articles** to an Articles-filtered Content Editor workspace; no separate Blog business capability or editorial GUI is required.


## Registered document types and generated content — editorial GUI (15 November 2026)

**Agreed allocation:** The generic editorial workspace must handle any authorised Publisher-registered type, including articles, news, pages, announcements and application-generated documents. The type selector, filtered lists, field/form controls, safe rich-text editor, history, revision conflict resolution, preview and lifecycle controls derive from Publisher's published type/schema/permission and operation surfaces, not hard-coded assumptions about a specific blog or document schema.

**Inbound conceptual interfaces:** host-supplied trusted site/tenant/caller and selected type; Publisher's authorised document-type descriptors, field profiles, list/detail/history/backlinks and current document version; permitted lifecycle actions, source-owned approval evidence, optional Media/Metadata context and user commands. Generated documents must first be accepted by Publisher through its authorised create/import contract; they appear in the same editorial interface subject to permissions and provenance.

**Outbound conceptual interfaces:** generic accessible document management views, drafts/previews/forms, source-confirmed statuses, reviewed command requests sent to Publisher with expected version and applicable backlink acknowledgements, safe feedback for rejected/stale/held/unsupported operations, and host-reusable navigation affordances. Content Editor creates **no** content authority or business events; it must not convert a pending command, an external receipt or an event into a claim of published content.

**Availability and acceptance:** without Publisher or trusted authorisation the relevant editorial functions fail closed; optional Media/Metadata/Workflow controls degrade only when their own features are unavailable and legal/policy constraints still hold. Accessibility (WCAG 2.2 AA), i18n, Theme Manager vocabulary, site/tenant negative isolation, generation provenance, safe-tree rendering, unsaved work, stale revisions, permission changes, no-store admin responses and removable/replaceable presentation must be verified in its later dedicated review. Its actual implementation remains unverified.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Provide reusable authored policy document GUI (draft, version, review, publish via Publisher); do not own policy validity or source regulatory duties. Host routes and role-scoped navigation remain host-owned.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Presentation only:** Content Editor shows Publisher and Media eligibility, scan pending/unknown, quarantine, editorial holds, appeals and approved reviewer actions via their public contracts. It may offer reports and case navigation from proposed Moderation but must not persist independent publication, safety verdict or case state. Never let a client-side green indicator substitute for server-side publication gating. Show accessible and internationalised pending/refused/appeal states.

## Dedicated conceptual review — Content Editor (17 November 2026)

**Status:** Working proposal on draft PR #54; CED-01 and existing approved allocations above remain approved, but the following detailed interface/GUI elaboration and alternatives are **not** implicitly owner-approved. **Classification:** Presentation, not a document domain authority. **Actual directory:** `content_editor`; published capability name `content-editor`.

### Authority and implementation evidence

- Governing baseline: `architecture-rules` master `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`. Blueprint baseline: `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`. Relevant accepted ADR-0009 (separable presentation), ADR-0011 (generic field editor, safe rich text), ADR-0012 (independently usable consumer contract and host composition), ADR-0016 (public-contract dependencies, acyclicity), and normative Capability Standard (Presentation classification). ADR-0018 was **proposed** at this baseline; do not independently promote it to binding authority.
- Publisher `master` root `CONTRACT.md` read (blob `6d51c98cf2fcd40e0de4f476540a63b260f76b42`); published editor slot `types()`, `documents()`, `document()`, `history()`, `backlinks()`, `create()`, `act()`, `remove()`; registered schema and `richTextFields`, per-type `may` permissions. Publisher remains fully headless. Evidence **documented**, not independently run/verified.
- Rich Text `master` root `CONTRACT.md` read (blob `64b97ab6ce745c56eed507a200180e18e6025be3`): `inline`, `block`, `document` profiles; source Markdown, normalisation/checks and safe rendered trees. Documented, not independently executed.
- `nuxt-layers/content-editor` repository identity exists on `master`, but a root `CONTRACT.md` retrieval returned 404. **Implementation status unverified**; no independently usable published Content Editor contract was established. Do not claim any GUI or API is delivered.

### Purpose, scope, authority and exclusions

Provide two **separable presentation surfaces**: (1) reusable generic formatted-field editor accepting profile/max and returning edited source without knowing or storing the owner; (2) schema-driven **Publisher editorial workspace** encompassing allowed document types, list/filter/search supplied by Publisher, editing, preview, revision comparison, history, approvals, backlinks, lifecycle actions and recovery. CED-01 approves this broad GUI direction. The host may integrate either surface independently; the host may substitute its own presentation, and Publisher remains usable without the editor.

Content Editor owns **no authoritative document, revision, media asset, user, tenant, approval, publication, policy, moderation, search index, retention record, domain event, durable outbox or business audit evidence**. A screen's unsaved form state is transient local interaction state only, not an alternative domain copy. Persistent browser drafts, if ever proposed, need a separate storage/privacy threat and consent review; not assumed here. Editing another capability's formatted field uses a generic input/output component, not a second editing business API. General-purpose forms are ordinary `ui` controls; the editor does not duplicate Profile, Configuration or arbitrary domain administration.

### Idealised public inbound contract

| Interface / source | Data or action supplied | Source authority; validation and absence semantics |
|---|---|---|
| Host composition (required for workspace) | Trusted site/tenant context, permitted navigation mount, caller resolution, source service bindings, locale, UI configuration | Host/Identity/Authentication/Authorisation retain authority; **never trust browser-selected tenant or caller**; absent trusted context closes protected workspace |
| Publisher public editor slot (required for document workspace, not standalone field editor) | Authorised registered type descriptors, schema/field constraints, rich-text fields, allowed actions; scoped lists/details, revision, history, backlinks, previews | Publisher owns types/content/actions; treat descriptors as untrusted for UI safety and stale until refreshed; unavailable/disabled API demands supported server adapter or honest unavailable state, not private fallback |
| User (intent, not authority) | Type selection, field edits, save, review, request approval, publish/schedule, withdraw, archive, restore, delete, backlink acknowledgement | Validate UI shape and prohibit unsafe editor output; Publisher revalidates content, permissions, workflow state, expected version and every transition; client intent never authorises an action |
| Generic formatted-field consumer (required for field mode) | Original source, `inline/block/document` profile, max length, labels, read-only/disabled, change/commit callback and invalid state | Owning capability defines field format and validates saves. Invalid/unknown profile must disable unsupported editing rather than widen permissible constructs |
| Optional published providers | Media/asset selection, Metadata taxonomy, Workflow approval evidence, Configuration options, Clock/localisation formatting, safety/moderation status, policy constraints | Each remains authoritative; optional feature disabled when absent. Unknown/held/quarantined states are not treated as approval |
| Source-owned revision and command feedback | Current revision, command receipt, stable errors/reasons, correlation/provenance, newly permitted actions | Refresh after command; stale/unknown pending results never become confirmed success; do not infer from delivery events |

No generic universal request shape is imposed. Pass site, owner, document, expected revision, assurance, idempotency/correlation and source-version context only where the actual owner contract requires or supports them.

### Idealised public outbound contract

| Surface / consumer | Output | Guarantee and explicit limitation |
|---|---|---|
| Generic field editor → owning form | Editable normalised source and validation hints; change/commit/cancel and unsaved-state signals | Presentation **intent**, not valid persisted content; source owner must validate on server; safe tree preview only through documented safe renderer |
| Workspace → authorised user | Accessible type/list/filter, schema-derived form, safe preview, revision/history/backlinks, lifecycle status, approval state, disabled/available actions | View of Publisher-owned state with provenance and freshness; no authority to assert publication or approval independently |
| Workspace → Publisher contract | Typed creation, save, submit, publish/schedule, withdraw, unpublish, archive, restore, delete requests; expected version and explicit required link acknowledgements | Requests subject to Publisher's permissions, origin checks, rich-text rules, legal holds, and concurrent revision protection |
| Owner result → user/host | Accepted/failed/pending result, source-confirmed current status/version, actionable stable error or reload link | Only a **confirmed owner response or authoritative subsequent read** warrants completed state; distinguish uncertain network result |
| Workspace → host | Optional route/navigation descriptors, document-type filtered workspace links, accessibility and i18n message keys | Host chooses route, URL, branding and menu permissions; never writes hidden capabilities' private storage |
| Events and reporting | **No Content Editor domain events or authoritative reporting facts** | Publisher publishes committed outbox events; Audit accepts business evidence from owners; Logging/Observability may receive redacted UI diagnostics, not content payloads |

Command requests must support version preconditions, explicit danger confirmations and safe retries/recovery. No exactly-once guarantee is inferred from UI retries; after timeout, query the source before resending a potentially irreversible action. Queries need source-specified scope, pagination, completeness/freshness and concealed-resource response semantics. No Content Editor domain event consumer contract is justified because it owns no domain transition.

### Native presentation behaviour and lifecycle

1. Entry: host mounts sidebar **Content Editor → Documents** (or a filtered **Manage articles** link) only when appropriately authorised; no shadow application routes.
2. Type discovery: fetch permitted Publisher types and `may` action metadata; show only available types; schema controls for plain fields, specialised rich text for declared rich fields, nested/repeated fields within documented schema support. Unsupported schema constructs fail visibly, never silently discard data.
3. Manage: authorised list/filter/pagination; create draft; open document with version, status and provenance; inline/block/document formatting toolbar must exactly respect field profile/max, keyboard interaction and safe links/assets; plain fields never acquire rich formatting.
4. Preview: use source-authorised previews and the safe-tree renderer, not raw HTML, arbitrary scripts or inferred public access; mark as **preview/non-public**. Preserve document structure, assets and accessibility.
5. Review: show history, compare revisions where source supports it, current approval/consent constraints and review requests; changing submitted content may invalidate approval. Do not invent an editor-owned approval workflow.
6. Lifecycle: show only Publisher-advertised actions; display backlinks before unpublish/archive and submit explicit acknowledged-link count; require clear confirmation for destructive operations; display schedule in locale/time zone without changing the source instant.
7. Conflict/failure: preserve unsaved edits during `version-stale` and offer load/diff/manual resolution, never blind overwrite; distinguish validation-failed, forbidden, step-up, not-found, conflict, held, still-linked, unknown availability and source timeout. Clear protected state upon context or permission loss; avoid leaking existence of hidden documents.
8. Recovery: rejected/uncertain actions do not show success; refresh and reconcile authoritative version/status; availability of optional provider changes only the associated controls. Source-owned delete/retention/erasure cannot be undone by a local editor cache.

**Presentation standards:** WCAG 2.2 AA; one logical main landmark per screen, keyboard-only toolbars, labelled fields/errors, focus restoration on modal or result, accessible comparison and status announcements, responsive layout, Theme Manager semantic tokens and contrast, BCP 47/CLDR formatting, editable translated message keys, right-to-left where applicable. Admin pages require non-cacheable, non-frameable responses and no referrer disclosure. Rich-text preview receives safe tree only; the source owner checks profile and max at save.

### Cross-capability dependency and reciprocal matrix

| Counterpart | Direction and required information | Authority / absence |
|---|---|---|
| Publisher | Editor → Publisher's **public** types, commands, queries and outcome interface; Publisher may advertise an editor slot but must not depend on the GUI | Required **only for document workspace**; headless Publisher independent |
| Rich Text / UI / Theme Manager | Field editor → Rich Text's profile rules and source format; UI safe renderer and controls; Theme Manager tokens | Rich Text is a library, not a domain event dependency; UI/Theme are presentation composition dependencies with declared absence/replacement behaviour |
| Host / Identity / Authentication / Authorisation | Host injects trusted site/context; source server authorises; editor shows source-advertised permissions and step-up UX | Required protected context; no client permission authority; no tenant inheritance |
| Media / Storage | Optional asset picker via Media's authorised selection and Publisher's link-resolver; never direct bucket access | Media owns asset/alt/eligibility; Storage owns bytes; unknown or quarantined asset cannot be published |
| Metadata / SEO / Search | Optional taxonomy selection, preview of SEO metadata, navigation into source-scoped search | Metadata/SEO/Search own their data and derived results; no indexing or canonical address mutation by editor |
| Workflow / Notifications / Scheduler / Clock | Show source-owned approval and notification status, schedule options and confirmed effective instants | Workflow owns approval process; Publisher owns scheduled document state; Scheduler executes due work; Clock formats/interprets time. No editor-owned job or notification |
| Configuration / Profile / Localisation | Host supplies presentation options, person display context and translated copy; field component reusable for permitted formatted fields | Each owner validates persisted values; editor doesn't become generic policy/person data manager |
| Privacy / Legal Compliance / Content Security / Moderation | Display qualified holds, purpose/consent and safe moderation states through responsible owner's published results | No self-certification of safety/legal compliance; unknown gates fail closed for destructive/public transitions |
| Audit / Logging / Observability / Reporting | Publisher emits business transitions and audit evidence; editor supplies redacted interaction diagnostics only where approved | No business-event duplication, content-bearing logs or popularity/engagement scoring |
| Integrations / Federation | Show source-qualified outbound publication/syndication status only if published by owners | External delivery is not evidence of document publication; editor does not control remote nodes |

**Directionality:** generic field editor does **not** import Publisher; Publisher does **not** import Content Editor. The document workspace consumes Publisher's public contract through composition. No architectural cycle is introduced by a Publisher *documentation reference* to its compatible editor. Content Editor is not required by consumers who use plain forms/headless calls.

### Conceptual contract acceptance examples

| Input → operation | Expected result → accountable authority |
|---|---|
| Host supplies permitted registered type and caller; editor creates draft | Form follows supplied schema; Publisher confirms document ID/version; editor displays confirmed draft, Publisher owns it |
| Formatted field profile `inline` receives table/image | Formatting affordance unavailable; invalid source rejected by storing owner; Rich Text defines profile, Publisher validates stored field |
| Create/save with stale expected version | Publisher returns `conflict/version-stale`; editor retains local work and offers reconcile, not overwrite |
| Different tenant / hidden document / revoked permission | No leaked type/document detail; source returns indistinguishable not-found where required; editor clears sensitive state |
| Unpublish with backlinks | Editor displays count, requires explicit acknowledgement; Publisher checks and returns success or `still-linked` |
| Publish during pending Content Security or legal hold | Editor depicts non-final status; Publisher refuses prohibited transition; editor never claims publication |
| Workflow approval changed after draft revision | New source version invalidates old digest/approval; editor shows review required; Workflow/Publisher determine state |
| Optional Media unavailable | Media picker disabled, other supported plain fields remain usable; Publisher rejects any unresolved required asset |
| Timed publication requested with local date/time | Explicit zone/offset and disambiguation passed to authoritative scheduling; Publisher confirms scheduled instant; Clock formats |
| Delete times out after network request | Editor reloads source status before retry, avoiding a fictitious completion or blind duplicate |
| Host does not mount editor | Publisher client/server API remains available, with plain text controls or alternative UI |
| Source exports administrative history for Reporting | Reporting reads approved source data; editor supplies no separate authoritative history |

### Decisions, investigations and alignment

- **Established:** Presentation classification, ADR-0011 generic rich-text field boundary, Publisher schema/permission editor slot, Publisher-owned lifecycle and security floor; published contracts are documentation evidence, not runtime verification.
- **Approved:** CED-01 full generic Publisher GUI, no independent document lifecycle, host-owned routes, separable headless alternative; existing Publisher/registered document-type allocation.
- **Owner-approved CED-02 (17 November 2026, clarified):** Ordinary plain-text and multi-line fields use standard semantic HTML `<input>` and `<textarea>` controls (or accessibility-preserving UI wrappers), **not** a special rich-text editor. Reusable Content Editor formatted-field components are used only for fields whose source contract expressly permits formatting. The separate full document workspace is approved; it composes plain HTML controls, richer formatted fields and source-driven management functions. No competing generic plain-text editor or document authority.
- **Owner-approved CED-03 (17 November 2026, clarified):** Do not retain permanent uncontrolled browser-local drafts by default. Provide authorised server-side autosave/checkpoint recovery for substantive documents and collaborative sessions, with source-owned revision/approval rules; warn about unsaved changes and preserve volatile editing state on transient failures. Offline persistent browser storage is a separate privacy/security/storage-register design decision, not silently enabled.
- **Owner-approved CED-04 (17 November 2026):** Source-published schemas, field types, permissions and available actions determine document forms and controls. Appropriate specialised widgets may replace basic inputs for complex content, while source owners retain server validation and business decisions. Neither rigid hard-coded forms nor unrestricted dynamic widgets are acceptable.
- **Owner decision CED-05 (17 November 2026):** Real-time multi-user collaborative editing **must ship in the first release**. This is an agreed product requirement, not a claim of implementation or approval for any specific CRDT/provider. Concurrent presence, live changes, reconnection, safe conflict/revision reconciliation, server-authorised participation and durable source-owner save/revision outcomes are required. Design must reconcile the collaborative session with Publisher's expected-version/approval-digest lifecycle without moving document authority into the collaboration transport.
- **Technical investigation:** verify target repository's root CONTRACT/actual API, Nuxt package shape, field-level schema renderer, type descriptors, preview/history support and i18n implementation before claiming any implementation alignment. Verify Publisher compatibility and host 50-line integration in CI/user acceptance, not in this blueprint review.
- **Implementation alignment:** create/repair independently usable root `CONTRACT.md` in implementation work **only after separate authorisation**, document public components and mount/disable contracts; ensure editor never bypasses Publisher server validation.
- **Conceptual sign-off:** **pending owner review**; this PR is non-normative and must remain unmerged without explicit approval.

## First-release collaboration and expanded editing investigation (17 November 2026)

**Owner direction:** CED-05 collaboration is mandatory for first release. **Approved intended use:** one reusable editing suite for formatted document authoring, spreadsheet editing and whiteboard/diagram editing, using suitable permissively licensed open-source libraries where practical. This approves the product scope and conceptual presentation model, **not** a specific library, feature-completeness claim, implementation package or source-of-truth ownership change. Detail and provider selection are deferred to implementation design, subject to published contracts, licence and security checks.

**Collaboration design:** Reusable session/transport may employ permissively licensed Yjs (MIT) and a self-hosted provider such as Hocuspocus (open-source backend), with server-enforced per-document access, tenant boundaries, revocation, awareness, rate limits, durable checkpointing, reconnection and lawful retention. Publisher remains authoritative for committed document version, approval digest and lifecycle; collaborative live operations are transient pending material until validated/committed through Publisher. A publication action must use a stable committed snapshot. Separate read/edit/publish privileges; no reliance on a WebSocket join token as indefinite authority. No raw draft content in Audit or Logging. Provider choice and implementation contract remain unapproved.

**CED-03 implementation-design constraint, owner-approved:** No automatic **persistent local browser** drafts by default, not a prohibition of authoritative server-side autosave. Design server autosave/checkpoints with version, approval invalidation, conflict and recovery semantics; require a published Publisher contract adjustment if current commands cannot support concurrent autosave safely. Browsers may retain only volatile unsaved interaction state by default. Any offline/persistent local drafts require explicit per-tenant privacy, storage register, device trust and erasure policy.

**Expanded editor types and ownership questions:**

- Reusable text authoring: Tiptap (MIT) with Rich Text's **existing** safe Markdown/profile boundary; do not make the WYSIWYG editor's proprietary document JSON the automatic domain master.
- Spreadsheets: investigate Univer's Apache-2.0 **core**, but do not assume collaborative server, Office import/export, charts or advanced functionality are in that permissive edition; commercial modules require separate licence/fit review. A workbook/cell/formula source-of-truth, version/revision and calculation authority are not established by Publisher's current document schema.
- Whiteboards: investigate Excalidraw (MIT) for editable canvas scenes and self-hosted sessions; board state, objects and permissions need an explicitly designated domain owner rather than implicit Media/Content Editor persistence. tldraw production licensing is not equivalent to permissive open-source licensing.
- Office-style file fidelity and round-trip import/export must be investigated as a separate requirement; ONLYOFFICE Community is AGPL-3.0, not permissively licensed, and should not be selected without legal approval.

**Architecture option for decision:** Content Editor becomes the reusable presentation *suite*, comprising field editor, Publisher document workspace, spreadsheet editor and whiteboard editor. Each adapter consumes an owning source's **public format/session/persistence contract**, with distinct format/provenance and no private database coupling. Publisher may be a versioned container/reference if its contract is extended by approval, or a separate well-justified workbook/board domain may own complex files; do not silently extend Publisher's current rich-text/document schema to formulas/canvases. Shared collaboration is a service boundary, not a right to mutate domain records. Different editor libraries may need different collaboration adapters; interoperability is not assumed.

**Open architectural decisions:** Where workbook/board canonical state and formulas live; whether spreadsheet/board version lifecycle belongs to Publisher or a separate document owner; which editing and collaboration features must be permissively available at first release; whether server autosave counts as a domain revision and when approval is invalidated; file import/export fidelity and licensing; storage/compute costs and graceful provider failure.

## Owner clarification and conceptual resolution — CED-02 to CED-05 (17 November 2026)

**Interpretation:** The owner's reference to CFG-02 through CFG-05 in the Content Editor conversation is recorded against **CED-02 through CED-05**, not the separate Configuration review's CFG decisions.

- **CED-02 agreed:** Use **native HTML text inputs and multi-line textareas** for ordinary plain text. Only invoke a specialist rich-text component when the publishing/domain field explicitly permits formatting. A complete document editor remains a distinct workspace assembled from appropriate plain and advanced controls. The editor adds no redundant plain-text abstraction.
- **CED-03 agreed:** Avoid permanent browser-local draft copies by default; give authors reliable authorised server autosave, reconnection and recovery, with source-owned versions and explicit failure feedback. Storage security and practical checkpoint details belong to implementation design.
- **CED-04 agreed with qualification:** Render forms and available actions from the owning capability's published description, including use of specialist controls for documents, spreadsheet grids, canvas boards or other complex structures when supported. Keep final validation, permissions and outcomes with the owner.
- **CED-05 agreed for initial release:** Real-time collaboration is mandatory. Collaboration must cover the editing modes selected for first release without claiming a single technical protocol works unchanged across formats. Presence, concurrent editing, conflict-safe recovery, revocation and source-confirmed saves are conceptual expectations; exact providers and design are deferred.
- **Suite intent agreed:** Content Editor is a reusable **presentation suite** for formatted text/documents, spreadsheets and whiteboards. Do not create new capabilities or appropriate Publisher's authority solely because these features are desired. Investigate what authoritative workbook/board lifecycle contracts are needed during implementation design. Permissive licences preferred; commercial/reciprocal components require explicit review rather than assuming eligibility.

**Remaining open technical architecture (not decision re-opening):** workbook/whiteboard owner and format, simultaneous editing transport by format, Publisher integration and autosave revision semantics, open-source versus commercial feature boundaries, storage/recovery/privacy, Office import/export fidelity and host compatibility. These require evidence and design work, not a fresh vote on approved intended use.

## Content Security — reciprocal interface (17 November 2026)

**Status:** Proposed in [Content Security PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55); concurrent content_editor draft review is provisional and must be reconciled before integration. See [Content Security record](../content_security/capability-record.md).

Content Editor is a presentation consumer, not an assessment or publication owner. It should display authorised revision-bound Content Security check status and incomplete/stale explanations through Publisher's public workflow, with safe recheck affordances if Publisher permits; no detector tables, final safety adjudication or extra editor-owned state.

## Reciprocal decision — redundant Document capability retired (17 November 2026)

**Owner-approved resolution, 17 November 2026:** `document` is retired as a standalone capability. Content Editor continues to own only the generic editorial presentation of Publisher-registered types and no document domain authority. No separate Document management GUI is proposed. The superseded conditional review is retained at [Document history](../../../reviews/document-directory-removal-2026-11-17.md).

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed content_editor review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Course requires a structured curriculum editor (outcome builder, unit/prerequisite graph, revision comparison, publication state and content reference selection) via the Course public conceptual contract. Generic Content Editor may present declared course field/action descriptors, but does not own Course state or infer domain rules from arbitrary rich text. Coordinate with provisional PR #54 without treating that PR as accepted.

## Gallery reciprocal presentation interface — 18 November 2026 (proposed; PR #70)

[Gallery](../gallery/capability-record.md#dedicated-conceptual-review--gallery-18-november-2026) offers a type-specific ordered-media field/editor contribution for Publisher-registered album and featured-photo types, plus an album viewer/lightbox and optional submission experience. **Content Editor** retains generic Publisher document administration, schema-driven form, review/history and publication screens. Neither duplicates Publisher's authoritative lifecycle nor owns moderation case decisions. Review intake for member submissions must be wired to an actually published source-owned contract; the legacy Gallery design's `publisher.<type>.moderate` permission is not evidenced by Publisher's current root `CONTRACT.md`. GUI routes and sidebar integration remain host-controlled.


## Reciprocal conceptual note — Help review (18 November 2026)

**Status:** Proposed in [Help draft PR #72](https://github.com/nuxt-layers/architecture-blueprint-review/pull/72); not approved, implemented or an amendment to published `CONTRACT.md`. See [Help conceptual contract](../help/capability-record.md).

Help authors and editors use Content Editor's generic Publisher-backed document-type editing, version history, preview and publication workflows; the proposed Help mapping/coverage screens are separate narrow reference-administration presentation, not another text editor. Content Editor does not own contextual mappings or publication state.


## Reciprocal conceptual note — Metadata review (19 November 2026)

**Status: Proposed in [Metadata draft PR #95](https://github.com/nuxt-layers/architecture-blueprint-review/pull/95), not an approved implementation contract or completed review of this adjacent capability.** [Metadata conceptual contract](../metadata/capability-record.md#dedicated-conceptual-review--metadata-19-november-2026).

Content Editor may offer optional taxonomy/category selectors backed by Metadata public term and assignment queries. It renders authorised choices and submits user intent to the authoritative owner; it owns neither term vocabularies nor assignments and must not bypass Publisher's server-side revision or permission checks. Missing Metadata disables only contextual selection. Conceptual cooperation is optional and host-wired through public contracts; avoid circular required package dependencies.
