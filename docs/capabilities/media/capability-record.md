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

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Media remains authoritative for uploads, image/file versions, variants and visibility; Content Security evaluates only properly authorised snapshot/byte references, links and applicable risks, returning revision/digest-bound evidence. Incomplete or stale checks never silently authorise derivative/public delivery; Media handles hold and CDN/original exposure, Storage bytes remain separately owned.
