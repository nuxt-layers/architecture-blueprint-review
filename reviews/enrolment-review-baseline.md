# Enrolment conceptual review — opening baseline

**Status:** Draft, non-normative; no conceptual approval or implementation claim.
**Date:** 17 November 2026.
**Target:** `docs/capabilities/enrolment/capability-record.md` (directory name verified).
**Review branch:** `review/enrolment-conceptual`.
**Governing master at opening:** `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
**Blueprint master at opening:** `b0b026931c4b66ec4bfc445489147045497db890`.
**Protocol:** `docs/review-protocol.md` on opening blueprint master.

## Opening evidence and scope
- Target record is currently an unfilled capability pro-forma; working register describes enrolment as a **domain candidate**, concerned with course/learner participation and allocation, not a verified implementation.
- A repository-wide search for open PRs explicitly mentioning enrolment returned none at opening; parallel reviews of related capabilities may still affect shared records.
- Establish applicable accepted ADRs and normative authority; inspect relevant published root CONTRACT.md files only; distinguish conceptual designs from verified behaviour.
- Specify ownership/exclusions, native lifecycle, idealised public **inbound and outbound** contracts, command/query/event semantics, authorisation, provider/failure handling, cross-capability cooperation, reciprocal notes, GUI and acceptance examples.
- Reconcile any concurrent edits and perform mandatory technical/architectural consistency review against the latest master before requesting merge approval.

**Guardrails:** No implementation changes, local tests or merge. All review changes remain in the initial draft PR.
