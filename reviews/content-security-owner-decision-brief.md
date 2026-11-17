# Content Security — scope clarification and owner decision brief (17 November 2026)

**Status:** Proposed clarification in the existing draft PR #55. This is not owner approval, implementation design, or merge authorisation.

## Current baseline change

Blueprint `master` advanced from `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299` to `b0b026931c4b66ec4bfc445489147045497db890`, including merged Configuration PR #53 and Content Editor PR #54. At the first post-merge comparison, this branch was 15 commits ahead and 2 behind; overlapping documentation includes `configuration`, `content_editor`, `content_security`, `publisher`, `privacy`, `media`, `audit` and `logging`. Both Git conflicts and semantic differences must be reconciled on **this PR** before merging; the original master-baseline technical review is now historical and insufficient.

## Naming correction

The owner has identified underscores in capability directory names as a typo and wants canonical **hyphenated capability names** (e.g. `content-security`, `content-editor`, `comments-engine`). The existing `docs/review-protocol.md` explicitly requires real current paths rather than inventing hyphen aliases. A platform-wide path normalisation affects many active concurrent PRs and relative references, so it needs a **separately scoped, coordinated directory/link migration** after confirming its scope and collision-free sequencing. Until that migration, preserve actual checked-in paths and distinguish canonical names from filesystem paths; do not claim a rename has occurred.

## Ownership clarification

- **Content Security** is a reusable detection/assessment service for potentially untrusted content and link/file signals, with versioned scope/completeness/unknown states. It does not own a global safe/unsafe publication judgement.
- **Moderation** (still a candidate) is cross-domain report/case/investigation/adjudication/appeal coordination. It does not duplicate automatic scanning or directly mutate every source.
- **Originating owner** (Publisher, Comments Engine, Media, Marketplace, and where justified Document) performs input validation, chooses an appropriate public-content exposure policy, invokes the public assessment contract when required, and authoritatively holds/publishes/removes its own revisions. Content Editor is a presentation consumer of those controls, not a second content owner.
- **Security everywhere** means every content-producing/importing/transforming/distributing capability must have applicable safe-processing/permission/rendering safeguards, not that every private byte must be shipped to an external classifier. Assessment coverage is risk-, modality-, audience-, purpose- and jurisdiction-specific; file malware screening is distinct from text abuse and legal review. Old scan results do not apply to new content revisions; links may need rescanning; caches, previews and Hubs require independent withdrawal enforcement.
- **Publisher** must call Content Security through its published interface for required checks, and preserve independent authoritative publication/hold state. Media owns media variant exposure and secure bytes access through Storage. Document lifecycle ownership remains under separate review, and should not be prematurely transferred from Publisher.

## Decision options — not approved yet

| Proposed ID | A | B | C (recommended) |
|---|---|---|---|
| CS-09: timing and coverage | Universal intensive pre-use scanning | Minimal selectively applied scanning | Baseline validation for untrusted inputs plus risk/medium/exposure-dependent mandatory checks; required missing checks produce protective incomplete state |
| CS-10: disclosure | Full detector evidence to all viewers | Opaque notices | Plain-language status/reason and appeal, privileged detail only for authorised reviewers, no evasion-enabling methods or private content leakage |
| CS-11: evidence retention | Copy and retain all scanned content | Delete all evidence immediately | Keep minimal provenance/assessment records; strictly scoped sensitive evidence only where justified by purpose, retention and qualified legal duty |
| CS-12: compromised detector | Continue using it | Disable all checks | Immediately isolate affected detector; use approved replacement where possible; hold affected exposure where mandatory checks unavailable; audited emergency change |

**Owner approval required:** CS-09–CS-12 and earlier CS-01–CS-08 remain proposals unless already supported by an explicitly approved prior cross-capability principle. No owner approval to merge is implied. Decisions must preserve applicable legal/security floors and protect private/E2EE material from indiscriminate scanning.

## Revalidation gates

Once decision text is confirmed, reconcile merged #53/#54 with all affected reciprocal files, review any concurrently merging PRs, compare against latest `master`, inspect real PR mergeability/CI, links, historical notes and decision statuses, and request explicit squash-merge approval. No local tests/builds or implementation changes.
