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

## Review notes — Accounting frameworks, taxation and regulatory constraints (14 November 2026)

**Status: Provisional conceptual note, not a completed Legal Compliance specification.** The governing Capability Catalogue assigns legal obligations, jurisdictional constraints and legal holds to `legal-compliance`; it expressly consolidates the former `policy-map` concept into `legal-compliance`. A root `CONTRACT.md` was not retrievable in this review, so no implemented ports are asserted.

- **Established boundary:** Legal Compliance does not own Accounting's journals or tax calculation results. It records or resolves applicable legal duties, effective-date constraints, restrictions, holds and compliance evidence for the relevant entity and activity; the actual jurisdictional rule set and determinations require qualified validation.
- **Proposed interaction:** Provide the governing obligation/restriction context for Accounting's [framework, effective-policy, tax and regulatory interfaces](../accounting/capability-record.md). Distinguish mandatory law, permitted accounting election, tenant configuration and unresolved legal uncertainty; an organisation's assertion is not automatically proof of legal validity.
- **Enforcement:** Accounting validates its own ledger invariants and applies authorised financial rules; mandatory legal refusal or unavailable necessary compliance evidence should not be silently bypassed. Legal Compliance does not directly mutate Accounting's records or substitute for Authorisation.
- **Government portals:** Accounting prepares authoritative reconciled returns and retains filing evidence. Integrations handles authenticated transmission and acknowledgement. Legal Compliance records duties and constraints, not credentials, submission transport or financial balances.
- **Open:** how is applicability determined for multi-jurisdiction entities, changes in law, tax elections, cross-border activity, effective dates, evidential review, legal holds, filing deadlines and statutory retention? Define minimal public compliance decision port before deciding any package dependency.

### Cross-capability relationships and evidence status

- **Governing evidence:** `architecture-rules/docs/catalogue.md` names Legal Compliance's obligation/constraint boundary and aliases `policy-map` to it; root implementation contract not verified.
- **Proposed relationships:** [Accounting](../accounting/capability-record.md), [Configuration](../configuration/capability-record.md), [Integrations](../integrations/capability-record.md), [Invoice](../invoice/capability-record.md).
- **Next review gate:** At the alphabetical review, inspect its repository and published root `CONTRACT.md` (if present), refine these boundaries and only then assess published service edges.

### Cross-capability note — Authentication legal restrictions (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns credentials, sessions and authentication security records; Legal Compliance owns the applicability and meaning of legal requirements and holds. **Agreed conceptual direction (AUT-11):** a valid legal hold restricts disposal only of records it covers, with attributable access, review and release; neither routine account closure nor a generic retention option silently overrides mandatory obligations. **Open:** jurisdiction-specific obligations, lawful basis, hold authority, scope and confirmed provider deletion. This does not complete Legal Compliance's separate review.

## Cross-capability note — Billing tax and statutory constraints (15 November 2026)

**Proposed reciprocal interface, not a completed Legal Compliance review or tax determination engine.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) needs applicable jurisdiction, legal-entity, tax-treatment/point, preservation, mandatory communication and permitted disclosure constraints for supported charge scenarios. Legal Compliance supplies governed legal obligations/constraints or validated references, **not** automatically tax calculations; statutory tax-decision ownership requires later explicit allocation and qualified jurisdictional validation. Billing exposes charge decision/version and required factual context to authorised consumers; Invoice owns legal documents and Accounting tax posting/returns. Missing mandatory legal/tax evidence holds relevant finalisation/handoff; no permissive default or regulatory conformity is claimed.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Supply qualified applicable duties, restrictions, holds, source/jurisdiction/activity/effective-time provenance and unresolved verification states for tenant governance, controller disputes, purchases, subscription cancellation, privacy and statutory disclosures. Do not assume a director's title proves authority or that published Modern Slavery, privacy or safety statements guarantee compliance. Specialist company/counterparty authority ownership remains open. The obligation and statement document have distinct lifecycles.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Online Safety Act applicability:** Qualify UK OSA 2023 duties by actual regulated service category (user-to-user/search/combined as applicable), audience, risk, jurisdiction and effective-date Ofcom requirements; distinguish priority offences, other illegality, lawful harms, child-specific duties and service policies. Supply validated reporting/retention/disclosure constraints, statutory notices and uncertainty with qualified legal provenance. Do not assert installing Content Security/Moderation automatically achieves compliance, and do not equate closed groups with statutory exemption or E2EE with unqualified regulatory immunity. The source owner enforces operational restrictions.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Legal Compliance qualifies applicable UK OSA and other jurisdiction/service-specific age assurance, identity, seller verification, parental/child safeguards and statutory evidential/reporting obligations, with source/effective-date provenance. It must distinguish age threshold from personal identity and establish when highly effective age assurance is actually required. This does not certify any particular provider, ZKP technique or deployment as legally compliant.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Verification may accept lawful national schemes (China national internet ID, Russian digital IDs, Saudi Nafath/Absher) via provider-neutral adapters, but Legal Compliance alone qualifies service-specific national real-name, age, KYB, localisation and privacy requirements and effective dates. Credential integrity is not legal compliance or proof that a Hetzner-hosted Node can lawfully operate in every country.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); not an accepted public contract. See [conceptual record](../comments_engine/capability-record.md).

Legal Compliance qualifies site/service/jurisdiction-specific participation, harmful-content obligations, age/child safeguards, retention and legal holds with effective dates and provenance. Comments Engine enforces qualified constraints for comment submission, visibility, removal and erasure, returning completion/exception receipts; it cannot claim Online Safety Act compliance merely through scanning, nor independently interpret a statutory reporting duty.

### Comments Engine — approved CE-02/CE-05/CE-07 refinement (17 November 2026)

**Status:** Owner-approved conceptual boundary for [PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); non-normative, not a published implementation contract.

**17 November 2026 CE-02/CE-05/CE-07 agreed refinement:** Comments Engine applies qualified OSA and privacy/retention duties based on actual service, audience and risk, without blanket adult verification. Privately addressed comments are not automatically OSA-exempt; a genuinely internal business service may qualify under Schedule 1 paragraph 7 subject to full conditions. Author erasure is default, with time-limited narrowly justified complaint, legal-hold or claims evidence; Legal Compliance owns the applicability/retention qualifications, not source comment deletion.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Legal Compliance supplies jurisdiction/time-qualified mandatory constraints and holds. Configuration may store bounded approved choices but cannot independently interpret legal requirements or treat unknown obligations as permissive. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Content Security consumes qualified jurisdiction/service classification, retention/transfer constraints and applicable duties, not generic assumed UK OSA universality. It produces detector evidence and uncertainty, not statutory judgments. Legal Compliance supplies scoped requirements and holds; domain owners independently enforce publication/removal and Moderation manages review cases.

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed legal_compliance review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Legal Compliance determines applicable education/children's protection, data protection, accessibility, licensing, retention, accreditation and hold constraints per jurisdiction/effective date. Course enforces publication, import/export and withdrawal gates but does not certify legal validity, accredited course standing or learner qualifications. Unknown mandatory legal restrictions block relevant actions rather than defaulting to approval.

## Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)

**Status: Owner-agreed boundaries, no independently completed legal_compliance review or implemented API.** [Course](../course/capability-record.md) and [Assessment candidate](../assessment/capability-record.md): **COURSE-10 agreed principle:** Legal Compliance qualifies jurisdiction-specific recognition, licensed award authority, authorised delegation, validity windows, provenance and mandatory restrictions. An organisation's platform role or an Integrations claim is not external power to grant a qualification. **COURSE-11 agreed:** safeguard minors/vulnerable learners, review/publication controls, retention, holds, credit recognition and version migration must meet applicable effective law and organisational policy. Do not assert a universal statutory retention schedule or automatic accreditation.

## COURSE-12 — Qualification authority reciprocal note (18 November 2026)

**Status: Owner-approved conceptual responsibility; detailed Qualification review and implementation pending.** [Qualification candidate](../qualification/capability-record.md): **COURSE-12 owner-approved:** Legal Compliance supplies applicable jurisdiction/qualification/accreditation, safeguarding, data rights, retention and withdrawal requirements; Qualification owns application of qualification scheme, issuer delegation, evidence and award lifecycle rules. An accreditor remains authority for actual recognition and an external awarding organisation for its own award decisions; do not hard-code universal legal validity or retention periods. No change to previously approved legal_compliance ownership.


## Credentials CRED-17/CRED-18 reciprocal policy and standards note (18 November 2026)

**Status: CRED-18 conceptual policy framework resolved for owner architectural sign-off (18 November 2026, PR #62); no country-law compliance asserted.** Legal Compliance supplies an authoritative dated applicability decision by issuer/tenant, claim/scheme, jurisdiction(s), regulated activity, audience, effective time and source authority; plus binding disclosure/recognition, guardian, retention, appeals, transfers and policy conflict rules. Credentials enforces the decision for issue/verify/revoke/replace/rights action, publishes qualified applied-policy outcome and accurate historical/current status; absence, conflict or stale mandatory rule holds affected action, not permissive default. Legal Compliance owns legal interpretation and per-jurisdiction policy maintenance; Credentials never overrides statutory floors. Specific UK/EU or other legal schedules require legal evidence and review before regulated deployment. See [resolution](../../../reviews/credentials-standards-jurisdiction-resolution.md).

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** Legal Compliance supplies qualified jurisdiction/activity/effective-time disclosure, preservation, data-transfer and accessibility obligations to the authoritative domain/Reporting export workflow; uncertainty in mandatory conditions holds unsafe disclosure. Export renders formats without claiming legal, PDF/UA or archival conformity. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Legal Compliance determines applicable obligations and restrictions; Integrations enforces supplied constraints for external transfers, processor/residency rules, regulator/government portal submissions and retention. Authenticated transport/acknowledgement is not regulatory acceptance, and missing mandatory jurisdictional permission fails closed. Qualification of lawful basis, provider certification and high-risk approval remains a specialist/owner decision (INT-09). See [Integrations conceptual contract](../integrations/capability-record.md#configuration-legal-security-and-privacy), PR #76, proposed only.


## Reciprocal conceptual interface — Membership (19 November 2026; draft PR #93)

**Status: proposed, not owner-approved or implemented; this does not complete the legal_compliance review.** [Membership](../membership/capability-record.md) is a candidate *scheme participation* domain distinct from Identity group membership, Subscription plan entitlements, commercial settlement and application access. Legal Compliance qualifies applicable cancellation, refund, age/qualification, retention, disclosure and hold duties, with jurisdiction and effective time; Membership applies those restrictions to its own scheme lifecycle. No generic programme rule can override mandatory law. Consume only published public interfaces; no direct package dependency is inferred. Missing, stale, contradictory or unauthorised evidence must not be promoted into confirmed outcomes.
