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

## Cross-capability note — Audit evidence attachments and custody (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** Storage owns bytes and provider-agnostic file delivery, not Audit evidence ownership. **Proposed:** [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026) may use the published StorageService shape for protected attachments, keeping evidence associations, integrity manifests, holds/disposal decisions and disclosure in Audit. Missing bytes yield explicit unavailable/partial verification, not fabricated authenticity. No assumption that generic object storage provides immutable audit custody. Storage's conceptual review remains incomplete.

## Cross-capability note — Authorisation of protected files (15 November 2026)

**Status:** Proposed relationship; no new Storage access-decision ownership. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) may evaluate owner-supplied verified file/resource context and requested read/write/share/export permission. Storage remains responsible for file bytes and provider-neutral file operations, while the content/domain owner retains business metadata and disclosure rules. Signed links, caches, derivatives and file exports need tenant scoping, bounded lifetime and revocation semantics; a storage success does not itself prove lawful or authorised disclosure. Storage's conceptual review remains incomplete.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy refinements proposed, implementation not assumed.

Own tenant/group scoped bytes and usage, not commercial entitlements. Current root CONTRACT says usage is not a limit. Proposed quota-admission must enforce paid logical GB/object limits including parallel uploads and downgrade, without bucket-per-tenant provisioning. Hetzner S3 reserved for images/files.

See [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md) for conceptual inbound/outbound authority, absence, failures and acceptance. No package dependencies inferred.

## Reciprocal decision — redundant Document capability retired (17 November 2026)

**Owner-approved resolution, 17 November 2026:** no standalone Document capability will duplicate records or custody. Storage continues to own provider-neutral file bytes, not the business meaning or legal retention decisions for files owned by Publisher or domain capabilities. These owners must enforce authorisation and applicable holds before disclosure/disposal. Historical proposed custody design: [Document](../../../reviews/document-directory-removal-2026-11-17.md).

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** Export Library yields file bytes/stream and optional digest only; it does not own object keys, signed URLs, retention or stored artefacts. A caller or Reporting-owned workflow uses Storage's public service for generated files and remains accountable for artefact metadata, tenant boundaries, authorisation and revocation. Storage owns bytes, not content or business disclosure decisions. No direct Export dependency on Storage is mandatory. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.


## Infrastructure reciprocal interface — 18 November 2026

**Proposed reciprocal review — 18 November 2026:** Infrastructure [conceptual contract](../../../reviews/infrastructure-conceptual-architecture.md) provides trusted S3/provider deployment, credentials and resource readiness while Storage's published contract continues to own consumer-facing object operations and each consumer retains file access decisions. Postgres, Temporal and infrastructure backups are not reclassified as Storage objects; no automatic tenant bucket allocation or quota enforcement is inferred. Proposed only.


## Media reciprocal conceptual interface — 19 November 2026 (proposed; PR #92)

**Status:** Provisional Media review, not approved as the storage public implementation contract. See [Media dedicated conceptual review](../media/capability-record.md#dedicated-conceptual-review--media-19-november-2026).

Media is the authoritative owner of image asset records, processing and visibility, and consumes Storage's ADR-0012 Files port for staging, byte operations, signed delivery, revocation and usage. Storage retains bucket/provider/byte lifecycle; a signed byte address never grants Media publication eligibility. A private original or quarantined/removed variant must remain inaccessible notwithstanding byte-store capability. Reconcile idempotent claim, orphan cleanup, deletion, CDN purge, tenant/group scoping, measured usage and backup/erasure replay through published interfaces. Required port absence fails closed.
