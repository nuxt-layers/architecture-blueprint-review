# Media — conceptual review baseline

**Status:** Draft, non-normative; subject to architectural review and owner approval.
**Target:** `docs/capabilities/media/` (existing exact directory).
**Branch:** `review/media-conceptual-20261119`.
**Governing `architecture-rules/master` opening SHA:** `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
**Blueprint `architecture-blueprint-review/master` opening SHA:** `6dac83a03da8704f7945ee1bc894f2248300445a`.
**Related work:** Existing media reciprocal notes regarding Content Editor, Gallery, Content Security, Course, Moderation and online safety. No active PR with media in title found during opening check. All concurrent PR findings remain provisional until merged.

## Scope

Inspect governing accepted ADRs, current catalogue and public implementation `CONTRACT.md`; distinguish verified interfaces from idealised design. Establish authoritative media ownership and native lifecycle, idealised public inputs/outputs, commands/queries/events, provider and failure semantics, cross-capability reciprocity, security/privacy/content safety, GUI and host integration, and conceptual acceptance scenarios. Update relevant catalogue/register and reciprocal documents without replacing neighbouring work. Conduct latest-master technical and architectural consistency review before any merge; no implementation changes, tests or merge in this review.


## Technical and architectural consistency review — 19 November 2026 (draft, not pre-merge authorisation)

- Latest governing `master` remains `b920ce0d8b361de000a6739a16123dbdc56df7a7`; latest blueprint `master` remains `6dac83a03da8704f7945ee1bc894f2248300445a` at review. Branch compare: **11 ahead / 0 behind**, no newer master reconciliation presently needed.
- PR #92 changed-file scope: Media record, seven dated bounded reciprocal capability records (Storage, Publisher, Content Editor, Gallery, Content Security, Moderation, Course), working catalogue/register and this baseline; no implementation files. Existing reciprocal content preserved.
- **Authority:** accepted ADR-0012 requires provider-neutral `storageFor('media')`, same structural caller/access ports, capability-owned outbox and <50-line Nuxt composition; accepted ADR-0016 requires acyclic declared relationships. Media is state-owning Platform; Storage owns bytes, Publisher owns document links, Content Security detection, Moderation cases only provisionally, and Media enforcement. No duplicate business authority proposed.
- **Document boundaries:** documented input/output interfaces are explicitly conceptual; root Media `CONTRACT.md` missing and README says unbuilt. Publisher published `assets.resolve` expectation is consumer evidence only. No test, runtime, legal compliance or signed-off contract claim.
- **Concurrent work:** open adjacent draft PRs include Marketplace #91, Mailer #90, Logistics #89, Logging #88, Location #87 and other parallel reviews. They may advance or change shared records before merge. Recheck files, SHA, statuses and architecture immediately prior to a separately approved merge.
- **Git readiness limitation:** GitHub PR metadata currently reports `mergeable: false` despite a clean ancestry compare; this must be diagnosed at pre-merge review. No combined commit-status entries were returned; that is **not** evidence of passing CI. No tests executed.
- **Open:** owner decisions MEDIA-01–MEDIA-08, published Media/Storage contract reconciliation, concrete safeguarding/legal qualification, expiry/revocation/CDN and original-download acceptance, and CI checks. The initial review is **draft only**, not conceptually approved or ready to merge.
