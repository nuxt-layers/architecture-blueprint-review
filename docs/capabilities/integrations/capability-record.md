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

## Review notes — contacts, financial providers and ownership (14 November 2026)

**Provisional conceptual notes only; verify root public contract before detailed Integrations specification.**

- Provider connectors (e.g. Xero/QuickBooks, payroll, procurement, banking, CRM) manage connections, provider-specific identity and field mapping, transport, checkpoints, provider limitations and status; they never silently become the owner of Product, Inventory, Asset, Order or Accounting domain facts.
- Accounting and Invoice independently select an approved authority per tenant/accounting context and supported service. Provider scope and compatibility must be verified; no assumption a connected product implements every accounting or invoicing operation.
- A connected customer/supplier directory may be externally authoritative under a specific approved mapping, but **Identity** and **Profile** remain authoritative for platform identities and personal-data disclosure.
- Provider outage does not silently switch authority. Changeover requires approved mapping, reconciled balances and outstanding work, source/remote IDs, versioned checkpoints and explicit cut-over.
- Imported financial transactions, asset registers, stock costs, supplier records and contacts must be validated and authorised by their owning domain, with provenance and replay/deduplication handling.

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Provider-neutral connection and transport mechanisms; never own commercial, physical-stock or financial domain records.
- **Related capability notes:** [accounting](../accounting/capability-record.md), [invoice](../invoice/capability-record.md), [order](../order/capability-record.md), [product](../product/capability-record.md), [inventory](../inventory/capability-record.md), [logistics](../logistics/capability-record.md).
- **Open architectural questions:** Per-tenant authority/connector selection, provider compatibility, external party-directory mappings and reconciled changeover.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.
