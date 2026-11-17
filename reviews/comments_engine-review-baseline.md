# Comments Engine — conceptual review baseline

**Opened:** 17 November 2026  
**Status:** In progress; non-normative blueprint review; no conceptual approval implied.  
**Target:** `docs/capabilities/comments_engine/capability-record.md`  
**Review branch:** `review/comments_engine-conceptual-20261117`

## Phase 0 immutable opening baselines

- Governing `nuxt-layers/architecture-rules` `master`: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
- Blueprint `nuxt-layers/architecture-blueprint-review` `master`: `49a12948c18f35bfd58fec632f1cbd4fd67b9a25`.
- Procedure: [parallel capability review protocol](../docs/review-protocol.md).
- The target record exists and contains its original pro-forma and the 17 November Online Safety/Moderation reciprocal note.
- Preliminary PR/title search found the merged review protocol PR #51 and online safety governance PR #47; no dedicated Comments Engine review branch was found by branch-name search. Recheck concurrent work during review and pre-merge.

## Review scope and intended deliverables

- Classify independent responsibility and ownership of comment/thread records, visibility, edit/deletion, moderation-specific state, native operations and exclusions.
- Verify current accepted governing ADRs, normative standard, working catalogue and active proposals; distinguish binding authority from provisional concepts.
- Inspect whether a Comments Engine implementation repository and root `CONTRACT.md` exist; related implementations only through root contracts.
- Define idealised public inbound/outbound semantics, commands, queries, events, evidence, provenance, failure, recovery and conceptual acceptance.
- Document relationships and dated reciprocal findings in relevant capability records, particularly Moderation, Content Security, Authorisation, Authentication, Audit, Logging, Reporting, Notifications, Publisher and Federation where justified.
- Examine UK online safety/privacy risk, content integrity, rate limiting, abuse, retention, moderation escalations and host-owned GUI integration.
- Apply full technical **and** architectural consistency checks against current master before any merge request; leave decisions requiring owner consent explicitly open.

**Constraints:** Blueprint documentation only; no implementation changes, local tests/builds, governing edits or merge without explicit owner approval.
