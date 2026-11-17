# Course conceptual review — opening baseline

**Status:** In progress; non-normative proposal, not approved.

- Target: `docs/capabilities/course/capability-record.md` (existing directory `course`).
- Review branch: `review/course-conceptual`.
- Governing `nuxt-layers/architecture-rules` master: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
- Blueprint `nuxt-layers/architecture-blueprint-review` master: `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`.
- Protocol: `docs/review-protocol.md` at opening blueprint baseline.
- Target record presently an unfilled pro-forma; substantive ownership, interfaces and GUI remain to be reviewed.
- Initial PR search: no open PR matching `course`.

## Planned scope

Establish precise Course classification, native behaviour, authoritative course records and lifecycle, input/output public contracts, cross-capability boundaries and reciprocal notes, security and privacy, administrator/learner GUIs, acceptance scenarios, and open owner decisions. Validate consistency against current master before any future merge. No implementation changes, local testing or merge are authorised.


## Technical and architectural consistency checkpoint — 17 November 2026

**Compared with live master after substantive edits:** governing `architecture-rules/master` remains `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint `master` remains `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`. `master...review/course-conceptual` comparison reports **ahead 22, behind 0**, with all changes confined to this branch. PR #56 is draft/open, **GitHub reported mergeable=false** at the checkpoint, so merging is not ready regardless of Git branch ancestry. The combined commit-status endpoint returned no statuses; this is **not** evidence of passing branch checks or CI. No tests/builds have been run.

**Document scope:** one substantive Course record, this baseline/checkpoint and additive notes in 20 related capability records; no implementation or governing repository files edited. Links use same-directory relative capability paths; `course`, `enrolment`, `training`, `content_editor`, `content_security`, `legal_compliance` are literal, verified directories. Catalogue/register already identify Course as Domain candidate and Enrolment/Training separately, so no classification promotion is made. No decision status is represented as approved.

**Architectural boundary challenge:** Course owns outcome **definitions** and frozen course revisions; Enrolment owns learner admissions and allocation; Training owns verified achievement/completion; Publisher owns learning-material documents; IAM retains identities and access. Course's downstream event subscribers are not reciprocal code imports; no required capability import cycle was introduced. Security/privacy/provider/GUI and error/unknown semantics are proposals rather than runtime claims. No Course implementation repository was found; actual CONTRACT.md and acceptance evidence are unavailable.

**Concurrent integration risks:** PR #53 Configuration, #54 Content Editor, #55 Content Security overlap reciprocal documents and remain **unmerged/provisional** at this checkpoint. Review their latest patches before integrating; reconcile additive notes without discarding other reviews, and repeat current-master checks if any base advances. There may be other publication, legal and training proposals not yet reconciled. Course's assessment/cohort/accreditation authority choices (COURSE-08–11) require owner discussion and/or future adjacent reviews.

**Outstanding pre-merge blockers:** GitHub mergeability currently reported false; protected branch/required checks not verified; no explicit owner conceptual approval or merge authorisation. Re-run technical conflict analysis, normative ADR and architectural consistency against fresh master immediately before any authorised squash merge. No merge attempted.
