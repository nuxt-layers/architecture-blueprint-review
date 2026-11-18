# IAM Integration — conceptual review opening baseline

**Status:** In progress; non-normative; no conceptual sign-off.
**Target directory:** `docs/capabilities/iam_integration/` (underscore preserved).
**Branch:** `review/iam_integration-conceptual`.
**Opening governing master:** `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
**Opening blueprint master:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
**Procedure:** `docs/review-protocol.md` on opening blueprint master.

## Scope
Review IAM suite integration classification, no-domain-state ownership, cross-capability provisioning, suspension, revocation, recovery, assurance and data-subject choreography, ideally public inbound/outbound contract, bounded consistency/recovery and audit evidence. Investigate target published implementation contract and adjacent interfaces; document reciprocal notes, host-facing GUI, privacy/security/tenant isolation, acceptance cases and open architectural decisions. Preserve approved governing decisions; no implementation edits or tests.

## Existing evidence and neighbouring work
Current IAM Integration record has provisional reciprocal notes dated 15 November 2026 from Authentication, Audit and Authorisation. Governing catalogue identifies `iam-integration` as a no-data IAM suite integration component under ADR-0005. Existing proposals are not considered approved. Check overlapping active PRs and latest `master` again before completion.

## Review and merge discipline
Maintain all changes in this initial draft PR. No merge without explicit owner approval. Before requesting merge, re-check technical Git mergeability, normative governing rules and cross-capability architectural consistency against latest `master`.
