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
