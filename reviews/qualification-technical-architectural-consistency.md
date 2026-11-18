# Qualification — technical and architectural consistency (18 November 2026)

**Status:** Non-normative draft PR #65, revised for governing authority and latest user decisions on 18 November 2026; rerun immediately before any approved merge.

## Baselines and exact scope

- Governing `architecture-rules/master`: opening `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; latest reviewed `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (one subsequent commit accepting ADR-0017 and ADR-0018).
- Blueprint `architecture-blueprint-review/master`: `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9` (unchanged from opening).
- Draft branch `review/qualification-conceptual`, comparison at review: **14 commits ahead, 0 behind** at review checkpoint, twelve files changed; no recorded status checks for last observed head. This verifies commit ancestry and changed-file scope, **not GitHub PR mergeability or green CI**.
- Files: Qualification record; bounded additive reciprocal notes in Course, Assessment, Training, Enrolment, Credentials, Integrations, Employment, Job and Verification; opening baseline and this consistency report. Catalogue and register already list the target, so avoid redundant reclassification.
- Target exact path: `docs/capabilities/qualification/capability-record.md` (not a hyphenated alias). Proposed reciprocal relative links `../qualification/capability-record.md` and baseline `../../../reviews/qualification-review-baseline.md` resolve by repository structure.

## Governing status review

- Accepted ADR-0012: independent consumer contract, one composition call, 50-line Nuxt budget, shared caller/access shapes, capability-owned outbox.
- Accepted ADR-0016: explicit acyclic dependency and extension graph; domain information exchanged both ways does not justify circular package imports.
- Normative architecture and Capability Standard: bounded state and authority, server-side access decisions, provider neutrality, defaults, WCAG 2.2 AA, OWASP ASVS 5 L2 (risk-based L3).
- **Newly accepted ADR-0017 and ADR-0018:** governing master advanced after opening, changing both headers to **Accepted**. Qualification's tenant separation, independently evidenced accountable legal/issuer powers, explicitly governed versioned business policy, qualified legal constraints, non-transitive tenant access and settings not creating authority align with these requirements. No ownership transfer or new capability package is implied. Cross-capability contract impact must be reviewed again if further normative changes land.

## Architectural challenge

1. **Unique owner:** Qualification owns scheme rules, local formal awards and source-qualified external decision references. Course owns curriculum; Assessment owns marks; Training owns actual achievements; Enrolment owns admissions; Credentials owns credential lifecycle; Integrations owns providers, not accreditation decisions. No new generic Awarding domain justified.
2. **Authority:** External regulator/accreditor/awarder remains authoritative for its own recognition and decisions. An IAM role, configured value or technical connector cannot bestow mandate. Expired, disputed and unknown powers must block new formal decisions. Delegated and external-only paths remain distinct.
3. **Lifecycle:** Immutable versions, appeals, teach-out and historical awards with applicable effective time; late provider events and corrected evidence trigger case reconciliation, never overwrite source facts or automatically revoke an award.
4. **Public contract:** Conceptual inbound/outbound, command/query/event semantics, completeness, status, provenance, idempotency and separate Credentials acknowledgement are documented. Actual package signatures and root `CONTRACT.md` remain implementation alignment, not verified.
5. **Employment interoperability:** Job/employer owns versioned requirements, Qualification offers qualified criterion-level education evidence, Verification handles generic trust proofs, Employment enforces legitimate ongoing engagement prerequisites, and hiring authorities decide selection. Missing/foreign qualification evidence remains inconclusive unless authorised equivalence is evidenced; changes cannot auto-terminate. Minimised data sharing follows UK GDPR purpose and source-provenance constraints. The new API is proposed, not a published contract.
6. **Cycles:** Host-supplied ports, externally published immutable source references and committed events allow reciprocal knowledge without requiring runtime imports in both directions. Future implementation must prove actual import graph.
7. **Privacy/security:** Qualification case evidence may be high-risk personal data; enforce strict tenancy, least privilege, actor assurance, retention/legal constraints, issuer mandate checks, external-source trust and disclosure minimisation. No verified legal-compliance claim.
8. **GUI:** Optional dashboard and role-scoped decision/appeal/recognition workspaces over public headless contract; host owns sidebar/routing and Theme Manager styling. Test architecture for accessibility and suppressed administrative exposure later.
9. **Parallel changes:** #60 Enrolment, #62 Credentials, #63 Training, #64 Assessment and #57 Department remain provisional, with overlapping reciprocal records. Reconcile after any merges, preserving their independent owner decisions. No authoritative conflicts identified in current master, but concurrent draft work is not incorporated here.
10. **External evidence:** A `nuxt-layers/qualification` implementation repository was not located by organisation repository search. Absence of a result is not proof that no private/inaccessible repository exists. No target implemented contract, provider/API or acceptance evidence claimed.
11. **Scope and approval:** All changes stay in the original PR #65; no normative repository or implementation modification and no local tests. QUAL-06–08 are owner-agreed, QUAL-09 trust/policy framework accepted in principle with jurisdictional specifics pending, QUAL-10 technical investigation, QUAL-11 future implementation alignment.

## Pending pre-merge gates

- Re-fetch exact governing/blueprint `master` SHAs, newly accepted ADRs, PR head and diff.
- Inspect and resolve GitHub mergeability, merge conflicts and concurrently merged changes, *including both sides of reciprocal additions*; do not equate ahead/behind with conflict-free.
- Inspect required GitHub checks/CI, protected-master policy, broken links, accidental deletions and decision statuses. No tests/builds were run by assistant; CI/user is responsible.
- Confirm independent contractual consumer and domain workflow acceptances and obtain explicit owner approval before protected squash-only merge.

**Judgement:** Suitable for owner conceptual review; **not cleared for merge** until current GitHub mergeability/checks and updated governing/parallel architecture are verified, owner decisions resolved, and explicit approval received.

## Final pre-merge validation — 18 November 2026

Owner has approved QUAL-06, QUAL-07 and QUAL-08; QUAL-09 accepted as a framework with individual jurisdiction-specific rules, comparability decisions, awarding mandates and appeals/teach-out arrangements deliberately requiring later source-specific approval. This is sufficient to merge the **conceptual blueprint**, not to operate regulated awarding.

Latest verified governing `master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (ADR-0017 and ADR-0018 Accepted). Latest verified blueprint `master`: `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9` (same as opening). On final inspection, branch comparison returned **ahead 15, behind 0** with 12 files: main record, nine bounded adjacent records, and two reviews. GitHub reports PR #65 **open, draft, mergeable true** with base `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9`, head `1cadce0b57d1939100dd5b00773d643aa2a5a37b`. No reviews, GitHub status checks or PR-triggered workflow runs were reported for that head; **absence of reported checks is not a green CI run**. No local tests were executed (per instruction).

Technical/architectural review: no changed files deleted; only intended Qualification and reciprocal capability records changed, plus review evidence. Catalogue/register already locate `qualification`; paths and relative links follow their actual directories. No implementing APIs or compliance claimed; provider-neutral trust chain and privacy-scoped employment assessment do not transfer awarding, generic verification, job or employment authority. No direct private-code dependency or mandated circular import is introduced. Open concurrent PRs (#60 Enrolment, #62 Credentials, #63 Training, #64 Assessment, #57 Department) remain provisional and have not changed `master`; bounded notes must be reconciled on their own merges. No conceptual contradiction with currently accepted governing ADRs identified. Future live contracts require independently assessed jurisdiction/issuer requirements and appropriate CI/consumer acceptance.

This report records the pre-merge evidence only. Recheck exact head/base, mergeable status and checks immediately before an owner-approved protected squash merge. The owner's instruction to 'proceed' is treated as approval to merge the documented conceptual review if repository protections permit it.
