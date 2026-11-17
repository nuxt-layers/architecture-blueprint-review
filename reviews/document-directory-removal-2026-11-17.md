# Retired Document capability — directory removal

**Date:** 17 November 2026
**Status:** Owner-approved retirement; documentation cleanup, not a new capability review.

The owner explicitly confirmed that `document` is redundant as an independent capability. PR #58 merged the catalogue/register retirement and reciprocal boundaries, but retained `docs/capabilities/document/capability-record.md`. This follow-up removes that directory as requested.

## Preserved architectural decision

- Publisher owns the versions, approvals, publication, addresses, feeds, and lifecycle of its registered document types.
- Content Editor is the generic editorial presentation over Publisher's public contract.
- Storage owns file bytes, not business-document semantics.
- Source business capabilities remain authoritative for their domain records and corresponding constraints; Publisher does not automatically acquire those records.
- No separate `document` capability, master store, public API, event stream, or dashboard is authorised.
- The conditional custody design from the superseded Document review was **exploratory only**, not an approved requirement.

## Traceability

- [Merged PR #58](https://github.com/nuxt-layers/architecture-blueprint-review/pull/58): classification decision and existing reciprocal boundaries.
- [Document review opening baseline](document-review-baseline.md): original review context.
- The deleted capability record remains accessible through repository history and PR #58; this note supersedes it for active documentation.

No implementation repository change or local build/test is required for this documentation-only cleanup.

## Final content-preservation audit — 17 November 2026

**Decision: safe to remove the active capability file, with historical preservation.** Reviewed the entire 117-line, approximately 22 KB former `docs/capabilities/document/capability-record.md` on `master` (blob `1c05f8e37b0a04611bda122c8887d88bdd34f421`) against Publisher's root `CONTRACT.md` and related working records. The file clearly marks DOC-01 as the owner-approved retirement; DOC-02/DOC-03, seven idealised inbound and six outbound interfaces, illustrative events, custody lifecycle and optional GUI are **conditional, superseded proposals**, not approved architecture, published API or verified functionality. The complete original is recoverable at [the pinned historical blob](https://github.com/nuxt-layers/architecture-blueprint-review/blob/1c05f8e37b0a04611bda122c8887d88bdd34f421/docs/capabilities/document/capability-record.md) and [merged PR #58](https://github.com/nuxt-layers/architecture-blueprint-review/pull/58).

### Distinct concerns to preserve without assigning a new capability

| Concern from superseded exploration | Retained responsibility / future review trigger |
|---|---|
| Private originals, custody receipts, classification and evidence integrity | The originating business-domain record owner owns business meaning and its authoritative record. Storage retains bytes, Audit retains its own independent event/evidence trail. An unsatisfied **generic cross-domain records-custody** requirement is **not proved or accepted**; reassess only if concrete consumers and independent invariants emerge |
| Provenance, version/digest verification and missing or altered files | Originating record owner coordinates object identity, digest and recovery; Storage provides file operations; Content Security assesses submitted bytes where applicable. A successful upload is not proof of record acceptance |
| Legal holds, purpose, retention, erasure, disposal and authorised disclosures | Legal Compliance and Privacy provide applicable constraints; the originating owner enforces record-specific transitions and receives confirmed outcomes. Qualified jurisdictional review is required; no universal policy or period is imposed |
| Tenant isolation, recipient checks, temporary links, redaction, export | Authorisation and record owner enforce access/purpose; Storage and Export cannot confer business permission or legal disclosure authority |
| Third-party office/DMS authority, replication, migrations and uncertain remote receipts | Integrations owns transport/provider coordination; each record owner declares its external authority strategy. Provider selection and reconciliation remain domain-specific, unapproved where not already documented |
| Failure/recovery, idempotent commands, durable outbox, audit evidence | Apply existing governing contracts to each actual state owner; do not transplant illustrative `document-record.*` event names or create a duplicate event stream |
| Editorial GUI versus private records UI | Content Editor continues to present Publisher types. Private business documents, if needed, are viewed/managed through their owning domain's public contract and application presentation; no generic Document menu is justified |

**Scope qualification:** This deletion **does not prove** that Publisher can act as a general-purpose private records-management system. Publisher's verified root contract covers host-registered publishing-document types. Requirements not covered there are obligations for their actual domain owners or future independent architectural review, **not** implicitly transferred into Publisher or discarded as business needs.

### Review verification and limits

- The approved classification and required ownership boundaries are preserved in this review note and adjacent records; catalogue/register entries were removed in merged PR #58.
- On PR #61 the sole document directory file is deleted, and five known direct relative links (Publisher, Content Editor, Storage, Export, Search) point here instead. The branch comparison should be rechecked immediately before merge.
- No new technical capability or runtime contract is approved by this audit. Historical PR/blob retains the full conditional design for reference. No implementation repository changes, builds, or tests were performed.
