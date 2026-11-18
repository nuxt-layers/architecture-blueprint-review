# Credentials — technical and architectural consistency checkpoint (18 November 2026)

**Scope and approval:** Proposed conceptual review PR #62; no merge authorised. This is a revision-scoped pre-merge checkpoint, repeat if either master or neighbouring PR materially changes. No local build or test performed.

## Current verified baselines

- Governing `nuxt-layers/architecture-rules/master`: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953` (unchanged since opening).
- Blueprint `nuxt-layers/architecture-blueprint-review/master`: `ac1125a7ba4ea15d6b963aebf07d83cd8cd701b9` (unchanged since opening).
- Opening approved source: COURSE-12 Qualification domain creation and award authority division; CRED-01 candidate creation. Detailed CRED-07–18 are proposals, not accepted.
- Compare immediately before writing this checkpoint: branch ahead **12** commits, behind **0**, merge base exactly blueprint master; 12 changed files, no deleted files, no divergence reported. This does **not** independently establish GitHub's final PR mergeability or CI pass.
- Current neighbouring draft PRs include **#60 Enrolment, #63 Training, #64 Assessment, #65 Qualification** (plus #57 Department). All are provisional and must be reconciled before integration. Newly opened #63–65 overlap reciprocal records and source-authority contracts; coordinate their amendments rather than silently treating these drafts as settled.

## Technical review

1. **Repository scope:** Changes remain in the one PR, comprising the Credentials record, opening baseline and bounded reciprocal additions to Qualification, Verification, Publisher, Assessment, Training, Integrations, Privacy, Authorisation, Audit and Notifications. No implementation or governing repo changes.
2. **Published implementation evidence:** GitHub organisation repository search found no target `credentials` implementation; no target root `CONTRACT.md` verified. No concrete API signatures or working functionality claimed. External integration and proof standards remain proposals.
3. **Normative alignment:** Accepted ADR-0012 provider-neutral caller/access/outbox/task/files shapes, ADR-0016 acyclic contracts, ADR-0009 optional presentation, capability-owned storage, 50-line Nuxt composition ceiling and independent root contract requirement are not overridden. Headless operation remains explicit. Security/privacy, localisation and accessibility are defined as required targets, not certified compliance.
4. **Document integrity:** Actual directory `credentials` verified. All reciprocal relative links target existing capability records as used in source text; prior pro-forma and COURSE-12 are retained. Proposed CRED identifiers do not overwrite CRED-01–06. No catalogue/register category change is necessary: Credentials is already registered as a Domain candidate on current master.
5. **CI/mergeability:** Final GitHub mergeability, protected-branch reviews and CI status must be rechecked before owner-approved merge; a clean compare is not equivalent to passed checks.

## Architectural challenge

- **Authority:** Qualification owns awards; Assessment owns grading; Training owns participation; Credentials owns credential issuance/status and does not independently award qualifications. External awarding body/registry retains externally authoritative state. Actor's platform role is not a legal mandate.
- **Verification overlap:** Verification owns independent trust assessment of presented claims; Credentials owns issuer registry/status for its own credentials. Do not introduce a mutual static contract/package dependency. Define verification port direction in future implementation.
- **Publisher overlap:** A certificate document is an artifact, never an award or live credential status. No restored Document capability.
- **Event and security semantics:** Write command is server-authorised and domain-validated; event transport is not permission. Credential-owned durable outbox; retry/replay/idempotency and remote source uncertainty are explicit. Status of credential, underlying decision and cryptographic proof is separate; do not conflate source outage with revocation.
- **Unresolved:** Owner confirmation of CRED-07–15, source authority for otherwise unsupported non-qualification claims (CRED-16), acceptable portable proof profiles (CRED-17) and jurisdiction/retention/legal details (CRED-18). Review draft #65's qualification mandate interfaces and #63/#64 source event contracts before integration.
- **Acceptance:** Conceptual scenario set covers legitimate issue, invalid source, isolation, replay, source correction, delivery failure, offline proof freshness, key compromise, status invalidation and headless GUI equivalence. No executable acceptance evidence claimed.

**Assessment:** Suitable for owner review as a **draft conceptual proposal**, not ready for merge until substantive open decisions and concurrent PR interfaces are reconciled, then final latest-master technical and architectural check, branch protection/CI and explicit approval.
