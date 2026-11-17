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

## Cross-capability note — Scanning outcomes and evidential accountability (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** Content Security owns scanning and safety verdicts; relevant domain owner owns content disposition and override. **Proposed:** trusted classified verdict/override assertions may pass to [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026), which records provenance, receipt and review without treating a scan flag as legal guilt or copying risky raw content. Missing scan or verifier results remain unknown. Content Security's conceptual review remains incomplete.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Detection, not adjudication:** Content Security owns classifier/hash/URL assessment requests and provenance-qualified verdicts, including provider/dataset/model version, scope, confidence, unknown/failure and retention. It must not declare criminal guilt, change Publisher/Media/Marketplace records or substitute its scan flag for the proposed Moderation case. Mandatory unknown verdicts require the source owner's risk-defined protective behaviour; no false `clear`. External IWF/NCII/classifier services need vetted lawful terms, sensitive-data minimisation, costs and alternative failure modes.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine submits bounded candidate text/link evidence with comment/target revision, classification context and purpose. Content Security returns provenance/version-qualified assessment or explicit unknown; it does not approve publication or adjudicate legality. Comments Engine enforces risk-defined hold/pending/reject, reassesses material edits, and must not expose unscanned text when required checks are unavailable. Prohibit private reporter leakage and unrestricted foreign provider transfer.

## Reciprocal conceptual note — Course (17 November 2026)

**Status: Proposed, pending owner approval.** [Course review](../course/capability-record.md), draft PR #56: Course submission and linked learning content must meet required Content Security checks before public exposure; Course owns curriculum publication, Content Security owns scanning verdicts. Failed/unknown required verdicts block exposure; concurrent Content Security PR #55 remains provisional. This does not complete content_security's own review.
