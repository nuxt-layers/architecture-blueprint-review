# Inventory conceptual review — opening baseline

**Date:** 18 November 2026  
**Status:** In progress; non-normative draft
**Target:** `docs/capabilities/inventory/capability-record.md`  
**Review branch:** `review/inventory-conceptual-20261118`  
**Governing master SHA:** `0725f314abc9ad13f1a65247f54a7ff80772f0b2`  
**Blueprint master SHA:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`

## Starting evidence and intended work

- Existing Inventory record contains provisional material-flow, stock/asset conversion, costing and Booking interface notes; it is not an approved complete contract.
- No open PR matching inventory was found at the opening check; no existing inventory review branch was found.
- Review current accepted ADRs and relevant catalogue, root CONTRACT.md evidence where available, adjacent owner records and active parallel reviews.
- Define source authority, lifecycle, native services, idealised inbound/outbound commands, queries and events, failures, validation, security, GUI, reciprocal contract notes and acceptance scenarios.
- Preserve unresolved decisions distinctly from approved authority; perform current-master technical and architectural consistency review before any merge request.

**Restrictions:** Blueprint documentation only. No implementation changes, local tests or merge without explicit approval.


## Owner approval and latest-master reconciliation (18 November 2026)

The owner expressly approved the Inventory conceptual definition and requested squash merge. This approval adopts Inventory's conceptual boundary, public inputs/outputs, core lifecycle, GUI and cross-capability principles including INV-01/06/07. INV-02/03/04/05/08 remain detailed design and implementation choices, subject to their approved non-duplication and authority constraints; no fictitious resolution is asserted.

The blueprint `master` advanced from `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` to `cf9804f0f44cc52d996f22c273a56df1ab0bdbf6` while governing `master` remained `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. The review was reconciled onto that newer blueprint baseline, preserving Booking's concurrent Events/Attendance interface notes. No implementation repository or local tests were changed.

**Authority review:** Inventory owns physical stock ledger, movements and quantity reservations. Identity/Authorisation own trusted context/access; Booking owns reservations of time/capacity, Attendance owns participation, Events owns event lifecycle, Order owns commercial obligations, Warehouse owns physical work, Product owns descriptions, Asset owns stewardship, Accounting owns ledger recognition, Logging owns technical diagnostics, Audit owns accountable evidence, Reporting owns derived reports, and Message Queue transports Inventory's outbox. These responsibilities remain separate. The proposal is not a runtime implementation or new normative ADR.
