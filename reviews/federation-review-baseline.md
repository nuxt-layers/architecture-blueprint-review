# Federation — conceptual review baseline

**Date:** 18 November 2026  
**Status:** Work in progress, non-normative; owner approval pending.  
**Target directory:** `docs/capabilities/federation/`  
**Branch:** `review/federation-conceptual`

- Governing `nuxt-layers/architecture-rules` `master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
- Blueprint `nuxt-layers/architecture-blueprint-review` `master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
- Current review protocol: `docs/review-protocol.md`; complete Phase 1 authority review follows.
- Active PRs specifically matching federation at opening: none returned by repository PR search; parallel related reviews may exist.

## Scope

Review Federation's independent justification, Node/Hub roles, source-of-truth and exchange boundaries, opt-in peer lifecycle, protocol neutrality, durable public inbound/outbound contracts, subscriptions, synchronisation and withdrawal, trust, privacy, authorisation, failure and replay, cross-capability reciprocal notes, headless and host GUI composition, acceptance scenarios, and outstanding owner decisions. Review existing Node–Hub architecture and adjacent conceptual records. No implementation edits, local tests, governing changes or merge are authorised.

## Baseline evidence

The working catalogue identifies Federation as a platform capability candidate, Node as a deployment/network participant rather than a capability, and Hub as an application composition/operator role; operational or implementation conformance is not verified. These remain provisional until the dedicated review and owner decision.
