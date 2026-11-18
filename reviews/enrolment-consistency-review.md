# Enrolment — independent conceptual and technical consistency review

**Date:** 17 November 2026. **PR:** [#60](https://github.com/nuxt-layers/architecture-blueprint-review/pull/60). **Status:** Independent documentary challenge completed on the then-current master; **owner decisions and pre-merge checks still outstanding**. Non-normative.

## Baselines and actual diff
- Governing `architecture-rules/master`: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953` at opening and documentary consistency check.
- Working `architecture-blueprint-review/master`: `b0b026931c4b66ec4bfc445489147045497db890` at opening and comparison.
- `master...review/enrolment-conceptual`: ahead six commits, behind zero at documentary comparison; six affected files (Enrolment, Course, Training, Booking, Identity and review baseline).
- Target directory `enrolment` verified. Main capability pro-forma previously unfilled; Course/Training neighbouring pro-formas unfilled. Booking and Identity have substantive existing text, retained with additive reciprocal notes.
- Governing catalogue explicitly classifies Enrolment, Course, Training and Booking as distinct *candidates*; it does not confirm existence or implementation of their APIs. Identity and Authorisation root `CONTRACT.md` were inspected read-only; target `enrolment`, `course`, `training` and `booking` published root contracts were not retrievable. No claimed runtime tests or package compatibility.
- ADR-0017/0018 document headers retain wording “Proposed for acceptance in this PR” despite the documents being visible on governing master. Their effective acceptance/status should be verified from governing merge history before claiming binding governance; all record references remain conditional on accepted authority.

## Challenge findings
1. **Independent boundary:** course content/offering, learner identity, verified learning achievement and paid transactions remain outside Enrolment. Case/offer/admission/withdrawal authority is independently specified, subject to ENR-02 and confirmation of distinct need.
2. **Capacity:** ensure exactly one capacity owner per cohort. The recommended ENR-01 path has no second writable availability/seat ledger. Booking remains conditional. Cross-service atomicity is not promised.
3. **Access and assurance:** no group membership/tenant parent, guardian claim, provider notification or enrolment event is itself a grant. Represented minors and personal education data require specialist applicable constraints.
4. **Reliable operations:** idempotent commands, stale version handling, durable owner events, read-back reconciliation and linked transfer exception are explicit. Ensure provider cutovers cannot create simultaneous authoritative masters.
5. **Policy:** configuration does not overrule legal/security floors. Accepted ADRs take precedence over conceptual suggestions; provider-neutral ports avoid direct package cycles.
6. **Presentation:** learner, guardian, admissions and operator dashboards use public contracts, with host navigation, disclosure discipline, WCAG 2.2 AA, localisation and accessible failure states.
7. **Reciprocal documentation:** additive notes are made in Course, Training, Booking and Identity; their independently pending reviews are not silently completed or approved. Catalogue/register candidate classifications are already accurate and therefore were not reclassified.
8. **Open decisions:** ENR-01–ENR-07 remain owner approval items. They must not be presented as agreed or implemented.

## Remaining gate before merge
- Re-fetch both latest masters and all material concurrent PRs; verify statuses, authority and actual Git mergeability.
- Resolve substantive owner decisions ENR-01–ENR-07; reconcile any approved Course/Training/Booking changes or conflicts.
- Check changed paths, docs links, contract consistency, dependency acyclicity, authorisation and supplier authority. Check CI/review evidence available at merge time; **do not run local tests**.
- Obtain explicit owner approval **before** protected squash merge. No merge or implementation-repository modification is authorised.

## Owner decisions — update 18 November 2026

ENR-01 through ENR-07 were all expressly approved, with ENR-02 clarifying that application, admissions acceptance and enrolment confirmation are Enrolment-owned but distinct states, and ENR-07 explicitly requiring idempotent business rollback/compensations and reconciliation of irreversible or uncertain external changes. The original open-decision statements above describe the historical review state, not current approval status. Main Enrolment capability record has been updated. This approval **does not authorise merging**. The branch fell nine commits behind blueprint `master` as checked before this update; reconciliation, technical and architectural checks against latest master, and an explicit merge instruction remain outstanding.

## Contract, GUI and rollback clarification — 18 November 2026

Owner has expressly **closed ENR-02** and approved **ENR-07 including a hardened rollback utility**. The Enrolment record now documents its logical public commands/queries/events and recovery interface, a scoped input/output exchange with cooperating owners, and a proposed learner/admin/operator presentation following the read-only inspected `nuxt-layers-test/application-test-template` README and `theme-manager/CONTRACT.md`. No Enrolment root `CONTRACT.md` or implementation surfaces were verified. The host's accessible sidebar entry to a capability dashboard is a **proposal**; Theme Manager test mode must not be treated as production IAM. This remains a conceptual-only documentary change; current master alignment and actual PR mergeability require checks immediately before any later expressly approved merge.

## Final pre-merge gate — 18 November 2026 (concept accepted; merge NOT authorised)

- **Conceptual acceptance:** owner explicitly accepted sufficient completeness. ENR-01–ENR-07 approved/closed. The Enrolment contract covers inbound evidence/commands, outbound results/queries/committed events, permissions, ownership, provider partitioning, capacity, admission and hardened transfer compensation. Public runtime `CONTRACT.md` and implementation remain unverified and are not part of this conceptual acceptance.
- **Current governing baseline:** `architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; normative Capability Standard inspected. ADR-0017 and ADR-0018 now explicitly say **Accepted** in their headers. Enrolment's tenant-isolation and bounded policy authority align conceptually with them.
- **Current blueprint baseline at checks:** `architecture-blueprint-review/master@e98833ebfe15f67362f0895b644dfe25916dc11e`. Initial PR branch diverged by nine upstream commits. These brought substantial Course/Training review records and additional reciprocal notes, unlike the original unfilled pro-formas. Branch files have been rewritten by preserving the newest `master` copies of Course, Training, Booking and Identity plus narrowly additive Enrolment reciprocal notes. Current Enrolment record includes the newer master's adjacent-capability reciprocal notes. This is **semantic/documentary reconciliation on the PR branch**, not yet a Git merge of latest master ancestry.
- **Technical gate:** GitHub PR #60 previously reported `mergeable=false` because of divergent/overlapping edits. The repository history must be **actually reconciled and mergeable** before any merge. No confirmation of a conflict-free Git merge or CI success exists yet. An absence of returned combined commit statuses is not a passing test.
- **Architecture checks:** no duplicate seat authority, learner identity, learning achievement, course specification, payments or audit custody; guarded verified external-provider and guardian facts; strict tenant/actor access, consent minimisation, versioned source/decision provenance; failure/compensation and provider uncertainty explicit; no claimed dependency cycle or automatic permission grant from events; host-owned dashboard navigation with optional headless/presentation split. Future acceptance testing remains a distinct implementation concern.
- **Review scope:** capability record, four reciprocal notes and review records only; no implementation repositories changed, no local tests run. Current documentation includes conceptual GUI screens and representative test-template usage.
- **Release gate:** conceptual status **accepted**, PR may be marked ready for review once actual mergeability is verified; **do not merge** without explicit subsequent owner authorisation, and recheck newest baselines/CI immediately before authorised protected squash merge.

## Git reconciliation completed — 18 November 2026

**Actual Git result:** resolved concurrent master changes using a two-parent merge commit `d6e4050f5ea8e2d64fad7a9c7b347d5a19ec44d2` (parents: PR review head `26659e8ddf865c26001f99f0a39bbf8ce34742a2`, then blueprint `master@e98833ebfe15f67362f0895b644dfe25916dc11e`). The resulting tree was based on the exact master tree, with the seven intended review paths replaced by their reconciled, preservation-checked PR versions. All other master paths remain unchanged.

**Preservation check:** the full master records for Course, Training, Booking and Identity occur unchanged in the reconciled files, followed by Enrolment-specific additive notes; all later master reciprocal notes are preserved in Enrolment's accepted record. The diff against master is seven paths only: Enrolment, the four reciprocal capability records, and two review records; no substantive new master content was overwritten or discarded. `master...review/enrolment-conceptual` reported **behind 0, ahead 18** immediately after reconciliation. GitHub's REST PR detail reported **`mergeable: true`, `mergeable_state: clean`** on the reconciled head, despite its compact PR summary briefly reporting a stale `false` while recalculation completed.

**Checks and authority:** governing `architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2` reviewed, including accepted ADR-0017/0018 and the normative Capability Standard. GitHub reports **zero check runs** for the merge head; this is not a CI pass. Branch-protection API access was refused by integration, so those controls are not independently verified. The technical check here covers documentary content/ancestry, not runtime tests or release evidence.

**Decision:** conceptual specification **accepted**; Git ancestry reconciled and GitHub reports content merge clean. Owner has **not authorised the protected PR merge**; do not merge without a separate explicit instruction. Recheck head/base and mergeability immediately before any later merge.
