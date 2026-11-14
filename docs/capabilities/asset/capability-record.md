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

## Review notes — operational assets and accounting (14 November 2026)

**Provisional conceptual notes only; Asset's status and independent owner remain to be reviewed.**

- A business asset may be machinery, tools, vehicles, equipment, fixtures, buildings or other identifiable property used in operations. **Asset** would own physical identity, custodian/owner references, location, condition, maintenance, inspection, warranty, service history, lifecycle and disposal evidence.
- **Accounting** owns financial treatment (capitalisation, acquisition cost, depreciation/amortisation where applicable, impairment, carrying value and disposal postings) and reconciliation to the operational asset record; it must not become the operational maintenance register.
- The **same car** may be sellable stock for a dealer, a company vehicle/fixed asset for another tenant, or equipment used in production. Classification depends on actual use, control, applicable financial policy and time; Product describes the item, Inventory tracks saleable stock, Asset tracks operational use.
- Not every consumable, spare or tool is a fixed asset. Some are expense items or inventory; policies and thresholds vary. Leased assets, rights of use, intangible assets, land and buildings require distinct financial treatment review.
- **Open:** is Asset an independent domain with durable maintenance/custody lifecycle, or a specialised use of other records? What evidence marks acquisition, commissioning, transfers, capital improvements, downtime, impairment and decommissioning?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Operational custody, use, maintenance and disposal of identifiable equipment and property; Accounting, not Asset, determines financial carrying value.
- **Related capability notes:** [product](../product/capability-record.md), [inventory](../inventory/capability-record.md), [accounting](../accounting/capability-record.md), [order](../order/capability-record.md), [employment](../employment/capability-record.md).
- **Open architectural questions:** Asset-versus-inventory classification, leased property, capitalisation evidence and where financial fixed-asset subledger functions live.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.
