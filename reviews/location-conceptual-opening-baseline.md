# Location — conceptual review opening baseline

**Status:** Proposed, non-normative; review opened 20 November 2026.
**Target:** `docs/capabilities/location/` (existing directory; retain exact spelling).
**Branch:** `review/location-conceptual-20261120`
**Governing master SHA:** `b920ce0d8b361de000a6739a16123dbdc56df7a7` (`nuxt-layers/architecture-rules`).
**Blueprint master SHA:** `6dac83a03da8704f7945ee1bc894f2248300445a` (`nuxt-layers/architecture-blueprint-review`).

## Initial evidence and scope

The blueprint catalogue describes Location as a platform candidate for coordinates, geospatial and place references, excluding ownership of all postal addresses or site tenancy. The existing record contains an Events interface reciprocity note dated 18 November 2026. This is a conceptual assessment, not an assertion of an implemented public contract.

This review will establish authoritative ownership, classification, provider-neutral native services and lifecycles, idealised inbound/outbound contracts and failure semantics, cross-capability reciprocal relationships, privacy/security, GUI/headless host presentation, acceptance scenarios, architectural alternatives and consistency findings. Review relevant accepted governing ADRs and published contracts before proposing changes. Existing concurrent reviews remain provisional until merged.

**Constraints:** No implementation repository changes, local tests/builds or merge without explicit approval. All review changes remain on the initial draft PR.
