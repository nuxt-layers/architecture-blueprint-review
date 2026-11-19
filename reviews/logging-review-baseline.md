# Logging conceptual review — opening baseline

**Status:** Proposed, non-normative; owner approval outstanding. **Date:** 19 November 2026.

- Exact target: `docs/capabilities/logging/capability-record.md` (existing directory `logging`).
- Branch: `review/logging-conceptual-20261119`.
- Governing `nuxt-layers/architecture-rules/master`: `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
- Blueprint `nuxt-layers/architecture-blueprint-review/master`: `6dac83a03da8704f7945ee1bc894f2248300445a`.
- Governing catalogue places Logging among Foundation candidates: structured technical logs, correlation and sinks, distinct from authoritative Audit and Observability metrics/traces.
- Existing target record is a pro-forma with numerous dated reciprocal notes; preserve all prior decisions and notes.
- Related active provisional reviews include Job #84, Legal Compliance #85 and Location #87; their unmerged content is not approved authority.

## Scope of this PR

Investigate target published root contract and normative ADRs; define independent classification, authority, native lifecycle, idealised inbound/outbound public contracts, commands/queries/events, sink/provider failures, data isolation and redaction, retention and access controls, interactions with Audit/Observability/IAM/Clock/Privacy and operational producers, GUI/headless expectations, reciprocal notes and conceptual acceptance. Review consistency against latest master before any proposed merge. No implementation edits, local tests or merger are authorised.
