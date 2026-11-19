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

## Cross-capability note — Authentication data and retention (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns sign-in identifiers, credentials, sessions and their security metadata; Privacy owns relevant retention and personal-data policy. **Agreed conceptual direction (AUT-11):** Authentication minimises collection, applies classified and lawfully bounded retention, cooperates in coordinated account closure and data-subject handling without transferring record ownership, and documents disclosures to external identity providers. Privacy requirements cannot be overridden by an optional provider. **Open:** exact data classes, retention periods and jurisdiction-specific obligations. Privacy's own conceptual review remains incomplete.

## Cross-capability note — Authorisation record minimisation (15 November 2026)

**Established:** [Authorisation](../authorisation/capability-record.md) owns access records and changes, not Profile personal details; Privacy defines relevant rights, collection and lawful retention constraints. **Proposed:** minimise principal identifiers, decision and denial metadata; govern security evidence retention, subject export/erasure and legal holds without hiding critical access provenance or making indefinite storage the default. **Open:** precise lawful periods, evidence classifications and necessary restricted disclosures. Privacy's review remains incomplete.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Booking participation and guest-data interface (15 November 2026):** [Booking](../booking/capability-record.md#focused-reciprocal-contract-clarifications) uses only necessary participant references, authorised contact/verification, acting-for proof and policy-constrained guest association; Privacy owns purpose, disclosure, lawful retention, data-subject rights and restrictions. Booking returns attributable correction/erasure/retention disposition without silently voiding lawful reservation history. Account closure, sensitive appointment metadata and guest access tokens require independent scoped handling, not unrestricted profile copies. No Privacy implementation contract is asserted.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Booking consumes lawful data-purpose, disclosure, retention and data-rights constraints for registered and guest participants; Booking retains only necessary party associations and returns attributable retention/correction/erasure disposition without silently rewriting reservation obligations. No currently implemented integration contract is implied.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Define and supply data-purpose/consent, cookie, retention, rights and lawful disclosure constraints to Identity governance and commercial onboarding; keep real-world authority evidence purpose-limited and protect disputed persons. Cookie/notice publication through Publisher is not consent enforcement. Owner recovery and data export must respect third-party personal data and legal holds.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Cross-capability note — Proposed Caching derived-copy lifecycle (16 November 2026)

**Agreed conceptual boundary; implementation unverified.** [Caching](../caching/capability-record.md) consumes applicable classification, purpose, retention/erasure, legal-hold and regional restrictions through published authority boundaries and supplies scoped deletion/eviction/reconciliation status with explicit partial completion. Privacy and Legal Compliance retain policy/obligation ownership; originating capabilities retain source records and disposition facts. Cached copies, restored snapshots and provider-held derivatives must respect privacy lifecycle and residency. Unverifiable provider compliance means refuse storage, not assume consent or compliance.

**Approved conceptual boundary (16 November 2026):** Backend independence never weakens region, purpose, retention or derived-copy deletion obligations. Caching supplies qualified purge/erasure progress and failure evidence through published interfaces; policy and legal authority remain with their owners, and Caching retains ownership only of cache validity and operational state.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); not an accepted public contract. See [conceptual record](../comments_engine/capability-record.md).

Privacy provides purpose/consent/retention and data-rights constraints; Comments Engine applies scoped disclosure, anonymous/pseudonymous participation rules, authorised portable exports, minimised source/provenance, erasure/redaction and legal-hold exceptions. Public comment state, restricted reporter/evidence, personal identifiers and technical logs must remain separate; preserve evidence of partial deletion rather than claiming complete erasure.

### Comments Engine — approved CE-02/CE-05/CE-07 refinement (17 November 2026)

**Status:** Owner-approved conceptual boundary for [PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); non-normative, not a published implementation contract.

**17 November 2026 agreed Comments Engine refinement:** Private comment audiences cannot exceed parent resource permissions; no public index, federation, cache or unrestricted notices. Author editing, departure and erasure rights must normally produce actual deletion or lawful anonymisation, with restricted time-limited evidence only where an identified legitimate legal/complaint purpose requires it. Preserve independent rights of other reply authors and acknowledge downstream-copy/back-up erasure limitations without claiming more deletion than verified.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Privacy owns rights/consent and retention constraints. Configuration applies them to its own change history, authorised export/disposal and disclosure; no alternative personal Profile record may emerge. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); no claim of implementation or approval. [Conceptual interface](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Protected previews, unsaved form state, telemetry and temporary buffers require purpose limitation and prevention of unintended disclosure. No durable browser draft store presumed; Privacy determines applicable consent/retention duties.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Content Security's inspection of user-provided content must use a justified purpose, minimised ephemeral references, gated sensitive evidence and controlled retention/transfer; provider use cannot assume consent or lawful access, especially for private/E2EE material. Privacy owns consent/retention/rights constraints and Content Security implements them over its own job/evidence records; source owner handles content erasure.

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed privacy review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Course defines learning offerings, not named learner transcripts; enrolment/achievement personal records remain with Enrolment/Training. Privacy supplies effective minimisation, permitted disclosure, retention/erasure and vulnerable-learner policy. Course must protect course-admin authorship/provenance and avoid personal roster disclosure in catalogue, exports, events and logs; legal holds and historical references require explicit coordination.

## Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)

**Status: Owner-agreed boundaries, no independently completed privacy review or implemented API.** [Course](../course/capability-record.md) and [Assessment candidate](../assessment/capability-record.md): **COURSE-11 agreed:** Course preserves only purpose-appropriate curriculum/version history and limited approval metadata; personal enrolments, assessment submissions/results and achievement records stay with Enrolment, Assessment and Training. Privacy supplies minimisation, child/vulnerable-learner safeguards, effective retention/erasure restrictions and rights handling. Legal holds and necessary proof of historical qualification must be reconciled with applicable lawful basis, not used to retain all learner data indiscriminately.

## COURSE-12 — Qualification reciprocal note (18 November 2026)

**Status: Owner-approved conceptual boundary, not an implemented public contract or a completed privacy review.** [Qualification](../qualification/capability-record.md): Qualification owns minimised applicant award cases and evidence references, not raw Course/Assessment/Training learner data. Privacy supplies lawful collection, disclosure, rights, retention and safeguarding policy; Qualification enforces relevant restrictions and keeps only lawfully necessary history for award provenance.


## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)).** Privacy supplies policy for lawful basis, purpose, consent where required, minimised verifier disclosure, retention and rights; Credentials enforces policy for holder/issuer/verifier access and records status/proof disclosure without creating a public learner registry. Historical evidence and removal requests must be reconciled with statutory holds; minors and verifier correlation require explicit assessment.


## Credentials CRED-17/CRED-18 reciprocal policy and standards note (18 November 2026)

**Status: CRED-18 conceptual policy framework resolved for owner architectural sign-off (18 November 2026, PR #62); no blanket jurisdiction compliance asserted.** Privacy supplies purpose, lawful basis, permission/consent where appropriate, disclosure limits, minimisation, minor/guardian safeguards, rights and record-category retention/disposal or holds, cross-border controls, and explicit decision version/freshness to Credentials. Credentials independently enforces policy for issuance, proof presentation, verifier read, export, erasure/restriction and credential lifecycle, returning safe applied-policy receipts with historical attribution and events. Do not publish discoverable student/employee registries, collect universal consent when another basis applies, or retain immutable personal payloads forever. If mandatory policy is undetermined, hold sensitive operation. See [resolution](../../../reviews/credentials-standards-jurisdiction-resolution.md).

## Attendance ATT-11 — standards and lawful guest-data retention (18 November 2026)

**Status:** Standards applicability note proposed in Attendance PR #79 (18 November 2026); ATT-09/ATT-10 are owner-approved, but ATT-11 standards mapping is not separately approved. References are design guidance unless an accepted governing rule or applicable law already makes a control mandatory. No implementation, certification or new dependency implied.

**Apply:** [ISO/IEC 27701:2025](https://www.iso.org/standard/27701) as privacy-information-management guidance and applicable [UK GDPR / ICO storage-limitation guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-protection-principles/a-guide-to-the-data-protection-principles/storage-limitation/) as legal/privacy inputs. [ISO 15489-1:2016](https://www.iso.org/standard/62542.html) guides trustworthy retained participation records, not unlimited personal-data retention. Define distinct purposes and lawful retention/disposal for invitations, contacts, sessions, attendance, corrections, access evidence, minors' records and claims; support subject access, correction, restriction and erasure subject to lawful exceptions/holds. Privacy supplies policy and rights handling; the original owner performs its domain-specific retention action. No universally mandated retention duration or consent-for-everything rule.

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** specialist Privacy constraints on lawful purpose, consent where applicable, minimisation, data subject rights and retention are assessed and enforced by the source/disclosure workflow before exporting and at subsequent download/delivery. Stateless Export processes the already permitted/redacted safe tree without retaining source personal data; remote converter transfers need separate evaluation. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.

## Gaming handles and live plugins — reciprocal conceptual note (18 November 2026)

**Status: Owner requirement; detailed design proposed, no published adapter.** [Gaming](../gaming/capability-record.md#owner-decisions--section-2-clarified-18-november-2026) proposes public pseudonymous handles and dynamically loaded game plugins. Privacy supplies the applicable consent, minimisation, disclosure and retention constraints; Gaming enforces its own public leaderboard/handle rules. A public handle can remain personal data when linkable to an account or identifiable through gameplay history. Live plugins must receive no unrestricted Profile/Identity data, authentication tokens or other player records and must disclose permitted data uses. Child safeguards, withdrawal, handle rename and historic scoreboard visibility require explicit policy. This does not complete the Privacy review.


## Notifications reciprocal conceptual interface — 19 November 2026

**Status: proposed in [Notifications draft PR #97](https://github.com/nuxt-layers/architecture-blueprint-review/pull/97), not owner-approved or implemented.** Optional notification channel consent/opt-outs, purpose classification, retention/erasure constraints and applicable lawful grounds remain Privacy-owned evidence. Notifications enforces them at routing and before deferred sensitive sends and owns only decision snapshots; mandatory statutory exceptions require qualified Legal Compliance input. Unknown consent/grounds do not become implied permission. This bounded reciprocal note preserves the independent privacy review and creates no direct package import.
