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

## Review notes — operating costs, supplier bills and accounting (14 November 2026)

**Provisional conceptual notes only; Billing versus Invoice responsibilities require later review.**

- Recurring utility charges, contractor services, subscriptions, leases and supplier bills may create **accounts payable**, accruals or prepayments, not necessarily a new sales Order. An approved supplier relationship and attributable document can exist without the supplier joining the application.
- Billing would govern charge calculation/periods and possibly payable charge intake under an approved boundary. Invoice owns issued/received document semantics where justified. Accounting owns financial posting, balances and reconciliation; Payment Gateway handles payment execution.
- Distinguish quote/contract, order, delivery or usage, accrued expense, bill/invoice, payment and bank settlement; each can occur in a different accounting period.
- **Open:** who owns inbound supplier invoice capture and disputes; recurring commitments and payment schedules; invoice-to-ledger confirmation and external provider mapping?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Charge calculation and recurring commercial periods; Invoice records issued/received billing documents, Accounting recognises liabilities and expenses.
- **Related capability notes:** [invoice](../invoice/capability-record.md), [accounting](../accounting/capability-record.md), [order](../order/capability-record.md), [employment](../employment/capability-record.md), [logistics](../logistics/capability-record.md).
- **Open architectural questions:** Ownership of supplier-bill intake, recurring utilities, accrual triggers and charge/credit disputes.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.
