# Comments Engine — Phase 9/10 review and consistency assessment

**Date:** 17 November 2026. **Status:** Pre-approval assessment, not an authorisation to merge. **PR:** [#52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52).

## Source and authority check

| Source | Verified master at opening and most recent check | Interpretation |
|---|---|---|
| `nuxt-layers/architecture-rules` | `2b5c0628e88b9698c9ad6ad57cc5315c8f879953` | Accepted governing baseline; catalogue establishes Platform `comments-engine`; ADR-0009, 0011, 0012 and 0016 inspected as applicable |
| `nuxt-layers/architecture-blueprint-review` | `49a12948c18f35bfd58fec632f1cbd4fd67b9a25` | Current blueprint base and opening baseline at check |
| `nuxt-layers/comments-engine` | `17d22bf9c92ee033b572391c6b53f3c3cfc22a72` | Repository exists with initial commit, but `CONTRACT.md` is not found at `master`; implementation APIs **not verified** |

Governing Charter, README, Catalogue, Capability Standard and relevant accepted ADR content were inspected. Source hierarchy remains accepted governing ADRs and standards over blueprint concepts. Working Online Safety/Moderation and Node–Hub/Federation notes are **conceptual**, not accepted governing changes. Related open PR search at the time of the check found only #52 in the blueprint repository; search results are a time-bound observation.

## Architecture and scope review

- **Classification:** Platform comments capability remains independently justified by comment/thread state and lifecycle; not UI-only nor the owner of Publisher documents.
- **Source ownership:** target resource remains with Publisher/other source owner; comments, revisions, local moderation enforcement and receipts with Comments Engine; cross-domain cases with proposed Moderation; scanning with Content Security; source evidence custody with Audit; diagnostics with Logging; aggregates with Reporting.
- **Composition:** public one-way host-supplied ports; no private imports or proposed mutually extending layers. Source-owned outbox and one-operation/50-line acceptance remain future implementation obligations.
- **Authority caution:** source comment state does not prove case resolution, downstream notification, remote Hub/cache withdrawal or statutory compliance.
- **Failure semantics:** unknown or required-scanner failure cannot produce clearance; deny unknown access; reconcile stale target/subject and remote withdrawal; preserve replay/idempotency and revision conflicts.
- **Security and privacy:** protected reporter and child evidence, sanitised logs, erasure/hold conflicts, bounded retention, tenant isolation, jurisdiction-qualified safeguards.
- **Presentation:** optional headless-safe sidebar-to-dashboard admin pattern plus contextual thread UI, separated from host navigation and cross-domain moderation case screens.
- **Documentation:** exact underscore target path retained, existing 17 November moderation reciprocal text preserved, no governing or implementation files edited. Reciprocal notes are explicitly labelled *proposed*, preserving other capability reviews.

## PR scope checked

Added `reviews/comments_engine-review-baseline.md`, this assessment, the target record, and additive reciprocal notes in Audit, Authentication, Authorisation, Configuration, Content Security, Federation, Identity, Legal Compliance, Logging, Moderation, Notifications, Privacy, Publisher and Reporting. No catalogue/register changes recommended: existing Platform classification/entry is retained.

**Git comparison (before this assessment commit):** current `master` is the opening base, branch 16 commits ahead/0 behind; PR #52 is open, draft and reported mergeable by GitHub. No other open blueprint PR was returned at the time of search. Existing status API returned no commit statuses; this **does not establish CI success or satisfaction of branch protection**. Compare, mergeability and checks must be repeated after material base/head changes and immediately before any explicitly authorised merge.

## Outstanding approval and acceptance

- **CE-01–CE-07 are proposals**, not accepted decisions. Owner should review host-registered target classes, guest/minor access, rich-text/attachments, federation, revision history/retention, counts/reactions and orphaned target threads.
- Architectural investigation remains for the actual published `comments-engine/CONTRACT.md` (absent), target-owner public registration interface, precise legal-policy applicability, external provider data handling, source cache/search invalidation and secured reader performance.
- A later implementation must independently evidence storage register, actual durable outbox, minimal-host composition and applicable 50-line cap, server-side authorisation, threat modelling, accessibility and user/CI-run tests. Nothing in this PR asserts these exist.
- **Pre-merge gates not yet satisfied:** owner conceptual approval, normative/public-contract reconciliation when implementation is available, current protected branch/check requirements, fresh comparison and explicit approval to squash merge. Remain **draft**; do not merge.

## Cross-capability and concurrent-change watch

Re-evaluate Moderation/Federation/Verification and online safety proposals if governing standards or their reviews change; pay particular attention to concurrent edits to Audit, Logging, Authorisation, Publisher, Content Security and Reporting. An additive note does not settle the neighbouring capability's own pending review.
