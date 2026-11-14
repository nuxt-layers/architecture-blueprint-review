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

## Review notes — product, assemblies, bundles and accounting (14 November 2026)

**Provisional conceptual notes only.** Preserve the pro forma for the later alphabetical Product review. No Product implementation or public contract is asserted.

- **Product definition:** a versioned description of an item or service, including variants, units, commercial identity and references to component definitions; not stock quantity, ownership of a physical unit or accounting value.
- **Assembly / bill of materials:** an assembled car may be a finished product with a versioned component structure (engine, tyres, electronics). Define BOM versions, quantities, substitutes, traceability and effective dates. Whether manufacturing orders and their execution warrant a separate Process/Production domain requires review.
- **Commercial bundle / kit:** a store may sell several products together under one offer or listing. A **virtual bundle** draws from the component stock and does not automatically create a new stocked unit; a **prepacked kit** may involve actual stock conversion. Distinguish assembly/BOM from sellable bundle composition.
- **Serialised or unique goods:** one used car can have a product/model definition and a uniquely identified physical stock item with its own provenance, condition, cost and sale history.
- **Accounting connection:** define no book value solely from the product description or sales price. Inventory and production facts supply actual cost/movement evidence; Accounting applies financial classification, valuation, cost-of-goods-sold and recognised postings. A product used by the business instead of sold may become an Asset.
- **Open ownership:** which capability owns BOM/production engineering, versioned assembly change control, commercial bundles and manufactured-unit traceability? Confirm with Inventory, Order, Warehouse, Asset and Pricing in their alphabetical reviews.

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Sellable definitions, component assemblies and commercial bundle structures, not physical stock or financial book value.
- **Related capability notes:** [inventory](../inventory/capability-record.md), [warehouse](../warehouse/capability-record.md), [order](../order/capability-record.md), [asset](../asset/capability-record.md), [accounting](../accounting/capability-record.md).
- **Open architectural questions:** Versioned bills of materials, serialised units, kits versus virtual bundles, and production/process ownership.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.
