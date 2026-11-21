

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking conceptual completeness note (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) supplies permitted booking notice intent through Notifications where configured; Mailer owns mail transport, receipt/failure diagnostics and delivery, not the reservation or notification workflow. A mail transport acknowledgement is neither a Booking confirmation nor proof the guest received or read a message. Sensitive booking/participant data must be minimised and protected; this is not a completed Mailer review.

## Cross-capability note — Booking notification transport (15 November 2026)

**Approved Booking scope; Mailer's review incomplete.** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) emits authorised and minimised booking confirmation/change/cancellation/reminder intent through Notifications where configured. Mailer owns mail transport and technical delivery status, never reservation commitments or recipient attendance. A mail acceptance result does not imply Booking confirmation or actual receipt by the person. Protect guest contact details, purpose, localisation, retention and delivery failure; optional mail outage cannot cancel an already confirmed booking. No existing Mailer implementation adapter is asserted.


## Notifications reciprocal conceptual interface — 19 November 2026

**Status: proposed in [Notifications draft PR #97](https://github.com/nuxt-layers/architecture-blueprint-review/pull/97), not owner-approved or implemented.** Notifications delegates only channel email send/qualified provider status to Mailer; Notifications owns source-scoped notice intent, recipient-policy routing, inbox, retry coordination and notification lifecycle. Mailer must not treat provider acceptance as human receipt; callback evidence and idempotency/reconciliation are proposed public channel ports. Reconcile with draft Mailer PR #90. This bounded reciprocal note preserves the independent mailer review and creates no direct package import.
