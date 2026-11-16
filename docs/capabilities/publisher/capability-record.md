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
