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
