# Mailer conceptual review — opening baseline

**Status:** Proposed, non-normative; conceptual review in progress (19 November 2026).

- Target: `docs/capabilities/mailer/` (exact existing directory).
- Branch: `review/mailer-conceptual-20261119`.
- Governing `architecture-rules/master` opening SHA: `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
- Blueprint `architecture-blueprint-review/master` opening SHA: `6dac83a03da8704f7945ee1bc894f2248300445a`.
- Existing evidence: Mailer record currently contains Booking reciprocal notes; no completed independent Mailer design. Booking sends authorised notices through Notifications; Mailer handles mail transport, not Booking decisions or proof of actual human receipt.
- Scope: classification and boundaries; native mail services and lifecycle; idealised public inbound/outbound commands, queries and events; provider neutrality; security, privacy and compliance; cross-capability reciprocal contracts; GUI/headless design; acceptance criteria and unresolved decisions.
- Concurrent open capability reviews observed: logistics, logging, location, localisation, legal_compliance and job. Reconcile their provisional interfaces; do not treat them as accepted.
- Review protocol: `docs/review-protocol.md`; no implementation changes, local tests or merge without owner approval.
