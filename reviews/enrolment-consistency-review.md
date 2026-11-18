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
