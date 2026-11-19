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




## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Asset-specific safeguards:** Media owns uploaded media records, metadata, processing/derivative lifecycle and access to assets, with Storage providing byte-store operations through its port. Media must quarantine uploads/variants pending applicable safety gates, prohibit unapproved public/signed access, enforce removal and restoration, and issue authoritative lifecycle/outbox evidence. Content Security supplies detection; proposed Moderation handles reports/cases and appeals; Audit preserves minimal receipt evidence. Protect CSAM/NCII evidence by minimising access, transfers and retention; operator review requires independent safeguards.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed contract alignment in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not a completed media review, normative rule or implementation change. See [Content Editor conceptual boundary](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

The editor may request Media's authorised picker/asset metadata through public contracts; Media owns asset status, alt/access eligibility and quarantine, with Storage owning bytes. Unavailable or pending assets cannot silently become publishable Publisher references.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Media remains authoritative for uploads, image/file versions, variants and visibility; Content Security evaluates only properly authorised snapshot/byte references, links and applicable risks, returning revision/digest-bound evidence. Incomplete or stale checks never silently authorise derivative/public delivery; Media handles hold and CDN/original exposure, Storage bytes remain separately owned.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course references versioned safe learning assets; Media owns asset metadata, quarantine, derivative lifecycle, Storage owns bytes. Course honours safety and access gates before exposure. This note does not complete the separate media review.

## Gallery reciprocal interface — 18 November 2026 (proposed; PR #70)

[Gallery's conceptual presentation contract](../gallery/capability-record.md#dedicated-conceptual-review--gallery-18-november-2026) consumes Media's current authorised variant metadata, alt text, safe thumbnail/lightbox delivery, asset picker/upload and original-download entitlement decisions; it holds no image bytes or authoritative asset state. Media must independently enforce member-only access, quarantine, removal and revocation for original and every derivative, URL, cache and CDN exposure; Gallery's visible button or Publisher publication does not grant access. Gallery's member submission intent is not a Media acceptance receipt. **Evidence gap:** Media's root `CONTRACT.md` was not retrieved; exact private delivery, picker and original-download public interfaces remain unverified. Existing online-safety and Content Editor findings are preserved.


## Reciprocal conceptual note — Metadata review (19 November 2026)

**Status: Proposed in [Metadata draft PR #95](https://github.com/nuxt-layers/architecture-blueprint-review/pull/95), not an approved implementation contract or completed review of this adjacent capability.** [Metadata conceptual contract](../metadata/capability-record.md#dedicated-conceptual-review--metadata-19-november-2026).

Media owns media-asset identity, descriptive media fields and file lifecycle; optional shared vocabulary/assignments are Metadata-owned and source-scoped. Tags cannot reveal unavailable media or override Media's ownership, permissions, safety holds or source removal; the generic taxonomy interface is not a replacement for asset alt text. Conceptual cooperation is optional and host-wired through public contracts; avoid circular required package dependencies.
