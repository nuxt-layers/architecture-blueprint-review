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

## Review notes — storage, transport, fulfilment cost and accounting (14 November 2026)

**Provisional conceptual notes only.** Logistics is not yet specified as an independently implemented domain.

- Logistics may govern **movement planning and delivery execution**: shipments, carriers, freight quotations, transport legs, tracking, delivery confirmation, returns transport and actual transport charge evidence. It should not take over Order commitments, Inventory quantities, Warehouse physical storage work or Accounting postings.
- **Physical storage operations** (locations, occupancy, handling and custody) ordinarily belong to Warehouse. Storage contracts, externally billed space, detention/demurrage and charge calculation may belong to Logistics, Billing or an independently justified facilities/service responsibility; choose the owner based on the specific lifecycle, not the word “storage”.
- Potential cost evidence includes carrier charges, postage, fuel, packaging, handling, pallet/container fees, storage duration/volume, insurance, customs duties, third-party logistics (3PL) invoices, returns and damage claims. Separate **estimated/quoted** costs from **incurred/verified** costs, and record who owes or pays them.
- Costs may be allocated to **inventory acquisition/landed cost**, manufacturing/WIP, **cost of sales**, selling/distribution expense, a customer charge or a recoverable amount, depending on the actual economic event and approved accounting policy. Logistics supplies quantities, services, rates and evidence; Accounting decides recognised valuation, period, classification and journals.
- An Order may quote a customer delivery fee, Invoice may charge it, and Payment Gateway may settle it. These are **not** the same as the carrier's actual cost; reconciliation should explain margin or difference without transferring source ownership.
- Integrations could connect transport carriers and 3PL/warehouse providers. Connectors should record verified remote identifiers, checkpoints and price evidence without becoming the authoritative logistics or financial domain.
- **Open:** where do warehousing rate cards, billable occupancy, freight procurement, carrier contracts, landed-cost allocation, customs/tax, reverse logistics and third-party warehousing charges belong? Which events are authoritative for accrued versus actual costs?
