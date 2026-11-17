# **Capability Record**

## Capability Name:

`credentials` — authoritative records and lifecycle of issued credentials, with verifiable status and issuer provenance.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

**Proposed — owner-authorised candidate creation (17 November 2026).** Not established as Available, Installed, Configured, Operational, Enabled or Authorised. This is the standard capability-record pro-forma populated with findings from the Course conceptual review, **not a completed Credentials conceptual review or an implemented public contract**.

## Purpose

Manage verifiable representations of achievements, qualifications, licences, accreditations or similar claims *only when* an authorised issuer has made the applicable underlying decision. Maintain reliable issuance, correction, replacement, expiry, suspension, revocation and verification without pretending that a certificate document or examination mark is itself an award.

A Credentials record must distinguish **the award/claim decision**, **the issued credential**, and **the credential's present verification status**. The source of each must be explicit.

## Classification

**Domain candidate**, with potential wider platform uses subject to its own future classification review. Independent status/replacement/revocation and verifier-facing lifecycle justify a candidate distinct from Assessment. No repository/package, implementation technology or deployment choice is approved by this creation.

## Dependencies

**Conceptual cooperation only; actual public contracts and package edges are deferred.**

- [Course](../course/capability-record.md) owns versioned curriculum, intended learning outcomes, completion requirements and provenance-marked external accreditation references. It does **not** issue awards.
- [Assessment](../assessment/capability-record.md) owns instruments, attempts, marking, assessed results, moderation and appeals. A pass or mark is not an issued credential or a qualification award.
- [Training](../training/capability-record.md) owns verified participation, competencies and course completion evidence. Completion alone does not automatically confer an externally recognised qualification.
- External **accrediting/recognition authority** owns its actual accreditation decisions and applicable conditions; the **authorised awarding body** (or demonstrably delegated awarding institution acting within its mandate) owns the formal **individual award decision**. A future separate qualification/award-decision authority inside the platform may be justified. Credentials must **not silently acquire legal awarding powers** by recording a credential.
- [Integrations](../integrations/capability-record.md) handles provider-specific authoritative registries, issuer APIs, signed verification, remote award responses, callbacks and synchronisation. The provider remains authoritative for its own evidence.
- Identity, Authentication, Authorisation, Profile, Privacy, Legal Compliance and optional Verification: subject/issuer identity, trusted representation, access and assurance, disclosure, effective delegation/qualification restrictions, retention and legal constraints. IAM platform permissions **do not** create external accreditor or statutory awarding authority.
- Publisher/Storage/Media may render or store certificate files but do not certify the underlying award; Audit/Logging/Reporting/Notifications and Clock participate through bounded public contracts.

All actual dependencies must be declared, directional and acyclic; cross-capability collaboration is not permission to import private schema or share another capability's master record.

## Optional integrations

Issuer/awarding-board registers; professional and education accreditation authorities; credential status/revocation lists and verification networks; digitally signed verifiable credentials; third-party registries and certificate delivery services, via approved provider-neutral adapters. Support a **native mode for legitimate internally issued credentials** under appropriate authorised policy. Externally recognised credentials require independent, correctly scoped evidence and authority.

## Version

**No release/version established.** Proposed stable credential ID and revision, immutable underlying award/claim reference, issuer and subject identifiers, claim type, issued/effective/expiry timestamps, verification/provenance timestamps, signature or evidence reference, supersession/replacement chain, status history and schema/format version.

## Availability

Credential issue/view/verify/export/revoke permissions differ. A subject may view only their authorised records; an external verifier may receive **minimum permitted proof and live status**, not the learner dossier. Unknown/stale/outage status must not appear as “valid”. Capability availability and issuer authority are separate concepts.

## Capabilities offered

**Initial proposed responsibility and lifecycle:**
1. **Register trusted issuer context:** distinguish original awarding authority and delegated issuer, verify organisation identity and award scope, explicit delegation evidence, effective interval, restrictions and revocation. Check current mandate status for any issuance that depends upon it; do not treat a role assignment as external permission to award.
2. **Issue:** consume an authoritative, verified award/claim decision with provenance, effective dates, claimant/subject matching, status and permitted disclosure. Produce an attributable credential record and optional signed/portable representation only if issuance is authorised. Merely passing an assessment does not trigger an award.
3. **Verify:** provide scoped validity/status for a supplied credential reference or permitted proof, distinguishing genuine issued status, source award validity, expiry, supersession, suspension, revocation, unknown and stale source status.
4. **Correct or replace:** preserve original version and correction reasons, revoke/supersede old public proofs where necessary, and explicitly link replacement; never silently edit an issued historical credential.
5. **Suspend/revoke/expire:** process authenticated decisions from authoritative issuer/award authority, enforce local lifecycle restrictions and publish safe status changes; never confuse a provider outage with a revocation.
6. **Export/present:** provide portable representations and human-readable certificates via separate presentation/document ports, with least-privilege disclosure, provenance and verifiability. A rendered PDF alone is not proof of a valid award.
7. **Reconcile:** handle remote provider updates, delegated mandate withdrawal, signed status proofs, retries, idempotency and conflicting evidence. Fail closed for new externally recognised issuance when mandatory issuer verification is unknown.

### Idealised input/output notes — to be completed at dedicated review

| Inbound interface (source) | Required meaning and authority |
|---|---|
| Authoritative award/claim decision (external awarding body or verified delegate; potentially a future qualification/awards capability) | Award reference, qualification/claim type, subject, issuer, qualification scope, original decision, validity/effective dates, assurance, revision and source. **Not a raw Assessment mark.** |
| Verified learning/assessment evidence (Training, Assessment) | Versioned completion and result references where necessary to check the specific award requirements; these remain owned by their source capabilities and do not themselves authorise awarding. |
| Issuer/delegation evidence (authority registry/Integrations/Verification and legal policy) | Identity, permitted action/scope, legitimacy, effective period, status, limits and provenance. Unknown required evidence blocks recognised issuance. |
| Issue/replace/suspend/revoke command (authorised principal or trusted issuer) | Explicit issuer authority, trusted caller, expected revision, reason/effective time, unique idempotency/correlation key and applicable release/legal rules. |
| Presentation/status request (subject/verifier) | Consent/authorised purpose or other lawful disclosure basis, permitted proof scope, source reference and verification freshness. |

| Outbound interface (authorised consumers) | Guarantee and limits |
|---|---|
| Credential record/portable representation (subject, permitted issuer/recipient) | Credential ID, stable source award reference, subject, issuer/delegate provenance, claim, validity/effective dates, version, evidence/signature references and status; no promise of separate statutory recognition. |
| Verification status/proof (permitted verifier) | Explicit status and as-of time, signature/issuer/source validity where checked, unknown/stale indicators, minimum disclosed claims; verification outcome must not manufacture original awarding authority. |
| Status/correction/replacement history (authorised subject/issuer/auditor) | Attributable lifecycle decisions and immutable chain of corrections; actual underlying qualification award stays with its authority. |
| Committed domain events (authorised subscribers) | Issued, Replaced, Corrected, Expired, Suspended, Revoked, VerificationStatusChanged, with safe provenance and tenant/subject minimisation. At-least-once delivery, replay and idempotency; no exactly-once promise. |

**Conceptual service shape:** commands for issuance and lifecycle, queries for authorised records/status, and durable committed events; stable domain errors, version preconditions, verified-at timestamps, tenant isolation and disclosure restrictions. Exact structures/ports and acceptances are deferred.

## Configuration

Possible issuer registry/provider choice, accepted credential types/formats, internal award restrictions, trust roots and validation methods, revocation-status freshness policy, allowed proof disclosures, verification access, retention, replacement rules, localisation and integration keys supplied through authorised host secret management. No configuration setting, template or user role can manufacture accreditation or an external legal mandate.

## Findings carried from the Course conceptual review (17 November 2026)

**CRED-01 — Owner-approved creation and three-way assessment boundary.** The owner authorised creating a separate `credentials` capability record, after approving Course / Assessment / Training responsibility separation (COURSE-08). Credentials is **not** part of Assessment. Its precise internal contract is proposed, not yet separately reviewed or approved.

**CRED-02 — Distinct authorities (COURSE-10 principle agreed).** External course accreditation, learner assessment/achievement and individual qualification awards are different facts. Course keeps recognition references; Assessment owns examination results; Training owns completion. An external awarding body, or delegate with demonstrable and appropriately scoped authority, remains the award decision-maker. Credentials manages the representation and status of that decision rather than asserting that it can create the award.

**CRED-03 — Delegation and external authorities (proposed design).** Keep an explicit, verifiable issuer/authority identifier, accreditor/qualification scope, issuer-delegate chain, effective dates, revocation, geographic/organisation restrictions and authoritative provenance. Source verification must distinguish identity, legal/accreditation standing and platform authorisation. External evidence may be out of date or disputed; report uncertainty and never silently replace a source authority.

**CRED-04 — Credential state (proposed design).** Issue, verify, reissue/replace, correct, expire, suspend and revoke with durable audit and safe status propagation; retain source references and lawful history. The provenance and meaning of a historical award must not automatically change because a course's later accreditation expires; verify individual award-specific rules. Correcting a credential is distinct from regrading the assessment or overturning the award itself.

**CRED-05 — Presentation and disclosure (proposed design).** A credential may have a certificate viewer/download and verifier view, but a Publisher PDF/document is an output, not the authoritative decision. Verify minimum claims with explicit authorisation/privacy; avoid publicly enumerable learner qualification histories. Accessibility, i18n, responsive GUI, Theme Manager and optional headless operation are future review requirements.

**CRED-06 — Safeguarding and governance (proposed design).** Explicitly handle child/vulnerable-person data, personal identity matching, retention/erasure versus lawful evidential preservation, appeals, fraud, issuer compromise, replay, historical corrections and external connector outage. Audit accepts evidence; Legal Compliance determines applicable statutory constraints.

**Open issues for the independent Credentials review:** Does this capability also own *internal award decisions*, or should qualification/awarding be a separate authority? What qualifies an issuer/delegate and how is mandate status maintained? Which credential formats and trust frameworks are justified? How are learner consent and public verification balanced? What are reissue/revocation semantics when the awarding body is external? Can the credential survive offline verification? Which validity/retention regimes apply? No premature answer is imposed.

**Conceptual GUI:** credential/issuer dashboard, evidence and issuer-status inspection, issuance and replacement queues, revocation/appeal administration, subject wallet/view and privacy-scoped verifier portal, with headless interfaces. These are design targets, not implemented screens.

**Acceptance examples (proposed):** valid authorised external award and live issuer mandate → issue traceable credential; raw exam pass only → reject qualification issuance; missing/expired delegation → block recognition claim; issuer status service down → return unknown/stale rather than valid; authorised revocation → update status and publish safe event; cross-tenant verifier request → deny/minimise; correction → preserve original and replacement chain.

**Record status:** Pro-forma created for later full conceptual review. Do not change normative catalogue classification or assert implementation/approval based solely on this candidate file.
