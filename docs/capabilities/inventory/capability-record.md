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

## Review notes — inventory, material flow and accounting (14 November 2026)

**Provisional conceptual notes only; not a completed Inventory specification.**

- Inventory is authoritative for **physical stock and movement**: raw materials, components, work in progress (WIP), finished goods, returned goods, consumables held for production, reservations, custody/location and quantity adjustments; whether all these states are first-class must be separately reviewed.
- Distinguish **raw stock**, **serialised unique units**, **completed assemblies**, **prepacked kits** and **virtual sales bundles**. A virtual bundle must not double count component stock; assembly/kit production consumes input units and creates traceable outputs, including scrap or yield differences.
- Inventory records acquisition/cost provenance and movements necessary for valuation; Accounting owns **financial ledger and approved valuation policy**, including cost formula, recognised inventory carrying amounts, WIP, cost of goods sold, loss and write-downs. Warehouse owns physical handling/fulfilment work, not a competing quantity ledger.
- Relevant costing questions: purchase cost, freight/duties, supplier credits, material/labour/production overhead allocation, FIFO/weighted-average/specific identification where appropriate, period cut-off, returns, write-offs and reconciliation between quantity and value.
- **A list price is not the carrying value of stock.** Financial recognition rules depend on the reporting basis and jurisdiction; IFRS IAS 2 is a useful reference, not automatically a rule for every tenant.
- **Open:** who owns valuation input evidence and landed-cost allocation? How do inventories transfer into fixed assets, and vice versa, through authorised classified movements without double recognition?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Authoritative physical units, quantities and movements, including parts, WIP and bundled stock conversions; Accounting owns financial valuations.
- **Related capability notes:** [product](../product/capability-record.md), [warehouse](../warehouse/capability-record.md), [logistics](../logistics/capability-record.md), [asset](../asset/capability-record.md), [accounting](../accounting/capability-record.md).
- **Open architectural questions:** BOM and production ownership, landed-cost evidence, inventory cost methods, and controlled transfer into or out of fixed assets.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

### Asset conceptual-review cross-reference (14 November 2026)

**Proposed:** [Asset](../asset/capability-record.md) owns operational stewardship of individually identifiable managed equipment/property, regardless of legal ownership. Inventory remains authoritative for saleable/production stock quantities and movements. Conversion of a serialised item from stock to operational use (and back) needs an authorised cross-owner handover and Accounting reconciliation, without double-counting or duplicated authority. Protocol details remain open for Inventory's own review.
