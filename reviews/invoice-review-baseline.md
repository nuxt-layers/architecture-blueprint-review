# Invoice conceptual review — opening baseline

**Status:** Draft, non-normative; owner approval pending. **Date:** 18 November 2026.

- Target: `docs/capabilities/invoice/capability-record.md` (actual directory `invoice`).
- Branch: `review/invoice-conceptual-20261118`.
- Governing `nuxt-layers/architecture-rules/master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2` (ADR-0017 and ADR-0018 now accepted).
- Blueprint `nuxt-layers/architecture-blueprint-review/master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
- Initial evidence: invoice pro-forma contains provisional 14 November invoice/provider-mode notes, 15 November Billing BIL-01–06 approved reciprocal note, and 16 November tenancy/governance notes. No verified invoice implementation contract or acceptance established yet.
- Scope: invoice authority, classification, native and connected lifecycle, idealised public inbound/outbound contracts, validation and recovery, cross-capability input/output boundaries and reciprocal notes, security/legal/provider boundaries, GUI, acceptance examples, and owner decisions.
- Neighbouring open work includes Integrations PR #76 and Inventory PR #77; all unmerged findings are provisional. Concurrent updates must be preserved through reconciliation.
- Review against latest governing and blueprint `master` before merger; do not run local tests, edit implementations or merge without explicit approval.

## Technical and architectural consistency checkpoint — 18 November 2026

- Re-read the current governing `docs/platform-charter.md`, `docs/architecture.md`, `docs/capability-standard.md` and `docs/catalogue.md`. Governing master remained `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. The accepted ADR-0017/0018 and ADR-0012/0016 rules are preserved. No governing changes proposed.
- Blueprint master remained `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. Git compare found the review branch **7 commits ahead, 0 behind** and seven intended changed files, no file removals. This is not a substitute for final GitHub conflict/check status or the mandatory immediate pre-merge recheck.
- Reviewed Billing's owner-approved BIL-01–06 against the Invoice handoff, Accounting ledger boundary, Order source facts, and provisional Integrations provider contract. Kept the proposed Invoice public contract non-normative and all INV-01–06 open. No unsupported claim of functioning invoice repository was made; search returned no matching repository (absence not universally proved).
- Reciprocal notes are bounded and additive in Billing, Accounting, Order, Integrations and Payment Gateway. Concurrent Integrations PR #76 may touch the same file; Inventory #77 and other open reviews may introduce related source/evidence changes. Resolve exact file conflicts and semantic authority differences against the latest branch revisions before integration.
- Business invoice authority remains with Invoice; monetary source decisions, ledger, payment execution, provider transport and legal policy remain separately owned. Provider unknown, retries, numbering and settlement projection are intentionally marked as safety and approval gates.
- GUI consumes only public Invoice semantics and is optional; CI/user (not this review) must validate composition, contract acceptance, accessibility, security and local/runtime evidence.
- **Remaining gates:** independent statutory/jurisdictional qualification, owner decisions INV-01–06, related active-PR reconciliation, PR mergeability/status checks and explicit owner approval. Do not merge until technical **and** architectural review is repeated immediately before approved squash merge.

## Extended review and changed-master checkpoint — 18 November 2026, evening

- Owner approved the earlier high-level recommendations as conceptual direction. INV-01–INV-06 are **not** individually settled; the implementation/public root `CONTRACT.md` is still unverified.
- Governing rules `master@0725f314abc9ad13f1a65247f54a7ff80772f0b2` remained unchanged on recheck; blueprint `master` advanced to `a88f0c9a7c25262a97d220515c5d7031e937d124`, including merged Infrastructure #75.
- The Invoice review branch **diverged**, initially 8 commits ahead and 13 commits behind after the new baseline. As the branch and current master have separate edits, resolve integration and newly merged reciprocal-document differences against current master before any squash merge. Do not claim a mergeable or CI-green state from compare metadata alone.
- Expanded Invoice's proposed business public inbound/outbound surfaces, precise reciprocal Logging/Audit/Reporting semantics, jurisdiction-specific EN 16931/UBL/Peppol/HMRC/UK 2029 e-invoicing considerations, permissively licensed replaceable OSS candidates, and GUI following the actual application-test-template navigation described in its `README.md`. Corresponding bounded notes were appended to Logging, Audit and Reporting records on **this** review branch.
- Current external-source research supports decimal.js, Zod, Ajv, fast-xml-parser, KoSIT validator, pdf-lib, bwip-js and Pino as initially permissively licensed candidates; no adoption or compliance guarantee, and transitive licensing/maintenance/security must be re-evaluated at implementation selection.
- Other currently open related proposals include Integrations #76 and Inventory #81. Their unmerged findings are provisional; overlap is to be reconciled without overwriting or presuming approval.
- CI/local builds/tests were **not** run. No implementation repository was edited. No merge authorised or performed.

## Owner approval checkpoint — 18 November 2026

The owner expressly stated: “I approve the `invoice` conceptual design to this point.” This approves the conceptual direction documented in the Invoice record, including the extended public input/output surfaces, reciprocal Logging/Audit/Reporting boundaries, interoperable standards, permissive OSS evaluation, and optional sidebar/dashboard GUI. It does not establish implementation readiness, a verified root `CONTRACT.md`, governing ADR adoption or approval to merge. **Superseded by the subsequent explicit approval below:** INV-01–INV-06 are now all approved and closed. Technical/legal/implementation checks remain.

**Current baseline recheck:** governing `master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master@753931135d470355af3a7f421e96f9aa2663bc16` (advanced again). Before this approval note the review branch compared 13 commits ahead / 14 behind. Reconciliation, CI/mergeability and current-master architectural review must precede any separately authorised merge. No implementation changes or local tests.


## Owner closure of INV-01–INV-06 — 18 November 2026

The owner explicitly **approved INV-01 through INV-06 with the recommended standards-based resolutions, and directed that all six conceptual items be closed**. Invoice's capability record now shows **APPROVED / CLOSED** for each decision with the adopted boundary, invariants and separately labelled evidence still required. This supersedes the earlier references to these IDs as open; preserve those references above solely as chronological review history.

**Closed conceptual decisions:** INV-01 incoming/outgoing supplier invoice document ownership; INV-02 jurisdiction-aware atomic numbering and linked corrective documents; INV-03 document settlement projection versus Accounting-owned financial books and Payment Gateway execution; INV-04 exactly one native/connected issue authority per scope and effective period with governed cut-over; INV-05 authoritative shared business-party source and immutable Invoice snapshot; INV-06 reuse of generic rendering/editor/storage with independent Invoice lifecycle authority.

**Separate follow-up tracks, not unresolved conceptual IDs:** (a) legal/jurisdictional invoice/VAT/e-invoicing and records compliance validation; (b) actual published public Invoice and related business-party contracts including precise commands, errors, auth, event and provider modes; (c) implementation/CI-based independent acceptance, failure recovery, migrations, security, accessibility and provider interoperability. Neither a software implementation nor its legal compliance is verified.

**Git rule:** keep this in draft PR #78; no implementation repository changes, local tests or merge. Refresh and reconcile advanced blueprint master before a separate explicitly authorised squash merge.


## Latest-master reconciliation and owner-authorised pre-merge check — 18 November 2026

**Authority checked:** `nuxt-layers/architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; accepted ADR-0012, ADR-0016, ADR-0017, ADR-0018 and the normative Capability Standard remain governing. **Blueprint master at reconciliation:** `54060e79dc24c8e84bee98a648036bd475b1474f`, including merged Integrations PR #76 and owner-approved Inventory PR #81, plus the earlier infrastructure and other review changes. The old Invoice PR branch originated at `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` and was 17 commits ahead / 15 behind; its changes have been reconstructed on top of the latest accepted baseline in the **same PR**.

**Document reconciliation:** The Invoice canonical record on current master was byte-identical to the original opening baseline, so the owner-approved complete Invoice record is preserved without discarding newer Invoice edits. For Accounting, Audit, Billing, Integrations, Logging, Order, Payment Gateway and Reporting, the Invoice PR's changes were additive notes relative to their original baseline. The latest master version of each reciprocal document was retained, and only Invoice's bounded reciprocal note was appended. This preserves newer approved Integrations and Inventory findings, including provider user-scoped permissions and authoritative Inventory movement/cost evidence, without transferring legal invoice, ledger or payment authority. Historical review notes are retained; superseding decision status identifies INV-01–06 as **APPROVED / CLOSED**.

**Architectural challenge:** Invoice remains the only platform-facing authority for formal document issue, numbering, supplier bill capture and correction, independent from Billing charge calculations, Accounting postings and balances, Payment Gateway payment operations, Integrations connector transport, Inventory stock authority, Audit custody, Logging diagnostics and Reporting derived outputs. A timeout is not confirmed issue; a payment event cannot amend invoice issue history; provider authority scope is exclusive. Public-only exchanges, capability-owned outbox and domain persistence, server-side access, explicit tenant/legal-entity scope, signed-off policy/legal applicability, and optional themed headless presentation preserve governing direction. No new dependency cycle or implementation claim introduced; external legal-party owner classification remains adjacent future work under approved INV-05.

**Scope and checks:** Exactly ten documentation files are expected: the Invoice record, eight bounded reciprocal capability records and this review evidence file. No implementation repository was modified, no local tests/builds were run, and no normative ADR was changed. Before squash merge verify the PR is up to date with the exact latest master SHA, inspect changed file list, GitHub mergeability, all available commit statuses and PR workflow runs, and honour protected-branch restrictions. Explicit owner authorisation to complete the squash merge was given in this conversation; the merge endpoint remains final arbiter of repository permissions and branch policy.
