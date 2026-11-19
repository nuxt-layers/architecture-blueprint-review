# Message Queue conceptual review — opening baseline

- Target: `docs/capabilities/message_queue/` (directory spelling verified).
- Review branch: `review/message_queue-conceptual`.
- Blueprint master at opening: `6dac83a03da8704f7945ee1bc894f2248300445a`.
- Governing architecture-rules master at opening: `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
- Protocol: `docs/review-protocol.md` on opening blueprint master.
- No open PR matching `message_queue` found in initial target PR search.
- Relevant preceding work: owner-approved Event Bus consolidation (EB-05) and source-owned durable outboxes; existing reciprocal notes for Authentication, Booking, Configuration, Events, Federation and Integrations.
- Scope: establish authoritative transport boundary, native and provider-backed behaviour, idealised published inbound/outbound interfaces, security and operational controls, producer/consumer relationships, reciprocal documentation, conceptual GUI and acceptance scenarios.
- Status: review opened; conceptual findings not yet approved; no implementation or CI claims. All work remains in this draft PR; no implementation repository changes, tests or merge.
