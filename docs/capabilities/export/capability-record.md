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

## Cross-capability note — Authorisation of bulk export (15 November 2026)

**Status:** Proposed reciprocal interface, not an implemented Export/Authorisation integration. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) supplies current action/resource permissions and bounded visible scopes; each owning domain supplies the source records and applicable legal/privacy restrictions. Export must separately enforce bulk-disclosure permission, tenant boundaries, snapshot freshness, recipient/destination controls and the difference between export job acceptance and completed disclosure. Download links and derived copies must not bypass revocation or become cross-tenant bearer access by default. Export's review remains incomplete.

## Cross-capability note — Billing data export, scope and authority (15 November 2026)

**Proposed reciprocal relationship, not an implemented Export adapter.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) supplies scoped, versioned and authorised commercial charge queries/snapshots with lineage, currency/period and completeness indicators. Export owns the generated file/package, recipient/destination, job and delivery/retention lifecycle; it cannot independently broaden source access or become Billing's authoritative charge archive. Rights must be rechecked for the requested dataset, sensitive columns, recipient and saved artefact, including cross-tenant/party and bulk export. Privileged exports produce risk-selected Audit evidence. External provider authority migration requires reconciled identifiers, revisions and corrections, not a raw file assumed complete. An Export outage must not prevent native Billing transactions.

## Reciprocal conceptual note — private record production (17 November 2026)

**Status: proposed in [Document draft PR #58](https://github.com/nuxt-layers/architecture-blueprint-review/pull/58); not a completed Export contract.** If private custody records are independently justified, their authorised owner supplies source-scoped, revision-pinned, redaction-aware artefacts to Export, which owns conversion/package generation and delivery lifecycle, not the original's custody, hold, retention or disclosure authority. Export must independently evaluate recipient, purpose, bulk-access rights and revocation/expiry, report partial/error/reconciliation outcomes, and never treat conversion, package acceptance or a signed link as a completed lawful disclosure. Publisher's ordinary document export and the existing Rich Text safe-tree conversion remain unchanged. See [Document conditional contract](../document/capability-record.md).
