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

## Review notes — commercial orders, counterparties and accounting (14 November 2026)

**Provisional conceptual notes only; Order is a candidate, not verified implementation.**

- **Sales order:** accepted customer commitment, agreed items/quantities/prices/terms, delivery/service obligations, change/cancellation and provenance. **Purchase order:** commitment to acquire goods/services from a supplier, with approval, receiving and fulfilment status. Neither is a posted journal or necessarily a legally issued invoice.
- Order references Product and Pricing definitions and an authorised **counterparty record**; it does not own the customer's Profile, supplier's entire identity or financial ledger. A service may have an order without inventory; an invoice can exist without a prior formal order.
- **Customer and Supplier are business roles**, potentially held by the same person or organisation. Propose a **Business Contacts / Parties** conceptual owner for tenant-scoped counterparties, address/contact methods, terms and role history, subject to a separate owner/lifecycle review.
- A party **does not need** an application Identity. Business records and legally necessary transaction communications must work for nonmembers. An optional linked Identity is a consensual, verified association with the party, not transfer of Profile ownership.
- **Discovery/invitation:** opt-in discoverable public handle or verified consented identifier; otherwise invitations must not reveal whether the addressee has an existing account. Rate-limit, verify contact possession, allow opt-out and protect against account enumeration. Existing Identity group invitations are **not** proof of a public business-party linking API.
- **Accounting consequence:** orders may create commitments and later evidence for accruals, costs, revenue or receivables/payables, but do not automatically recognise revenue at order creation; recognition requires actual policy and completed relevant economic events.
- **Open:** who owns customer/supplier business counterpart records; how do guest transactions, Identity linking/revocation and purchases across multiple tenants reconcile safely?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Sales/purchase commitments and business-party references; accounts and invoices retain their independent financial/document lifecycles.
- **Related capability notes:** [product](../product/capability-record.md), [inventory](../inventory/capability-record.md), [invoice](../invoice/capability-record.md), [accounting](../accounting/capability-record.md), [integrations](../integrations/capability-record.md), [billing](../billing/capability-record.md).
- **Open architectural questions:** Business Contacts / Parties owner; opt-in user discovery and identity linkage versus guest transactions, plus purchase-order/contract boundaries.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

## Cross-capability note — Orders as Billing evidence (15 November 2026)

**Proposed; BIL-01 remains open.** [Billing](../billing/capability-record.md) may consume Order's versioned acceptance, change, cancellation and fulfilment evidence to assess chargeability. Order remains authoritative for ordered goods/services and commercial acceptance; Billing owns resultant charge decisions. An accepted Order is not automatically an invoice, ledger posting or payment, and not all charges require an Order. Billing supplies charge/billing-status references back by public contract/event without Order reading Billing persistence.
