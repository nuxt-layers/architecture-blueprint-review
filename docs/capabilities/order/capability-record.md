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
