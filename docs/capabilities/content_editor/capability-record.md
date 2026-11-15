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

## Cross-capability note — Blog article editing (15 November 2026)

**Proposed reciprocal relationship; independent Content Editor contract not verified.** [Blog](../blog/capability-record.md) uses Content Editor's approved generic editorial GUI and reusable formatting controls for host-registered Publisher article types through Publisher's documented editor slot, type schema, safe rich-text profiles and save/transition interfaces. Content Editor owns presentation behaviour only: it must not store article versions, make publishing decisions, bypass Publisher's validations or assume a direct private import. The host may replace the editor; source authorisation remains server-side. This note does not complete Content Editor's conceptual review.

## Approved conceptual direction — complete generic editorial GUI (15 November 2026)

**CED-01 — Agreed conceptual direction, explicitly approved by project owner:** Content Editor is the platform's **complete generic editorial user interface**, not merely a rich-text input. It presents authorised document-type selection, listing/filtering, generic dashboard/status queues, creation, editing of plain and formatted fields, preview, revision/history, approval/review state, scheduling/publishing/withdrawal, backlink warnings, archive/restore/deletion and clear errors/recovery. It uses the owning source's **public contract** and host-supplied composition, especially Publisher's editor slot (`types()` with schema, `richTextFields`, allowed actions; `create`, `act`, `documents`, `history` and `backlinks`); it may expose smaller reusable field/editor components and must support a presentation-off/headless host alternative. The host owns navigation, routes, branding and trusted site/identity context; Theme Manager owns semantic tokens. A derived test host may link **Capabilities → Content Editor → Documents**, with an Articles filter; `blog` may link to the same workspace instead of owning an editor or management dashboard.

**Explicit exclusion:** Content Editor is **Presentation**, with no article/document business record, publishing lifecycle, approval policy, permissions authority, durable domain event or duplicated persistence. Publisher continues to validate and authorise commands server-side, own versions, content, addresses and transitions, and publish its own authoritative events; other source owners retain their facts. Application-generated content is created/imported into Publisher through its authorised contracts and may subsequently be reviewed in Content Editor. Consent, legal holds, tenant isolation, safe rich text, expected-version conflicts, accessibility and i18n apply regardless of which UI sends an action.

**Conceptual public boundary (proposed elaboration of approved scope):** inputs: resolved site/caller/permissions, selected owner/type/schema, scoped document reads, revision and lifecycle state, optional approval/media/metadata context, user editing and management intents. Outputs: accessible lists/forms/editor/preview/workflow controls, filtered links/navigation proposals, validated command payloads sent to the owning capability and source-confirmed results/errors; no Content Editor-owned document business events. Absent optional sources disable only their features; absent Publisher or required access fails closed for the relevant operations. A generic `content-editor` implementation `CONTRACT.md` has **not** been verified, and this allocation neither establishes implementation completeness nor completes Content Editor's alphabetical review.

**Reciprocal consequence:** [Blog](../blog/capability-record.md#approved-cross-capability-allocation--content-editor-workspace-15-november-2026) now owns no generic editorial screens. Its only prospective separate GUI is public reader-facing content presentation or an optional contextual link to the shared editor.
