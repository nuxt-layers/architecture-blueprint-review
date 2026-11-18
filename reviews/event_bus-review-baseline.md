# Event Bus conceptual review baseline — 18 November 2026

- Target: `docs/capabilities/event_bus/` (actual directory name; display name `event-bus`).
- Review branch: `review/event_bus-conceptual-20261118`.
- Opening governing `nuxt-layers/architecture-rules/master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
- Opening blueprint `nuxt-layers/architecture-blueprint-review/master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
- Governing `docs/catalogue.md` recognises `message-queue` as the owner of durable transport of capability outbox messages.
- Target's existing record is a blank template; neighbouring directory is `message_queue`. The separate `events` directory is about real-world scheduled programmes/sessions, not event transport.
- Active target PR search: no matching open `event-bus` review PR at opening.
- Scope: independent capability justification versus `message-queue`; source-owned events/outboxes; idealised inputs/outputs and delivery guarantees; reciprocal interfaces; GUI/admin requirements; catalogue/register alignment; architectural and technical validation.
- Initial decision state: **proposed review**, not yet owner-approved; no implementation claim. No implementation changes, local tests or merge.
