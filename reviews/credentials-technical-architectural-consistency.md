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


## Follow-up CRED-17/CRED-18 consistency checkpoint (18 November 2026)

**Latest read-only baseline:** governing `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (ADR-0017/0018 status reconciliation now accepted); blueprint `architecture-blueprint-review/master` `85db338a5bcc829a2bb236a83b43ed2292c66626`. Different from opening. On comparison before this note: branch ahead 21/behind 3, diverged; subsequent documentation commits do not constitute a Git merge or complete reconciliation.

**Conceptual review:** CRED-17 profiles evaluated against current authoritative W3C, OpenID, 1EdTech, UK and EU materials in [CRED-17/18 resolution](credentials-standards-jurisdiction-resolution.md). W3C VC 2.0 remains adopted as recommended *portable* baseline, W3C VC 2.1/status-list 1.1 drafts not automatically elevated. CRED-17A–H remain engineering decisions needing owner selection or approved technical evidence; no certification assertion. CRED-18 policy framework is complete at conceptual boundary, and its closure is recommended: legal/policy owners supply dated jurisdiction and scheme decisions, while deployment-specific legal reviews remain enforceable prerequisites. No global retention rule or universal legality claim.

**Parallel work:** #63 Training, #64 Assessment and #65 Qualification have now contributed to current master and its Credentials reciprocal record. Their three newly present dated reciprocal notes were copied additively into the PR #62 Credentials record, retaining prior accepted and proposed statuses; no conflict was silently suppressed. New master revisions still affect additional shared reciprocal files, so a full branch integration/compare is required before merge. Active #60 Enrolment and #57 Department remain separate and provisional.

**Technical/dependency challenge:** Credentials/Verification remain distinct for primary issued registry vs third-party presentation trust; Qualification retains award authority; status lists are projections of Credentials' own committed state; Legal Compliance and Privacy provide applicable policy with qualified unknown and effective version. Logging technical, Audit evidential and Reporting analytic contracts remain separate. No new policy or crypto capability required. No implementation files or local tests changed/run.

**Pre-merge status:** Not ready: branch still behind and diverged, must reconcile every modified reciprocal record, recheck accepted ADRs, protected master, GitHub mergeability and CI against latest master, then obtain explicit owner approval for merge. This checkpoint provides a design review, not a check pass.


## Owner-approved closeout direction — 18 November 2026

The owner explicitly approved CRED-17A–H and CRED-18 and authorised the protected squash merge **if** current-master reconciled technical, architectural, branch-policy and CI checks are satisfactory. The originally noted proposals have now been accepted at conceptual level. The branch began behind master when newer Assessment/Qualification/Training records landed; preserve those full source records and add the Credentials-specific reciprocal notes. Do not infer successful integration from a clean file-level append; verify the resulting head against newest master and branch checks.


## Final post-reconciliation technical and architectural review — 18 November 2026

**Current baselines checked:** `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; `architecture-blueprint-review/master` `85db338a5bcc829a2bb236a83b43ed2292c66626`. The governing branch now has accepted ADR-0017 and ADR-0018 (previous proposed-status discrepancy resolved).

**Git integration:** A two-parent reconciliation commit `1b328e3020235a8256422e2d3fd4eea222f22d36` takes the complete current master tree as base and preserves Credentials additions in overlapping files; Assessment, Qualification, Training, Audit, Integrations, Verification and Logging changes were reviewed and merged additively, with Training's newly rewritten current-master record preserved. GitHub comparison after the reconciliation commit: `ahead 27, behind 0, status ahead`. Resulting change scope: Credentials record, 13 bounded reciprocal records and 3 Credentials-specific review files (17 files total), no deletions, no unrelated governance or implementation changes.

**Authority and compatibility:** CRED-01–16 and CRED-17A–H approved, CRED-18 approved and conceptually closed. Qualification alone owns qualification award, Assessment owns marks, Training owns evidence/completion, Credentials owns issue/representation/status, Verification evaluates presented proof independently, Publisher documents are never credentials. No new awarding or policy capability, private coupling or static cyclic import required. Privacy/Legal Compliance supply dated jurisdictional applicability/retention; absence of mandatory authority blocks affected operation. Accepted ADR-0012 provider-neutral and owned outbox, ADR-0016 acyclic interfaces, security, accessibility, headless/GUI and source ownership retained. CRED-17 cryptographic-suite/wallet conformance, provider/regulatory certification and deployment-jurisdiction legal approvals remain **future acceptance evidence**, not conceptual design blockers or claimed implemented features.

**GitHub checks at reconciliation commit:** combined commit status returned **no individual statuses**; PR-triggered workflow query returned **no runs**. These are **not interpreted as passes**. Protected branch policy and GitHub itself must decide merge eligibility. No local tests/builds executed (per owner direction). Before merger, recheck master/head and use protected squash-only GitHub merge; if a required check/review is missing, stop and report, do not bypass branch protection.

**Final conclusion:** Documentation is coherent, additive and consistent at this checked revision; all owner approvals recorded, substantive CRED architecture issues resolved. GitHub's final mergeability and configured protection gate are the last operational requirement.
