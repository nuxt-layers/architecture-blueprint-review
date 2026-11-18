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

## Review notes — physical work versus financial inventory (14 November 2026)

**Provisional conceptual notes only.**

- Warehouse owns receiving, put-away, picking, packing, shipping, work assignments, physical locations and operational evidence. Inventory is authoritative for stock quantities, reservations and movements; Product describes goods and their assemblies.
- Assembly/build operations may physically consume raw materials and parts, produce WIP or finished stock, and generate labour/scrap/overhead evidence. Decide whether this is Warehouse work, a separate manufacturing/production process owner or both through published interfaces.
- Warehouse completion is **not** itself an Accounting journal. Validated Inventory movements and approved costing facts can produce financial consequences through Accounting, including inventory transfers, adjustments, shrinkage and cost of goods sold.
- A bundle picked for a sale may be purely virtual (components dispatched together) or a preassembled stocked kit; do not manufacture additional stock identity or valuation without a real conversion.
- **Open:** custody versus title, consignment stock, returns, serial tracking, outsourcing, WIP ownership and the boundary between manufacturing and warehouse operations.

### Storage charges and cost evidence — additional note

- Warehouse should record **physical** occupancy, pallet/bin/space use, handling, storage periods and relevant location/custody facts, subject to later contract review. Logistics or Billing may calculate **commercial storage and delivery charges** where it owns the applicable service/rate agreement; separate physical evidence from invoices and tariff rules.
- Accounting recognises approved inventory holding, warehouse overhead, external storage and transport costs under the applicable reporting rules. **Not all storage is capitalisable inventory cost**; avoid automatically valuing inventory from warehouse rental fees or treating sales-delivery costs as purchase landed cost.
- Distinguish quoted shipping fees charged to customers from actual freight/3PL costs, with source references so Accounting can reconcile them to Orders and Invoices.

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Physical storage, occupancy, handling and assembly-work evidence; Logistics may own carrier execution and service tariffs; Accounting recognises costs.
- **Related capability notes:** [inventory](../inventory/capability-record.md), [logistics](../logistics/capability-record.md), [product](../product/capability-record.md), [asset](../asset/capability-record.md), [accounting](../accounting/capability-record.md).
- **Open architectural questions:** 3PL contracts, storage rate ownership, WIP/production operations and allocation of storage expenses to inventory versus period cost.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.


## Reciprocal interface — Inventory conceptual review (18 November 2026)

**Owner-approved Inventory conceptual reciprocity (18 November 2026; PR #77):** Warehouse owns receive/pick/pack/put-away/stocktake handling and physical work evidence; Inventory validates and commits authoritative receipts, issues, transfers, holds, lot/serial quantities and variances. A warehouse work-completed event is not itself stock or accounting completion. Unavailable or contradictory Inventory confirmation leaves the work in an explicit exception/pending state. See [Inventory's proposed public contract](../inventory/capability-record.md#dedicated-inventory-conceptual-review--18-november-2026). This approves Inventory's conceptual interface only, not a neighbouring capability's unreviewed functionality or an implemented API.
