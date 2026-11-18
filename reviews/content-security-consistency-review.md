# Content Security — technical and architectural consistency review (17 November 2026)

**Scope:** Documentation-only review and Git reconciliation on the existing **draft PR #55**. Review of implementation and CI acceptance is not claimed; no merge approved.

## Governing and working baseline

- Governing `nuxt-layers/architecture-rules/master`: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953` at last check.
- Blueprint `nuxt-layers/architecture-blueprint-review/master`: `b0b026931c4b66ec4bfc445489147045497db890`, including merged **Configuration #53** (`45a2665`) and **Content Editor #54** (`b0b0269`).
- Opening blueprint baseline was `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`; review protocol `docs/review-protocol.md` was retrieved again on latest master.
- Existing branch `review/content_security-conceptual`, no separate PR. After correct ancestry reconciliation at `5f7f76505cf939227c5c9cdafa8f59e5f290ae8a`, `master...branch` reported **ahead 37, behind 0, 17 changed files**, limited to 13 targeted capability records and four review documents. Compare again on final head to verify no unrelated files reappear.

## Technical Git reconciliation: completed on branch

1. Compared the original common ancestor and both merged `master` changes with all 13 overlapping Content Security reciprocal records. All of the original Content Security additions were append-only on common ancestor except that the main target record is a full replacement. Configuration's expanded conceptual record was also preserved in full.
2. Reconciled merged Configuration and Content Editor content into each overlapping capability file; included Content Editor's reciprocal note in the full Content Security target record.
3. Corrected an intermediate ancestry merge tree that briefly omitted **unrelated** files from the merged PRs. This was detected by an independent diff showing unrelated deletions and was **repaired before concluding review** by rebuilding the tree directly on the latest master's Git tree with exactly the 17 intended file overrides. The corrected comparison includes no deletion of those master-only changes. This correction has its own follow-up commit on PR #55; no branch force-push was used.
4. GitHub's raw pull-request endpoint reported `mergeable: true`, `mergeable_state: clean` on corrected head `5f7f765...` while the PR remained a draft. The compact PR tool initially returned `mergeable: false`, apparently a transient result; the fresh raw endpoint and final head must be checked before any approved merge.
5. Combined commit statuses and PR-triggered workflow-run queries on that corrected head returned **no statuses / no workflow runs**. That is **not proof that required checks passed**. Protected-branch requirements and signed-commit compliance must be confirmed independently; no local tests or builds were run.

## Architecture and contract consistency

1. **Ownership:** Content Security remains Platform detection/evidence. The content-owning capability enforces secure ingress and source admission, holds and publication; Moderation owns cases/reviewer decisions/appeals, Legal Compliance qualifies applicable duties, Privacy controls lawful processing/retention, Audit holds independent trace. No duplicated publication authority or direct cross-capability private-schema writes were introduced.
2. **Execution:** Scans are invoked at the originating application's/Node's trusted server-side ingress via Content Security's public interface. Detectors are isolated local workers or qualified external services where permitted. Physical worker/container arrangement is an implementation choice; neither user browsers nor a Hub's foreign `clear` provide authoritative admission.
3. **Pre-admission:** CS-14 is **verify-before-admission**, not automatic quarantine in normal content stores. Temporary restricted ingress is a bounded technical inspection stage. Mandatory failure, unknown or unsupported results default to rejection; only separately justified evidence preservation is exceptional. Admission is not publication; changed revisions and later adverse intelligence have distinct holds/removal workflows.
4. **Coverage:** Screening catalogue S1–S5 distinguishes mandatory secure-by-construction input/rendering controls from required or optional specialist malware, image, URL and harmful-content assessments. Mandatory baselines are the owners' duty even when scanner unavailable. Profanity is not automatically illegal, and classifier indications do not prove guilt or total safety.
5. **Public contract:** Per-check coverage, limits, unknown/failed/not-applicable/stale, source revision/digest, policy/provider/model versions, idempotency, accepted versus completed assessments, expiration, restricted evidence and qualified results are conceptual inbound/outbound obligations, not asserted existing runtime APIs.
6. **Federation:** Receiving Nodes/Hubs evaluate admissible external evidence independently under their local policy; origin source authority, local index visibility and remote withdrawal receipts are distinct.
7. **Security and governance:** Accepted ADR-0012 and Capability Standard composition, separately owned persistence/outbox, privacy by design, WCAG 2.2 AA GUI and headless mode are retained; ADR-0018 was documented as proposed (not assumed accepted). No implementation repository edits or API invention.
8. **Contract/acceptance gaps:** The target implementation repository exists but a root `CONTRACT.md` was not verified; no scanner support, deployment, host composition budget, legal compliance, passing CI or independent runtime behaviour is asserted.
9. **Approved versus proposed:** **CS-09–CS-16** are expressly owner-approved conceptual principles (CS-14 with owner-approved restricted-ingress refinement). **CS-01–CS-08** were subsequently explicitly owner-approved on 17 November 2026. Thus **CS-01–CS-16** are all owner-approved conceptual principles; no decision remains pending in this register.

## Residual sign-off / merge gates

- Review final branch diff against current `master`; recheck if any new master PR lands. Active adjacent work includes Course #56, Department #57, Document #58, Employment #59 and Enrolment #60 and can alter future ownership/reciprocal notes.
- Check all links/decision statuses, semantic consistency of the Security catalogue and document lifecycle boundary, and final PR mergeability.
- Verify required CI/checks, signed commits and protected-branch policy through GitHub. The absence of reported checks is not a passing result; CI and the user, not this assistant, run tests/builds.
- **CS-01–CS-08 owner disposition completed:** all CS-01–CS-16 conceptually approved. Obtain separate **merge authorisation** after final checks. Conceptual completeness does not constitute operational availability or permission to merge.

**Disposition:** Reconciliation completed at documentation/Git level; conceptually coherent. **Draft PR remains unmerged**, pending the gates above.
