# Notifications conceptual review — opening baseline

**Status:** Draft, non-normative; no conceptual sign-off or implementation verification.

- Target: `docs/capabilities/notifications/capability-record.md` (directory `notifications`).
- Review branch: `review/notifications-conceptual-20261119`.
- Governing `nuxt-layers/architecture-rules` `master` opening SHA: `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
- Blueprint `nuxt-layers/architecture-blueprint-review` `master` opening SHA: `6dac83a03da8704f7945ee1bc894f2248300445a`.
- Procedure: `docs/review-protocol.md`; initial record has provisional reciprocal notes for Authorisation, Billing, Booking, Configuration, Course, Assessment, Credentials, Comments Engine and organisational governance.
- Parallel review: `mailer` draft PR #90 and `message_queue` draft PR #94, both provisional; preserve reciprocal contributions and reconcile before merge.

## Review scope

Establish governing accepted ADRs, classification and source-of-truth boundary; inspect target root `CONTRACT.md` if available. Specify native notification orchestration, authoritative state/lifecycle, public inbound and outbound interfaces, commands/queries/events, delivery uncertainty, consent/preferences, security and provider independence. Record cross-capability reciprocal interfaces, accessible user/admin GUI, conceptual acceptance scenarios, open decisions, and technical/architectural consistency against current `master`.

No implementation edits, local tests, or merge without explicit owner approval.
