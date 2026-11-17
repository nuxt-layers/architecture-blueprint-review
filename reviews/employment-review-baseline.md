# Employment — conceptual review baseline

**Status:** Open conceptual review; non-normative; no owner sign-off.
**Target:** `docs/capabilities/employment/capability-record.md` (exact directory: `employment`).
**Branch:** `review/employment-conceptual`.
**Opening governing master:** `nuxt-layers/architecture-rules@2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
**Opening blueprint master:** `nuxt-layers/architecture-blueprint-review@b0b026931c4b66ec4bfc445489147045497db890`.
**Review protocol:** `docs/review-protocol.md` (master at opening).

## Scope

Determine Employment's domain ownership, employee/worker/contractor engagement lifecycle, and boundaries with Identity, Job, Payroll candidate, Accounting, Configuration, Authorisation, privacy and external HR providers. Define native services, idealised inbound/outbound commands, queries, events, evidence, failure rules, reciprocal records, GUI and conceptual acceptance scenarios. Inspect governance and implementation evidence; classify open decisions. Carry out current-master technical and architectural consistency checks before requesting merge approval.

## Opening evidence and provisional work

Existing Employment record is a pro forma with 14 November notes distinguishing Identity group membership, employment engagements, Payroll and Accounting. No existing Employment target PR found in open PR search; concurrent adjacent reviews require reconciliation. Proposals are not approved contracts. No implementation edits or local tests; no merge without explicit owner authorisation.

## Review evidence, reconciliation and consistency — 17 November 2026

- Phase 1 authority: governing master `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint master `b0b026931c4b66ec4bfc445489147045497db890` at opening and at this comparison.
- Governing read: normative `docs/capability-standard.md`, `docs/identity.md`, `docs/catalogue.md`, ADR-0012 (Accepted); ADR-0017 and ADR-0018 documents are present on governing master yet their own headers still say "Proposed for acceptance in this PR", an internal document status inconsistency requiring governance clarification rather than silently recategorising them. Their tenant/legal-party separation and policy guidance are treated cautiously. No governing edits made.
- Existing Employment entry was an uncompleted pro forma with provisional 14 November notes. Direct accessible repository lookups for Employment and Payroll returned 404; no root public implementation contract was verified.
- No pre-existing open Employment PR appeared in the initial target search. Concurrent active review PRs at comparison include #55 Content Security, #56 Course, #57 Department and #58 Document. #59 deliberately avoids modifying these concurrently reviewed records; they still need future reciprocal reconciliation, especially Document/Department.
- Reviewed published blueprint context in Accounting, Billing, Job, Identity, Profile and Department. The Job and Department records are incomplete templates on master. No invented Job API or legal-party master is asserted.
- One review PR contains the Employment record, bounded reciprocal notes in Accounting/Job/Profile/Identity/Authorisation and this baseline document. These are proposed, not signed off. Cross-references are relative to existing capability paths.
- Git branch comparison against latest blueprint master: branch seven commits ahead, zero behind, seven changed files; no detected base advancement at comparison. The GitHub PR snapshot reports `mergeable: false`; this is **not** evidence of readiness, and actual reason/check status must be re-evaluated before merge.
- Architectural challenge: employment versus membership, position, provider authority, payroll calculations, accounting postings, medical/personnel confidentiality, legal employer and contractor categorisation are explicitly separated. Remaining decisions EMP-01–EMP-07 await owner review; legal classification and retention require qualified investigation. A Payroll domain, time/attendance owner and employer legal-party owner cannot be assumed implemented.
- No implementation repositories modified. No local tests/builds or merge performed. Mandatory current-master technical/architectural consistency check must be repeated after material changes and immediately before any owner-approved merge.

## Owner decisions — 17 November 2026

Owner explicitly approved EMP-01–EMP-07 Option B. For EMP-03, owner additionally asked where working hours should reside and identified scheduling as the planned-time owner. Proposed clarification (not separately approved yet): Employment contains bounded Time & Attendance ownership for actual worked-hours evidence; Workforce Scheduling owns planned rosters; existing platform Scheduler owns only background triggers. The Employment record and Scheduler reciprocal record now distinguish these domains. No separate Workforce Scheduling or Time & Attendance repository has been authorised. Before merging, reconcile all current master changes and GitHub checks; do not treat original consistency comparison as sufficient.

## EMP-03 follow-up resolution — 17 November 2026

The project owner approved the revised EMP-03 model: **independently owned Time & Attendance Domain responsibility**, separate from Employment's contractual terms, proposed Workforce Scheduling's planned shifts and infrastructure Scheduler's timed job execution. The initially proposed nested Employment Time & Attendance ownership is superseded. The working catalogue and register record `time-attendance` as an approved conceptual candidate and [the ownership note](../proposals/time-attendance-ownership.md) sets preliminary inputs/outputs, exclusions, risk and acceptance questions. A dedicated future capability review should establish the complete public contract and test the packaging gate. No implementation repository or new normative governing standard was created.

## Current-master reconciliation and pre-merge review — 17 November 2026

**Governing master:** `architecture-rules@2b5c0628e88b9698c9ad6ad57cc5315c8f879953`, unchanged from initial review.

**Blueprint current master:** `architecture-blueprint-review@59918b3ccd9c0d016039abb8c91df56507108fd9` (advanced by **two commits** after opening). Compared the opening master SHA with current master, and compared PR #59 with current master: branch is 21 commits ahead and two behind. Current master touched Content Security and Document conceptual records, reciprocal notes for Audit, Comments Engine, Configuration, Content Editor, Export, Federation, Legal Compliance, Logging, Media, Moderation, Privacy, Publisher, Reporting, Search, Storage, two one-line catalogue/register deletions and related review files. **There are no overlapping capability-record paths with PR #59**; catalogue/register were changed on both sides, so recheck additive Time & Attendance entries after GitHub completes its merge, preserving new base changes.

**Technical GitHub checks:** the live PR response at this review showed `draft: false`, `mergeable: true`, `mergeable_state: clean`, 12 changed files. The initial draft status and old `mergeable: false` snapshots cited earlier are **superseded**. GitHub check-runs endpoint for the then-current head returned zero check runs, combined commit-status endpoint returned no statuses, and PR reviews endpoint returned none. Branch-protection endpoint returned 403 (not accessible to this GitHub connection), so absence of checks does **not** establish compliance with branch rules or a passing CI requirement. Before any merge, inspect GitHub's live merge button/ruleset and update the branch if required.

**Architectural consistency:** agreed EMP-01–07 and separate Time & Attendance responsibility remain coherent with governing public-boundary, IAM ownership, no implicit group employment, source-owned data, acyclic contracts, provider-neutrality, server authorisation, retention and minimal host composition. Non-overlapping current-master Document/Content Security proposals do not themselves transfer employer agreement authority or personnel processing/record authority. A separately owned actual-time source does not displace Payroll calculations, Job positions, proposed Workforce Scheduling or infrastructure Scheduler. The added Time & Attendance pro-forma is explicitly **not** a second completed capability review. Potential downstream Document agreement/attestation and Content Security evidence-screening interfaces should be addressed during implementation/reciprocal capability review; no private coupling or conflicting approved owner has been asserted here.

**Document-scope and approval checks:** exact target directory `employment` and new `time-attendance` directory preserved, 12 changed files within Employment and justified reciprocal/catalogue/proposal/review scope. EMP decisions and follow-up approval are traceable. Existing old assessment paragraphs in this file describe earlier *historical snapshots*, not the present state. No tests/builds, implementation edits, or compliance claims were made. PR may be considered **conceptually ready for owner sign-off**, subject to branch-protection/required-check validation and a final current-head and current-base verification immediately before the protected squash merge. It must not be merged merely because GitHub reports `mergeable: true`.
