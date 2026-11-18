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

**Agreed conceptual relationship: BIL-01 approved on 15 November 2026; implementation remains unverified.** [Billing](../billing/capability-record.md) may consume Order's versioned acceptance, change, cancellation and fulfilment evidence to assess chargeability. Order remains authoritative for ordered goods/services and commercial acceptance; Billing owns resultant charge decisions. An accepted Order is not automatically an invoice, ledger posting or payment, and not all charges require an Order. Billing supplies charge/billing-status references back by public contract/event without Order reading Billing persistence.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy refinements proposed, implementation not assumed.

Own purchase acceptance and amendments for paid tenant creation and additional capabilities, seats and storage, consuming verified scoped quote and payer authority; do not assert payment/entitlement/provisioning success.

See [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md) for conceptual inbound/outbound authority, absence, failures and acceptance. No package dependencies inferred.


## Reciprocal interface — Inventory conceptual review (18 November 2026)

**Owner-approved Inventory conceptual reciprocity (18 November 2026; PR #77):** Order sends versioned sale/purchase quantity commitments, cancellations, returns and fulfilment references; Inventory returns revision-scoped checked stock reservation, release, issue and shortage/uncertainty outcomes. Order owns commercial obligation and acceptance, never an independently maintained stock-availability counter. An Inventory hold alone does not mean the order was accepted. Cross-owner partial completion requires traceable compensation. See [Inventory's proposed public contract](../inventory/capability-record.md#dedicated-inventory-conceptual-review--18-november-2026). This approves Inventory's conceptual interface only, not a neighbouring capability's unreviewed functionality or an implemented API.


## Inventory reassessment reciprocal proposal — 18 November 2026 (PR #81)

**Status: proposed, not approved or implemented.** Order owns commercial purchase/sale commitments, customer/supplier obligations and cancellation/return facts. The **proposed** Inventory contract returns checked, versioned, idempotent reservation/issue/release and shortage/unknown outcomes; snapshot availability is not a guarantee. Order must not infer a seller's title from Inventory custody or a fulfilled sale from a committed stock movement. No duplicate availability ledger. See the [Inventory reassessment contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md) and [Inventory record](../inventory/capability-record.md#renewed-conceptual-design-challenge--18-november-2026-draft-pr-81). This note preserves earlier approvals in this capability and does not complete its independent review.


### Inventory manufacturing traceability — owner-approved conceptual reciprocity (18 November 2026; PR #81)

**Approved Inventory-side conceptual requirement:** Stock availability and fulfilment must account for items in raw stores, manufacturing WIP, outsourced coating, packing, finished stock, quarantine and pending movements. Order may request future delivery/production but cannot reserve WIP as finished saleable stock without the declared eligibility policy and Inventory's actual atomic commitment. An as-of shop-floor scan is not proof of order fulfilment. This note approves the **Inventory-side requirement only**, does not change this capability's independent approval status or claim a running integration. See [shop-floor flow and public contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026).

## Cross-capability note — Invoice conceptual public contract (18 November 2026)

**Owner-approved Invoice conceptual review (18 November 2026), implementation not verified.** [Invoice](../invoice/capability-record.md) may use versioned Order terms/acceptance/fulfilment as source evidence, returning issued/correction references via public events. Orders do not automatically authorise invoice issue; standalone invoices and supplier bills need no Order. Never let historical Order changes mutate issued document snapshots.
