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

## COURSE-12 — Qualification authority reciprocal note (18 November 2026)

**Status: Owner-approved conceptual responsibility; detailed Qualification review and implementation pending.** [Qualification candidate](../qualification/capability-record.md): **COURSE-12 owner-approved:** Qualification owns qualification specifications, authoritative individual award decisions and award status, including references to externally authoritative awards. Credentials independently owns issuer-backed credential creation/representation, proofs, issue, verification, reissue, suspension, replacement and revocation. Consume Qualification decisions by provenance-rich public contract, maintain separate status, and reconcile invalidation/appeals; a credential document never grants awarding power. Generic non-qualification Credentials retain their own domain-source authorities. No change to previously approved credentials ownership.


## Dedicated conceptual review — Credentials (18 November 2026; PR #62)

**Status:** Detailed **proposed** conceptual contract for owner approval. CRED-01 (creation) and COURSE-12 (Qualification division) are owner-approved; the CRED-07 onwards choices below are not automatically accepted. This adds no runtime or new repository. No `nuxt-layers/credentials` implementation repository was found in the organisation search at opening; consequently there is no verified root `CONTRACT.md` and all described operations are idealised, not published APIs.

### Independent responsibility and authority

**Classification proposal:** Domain. Credentials owns the issuance transaction, issued credential registry, representation metadata, cryptographic proof and status references, verification policy and credential-local amendments, invalidation, expiry, suspension, revocation, reissue and replacement chain. This is a real independent lifecycle even if no certificate/PDF is generated. Default modular-monolith deployment; independently usable headless core and optional Nuxt screens. It is not the same thing as Authentication's sign-in credentials.

**Source-of-truth split:** Qualification owns formal qualification schemes, individual awards, appeals and award-status changes; the actual external awarding authority owns externally decided awards. Other authoritative claim domains (for example professional licence, employer attestation or membership) must be specifically named and supply their own valid domain decision. Credentials must not become a generic adjudicator of every claim; no credential may be created solely from a raw grade, attendance log, user declaration, IAM grant or Publisher document. Verification owns independent trust evaluation of *presented* third-party claims; Credentials owns local issuance registry and primary status of credentials it issued. Verification can verify a Credentials proof via its published status/trust surface without taking over issuance or producing circular imports.

**Issuer versus authority:** Distinguish (1) claim-decision authority, (2) party authorised to issue the representation, (3) technical signing/key operator, (4) subject/holder, (5) permitted verifier. Delegated issue rights never imply delegated award rights. Issuer mandate, identity, authorised claim scope, effective dates, jurisdiction and delegated restrictions must be checked with trusted source(s); a role or connected provider account is insufficient. An unverified external source is neither approved nor revoked merely because it is offline.

**Minimal native mode:** Support a legitimately self-issued non-regulated claim only when a separately authorised owning domain has made the underlying claim decision. An independently valid Qualification decision (local or external) can support a qualification credential. Without an available, verified source decision and effective issuing authority, issuance must be refused or held with no public credential. Neither an external provider nor a printable document is mandatory for supported native records; proof signing/verification and status semantics remain mandatory when a representation claims cryptographic verifiability.

### Authoritative information and state

Stable credential ID, tenant and issuing-organisation scope, source decision ID/type/revision and authority, subject binding, issuer/delegate mandate and provenance, claim type, allowed disclosure, evidence digest/reference (not copied dossiers), representation profile/version, issue and effective times, expiration rules, key/proof references, issuer-controlled credential status and status-as-of time, source-award status observation and freshness, replacement/correction links, suspension/revocation reasons where disclosable, audit/correlation and immutable history. Credential source references survive correction; substantive source-decision changes require renewed source validation.

**Separate status dimensions:** (a) issuance processing: requested / held / refused / issued / delivery pending / delivered / delivery failed; (b) issued credential: active / suspended / expired / revoked / superseded; (c) source decision: confirmed / suspended / overturned / withdrawn / unknown / stale / disputed; (d) cryptographic verification: proven / failed / unsupported / unavailable / stale. None may be collapsed into one boolean `valid`. A correction that does not alter substantive claim still creates a traceable revision/replacement as appropriate. Revocation is never overwritten by replay of an old issue event. Expiry is derived from effective policy and time, with durable change/notification when needed. Cancellation before issue is not revocation. Delivery failure does not negate a successfully issued credential.

**Independent authority and reconciliation:** A source award withdrawal requires timely local credential hold/invalidation according to governing policy and verified source event; it is not a second award decision. Out-of-order and uncertain external evidence enters an explicit reconciliation state, preserving the last known authoritative observation. A compromised issuer key requires security containment, affected-credential identification, status update and safe reissuance without retroactively claiming that past signed data was never signed. Historical verification must distinguish validity *at issuance* from current status and from validity at a stated historical date.

### Idealised inbound public contract

| Input/source | Needed facts or commands; authority and validation | Requirement; absence/uncertainty |
|---|---|---|
| Qualification or other explicitly approved domain authority | Signed or independently authenticated award/claim decision reference, subject, claim, source revision, issuer, scope, effective status, decision finality and evidence provenance | Required to issue; missing, appealed, conflicting, revoked or stale essential authority => hold/reject, never infer award |
| Issuer governance / trusted external authority via Verification or Integrations | Legal/organisation issuer identity, issuing mandate, award/claim scope, delegation chain, effective period, key authority and bounded status freshness | Conditional for recognised/external schemes; unknown mandate blocks issuance; outage is not revocation |
| Caller/Identity/Authentication/Authorisation | Trusted tenant, subject, issuing organisation, assurance, server-side permission for issue/replace/revoke/view/verify and resource ownership | Required for protected actions; missing/denied/ambiguous => fail closed; distinct from professional awarding power |
| Requesting subject, authorised issuer or domain event | Issue, correct, reissue, suspend, resume, revoke, export and presentation requests; credential/source reference, expected revision, intended audience, purpose, reason, correlation and idempotency | Validate command actor, proof freshness, state, transition, policy, replay and concurrency; an event is not permission |
| Privacy, Legal Compliance, Configuration and Clock | Effective lawful disclosure, retention/hold rules, required representation profiles, source/issuer trust policy, date/time and localisation settings | Mandatory applicable floors fail closed; optional format/presentation omission degrades without widening access |
| Integrations / external signer or status registry / Storage / Publisher | Provider-specific proof, status acknowledgement, file output or document lifecycle receipts through published ports | Conditional; timeouts => pending/unavailable and idempotent recovery, no fabricated committed success |
| Holder or external verifier | Presented credential ID/proof, challenge/audience, proof of legitimate purpose or permitted disclosure path and freshness requirement | Reject enumeration and unauthorised data; missing verification infrastructure => indeterminate, not valid |

### Idealised outbound public contract

| Output | Consumers; guarantee and limits |
|---|---|
| Accepted operation receipt | Issuer/subject/workflow: accepted vs completed, stable operation and credential IDs, revision and explicit hold/failure; an accepted queue item is not an issued certificate |
| Authoritative issued credential summary | Subject/issuer and permitted partners: immutable source decision reference, issuer identity and mandate provenance, claim, issuance/revision, representation/profile, dates, status and source-observation freshness; source decision remains externally owned |
| Signed/portable representation and secure delivery reference | Holder or chosen recipient: explicitly profiled proof and claim disclosure, signature/key and status-check method; interoperability depends on the selected profile, not PDF rendering |
| Scoped verification response | Authorised verifier or independently public minimum-status route: authenticity/integrity, issuer trust, subject/audience binding, current credential status, source-status qualification, expiry, checked-at and freshness, indeterminate/unsupported reasons; never raw learner dossier |
| Credential history, correction chain and authorised export | Subject/issuer/compliance reviewers: attributable status transitions, replacement linkage, limited evidence, lawful retention and disclosure; no silent rewriting |
| Durable committed domain events | Authorised consumers: CredentialIssued, IssueHeld, CredentialReplaced, CredentialSuspended, CredentialResumed, CredentialRevoked, CredentialExpired, CredentialSourceStatusReconciled and CredentialProofCompromised (event vocabulary proposed); event contains minimum scope, references, revision and effective time, no raw PII by default |
| Delivery/verification diagnostics | Audit accepts accountable evidence; Logging/Observability technical diagnostics; Reporting aggregates privacy-safe counts; Notifications sends user-facing notices without owning status |

**Command behaviour:** Validate server-side scope/assurance, source decision, mandate, policy and expected revision; persist credential-local transition and durable outbox atomically; return stable domain errors and idempotent receipts. Do not send a publicly usable proof before committed issuance. Enforce uniqueness of issuance intent against the same source decision/profile/subject where policy requires, while allowing legitimate distinct issuer/credential types. Replays return attributable prior outcome. External delivery/signing must recover by operation key and reconcile duplicate callbacks; distributed exactly-once guarantees are not claimed.

**Queries:** Authorised get/list/history, current proof status, issuer/subject overview and limited verifier lookup; all distinguish current, last-checked, unknown and source-derived information. No searchable public directory of people or credentials. Offline proofs can establish signature/integrity within the selected profile, but cannot claim fresh revocation or source status without an appropriately recent trust/status artifact; show `status not checked` or equivalent.

**Events:** Only after committed owner changes from capability-owned durable outbox (ADR-0012); transport/Message Queue conveys events, not business authority. Consumer replay, reordering and retry are assumed. Changes in Qualification are consumed through a documented one-way source-decision port or event with source revalidation rather than creating a Qualification → Credentials → Qualification package cycle.

**Shared interaction context:** Tenant and issuer ownership; trustworthy caller/assurance; action-specific access and domain authority; source decision and revision; expected credential revision; request ID/idempotency and correlation; policy/profile version; effective time and authoritative Clock; source provenance, freshness, data-purpose and permitted audience. No mandated universal request object.

### Relationships, guarantees and recovery

| Neighbour | Credentials receives | Credentials supplies and boundary |
|---|---|---|
| Qualification | Formal award decision, current award lifecycle and authority reference | Credential issue/status receipts and invalidation reconciliation; never decide awards or mandate Qualification to import Credentials |
| Assessment / Training / Course / Enrolment | Indirect, scoped source references only when necessary to substantiate claim; Qualification mediates formal award eligibility | Credential reference/status for permitted users; no qualification on grades/completion alone |
| Verification | Independently scoped issuer/representation trust, holder/issuer proof checks as required | Locally issued proof, status and signing metadata via a public verification surface; avoid bidirectional static package imports |
| Identity / Authentication / Authorisation | Subject/issuer refs, authenticated caller, resource permission and assurance | Protected credential-resource identifiers, privacy-safe lifecycle events; no local identity or sign-in credentials |
| Legal Compliance / Privacy / Configuration / Clock | Jurisdictional rules, data rights, effective configuration, authoritative time | Evidence of enforcement, minimised source/status references and temporal decision record |
| Integrations | Provider-neutral remote registry/signing/status operation results | Explicit idempotent intents, provenance and reconciliation needs; provider outage not a revocation |
| Publisher / Storage / Export | Document rendering or file custody through owned public ports, where selected | Approved content/credential view model and lifecycle triggers; document is not credential authority |
| Workflow / Scheduler / Message Queue | Optional approval orchestration, due-task execution, outbox relay | Authoritative action completion receipts and owned committed events; no transfer of decisions |
| Audit / Logging / Observability / Reporting / Notifications | Purpose-limited ports and policies | Auditable actions, diagnostics, metrics and notification triggers; no independent status masters |
| Federation | Remote transport/presentation as configured | Proof and bounded verification response; remote Hub trust does not create local legal standing |

**Failure invariants:** source decision unavailable => no new recognised credential; mandatory mandate unknown => no issue; revoked source => block/hold and reconcile affected credentials; verification provider down => explicit indeterminate; rendering/email failure => issuance status unchanged, delivery retry; audit/outbox persistence failure for security-sensitive action => atomic rejection where mandatory; issuer compromise => quarantine/suspend affected credentials with restricted issuer actions; GDPR erasure and legal holds reconciled per purpose, not a blanket promise of deletion.

### Security, legal, presentation and privacy

Apply OWASP ASVS 5 L2 minimum and L3 controls where warranted by high-impact issuance/revocation; step-up assurance and separation of duties for materially consequential status changes. Threats: fabricated decisions, stolen signing keys, malicious issuer/delegate, forged signed PDFs, replay, status-oracle enumeration, cross-tenant disclosure, holder impersonation, false revocation, source compromise, unavailable external registry, key rotation, coerced proof disclosure and verifier tracking. Key/secrets custody is host/infrastructure governed; Credentials enforces issuance/key-use policy and maintains attribution and rotation/invalidation semantics. Minimise sensitive attributes; purpose/consent or other lawful basis, lawful retention and legal holds must be resolved by Privacy/Legal Compliance; minors need enhanced disclosure control. Cryptographic validity ≠ legal accreditation ≠ award decision ≠ current claim truth. Profile selection (e.g. W3C VC 2.0 / supported OpenID profiles) is a later interoperability decision, not a universal protocol commitment.

**GUI proposal:** optional Credentials dashboard linked from host sidebar; issuer/mandate status with warnings; authorised issuance queue, held/error/reconciliation cases, reviewable source-decision and consent context; separate replacement/suspension/revocation with reason, assurance and confirmation; subject credential wallet/details/download/status; privacy-minimised verifier entry and result with as-of/unknown; history, fraud/key incidents and operator diagnostics. A qualification appeal button routes to Qualification rather than editing underlying award. Host owns navigation; Publisher/Export owns generated documents; Theme Manager styles optional screens. WCAG 2.2 AA, semantic HTML, keyboard/screen-reader accessible status and error labels, responsive layouts, BCP 47/i18n and timezone-aware effective dates. A fully headless mode retains every operation, permission and error invariant.

### Conceptual acceptance — input → expected behaviour → owner

1. Confirmed qualification award, matching subject, live issuer mandate and authorised issue command → one committed credential and proof/status reference → Credentials; Qualification remains award owner.
2. Raw Assessment mark, attendance or course completion → no qualification credential; identify missing authoritative decision → Qualification/Assessment/Training remain sources.
3. Independent legitimate non-qualification domain claim and explicit issue mandate → native credential without mandatory third-party provider → Credentials, not generic awarding.
4. Expired/revoked delegate or unknown mandatory authority => issue held/refused, not public; issuer governance source remains authoritative.
5. Same issue operation replayed after retry => same recorded result, no duplicate usable credential; Credentials.
6. Cross-tenant credential query or enumeration => denied/minimised regardless of valid cryptographic proof; Credentials and Authorisation.
7. Award rescinded/appealed => source remains authoritative, affected credential state held/updated with attributable reconciliation; Credentials may not overturn award.
8. Replace misspelt certificate name => revision and supersession chain; past proof status preserved and old portable artifact not silently valid forever.
9. External signer/status provider outage => pending issue or indeterminate verification; no false issue/valid result; Credentials.
10. Signed proof verified offline without fresh status => authenticity may pass but current status remains unknown; Verification/credential status source.
11. Key compromise => affected credentials quarantined/reissued on trusted mandate; bounded, audited restoration; Credentials.
12. Delivery failure after committed issuance => delivery retry, credential remains issued; Publisher/Notifications only deliver.
13. Valid historical award but current recognition withdrawn => historical decision and current credential state separately adjudicated under effective policy, not retroactively rewritten.
14. Accessibility, localisation and headless consumer => same permissions, statuses and public contract without hidden screen-only functionality.

### Decision register and independent challenge

- **CRED-01 — agreed:** Candidate creation from Course review.
- **CRED-02 / COURSE-12 — agreed:** Qualification owns qualification decisions and recognition/delegation lifecycle; Credentials owns credential representations and independent status; non-qualification claims remain source-owned.
- **CRED-03–06 — previously proposed, not approved as detailed design.** Retained from original pro-forma; expanded by this review.
- **CRED-07 — proposal:** Domain classification with independent registry and status lifecycle; no new service/repository required.
- **CRED-08 — proposal:** Credential issue permission and qualification awarding authority are separate, validated at issuance and relevant status transitions.
- **CRED-09 — proposal:** Separate issuance, credential, source-decision and proof-verification states, with explicit stale/unknown and history.
- **CRED-10 — proposal:** Mandatory source-decision handoff for recognised claims; optional native self-issued non-qualification claims require their own source authority.
- **CRED-11 — proposal:** Risk-based proof-profile interoperability with portable/offline checks qualified by status freshness, no mandatory single technology.
- **CRED-12 — proposal:** Minimise public verifier response; lawful access basis and policy govern personal disclosure; no public enumeration.
- **CRED-13 — proposal:** Publisher/Export only format artifacts; Verification handles independent presented-proof assessments; prevent duplicate trust/status master.
- **CRED-14 — proposal:** Source award appeal/withdrawal and credential revoke/supersede are separate, reconciled transitions; cannot assume distributed atomicity.
- **CRED-15 — proposal:** Credential GUI optional; headless core mandatory.
- **CRED-16 — open owner choice:** Who authorises an issuer to generate a *non-qualification* claim when the claiming domain has no explicit approval/decision contract? Default: refuse until a documented source authority exists; do not invent generic awarding.
- **CRED-17 — open design choice:** Which interoperable proof/status profiles must be initially supported for the intended external consumers, and are issuer privacy-preserving verification methods a first-release requirement? Defer concrete profile choice to implementation design with compatibility test plan.
- **CRED-18 — open legal/policy review:** Jurisdiction-specific disclosures, minor safeguards, retention, post-revocation historical proof and offline freshness bounds; require mapped legal decisions, not an invented uniform law.

**Independent architectural challenge:** This boundary is justified only if Credentials is the *issuer and credential-status owner*, not another claim evaluation capability. Reusable signature/formatting utilities do not by themselves merit a domain, nor should Certificates, Awards or Wallets become redundant capabilities. Risks needing later architectural evidence: circular Verification trust/status imports, split authority for invalidation when remote registry remains primary, race between award correction and portable proof availability, issuer signing-key custody, bearer-verifier privacy and cross-node trust. Adopt a one-way provider-neutral port rather than mutual static dependencies; state remote registry authority separately per credential. A downstream consumer integrates through only these declared semantics, not private tables.

**Approval and delivery status:** Conceptual review drafted; CRED-07–18 not owner-approved. No implementation, contract release, external certification, legal sign-off or CI acceptance claimed. Before approval reconcile concurrent PRs, verify current master/ADRs/mergeability/CI and run the mandatory technical plus architectural review. No merge without explicit owner permission.


## Owner approvals and interoperability standards review (18 November 2026)

**Current decision status (supersedes earlier pending labels in the dedicated review):** **CRED-01–16 approved**, including the source-authority restriction for non-qualification credentials; **CRED-17 approved in principle**, but precise portable credential profiles, offline status freshness and conformance criteria remain for standards-based technical resolution; **CRED-18 jurisdiction-specific detail remains open**, with the general Legal Compliance/Privacy policy-based approach endorsed. The owner approved the separation of Logging, Audit and Reporting and requested explicit public-contract exchanges. Prior CRED-03–15 proposals above should be read as approved conceptual direction as of this note, not as verified implementation.

### Standards-based profile selection — CRED-17 technical follow-up

Adopt recognised international or jurisdiction-specific standards **where appropriate to the credential use case**; do not mistake conformance with any standard for authority to award, licence or certify. Review interoperability and current authoritative editions before implementation, pin an explicit profile/version, and specify conformance tests and update policy:

- **Base portable claims:** W3C Verifiable Credentials Data Model v2.0 and its recommended securing mechanisms (Data Integrity or JOSE/COSE as selected); consider W3C Bitstring Status List v1.0 for scalable status disclosure. These are recognised Recommendations, not a demand to implement every signature suite.
- **Issuance and presentation protocol:** OpenID4VCI 1.0 Final for interoperable issuance and OpenID4VP 1.0 Final for wallet/verifier presentation where required. Select matching wallet, proof, holder-binding, key discovery, revocation and privacy profiles through interoperability testing.
- **Learning/skills:** 1EdTech Open Badges 3.0 and Comprehensive Learner Record 2.0 where individual achievement and comprehensive educational records are required; evaluate European Digital Credentials for Learning for EU-facing education cases, including the required eIDAS seals and applicable accreditation distinction.
- **National and sector schemes:** UK Digital Verification Services trust framework v1.0 and its statutory/certification context where actually supplying in-scope UK digital verification services; EU eIDAS/EUDI wallet ecosystem for regulated EU cases; ISO/IEC 18013-5 and ISO/IEC TS 18013-7 only where mDL/mobile identity credentials are an actual requirement. Other regulated professions/awards require their authoritative national registers and scheme rules.
- **Offline guarantee:** offline cryptographic integrity may be checked with cached trust material; current issuer status, live award standing and revocation depend on bounded fresh proof/status data. Return explicitly partial/unknown when fresh status cannot be established. Define risk-based maximum age and fail-closed uses.
- **Trust and interoperability:** verify issuer identity, claim-specific issuing mandate, approved source award, key-control/delegation status, intended audience/holder binding and status independently; reject unsupported profiles without marking the presented proof fraudulent. Use provider-neutral adapters; keep formats and policies versioned.

**Source references reviewed:** https://www.w3.org/news/2025/the-verifiable-credentials-2-0-family-of-specifications-is-now-a-w3c-recommendation/ ; https://www.w3.org/TR/2025/REC-vc-bitstring-status-list-20250515/ ; https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html ; https://www.1edtech.org/standards/open-badges ; https://europass.europa.eu/en/how-issue-european-digital-credentials-learning ; https://www.gov.uk/government/collections/uk-digital-verification-services-trust-framework . These are technical candidates and applicable regulatory evidence, not an assertion of certification or adopted operational profile.

### Explicit Credentials ↔ Logging, Audit and Reporting public contract

| Cooperating contract | Credentials sends / provides | Cooperating capability returns / provides | Ownership and outage |
|---|---|---|---|
| **Logging** (diagnostic input/health output; optional) | Sanitised structured operational signals: issuer-signing timeout, validation failure class, key-status lookup, retries/idempotency collision, outbox delay, disclosure refusal, correlation and tenant-safe reference; never raw credential claims, secrets, signed token or personal dossier | Bounded accepted/rejected/unavailable delivery result, service health and operational diagnostics when offered by Logging public contract | Logging owns diagnostic sinks and retention only. Absence must not erase authoritative issuance or satisfy Audit coverage |
| **Audit** (governed evidence catalogue/intake/coverage output; mandatory for selected high-risk actions) | Authoritative security/business events with action, source event/revision, verified actor and mandate, tenant/resource ref, attempt/outcome, reason category, applicable version/effective time; expected source checkpoints and lawful retention classes | Accepted/pending/rejected/unknown evidential receipt, custody/integrity/coverage and gap reports, authorised timelines or review/attestation; receipt never grants award authority | Credentials owns lifecycle and durable outbox; Audit owns evidence custody and integrity. Mandatory evidence durability must fail safely at operation/outbox boundary when it cannot be guaranteed, and downstream capture gaps must be detectable/reconciled |
| **Reporting** (source reads/events and derived analysis; optional) | Scoped authoritative issued/status/expired/revoked/replaced counts and records; issuer, subject, tenant and period restrictions; source revision, award-vs-credential distinction, as-of/freshness and coverage; committed events for invalidation | Report execution/result reference, accessible dashboard/export, snapshot lineage/version, completeness, refresh/invalidity and delivery status | Reporting owns definitions/snapshots/calculations, never credential state. Report access, saved exports and small-cohort inference require separate authorisation; outage does not block issuance |

**Contract discipline:** All calls are through currently proposed public ports; neither Logging nor Reporting has a verified completed public `CONTRACT.md` in this review. Audit has a detailed proposed ten-surface conceptual contract, but no verified implementation. Do not invent import names/HTTP routes or assume synchronous cross-capability writes. Reporting events do not become data authority; Logging diagnostics do not become audit evidence; Audit review does not revoke credentials. The privacy and minimum disclosure controls apply to all three.

## CRED-17 engineering resolution and CRED-18 policy-framework closure (18 November 2026)

**Status:** CRED-17 owner-approved in principle; the engineering choices CRED-17A–H are documented as evidence-backed **recommendations awaiting owner approval** in [standards and legal-policy resolution](../../../reviews/credentials-standards-jurisdiction-resolution.md). CRED-18's conceptual policy contract and jurisdiction resolution are documented in the same review. Recommend **closing CRED-18 at architectural level** because jurisdiction/scheme-specific legal analyses are explicit prerequisites owned by Legal Compliance/Privacy, not missing Credentials domain responsibilities. Do not claim blanket legal compliance, final cryptographic profile, validated runtime contract or certification.

**Public inbound policy contract:** dated applicable-jurisdiction and claim-purpose/scope decision from Legal Compliance and Privacy, including precedence/conflict, lawful basis, guardian authority, field-level verifier disclosure, cross-border rules, retention schedules by record category, rights/hold/correction and historical-status policy. Mandatory absent/undetermined policy fails closed for the affected operation.

**Public outbound policy contract:** authorised decision receipt with applied source/edition/effective time and allow/hold/deny/unknown; minimised proof/status/as-of response; attributable rights/retention/disclosure actions, committed status events and source revision references. All persistent issued records and historical status remain Credentials-owned; Qualification remains qualification-award source and Audit owns received evidential custody.

**Status and standards:** W3C VC 2.0 is recommended portable model, not the private schema. Profile registry controls signing, issuance/presentation protocols, sector profiles, revocation lists, holder binding, key governance and offline freshness; none grants an issuer legal authority. Final CRED-17 profile approval and interoperability evidence remain outstanding.
