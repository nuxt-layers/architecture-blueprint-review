# Help — Capability Conceptual Record

**Status:** Proposed candidate for later alphabetical classification and full conceptual review (16 November 2026). This record captures initial intent only; no implementation, standalone repository, contract or dependency is approved.

## Purpose

Provide a coherent, version-aware help experience for people using applications composed from Nuxt Layers capabilities.

Two complementary surfaces are envisaged:

1. **Dedicated help system:** Authorised, searchable and indexable help articles and guides with maintained revisions, publication status, versions, localisation and links to relevant application/capability versions. Support an accessible help centre and navigable topics.
2. **Context-sensitive help:** Optional, configurable help buttons or links beside specific screens, fields, actions and workflows. The relevant help topic should be discoverable through stable documented identifiers and public contracts, preferably generated or validated from *explicit self-documenting metadata* maintained alongside the source and capability contracts, rather than invented by guessing from implementation code.

## Provisional boundaries to examine

- **Help** may own topic identifiers, mapping from documented UI/application context to help content, contextual resolution and presentation contracts. Whether it owns help-document lifecycle or delegates that lifecycle to **Publisher** requires classification before development.
- **Publisher / Content Editor** are the existing candidates for authoring, review, publication and generic editorial GUI. Do not introduce a competing document editor or content store without proof of independent ownership.
- **Search** may provide indexing and authorised retrieval, without Help duplicating the generic search engine or claiming ownership of other capabilities' documents.
- **Individual capabilities** should publish accurate, structured, versioned help metadata through their documented public interfaces, covering controls, operations, requirements, permissions, errors and user-facing semantics; private source inspection or automatically generated text is not a trusted source of truth.
- **Host/application composition** decides whether and where to show context-help buttons, navigates to the help centre and resolves the current page, locale, version and tenant context. No help link grants access to protected features.
- **Identity, Authorisation and Privacy** restrict context-specific and indexed content visibility. Public documentation and restricted tenant/administrator help must remain clearly separated.

## Questions for later review

Determine the authoritative help-content owner; stable topic/context identifiers and metadata generation pipeline; version-to-product compatibility and deprecation; search indexing ownership; localisation; publication/approval and accessibility; link integrity and offline/unavailable behaviour; security disclosure and permissions; whether one independent Help capability is justified or a composition of Publisher, Search and host GUI is sufficient.

## GUI expectation

A version-aware searchable Help Centre, plus an optional accessible **Help** control in relevant dashboard pages, forms, fields or sections. Contextual requests should open the correct approved help topic without requiring the user to leave their task unnecessarily. Placement and visibility are configurable by the host and remain subject to server-side access controls.

**Review gate:** Apply the established capability classification and ownership test before prescribing persistence, APIs, code generation technology, packages or a dedicated `nuxt-layers/help` repository. This is a brief statement of intent, not a finished `CONTRACT.md`.
