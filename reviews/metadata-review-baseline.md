# Metadata conceptual review — opening baseline (19 November 2026)

**Status:** In progress; non-normative proposal, no approval implied.

- Target: `docs/capabilities/metadata/capability-record.md` (exact existing directory `metadata`).
- Review branch: `review/metadata-conceptual-20261119`.
- Opening governing `architecture-rules/master`: `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
- Opening blueprint `architecture-blueprint-review/master`: `6dac83a03da8704f7945ee1bc894f2248300445a`.
- Protocol: `docs/review-protocol.md`; governing accepted ADRs prevail over working blueprint.
- Existing record: pro-forma plus provisional reciprocal notes from Content Editor PR #54 and Course PR #56; preserve prior work.
- Scope: establish precise taxonomy/ontology/classification authority, native lifecycle, idealised public inbound/outbound contracts, cooperating capability relationships, reciprocal notes, security/privacy and accessible GUI/headless presentation.
- Verify implementation repository and root CONTRACT.md, governing statuses, open overlapping PRs and any published adjacent contracts before substantive design.
- This branch is documentation-only. No implementation edits, local tests, or merge without explicit owner approval.


## Technical and architectural consistency review (19 November 2026)

**Current master baselines rechecked:** governing `b920ce0d8b361de000a6739a16123dbdc56df7a7`, blueprint `6dac83a03da8704f7945ee1bc894f2248300445a`; both unchanged from opening. Compared `master...review/metadata-conceptual-20261119`: **11 commits ahead, 0 behind, 11 files changed**, all documentation within the authorised blueprint repository. The GitHub detailed PR response currently gives `mergeable: true`; an earlier normalised metadata response returned `mergeable: false`, so this is a live status requiring immediate recheck before merge, **not a guarantee of branch-policy readiness**. Draft state remains true.

**Architectural challenge:** Metadata-owned taxonomy/assignments do not reown Publisher document revisions/visibility, Course outcomes, Media assets, Localisation translation workflows, SEO/page addresses, Search indexes, Identity membership or Authorisation permissions. Source eligibility/revision checks are explicit and source-owned; optional dependencies remain host-wired and do not imply circular direct imports. Shared catalogue and register retain governing Platform classification and mark the detailed contract provisional. Seven reciprocal records are bounded additive notes preserving pre-existing content; no prior review was overwritten. Relative links checked for target path and seven `../metadata/` sibling references.

**Evidence gaps:** `nuxt-layers/metadata` exists but has no retrievable root `CONTRACT.md`; no published Metadata runtime API or operational tests verified. Publisher's root contract independently verified as existing and its authority preserved. No automated tests/builds run by assistant, and neither GitHub combined commit status nor PR-triggered workflow list returned checks; CI/branch protection compliance is **not verified**. Concurrent unmerged capability PRs are provisional and may introduce later reconciliation.

**Open owner decisions:** MET-01 through MET-05 (not approved), notably advanced ontology reasoning versus bounded relations and owner-local classifications. MET-06 technical port reconciliation; MET-07 implementation alignment; MET-08 future acceptance. Review remains in draft awaiting owner decisions. Repeat technical and architectural checks and obtain explicit approval before any protected squash merge.
