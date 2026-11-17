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

## Reciprocal decision — redundant Document capability retired (17 November 2026)

**Owner-approved resolution, 17 November 2026:** no independent Document capability or source authority is needed. Export continues to produce authorised artefacts from Publisher's or the relevant domain owner's public data, without re-owning their records, permissions, holds or disclosure decisions. Historical conditional review: [Document](../../../reviews/document-directory-removal-2026-11-17.md).
