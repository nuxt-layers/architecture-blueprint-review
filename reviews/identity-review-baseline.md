# Identity capability — conceptual review baseline

**Status:** In progress; non-normative working blueprint, not owner approval or implementation evidence.

- Target directory: `docs/capabilities/identity/` (actual existing directory, preserved).
- Review branch: `review/identity-conceptual-20261118`.
- Governing `nuxt-layers/architecture-rules` `master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
- Blueprint `nuxt-layers/architecture-blueprint-review` `master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
- Evidence: `nuxt-layers/identity/CONTRACT.md` as read from `master`; existing Identity record holds provisional reciprocal notes on Authentication, Authorisation, Tenancy, Verification, Configuration, Employment and Enrolment.
- Scope: review governance, authoritative principal/tenant/group/membership lifecycles, published versus idealised public input/output, cross-capability boundaries, reciprocal documents, security/privacy, operating and failure modes, provider interfaces, GUI presentation, acceptance and outstanding decisions.
- Related work: other concurrent capability PRs are provisional until merged; preserve existing approved decisions and distinguish new proposals.
- No implementation repository edits, local tests or merge. Mandatory final technical/architectural reconciliation against current `master` and explicit owner approval remain required.

## Pre-merge reconciliation — 18 November 2026

Governing master retained `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. Blueprint master advanced from `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` to `1ef77412e760f2be953d50dd40024c945871fd6f`. For each of nine overlapping capability records, both histories consisted exclusively of appended notes after their common baseline. The reconciled tree preserves the latest master verbatim followed by the Identity review additions, retaining all concurrent approved/provisional notes without replacing them. The baseline review file remains on this original PR.

Architectural reconciliation: Identity continues to own principal, tenant, group, direct membership and digital governance state; Authentication keeps assurance/sessions, Authorisation decisions/grants, Profile personal details, Verification verified claims, IAM Integration orchestration, Audit custody, Logging technical logs, Reporting derived analysis. Accepted ADR-0017 obligations remain distinguished from published implementation gaps; unrelated Gaming and other recent reciprocal decisions remain intact. No new universal package dependency or circular private-store access is asserted. Existing open design investigations remain marked as such.

Final GitHub mergeability, protected branch and CI status must be rechecked after branch head reconciliation. No local tests or implementation edits.
