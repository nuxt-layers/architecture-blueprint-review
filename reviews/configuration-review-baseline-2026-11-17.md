# Configuration conceptual review — baseline (17 November 2026)

**Status:** In progress; non-normative. No implementation or governing rules modified.

- Target: `docs/capabilities/configuration/capability-record.md` (directory `configuration`).
- Review branch: `review/configuration-conceptual-20261117`.
- Opening governing `nuxt-layers/architecture-rules` master: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
- Opening blueprint `nuxt-layers/architecture-blueprint-review` master: `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`.
- Procedure: `docs/review-protocol.md`, PCR-01–PCR-10.
- Existing evidence: the Configuration record contains provisional or approved reciprocal notes for Accounting, Authentication, Authorisation, Booking, organisational governance, Caching, Clock, and Comments Engine. Their approval status must remain distinct.
- Scope: verify accepted governing rules and target published `CONTRACT.md`; define ownership/exclusions, native service lifecycle, scoped effective value and precedence semantics, input/output command/query/event contracts, security and provider boundaries, reciprocal capability interfaces, conceptual GUI, acceptance scenarios and unresolved decisions.
- Cross-review safeguards: inspect concurrent PRs before editing adjacent records; preserve their content and status.
- Pre-merge requirements: technical and architectural consistency against then-current `master`, review CI and conflicts, obtain explicit owner approval. Do not run tests, edit implementation repositories or merge unapproved.
