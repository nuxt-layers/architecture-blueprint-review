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
