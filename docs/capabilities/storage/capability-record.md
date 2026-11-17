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

## Reciprocal conceptual note — document custody and byte ownership (17 November 2026)

**Status: proposed in [Document draft PR #58](https://github.com/nuxt-layers/architecture-blueprint-review/pull/58), not a published integration.** Storage's public file service continues to own byte objects and provider-neutral retrieval/usage, not the underlying record's document identity, legal hold, record-classification, disclosure eligibility, chain of custody or disposition. If a separate Document custody authority is approved, it must validate stored file digests/readback, isolate tenant and recipient, differentiate committed record receipts from successful uploads, recheck access before temporary links, record missing/altered bytes as unavailable, and coordinate final destruction without claiming Storage deletion establishes lawful disposal. Domain owners or Publisher keep authority over their respective records unless separately delegated. See [Document conditional contract](../document/capability-record.md).
