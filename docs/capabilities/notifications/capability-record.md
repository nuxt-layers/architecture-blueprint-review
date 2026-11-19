# **Capability Record**

## Capability Name:

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

## Purpose

## Classification

## Dependencies

## Optional integrations

## Version

## Availability

## Capabilities offered

## Configuration

## Cross-capability note — Authorisation governance notifications (15 November 2026)

**Status:** Proposed relationship, not a published Notifications consumer. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) can emit selected role/grant changes, approvals, overdue access reviews and security-relevant revocations with safe recipient/context references. IAM/Identity determines current eligible persons/approvers and Profile or an approved contact provider owns addresses. Notifications owns dispatch, delivery/retry and template rendering; sending is not approval, evidence acceptance, revocation completion or confirmation of human receipt. Notifications' conceptual review remains incomplete.

## Cross-capability note — Billing event notification and delivery status (15 November 2026)

**Proposed reciprocal interface, not an implemented Notifications contract.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) may supply deduplicable, versioned notice intents with source event, permitted recipient reference, locale and purpose (charge finalised, dispute outcome, exception). Notifications owns dispatch coordination and may return queued/sent/failed/delivery-unknown result; Mailer or another provider owns channel transport. Billing does not assert that an invoice was legally issued, payment received, notice delivered or viewed merely because an intent was sent. Invoice owns issued-document notice content. Recipients/preferences, mandatory statutory notice rules, sensitive fields, tenant boundaries and reauthorisation must be enforced. Notification outages do not roll back a committed charge but mandatory notices must remain visible/pending under policy.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking conceptual completeness note (15 November 2026; agreed review direction):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) sends minimised and tenant-scoped confirmation, change, cancellation, reminder and exception notification intent with booking event/version, authorised recipient reference, locale and delivery purpose. Notifications owns routing, templates and message-delivery lifecycle, returning accepted/pending/failed results without modifying booking state. Optional delivery failure does not cancel a confirmed reservation; contact verification required before confirmation stays an explicit Booking-side dependency. No confirmed Notifications implementation interface is inferred.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Booking supplies tenant-scoped confirmation, change, cancellation and reminder intent with booking event/version, recipient reference and purpose; Notifications owns delivery orchestration/status and does not alter Booking state. Optional delivery failure does not reverse a confirmed booking. Required verification is a separately checked condition. No currently implemented integration contract is implied.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Supply scoped notices for invitations, proposed/approved ownership transfer, disputed recovery and appeals, policy changes, provisioning/payment problems, renewals, quota and seat warnings. Never treat successful delivery as authority to change governance or proof payment settled; respect privacy/disclosure and delivery uncertainty.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine may produce author/reply/mention, moderation decision and appeal disposition notice intents containing only authorised recipient references, bounded status/message keys and minimal comment links. Notifications owns channel choice, delivery and provider status; delivery does not prove comment publication, enforcement or receipt by a person. Suppress disclosure of hidden content, reporter identity and child-sensitive evidence.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Configuration supplies minimally scoped change-requested, decided and activated facts; Notifications owns authorised recipient delivery, templates and channel execution. Notification success never proves approval or activation. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course emits safe publication/review/withdrawal facts; Notifications owns delivery and retry. Dispatch cannot approve publication, grant enrolment or prove a learner received the message. This note does not complete the separate notifications review.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-09/11 agreed:** Notifications dispatches approved course, session, enrolment, assessment, learner migration or credential status alerts using minimised domain-source facts. Sending does not confer an award, constitute learner admission or demonstrate receipt. This note does not complete the separate notifications review.


## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)).** Notifications delivers opted/required issuance, expiry, revoked, replaced and status-action notices from committed Credentials events with authorised recipient context and minimised details. Delivery failures retry independently; neither successful email nor failed delivery determines whether credential issuance committed.


## Message Queue reciprocal conceptual interface — 19 November 2026

**Status: proposed in [Message Queue draft PR #94](https://github.com/nuxt-layers/architecture-blueprint-review/pull/94), not an approved API or implemented integration.** [Message Queue conceptual contract](../message_queue/capability-record.md#independent-message-queue-conceptual-review--19-november-2026) retains transport-only authority: originating capabilities own committed events and durable outboxes; Message Queue owns scoped subscriptions, transport custody, attempts, redrive/dead-letter and qualified acknowledgements. **Notifications owns intended recipients, consent/channel policy and notification delivery outcomes; MQ may forward authorised event notices and reports only transport status, not notification receipt or successful user contact.** No mutual direct package import is implied. Existing approved decisions remain unchanged; detailed MQ-01–10 decisions are not owner-approved.


## Message Queue reciprocal review — 19 November 2026

**Proposed in [draft PR #94](https://github.com/nuxt-layers/architecture-blueprint-review/pull/94); not an implemented or approved public API.** [Message Queue conceptual contract](../message_queue/capability-record.md#independent-message-queue-conceptual-review--19-november-2026): Notifications owns recipient/channel eligibility and actual notification outcomes; MQ conveys source events and transport receipts only, never proof of notification receipt or contact. Source capabilities own durable outboxes and event meaning; MQ owns scoped routing, custody, attempts, retry, dead-letter and replay. Duplicates, unknown receipts and scoped authorisation must be handled through public directional host-composed ports without cyclic imports. Preserve previous approvals.
