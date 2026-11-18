# Gaming — conceptual review baseline

**Status:** Proposed, non-normative; no owner sign-off.
**Target:** `docs/capabilities/gaming/capability-record.md` (existing pro-forma).
**Branch:** `review/gaming-conceptual`.
**Governing master at opening:** `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
**Blueprint master at opening:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
**Open gaming reviews found at opening:** None.

## Scope

Validate gaming as an independent domain rather than an application composition; define authoritative game/session/participant/score/ranking boundaries, native and external modes, lifecycle, idealised public inbound/outbound contracts, cross-capability exchanges, reciprocal notes, GUI, security, legal obligations and acceptance scenarios. Verify root implementation contract if present. No implementation edits, local tests, governance changes or merge.

## Pending decisions

Exact separation between game definitions and game runtime; competitive rankings, integrity/moderation and age-sensitive participation; ownership of rewards/financial elements; provider neutrality and interoperability.

## Architectural and technical reconciliation — 18 November 2026

**Recheck:** governing `master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2` unchanged; blueprint `master` `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` unchanged at this check. PR #71 compare: 10 commits ahead, zero behind, 10 expected documentation files only. GitHub PR metadata currently reports `mergeable: false`; this is **not a clean mergeability certification**, notwithstanding the compare status. Do not attempt merge or claim all protected checks passed. No local tests were run. No implementations were edited.

**Architectural review:** Gaming's independently meaningful core is games/match rules, participation, accepted turns, scores and rankings. Authority collisions were addressed with Identity, Authorisation, Events, Assessment, Moderation and Reporting through additive reciprocal notes. Persisted results are distinct from derived report views; financial transactions, wagering, general calendaring and educational credentials are excluded. ADR-0017 parent-tenancy denial and ADR-0018 policy authority applied. Still require owner decisions GAM-01–08, legal assessment for children/online-safety or prize-bearing play when actually in scope, and validation of any eventual implementation root contract.

**Concurrent reviews:** Events review PR #67 is open and may alter the same `docs/capabilities/events/capability-record.md`. Federation PR #69, Gallery PR #70, Export PR #68 and event-bus PR #66 also coexist; no unmerged proposal is treated as accepted authority. The reciprocal Events note is intentionally bounded; preserve both lines of work on later reconciliation. Shared catalogue/register edits may also intersect other open reviews. Re-fetch current master/PR changes and perform an actual mergeability/CI review after owner decisions and again immediately before any approved squash merge.

**Document integrity:** The target directory uses `gaming` exactly. Existing pro-forma sections are retained and populated, plus source/consumer link references. No deliberate deletions of another capability's content. These checks are review evidence only; link validation, CI and protected branch checks remain unverified.

## Approved decisions and reconciliation (18 November 2026)

Owner approved all Section 2 requirements including runtime-loaded isolated game plugins and public pseudonymous handles, and explicitly authorised squash merge following technical/architectural reconciliation. Latest governing `master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`, latest blueprint `master` `4adac0379d4df132c034688a35e5fbbd81548d46`. Preserve concurrent accepted content in reciprocal records. No implementation changes or local tests.
