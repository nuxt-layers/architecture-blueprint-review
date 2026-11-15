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

## Review notes — invoice construction and authoritative provider mode (14 November 2026)

**Provisional conceptual notes only; not a completed Invoice specification.**

- Invoice is the **tool and business record** for construction, calculation validation, numbering, issuing, rendering, delivery, status and correction/credit-note lifecycle. It is more than a PDF; a final issued invoice must preserve the approved financial facts and provenance.
- Publisher may provide suitable document lifecycle/publication mechanics and Content Editor may provide editing/presentation; Template Engine may render from approved data. None automatically owns Invoice's statutory/business identity, amounts or adjustment rules.
- **Tenant configuration:** native Invoice when no approved external invoice authority is selected; connected Invoice through Integrations when an external provider is the approved authority for the scope. Connected mode cannot create duplicate invoice numbers or claim locally issued authority at the same time.
- Invoice and Accounting may choose different providers where supported, but must reconcile issued bills, corrections, settlements and financial postings. An external provider outage does not silently switch invoicing to native issue.
- **Order relationship:** sales or purchase order may supply terms and source evidence, but invoices may be issued for services or other legitimate charges without an Order.
- **Counterparties:** invoices snapshot needed recipient, supplier/customer and tax/address data at issue time rather than depending entirely on a mutable Business Contact or Profile.
- **Open:** who owns supplier bill ingestion, credit notes, cross-border requirements, numbering sequences, financial amounts and transfer of authority when switching provider?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Issuance, document construction and corrections; provider authority may be native or externally connected, independently from Accounting's ledger choice.
- **Related capability notes:** [order](../order/capability-record.md), [accounting](../accounting/capability-record.md), [billing](../billing/capability-record.md), [integrations](../integrations/capability-record.md), [product](../product/capability-record.md).
- **Open architectural questions:** Supplier-bill intake, statutory issue/numbering rules, party snapshots and cross-provider reconciliation.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

## Cross-capability note — Billing charge-to-document handoff (15 November 2026)

**Agreed conceptual relationship: Billing BIL-01–BIL-06 approved on 15 November 2026; Invoice implementation remains unverified.** [Billing](../billing/capability-record.md#idealised-public-outbound-contract) supplies versioned, finalised charge batches, attributed commercial calculations and approved adjustment/credit requests. Invoice independently validates, constructs, numbers, issues, records and corrects formal invoice documents; it supplies authoritative issue/rejection/credit-document status and references. A charge finalisation or handoff request must never imply a legal invoice has been issued, and replay must not duplicate issuance. Supplier invoice intake is provisionally Invoice-owned; Billing may assess commercial obligations only. See approved BIL-01, BIL-03 and BIL-04. Invoice's alphabetical review is still pending.
