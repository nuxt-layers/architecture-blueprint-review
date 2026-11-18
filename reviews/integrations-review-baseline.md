# Integrations conceptual review — opening baseline

**Status:** In progress; non-normative; owner approval pending.  
**Target:** `docs/capabilities/integrations/capability-record.md` (actual directory: `integrations`).  
**Branch:** `review/integrations-conceptual`.  
**Opening governing master:** `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (ADR-0017 and ADR-0018 accepted).  
**Opening blueprint master:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.

## Review scope

Apply `docs/review-protocol.md`: establish authority and existing evidence; classify external integrations boundary versus domain authority; specify idealised inbound/outbound contract (commands, queries, provider events, uncertainty), native lifecycle, security, tenant isolation, provider governance, reciprocal capability notes, GUI/admin needs and conceptual acceptance. Challenge dependency cycles and concurrent PR proposals. Preserve already approved conceptual decisions.

## Opening concurrency and evidence

Federation draft PR #69 contains provisional reciprocal Integrations implications and is not an accepted baseline. Existing Integrations record includes numerous reciprocal proposals (Course, Qualification, Assessment and Credentials); determine exact statuses independently. No implementation readiness is presumed. Check further active PRs and current master before final technical/architectural validation. No implementation edits, local tests or merge are authorised.

## Current-master technical and architectural review — 18 November 2026

- **Current governing master:** `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (unchanged since opening). Accepted ADR-0012 / ADR-0016 and normative Capability Standard/canonical catalogue checked; provider-neutral boundaries and public-port dependencies retained. ADR-0017/0018 acceptance recorded; their detailed applicability requires continued check at owner review.
- **Current blueprint master:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` (unchanged since opening). The branch is **10 commits ahead, 0 behind**, with **10 changed files** (9 capability records and this baseline). All eight adjacent records receive small additive notes; main target replaces empty pro-forma with substantive definition while preserving its historical reciprocal content. No unintended capability directory deletion or implementation-file change.
- **Concurrent PR reconciliation:** #69 Federation, #75 Infrastructure, #74 Identity, #73 IAM Integration, #77 Inventory and #78 Invoice are open, as are #66–72. Any overlap is **provisional**, not adopted; proposed boundaries distinguish infrastructure operations, IAM composition, federation peers, and domain owner authority. Recheck their changed documents before merge; do not silently overwrite integrated competing notes.
- **Git:** compare API confirms ancestry (no divergence at check). PR metadata at opening reported `mergeable=false` immediately after creation; this can indicate pending mergeability computation and is **not a verified passing merge check**. No proof of protected branch checks or CI completion was retrieved. Treat Git mergeability and checks as unresolved; rerun immediately before explicitly approved merge.
- **Architecture:** no business-domain state centralised in Integrations, secret values remain host/vault-owned, provider authenticity does not establish domain truth, receipts distinguish accepted/completed/unknown, all logical dependencies use public contracts and must remain acyclic. Configuration selection and Integrations readiness remain separate; origin-owning outboxes versus Message Queue transport remain separate. Reciprocal changes are intentionally provisional, not approvals of neighbouring reviews.
- **Documentation:** target exact path `docs/capabilities/integrations/capability-record.md`; eight reciprocal paths checked through successful GitHub file updates. Relative links in new notes point to target record. Historic linked notes were retained without a full link checker. Catalogue/register remain unchanged because existing established classification and description still match; no governing ADR changed.
- **Evidence limits:** target repository exists, with only minimal README and no retrievable root CONTRACT.md; no implementation behaviour, vendor integrations, runtime compliance or automated acceptance certified. No local tests/builds executed.
- **Disposition:** conceptually documented for owner review, **not approved, not merge-ready** until owner decisions INT-07–09, external PR reconciliation and final Git checks. Owner authorisation required before squash merge.
