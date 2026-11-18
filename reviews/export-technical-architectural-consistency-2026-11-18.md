# Export — technical and architectural consistency review (18 November 2026)

**Status:** Completed preliminary conceptual PR consistency assessment, **not an owner-approved merge clearance**. Re-run Phase 10 against latest `master` after decisions EXP-01/09 and immediately prior to an explicitly approved merge.

## Exact live baselines at check
- Governing `nuxt-layers/architecture-rules/master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (accepted ADR-0017 and ADR-0018 present).
- Blueprint `nuxt-layers/architecture-blueprint-review/master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
- PR [#68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68), branch `review/export-conceptual-20261118`, latest content SHA before review note `2af58687deab44c9bd02cbcb3c2859e13ead9257`.
- Git compare: **ahead 13, behind 0**, common ancestor equals current base; 13 changed files, 0 deleted files. GitHub raw PR metadata reported `mergeable: true`, `mergeable_state: clean` at the checkpoint. Connector's separate normalised `mergeable` field reported `false`; do not treat this contradictory field as conclusive, and recheck at merge gate. No statuses were returned by combined status endpoint; this does **not** prove required checks passed. Draft PR, no merge.
- Parallel open reviews identified: [Events #67](https://github.com/nuxt-layers/architecture-blueprint-review/pull/67) and [event_bus #66](https://github.com/nuxt-layers/architecture-blueprint-review/pull/66). Their interface decisions are provisional, and no same-target Export PR was open before #68.

## Governing reconciliation
- Governing `docs/catalogue.md`: `export` is **Library** for rendering safe `rich-text` to PDF/.docx; this PR retains that scope and labels bulk-export orchestration owner **open**. It does **not** amend accepted governing catalogue.
- Accepted ADR-0011 safe-tree separation, ADR-0012 independently consumable public contract and composition/port rules, ADR-0008 independent delivery, ADR-0009 headless service, ADR-0016 public extension only, ADR-0017 tenant authority and ADR-0018 policy ownership are preserved at conceptual level.
- Separate `document` capability is retired by approved earlier review; Publisher and individual domains retain document/source authority.
- Actual target implementation repository `nuxt-layers/export` has no `CONTRACT.md` or public implementation on inspected `master`; no compatibility, acceptance or delivered-format claims are established.

## Cross-capability checks
- **Ownership:** renderer has no domain records; Billing, Publisher, Reporting and other owners retain source facts, Authorisation holds permission decisions, Storage holds only bytes, Audit evidential custody, Logging diagnostics. No duplicate master or cross-domain write proposed.
- **Contract:** explicit input safe tree/asset resolver/format and error semantics; output stream/file, metadata, diagnostics and capability catalogue; no invented implemented endpoint or universal request object.
- **Acyclicity:** public host composition edges only, no direct runtime code imports to other capability implementations. Conditional report/job workflow ownership prevents immediate cycle.
- **Security:** sensitive disclosure is checked before conversion and again for saved/released copies, including tenant/recipient, legal/privacy constraints; unknown/failed provider returns fail closed. Renderer itself never grants access or publishes.
- **Presentation:** headless Library has no standalone sidebar/dashboard. Host contextual actions and responsible owning workflows handle user-visible jobs in the representative application-test-template pattern.
- **History:** old Authorisation/Billing/Document reciprocal notes preserved in Export record, status clarified; nine appended reciprocal notes are dated and proposed. Catalogue/register original entries retained verbatim with additive clarifications.

## Outstanding issues / merge gate
1. **EXP-01/EXP-09 owner decision is material:** strict renderer-only boundary vs. independently governed durable bulk-export orchestration. PR retains proposed allocation, not accepted sign-off.
2. Format conformance/security methodology, root consumer `CONTRACT.md`, independent tests, provider evidence, exact APIs, CI and deployment statuses are **unverified**.
3. Recheck effective `master`/accepted ADR revisions, changed-file/relative-link scope, open parallel reviews, status checks, mergeable-state and protected-branch policy before merge. If other PRs touch reciprocal files, reconcile additively without discarding approved content.
4. Only CI or user runs tests/builds. **No local tests/builds were run.** No implementation repository edited. No merge attempted.

**Provisional verdict:** conceptual documentation is internally coherent *subject to owner decision on Export's boundary*. Git compare is currently non-divergent and raw GitHub reports clean, but this is not final merge permission or technical acceptance.

## Additional consistency checkpoint — 18 November 2026 (after approved research)

**Owner-approved:** EXP-01–EXP-09 conceptual direction, including retention of the governed stateless rendering Library, source-domain/Reporting-owned durable workflow, conditional tabular interfaces and permissively licensed replaceable engines. EXP-07 conformance research and EXP-08 implementation alignment remain incomplete. The approved GUI allocation is contextual production actions plus optional host-owned local test harness; the actual reference test template's `README.md`, `app/app.vue`, `app/pages/admin.vue`, `nuxt.config.ts`, and Theme Manager's current root `CONTRACT.md` were read. The latter explicitly documents an unresolved public-composition blocker; do not promise a tested Export host API.

**Latest base review:** governing `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master` **advanced** to `07596bff0f770e98526a485c652ebe5fbf6af3ea`. Comparison from the initial blueprint baseline now includes 4 merged commits (notably Events/Attendance and event_bus); several added notes affect `audit`, `authorisation`, `logging`, `privacy`, `reporting`, the shared catalogue and register. The Export review branch is **diverged (27 ahead, 4 behind)**; concurrent documents were deliberately not overwritten or deleted. New reciprocal append-only changes must be reconciled with the latest master preserving both approved lines of work before merge. A raw GitHub PR reading temporarily reported `mergeable: null`, `mergeable_state: unknown` while GitHub recalculated; no clean mergeability or CI passing assertion is made.

**Further check needed before merge:** integrate latest base safely, verify exact changed paths, links, new merged notes and potential conflicts and run GitHub checks; perform final protected squash validation only after explicit merge approval. No tests, implementation edits or merge actions performed here.
