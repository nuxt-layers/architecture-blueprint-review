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
