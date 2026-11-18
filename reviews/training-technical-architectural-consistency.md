# Training PR #63 — pre-merge technical and architectural consistency review

**Review:** 18 November 2026. **Scope:** conceptual blueprint documentation only, not implementation acceptance. **Owner authorisation:** all TRAIN-01–08 approved; user expressly authorised merge **if satisfied**.

## Current verified baselines and reconciliation

- Governing `architecture-rules/master` SHA `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. Compared to opening SHA `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`: ADR-0017 and ADR-0018 now explicitly **Accepted**; no other changed files found. Training's tenant isolation and effective policy-source/override/failure constraints have been recorded.
- Blueprint `architecture-blueprint-review/master` SHA `d4de483fc1860bc87e23450eb114f800474d5309`. New Qualification conceptual review merged after Training review began. All Qualification reciprocal content is retained in Training, Course, Assessment, Enrolment, Credentials and Qualification; Training's separately approved reciprocal notes are preserved with these additions.
- Training branch rebased as a new reconciled commit descending directly from current `master`, with lease protection against replacing unexpected branch changes. The compare after reconciliation was **ahead one, behind zero**; all changes remain within Training review, reciprocal capability records and review documentation.

## Architectural validation

- **Owner authority:** Course owns immutable curriculum/outcome rules; Enrolment owns admission/cohort; Assessment owns attempts/results/appeals; Training owns learning participation, independently assessed competence and training completion; Qualification owns qualified award decisions; Credentials owns issued credential proofs/status. Confirmed no Training-created qualifications, credentials or employment payable hours.
- **Independent native mode:** Training can verify approved standalone competencies without a Course or Enrolment; formal course completion needs the applicable course revision and any mandatory assessment outcomes; external LMS/provider remains optional.
- **Public inbound:** authorised training commands and source-qualified facts from Course/Enrolment/Assessment/Verification/IAM and applicable rules; explicitly pending/unknown/fail-closed where evidence, permission or effective policy is insufficient.
- **Public outbound:** scoped participation, competence, progress, completion, correction/history and limited evidence exports; committed changes notify authorised consumers via owned durable outbox, without granting awards.
- **Audit vs Logging:** Audit receives minimised accountable evidence of decisions and supplies custody/integrity/coverage outcomes; Logging receives sanitised diagnostics and supplies delivery/health outcomes where supported. Neither is an authority for Training business decisions. Mandatory Audit capture cannot be replaced by Logging.
- **Provider and failure behaviour:** origin/version/effective time, delegated evaluator authority, replay/idempotency, tenant isolation, data minimisation, historical corrections and downstream re-evaluation are explicit. No direct contract dependency cycle or private cross-capability storage access introduced.
- **Host/presentation:** headless core and optional GUI described; host owns navigation and wiring, WCAG 2.2 AA/i18n/Theme Manager apply.
- **Decisions:** TRAIN-01–08 all expressly owner-approved. Previous Course decisions retained. Adjacent assessment/enrolment/credentials PRs remain provisional; reciprocal notes do not claim those independent reviews completed.
- **Scope/docs:** actual `docs/capabilities/training/` directory used; previous record and Course history preserved; reciprocal changes are bounded and explicitly marked; no normative governing repository or implementation changed. Pro-forma fields now supplied as substantive conceptual sections. Relative links follow existing document layout.

## Technical checks and limitations

- Verified repository commit comparisons and changed file inventory, governed ADR statuses, overlapping merged Qualification material and the current set of open capability PRs.
- GitHub combined commit statuses and PR-triggered workflow runs returned **empty collections**, not affirmative CI passes. No local tests/builds run, per user constraints. These are documentation-only changes; do not equate conceptual review with implemented acceptance.
- Before merging, verify live GitHub PR mergeability, branch protection and current head/base, and use protected **squash-only** merge. If a new change or blocker appears, stop and reconcile.

**Conclusion:** Architectural consistency review supports merging the approved Training **conceptual blueprint** only, subject to the final live GitHub checks. This does not release a working Training implementation.
