# Content Security — technical and architectural consistency review (17 November 2026)

**Status:** Pre-merge review of conceptual documentation in draft PR #55; **not** merge authorisation. Recheck immediately before any proposed squash merge.

## Verified baseline and Git comparison

- Governing `architecture-rules/master`: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953` (same as opening read).
- Blueprint `architecture-blueprint-review/master`: `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299` (same as opening read).
- Opening and current protocol: `docs/review-protocol.md`, PCR-01–PCR-10.
- `master...review/content_security-conceptual`: **ahead 14, behind 0** at comparison; 14 changed documentation files, no implementation changes. This is Git history comparison, not certification of mergeability, branch protection or CI.
- The review is currently draft; **no merge attempted**. GitHub's PR mergeability must be rechecked independently after asynchronous recomputation and immediately before any approved merge.

## Architectural consistency

1. The governing catalogue already classifies Content Security as a Platform capability; no catalogue reclassification or new infrastructure service proposed. Its detection-only ownership respects the online-safety architecture and Comments Engine findings; Moderation owns cases, source owners decide and enforce publication, Legal Compliance qualifies obligations, Audit holds independent evidential accountability.
2. Accepted ADR-0012 provider-neutral one-operation composition and <=50 capability-specific host lines, ADR-0002 persistence ownership, ADR-0009 separable screens, and normative Capability Standard/Privacy/Security/WCAG apply. No new universal request shape, mandated provider, direct Nuxt extension or cross-owner database access introduced.
3. ADR-0018 file reads **Proposed for acceptance** even on governing master; treat as provisional. No claim of statutory OSA compliance, deployed coverage, implementation functionality or independently passed acceptance tests.
4. Source revision-bound scans, supported-check completeness and explicit unknown prevent scan/pub TOCTOU and false clear. The source owner must apply its own risk-based exposure rule; scanned and cleared are not equivalent to safe or lawful. Domain disposal, Moderation appeals and Audit evidence remain separate.
5. Existing preserved notes under target record survive; reciprocal notes are additive and provisional. Concurrent draft PRs #53 (Configuration) and #54 (Content Editor) both edit shared records, so **future merge conflicts/semantic reconciliation are expected if those PRs merge first**. PRs #56–#58 also active; check newly changed reciprocal files before integrating. No conflicting accepted decisions identified in currently read master.
6. The target implementation repository exists at `f27469c66aee3cc13e81a0e0fd0554125ab884cb`; root `CONTRACT.md` not retrievable. No runtime/CI proof established. Conceptual contract is deliberately **not** asserted to be an implementation API.
7. Internal links use actual underscore directories and relative paths; scope is documentation only. A further link, decision-ID, provenance, permission and cross-PR consistency audit is required if master changes.

## Outstanding before merge

- Owner review of proposed CS-01–CS-08 and open policy decisions (mandatory initial checks, user/Hub disclosure, sensitive evidence retention and emergency detector override).
- Reconcile concurrent PR #53/#54 shared records and any subsequent source-owner review, preserving both lines of work; compare against updated master and resolve real conflicts.
- Independently check PR mergeability, branch protection and required CI checks on current head. No local tests/builds were run under user instruction.
- Obtain explicit owner permission before protected-master squash merge. No repository merge is authorised by this review file.
