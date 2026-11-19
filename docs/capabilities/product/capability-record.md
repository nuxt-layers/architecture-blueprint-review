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

### Asset conceptual-review cross-reference (14 November 2026)

**Proposed:** [Asset](../asset/capability-record.md) records the identity and operational lifecycle of a particular managed physical unit, including third-party-owned leased or loaned equipment. Product retains saleable item/model/variant definitions and commercial descriptions; neither Product nor Asset alone determines stock balances or financial recognition. A product reference does not imply title or custody. Preserve the pending Product conceptual review.


## Reciprocal interface — Inventory conceptual review (18 November 2026)

**Owner-approved Inventory conceptual reciprocity (18 November 2026; PR #77):** Product supplies versioned physical item definitions, units, lot/serial tracking and virtual-bundle versus stocked-kit/BOM classifications. Inventory independently owns resulting stock identities, movements, lot/serial positions and quantity commitments. A virtual bundle cannot create additional stock; a physical conversion consumes components and creates traceable output. Production work-order authority remains open (INV-02). See [Inventory's proposed public contract](../inventory/capability-record.md#dedicated-inventory-conceptual-review--18-november-2026). This approves Inventory's conceptual interface only, not a neighbouring capability's unreviewed functionality or an implemented API.


## Inventory reassessment reciprocal proposal — 18 November 2026 (PR #81)

**Status: proposed, not approved or implemented.** Product remains authoritative for SKU/variant, UoM, serialisation/lot policy, effective versioned BOM and virtual-bundle vs physical-kit definitions. The **proposed** revised Inventory contract uses those inputs to record actual lot/serial stock positions, material conversions, WIP, scrap/yield and genealogy. Product does not create stock or determine financial carrying value. Manufacturing order execution ownership is still a separate decision. See the [Inventory reassessment contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md) and [Inventory record](../inventory/capability-record.md#renewed-conceptual-design-challenge--18-november-2026-draft-pr-81). This note preserves earlier approvals in this capability and does not complete its independent review.


### Inventory manufacturing traceability — owner-approved conceptual reciprocity (18 November 2026; PR #81)

**Approved Inventory-side conceptual requirement:** Product supplies stable billet/material/finished-part definitions, versioned units/BOM, kit/consumable classifications and manufacturing lot/serial rules. Inventory tracks physical unit, batch, WIP intermediate and finished-item genealogy through turning, milling, coating and packing; conversion consumes documented inputs, separately accounts for scrap and creates traceable outputs. Reusable work equipment is potentially Asset-owned; Product must not infer authoritative stock quantities or run manufacturing work orders. This note approves the **Inventory-side requirement only**, does not change this capability's independent approval status or claim a running integration. See [shop-floor flow and public contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026).

**Marketplace reciprocal — proposed, 19 November 2026:** [Marketplace review](../marketplace/capability-record.md#marketplace-conceptual-review--19-november-2026) consumes Product-authoritative item identity, permissible seller association and source revision to publish a seller/venue-specific listing. Marketplace owns publication, eligibility and market restriction, not Product description or product ownership; stale source data holds/flags affected listings. **Proposed only; no published Product API change.**
