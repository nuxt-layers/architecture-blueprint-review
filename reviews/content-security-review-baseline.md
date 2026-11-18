# Content Security — review baseline (17 November 2026)

- **Status:** Draft, non-normative capability conceptual review; no implementation or governing change approved.
- **Target directory:** `docs/capabilities/content_security/` (the directory uses an underscore, although the catalogue name is `content-security`).
- **Governing master opening SHA:** `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
- **Blueprint master opening SHA:** `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`.
- **Protocol:** `docs/review-protocol.md` at the opening blueprint baseline.
- **Existing evidence:** Governing catalogue describes submitted-content scanning for dangerous content, links and abuse, in addition to domain-specific validation. Existing reciprocal notes cover Audit, Moderation and Comments Engine; Comments Engine PR #52 is merged in the opening baseline. Root implementation contract and independent acceptance still to be verified.
- **Scope:** Authority and exclusions, native scanning behaviour and safety lifecycle; idealised inbound/outbound public contract; provenance and failure handling; classification and optional provider boundaries; Content Security/Moderation/domain-owner separation; relevant reciprocal capability documentation; privacy/UK Online Safety and policy constraints; dashboard and contextual GUI; conceptual acceptance cases; technical/architectural consistency review against latest master.
- **Open decisions:** Risk-based mandatory scanning, provider-dependent signals and unknown handling, data retention, reviewer permissions, scanning private/federated content and re-scanning/version invalidation all require qualified investigation and explicit status.
- **Concurrent safeguards:** Recheck active capability review PRs before shared documentation edits; keep additive reciprocal notes; preserve accepted content. This branch is the only intended PR for this review.
