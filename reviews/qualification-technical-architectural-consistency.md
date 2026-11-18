# Qualification — technical and architectural consistency (18 November 2026)

**Status:** Non-normative draft PR #65, review against current master at inspection; rerun before any approved merge.

## Baselines and exact scope

- Governing `architecture-rules/master`: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953` (unchanged from opening).
- Blueprint `architecture-blueprint-review/master`: `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9` (unchanged from opening).
- Draft branch `review/qualification-conceptual`, comparison at review: **9 commits ahead, 0 behind**, nine files changed; no recorded status checks for last observed head. This verifies commit ancestry and changed-file scope, **not GitHub PR mergeability or green CI**.
- Files: Qualification record; additive reciprocal notes in Course, Assessment, Training, Enrolment, Credentials and Integrations; opening baseline and this consistency report. Catalogue and register already list the target, so avoid redundant reclassification.
- Target exact path: `docs/capabilities/qualification/capability-record.md` (not a hyphenated alias). Proposed reciprocal relative links `../qualification/capability-record.md` and baseline `../../../reviews/qualification-review-baseline.md` resolve by repository structure.

## Governing status review

- Accepted ADR-0012: independent consumer contract, one composition call, 50-line Nuxt budget, shared caller/access shapes, capability-owned outbox.
- Accepted ADR-0016: explicit acyclic dependency and extension graph; domain information exchanged both ways does not justify circular package imports.
- Normative architecture and Capability Standard: bounded state and authority, server-side access decisions, provider neutrality, defaults, WCAG 2.2 AA, OWASP ASVS 5 L2 (risk-based L3).
- **Important status distinction:** ADR-0017 and ADR-0018 currently have headers **"Proposed for acceptance in this PR (normative only when merged)"** in the governing repository despite being mentioned by the current Capability Standard §9. Do **not** upgrade their individual proposal text to accepted ADR authority without confirming merge/status. This review's tenant/policy separations are independently consistent with existing accepted server-side isolation, decision and domain-ownership principles; any stronger specific obligations from ADR-0017/0018 are provisional pending governance reconciliation.

## Architectural challenge

1. **Unique owner:** Qualification owns scheme rules, local formal awards and source-qualified external decision references. Course owns curriculum; Assessment owns marks; Training owns actual achievements; Enrolment owns admissions; Credentials owns credential lifecycle; Integrations owns providers, not accreditation decisions. No new generic Awarding domain justified.
2. **Authority:** External regulator/accreditor/awarder remains authoritative for its own recognition and decisions. An IAM role, configured value or technical connector cannot bestow mandate. Expired, disputed and unknown powers must block new formal decisions. Delegated and external-only paths remain distinct.
3. **Lifecycle:** Immutable versions, appeals, teach-out and historical awards with applicable effective time; late provider events and corrected evidence trigger case reconciliation, never overwrite source facts or automatically revoke an award.
4. **Public contract:** Conceptual inbound/outbound, command/query/event semantics, completeness, status, provenance, idempotency and separate Credentials acknowledgement are documented. Actual package signatures and root `CONTRACT.md` remain implementation alignment, not verified.
5. **Cycles:** Host-supplied ports, externally published immutable source references and committed events allow reciprocal knowledge without requiring runtime imports in both directions. Future implementation must prove actual import graph.
6. **Privacy/security:** Qualification case evidence may be high-risk personal data; enforce strict tenancy, least privilege, actor assurance, retention/legal constraints, issuer mandate checks, external-source trust and disclosure minimisation. No verified legal-compliance claim.
7. **GUI:** Optional dashboard and role-scoped decision/appeal/recognition workspaces over public headless contract; host owns sidebar/routing and Theme Manager styling. Test architecture for accessibility and suppressed administrative exposure later.
8. **Parallel changes:** #60 Enrolment, #62 Credentials, #63 Training, #64 Assessment and #57 Department remain provisional, with overlapping reciprocal records. Reconcile after any merges, preserving their independent owner decisions. No authoritative conflicts identified in current master, but concurrent draft work is not incorporated here.
9. **External evidence:** A `nuxt-layers/qualification` implementation repository was not located by organisation repository search. Absence of a result is not proof that no private/inaccessible repository exists. No target implemented contract, provider/API or acceptance evidence claimed.
10. **Scope and approval:** All changes stay in the original PR #65; no normative repository or implementation modification and no local tests. QUAL-06–08 are proposed, QUAL-09 open, QUAL-10 technical investigation, QUAL-11 future implementation alignment.

## Pending pre-merge gates

- Re-fetch exact governing/blueprint `master` SHAs, newly accepted ADRs, PR head and diff.
- Inspect and resolve GitHub mergeability, merge conflicts and concurrently merged changes, *including both sides of reciprocal additions*; do not equate ahead/behind with conflict-free.
- Inspect required GitHub checks/CI, protected-master policy, broken links, accidental deletions and decision statuses. No tests/builds were run by assistant; CI/user is responsible.
- Confirm independent contractual consumer and domain workflow acceptances and obtain explicit owner approval before protected squash-only merge.

**Judgement:** Suitable for owner conceptual review; **not cleared for merge** until current GitHub mergeability/checks and updated governing/parallel architecture are verified, owner decisions resolved, and explicit approval received.
