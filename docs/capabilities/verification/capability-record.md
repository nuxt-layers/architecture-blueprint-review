# Capability Record — Verification

**Capability:** `verification` — **proposed Platform capability**; new candidate approved for blueprint classification on 17 November 2026.  
**Status:** Conceptual only. No implemented package, standalone repository, public `CONTRACT.md`, production provider or independent acceptance is asserted.  
**Authority:** Current accepted `nuxt-layers/architecture-rules`, IAM separation and Capability Standard; the blueprint is non-normative.  
**Related:** [Identity, Age and Eligibility Assurance](../../../reviews/identity-age-eligibility-assurance.md), [International verification comparison](../../../reviews/verification-international-jurisdictions.md), [Moderation](../moderation/capability-record.md).

## Purpose, classification and boundaries

Verification governs the **request, assessment, acceptance, lifecycle and disclosure of qualified claims** about people, organisations, age thresholds, legal representation and other externally or internally substantiated attributes. It owns the verification request, qualified attestation, provider/issuer trust evaluation, evidence references, status/expiry/reverification and narrowly scoped disclosure. It does not own the original civil identity, a national register, all source documents, local principal membership, authentication sessions, resource access grants, seller eligibility, or the legality of an underlying commercial transaction.

Proposed Platform responsibility is justified by a reusable, provider-neutral evidence/trust/status lifecycle independent of each application domain. **Age assurance is a specialisation/claim class, not an automatic separate package.** A coherent conceptual capability does not itself authorise repository creation, implementation or direct Nuxt coupling; apply ADR-0012/0016 and the classification gate.

## Approved principles VER-01 to VER-12 (conceptual)

| ID | Approved direction | Architectural consequence |
|---|---|---|
| VER-01 | Verification separate from Identity, Authentication and Authorisation | Do not conflate proofed claims with principal, session, permissions |
| VER-02 | Create `verification` as a *candidate* capability | Review independent records, interfaces and ownership before implementation |
| VER-03 | Separate identity, age, representation and eligibility semantics | Distinct claim types, evidence quality, scope and restrictions |
| VER-04 | Prefer minimal attestations over raw identity documents | External/holder evidence custody where legally suitable, restricted references only |
| VER-05 | Require issuer provenance, method, assurance, validity and revocation | Every qualified attestation carries verifiable status and expiry |
| VER-06 | Permit multiple providers and methods | Provider-neutral adapters, accessible alternatives, explicit failure modes |
| VER-07 | Standards-based issuance/presentation where appropriate | Evaluate W3C VC, OpenID4VCI/VP, NIST and applicable national schemes; no single mandated format |
| VER-08 | No automatic portable membership, permission or merchant standing | Local authorities independently decide and enforce |
| VER-09 | Each receiving Node evaluates trust and eligibility locally | No transitive Hub trust; peer trust is not access or eligibility |
| VER-10 | Bounded revocation freshness, expiry and reverification | Risk-specific rechecks, status, events, fallback and reconciliation |
| VER-11 | Privacy-preserving age claims without unnecessary identity disclosure/tracking | Prefer age-band/threshold proofs, unlinkability where feasible |
| VER-12 | Demonstrate legal age-assurance efficacy separately from cryptographic validity | Legal Compliance maps jurisdiction/service duties; test effectiveness |

## Authoritative data and custody

| Information or operation | Owner and restrictions |
|---|---|
| Source passport, face scan, company register or legal document | Original holder, lawful register or specialist provider by default; local custody only on separately justified, secured basis |
| Verification request, issuer policy evaluation, attestation, status, source reference and bounded lifecycle | **Verification candidate** |
| Local principal and tenant/group relationships | **Identity** |
| Credential and session proof, recency and authentication assurance | **Authentication** |
| Access permission and delegation | **Authorisation**, consuming qualified input |
| Seller eligibility, trading suspension and marketplace acceptance | **Marketplace** |
| Legally authoritative company mandate | Relevant external legal source; Verification assesses qualified assertion, Identity may link local relationship |
| Legal/service/jurisdiction obligations | **Legal Compliance** |
| Provider transport/secrets/billing context | **Integrations / trusted host**, with defined provider-neutral port |
| Audit receipts/integrity and technical logs | **Audit** (evidence), **Logging** (diagnostics) |
| Transmission between Nodes/Hubs | **Federation**; no transfer of domestic authority |

**No universal `verified: true` state.** Every attestation has explicit claim semantics and subject binding. Verification evidence is not inherently a central dossier; segregate tenant, purpose and relying party and limit re-use to lawful, permitted scope.

## Native conceptual lifecycle and failure semantics

**Request:** requested → challenge/provider pending → evidence assessed → qualified attestation issued, refused or indeterminate. **Attestation:** valid within permitted scope → suspended/expired/revoked/superseded; re-verification produces a new attributable result and links to the prior one where lawful. **Trust policy:** issuer trusted for specific claim and risk at specific time → revised/suspended/distrusted, with invalidation of dependent decisions. **Representational authority:** local company relationship may change independently of proofing status and expiry.

Track distinct validity of (a) evidence document, (b) issuer and cryptographic key, (c) subject/holder binding, (d) legal representation or factual claim, (e) local eligibility decision and (f) required freshness of status check. A valid credential does not guarantee the underlying fact remains true.

Return distinct **valid, invalid, expired, revoked, suspended, unsupported, unavailable, indeterminate** outcomes. A timeout is never successful verification; per-operation policy chooses denial/hold/recheck/safe alternative. Make idempotency, replay/challenge handling, revocation propagation and external outage observable. Use short-lived assertions, independently verifiable status lists or authorised online status checks, and event-driven invalidation where appropriate. Set bounded maximum staleness by risk; do not turn provider availability into unrestricted access. Avoid status endpoints that unnecessarily disclose a person's every visit to issuers.

## Proposed logical public contract — input and output

**Conceptual names only; no current API asserted.**

| Surface | Trusted inputs | Outputs and boundary |
|---|---|---|
| VER-C01 Request and intent | Subject or qualified relying party, claim type, purpose, threshold, audience, locale, lawful policy | Challenge/request status, acceptable methods, minimised disclosure and refusal reasons |
| VER-C02 Proofing/provider response | Trusted provider assertion, nonce, proof, issuer/key, subject binding, method and evidence class | Validated or refused attestation with assurance level, provenance and limits |
| VER-C03 Attestation status | Issuer/claim reference, relying-party/audience, accepted freshness and revocation requirements | Explicit valid/expired/revoked/unknown/indeterminate and last-known freshness |
| VER-C04 Age threshold/band | Requested threshold, permitted context, acceptable method/issuer | Minimal age claim and effective validity without default identity disclosure |
| VER-C05 Person/organisation identity | Proofing claim with source and strength requirements | Qualified identity assertion, never implicit local account or membership creation |
| VER-C06 Representation | Claimed natural-person-to-legal-entity mandate, action scope and effective time | Qualified mandate/provenance and bounded freshness or refusal/unknown |
| VER-C07 Domain eligibility handoff | Purpose-limited, authorised assertion references and source-owned domain context | Evidence packet for Marketplace/Publisher/other domain to decide; not permission |
| VER-C08 Issuer trust / federation | Validated issuer registry policy, remote assertion, peer context, local audience and controls | Independent trusted/untrusted/unknown decision, never transitive Hub approval |
| VER-C09 Evidence, rights and provider operations | Verification outcome, data-access/erasure request, lawful retention, cost record | Minimised audit assertions, lawful export/disposal, provider reconciliation/health |
| VER-C10 Management and presentation | Authorised verifier/admin/holder context, claim status, expiry/recheck/appeal actions | Role-limited status, method selection, revocation, provider diagnostics and accessible UX; headless supported |

**Required review:** caller trust, error shapes, tenant isolation, consent/lawful basis, standards profile, signature/status validation, key rotation, validation freshness, provider absence and emergency action semantics. Direct local dependence remains acyclic; transport is not a licence for direct private data imports.

## Cross-capability input and output matrix

| Cooperating owner | Verification receives | Verification supplies |
|---|---|---|
| Identity | Trusted opaque subject/tenant refs, standing and related-party identifiers | Qualified claims with validity/provenance; cannot change membership |
| Authentication | Authenticated holder binding and appropriate session/assurance evidence | Independent proofed-attribute claims; never issues local sessions |
| Authorisation | Required claim scope, risk, caller decision context | Qualified attributes/status to use in its resource evaluation; no grants |
| Marketplace / Publisher / Media / Comments / prospective Messaging | Relevant action and restricted-content/seller requirements | Age, representation, identity and other trusted evidence outcomes; domain retains eligibility and source-state decisions |
| Legal Compliance | Dated legal duty, permitted collection/disclosure, jurisdiction and service category | Proofing method/quality/status evidence; no guarantee of legal compliance |
| Integrations / host | Provider API connectivity, keys, quotas, rates, jurisdiction/lawful processing parameters | Purpose-bounded requests/responses and failure/expense evidence |
| Federation | Signed remote presented assertions with peer/issuer context | Trust-evaluated local assertion results, no automatic local account or authority |
| Audit / Logging / Reporting | Evidence schemas, diagnostic/aggregation ports | Minimized typed events, provider failures and qualified aggregates, no raw dossiers |

## Federation and Hub trust requirements

An independent Node can accept a proof presented by a subject or transmitted through another Node/Hub only after **issuer allow/trust criteria, cryptographic integrity, correct claim and intended audience, holder binding, effective date, fresh revocation status, assurance method and local permission/eligibility check**. Hub A trusting provider X never requires Node B to trust X. No global required verification directory. Federated holder identities and age tokens should avoid linkable unique identifiers across unrelated relying parties where possible. Provider compromise, key change, account unlinking, domain exit and revocation must invalidate dependent claims within documented bounds.

## Security, privacy, data lifecycle and storage

Threat model: forged identity/organisation evidence, manipulated age estimation, stolen credentials, replayed proofs, copied bearers, fraudulent providers, compromised issuer keys, forged mandates, biometrics leakage, status correlation, mass surveillance via universal ID, coercive government/provider access, cross-tenant leakage, abuse of verification refusals and accessibility exclusion. Require clear privacy notices, accessible alternative methods and redress. Retain only minimal attestations, source references and lawful status/provenance. Do not store arbitrary national ID scans in the Node's object storage. Retention, storage/register, encryption, purpose limits, rights, lawful transfers and segregation must be designed before implementation.

## Standards and international applicability

**Evaluate, do not preselect:** W3C Verifiable Credentials Data Model 2.0; OpenID4VCI/VP profiles; NIST SP 800-63-4; UK Digital Verification Services trust framework; applicable Ofcom highly effective age assurance; appropriate national e-ID and business register interfaces. Standards compliance of a signed credential is not proof of legal validity, legal applicability or effective fraud/age detection.

China's national internet identity service (effective July 2025) supports online ID and age attributes with reduced plaintext disclosures; separate legally required real-name procedures and sector-specific minor protections still apply. Russia combines age content classification, regulated service duties, national digital ID and potentially stringent personal-data localisation. Saudi Arabia uses national identity/Nafath/Absher and merchant/business verification mechanisms, with its PDPL and activity-specific age requirements. See [jurisdictional review](../../../reviews/verification-international-jurisdictions.md), which distinguishes examples, evidence and unresolved local legal requirements. **Never infer that accepting a national credential makes a particular Node deployable or compliant in that jurisdiction.**

## Conceptual GUI and acceptance

Optional verification dashboard: methods/providers, pending/expiring/revoked claims, user-friendly age-check choice and privacy notice, merchant onboarding representation status, verification appeals/alternative methods, staff-only issuer-trust and incident controls, monitoring and bounded provider costs. The host owns navigation; no global exposed identity dossier. WCAG 2.2 AA and internationalisation apply; headless integration must work. Tests should simulate raw-evidence minimisation, unknown provider, expired/revoked/compromised attestation, two Nodes with different issuer trust, reused age proof with no cross-Hub tracking, corporate authority change and inconsistent legal/data residency requirements.

## Open decisions and disposition

Choose exact verification proofing/age data custodian and data controller relationships; credential/status standard profile; issuer accreditation and trust governance; provider/legal category; permitted evidence reuse; offline validity/short-lived token design; revocation service guarantees; legal source of mandates; localisation and safeguarding; appeal independence; integration fees; and formal classification relative to IAM. VER-01–VER-12 are **approved conceptual principles**, not an implementation mandate. Next step: independent detailed capability review and, if warranted, governing ADR proposal.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-10 proposed cooperation:** Verification may validate purpose-specific issuer, accreditor, delegate and credential evidence only within its approved remit; it cannot create academic recognition, grant a qualification or reown Assessment marks. Credentials must preserve source authority, effective scope, provenance, freshness and revocation/unknown states. This note does not complete the separate verification review.

## COURSE-12 — Qualification authority reciprocal note (18 November 2026)

**Status: Owner-approved conceptual responsibility; detailed Qualification review and implementation pending.** [Qualification candidate](../qualification/capability-record.md): **COURSE-12 owner-approved interface direction:** Verification may validate issuer/centre identity, representation and mandate evidence only within its independently accepted scope; Qualification determines qualification-specific award authority/rule applicability and remains owner of local award decisions. Verification does not become an awarding organisation, create official recognition or replace external regulatory sources. No change to previously approved verification ownership.

## Assessment provider trust and cross-institution reuse — 18 November 2026

**Status: ASMT-06–14 owner-approved Assessment conceptual boundary; Verification interface detail proposed pending its own contract alignment.** [Assessment](../assessment/capability-record.md): Verification supplies source/issuer identity, scoped trust, evidence authenticity, mandate/recognition claims where independently supported, effective dates, verification assurance, freshness and revocation/unknown outcomes. A signed result and verified identity do not establish examination authority. Verification does not grade, accept an Assessment result for a receiving organisation, decide Course/Training achievement, or issue Qualification awards. Assessment independently decides admission of external grading evidence for its purpose; Training and Qualification independently determine downstream equivalence/awards. No universal trust score, automatic transitive Hub trust, or direct implementation coupling. Document qualified trust and its recheck/invalidation public surfaces in Verification's own independent review.

## Owner-approved reciprocal Assessment trust interface — 18 November 2026 (Assessment PR #64)

**Status: Approved Assessment/Verification conceptual boundary; Verification's own detailed public contract and implementation are still pending.** [Assessment's approved trust and contract note](../assessment/capability-record.md#owner-approval--external-assessment-trust-and-public-contract-18-november-2026) requires Verification to offer a purpose-specific issuer/source trust evaluation, conceptually `EvaluateIssuerTrust`, accepting provider/issuer identity, authenticated claim/result evidence, intended assessment type and use, relying institution, jurisdiction/effective time, assurance requirement and trust policy revision. The response must qualify identity, integrity, authorising mandate or verified recognition evidence where available, scope, assurance method, evidence provenance, last-checked time, expiry/revocation/staleness, verdict and caveats. Distinguish sufficient, insufficient, rejected and indeterminate; no universal provider trust score or transitive Federation/Hub authority. Authenticity and identity alone do not establish authority to provide an examination.

Verification owns this qualified evidence/issuer trust determination, not Assessment grading, locally permitted reuse or another body's qualification powers. Assessment applies its independently approved `EvaluateExternalAssessmentEvidence` decision against its instrument, marking/acceptance policy, lawful disclosure and licence constraints; Training and Qualification independently judge competence, equivalence or awards. Trust withdrawal and stale external status generate recheck/notification inputs; previously committed source and downstream decisions are not silently erased. This note preserves VER-01–VER-12 and does **not** claim Verification has a released API, that one trust taxonomy was approved globally, or that a new capability is needed. Reconcile the exact final signatures and validation/unknown guarantees in Verification's later independent public contract review.


## Qualification trust and employment interoperability — reciprocal proposal (18 November 2026)

**Status: QUAL-06–08 owner-agreed; QUAL-09 accepted in principle, details proposed in [Qualification PR #65](../qualification/capability-record.md).** Verification owns generic source/issuer attestation verification requests, trust methods, source validity, revocation freshness and privacy-preserving proof disclosure. Qualification consumes those source-qualified findings to interpret awarding-body recognition, scheme scope, delegated award power and individual award significance, retaining its own domain judgement and verified source references. An authentic signed certificate is not automatically a recognised qualification, licence to practise or proof of employer-specific eligibility. Qualification supplies its formal award decisions as source facts; Verification must not make awards. Avoid double-ownership of general trust registries or mutual imports. This note does not assert a published API or independent approval for verification.



## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)); Verification's approved principles remain intact.** Credentials owns locally issued credential/proof and authoritative credential-status registry. Verification independently evaluates externally presented claims, issuer/key/trust policy and relying-party scope; it may consume Credentials' published minimised status/proof contract. Do not build a duplicate credential issuance registry or a bidirectional package dependency. Signature verified does not establish a current award or credential status; unknown/stale status remains qualified. Cross-tenant enumeration and verifier tracking are disallowed by default.


## Credentials CRED-17/CRED-18 reciprocal policy and standards note (18 November 2026)

**Status: CRED-17 technical profile recommendations, 18 November 2026, PR #62; not an implemented API or universal standard mandate.** Credentials proposes W3C VC 2.0 portable model, selected JOSE/COSE or Data Integrity security profile, OpenID4VCI/VP 1.0 when wallet-supported, status list 1.0 where appropriate and qualified offline checks. Verification assesses independently presented proofs, issuer/trust roots, scope and revocation/status freshness through published Credential proof/status ports; do not create bidirectional package imports or treat a valid signature as sufficient authorisation or current award. Country/sector trust is independently assessed at the relying party. See [CRED-17 review](../../../reviews/credentials-standards-jurisdiction-resolution.md).

## Attendance ATT-11 — standards reference for guest/guardian assurance (18 November 2026)

**Status:** Standards applicability note proposed in Attendance PR #79 (18 November 2026); ATT-09/ATT-10 are owner-approved, but ATT-11 standards mapping is not separately approved. References are design guidance unless an accepted governing rule or applicable law already makes a control mandatory. No implementation, certification or new dependency implied.

**Apply:** [NIST SP 800-63A-4](https://csrc.nist.gov/pubs/sp/800/63/A/4/final) as guidance for identity-proofing evidence and assurance where a guest claim actually needs real-world attribution; [NIST SP 800-63C-4](https://csrc.nist.gov/pubs/sp/800/63/C/4/final) when federated assertions are used. Verification may substantiate identity/age/representation attributes and their provenance/expiry, but a successful check does not itself authenticate a session, authorise event access or confer enrolment/guardian legal standing. Attendance consumes bounded verification status through a public port; proofing must be proportionate to risk and no full proofing is mandatory for ordinary low-risk invitations.

## Federation — reciprocal conceptual contract (18 November 2026)

**Status: Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69); not an approved implementation API, and does not complete this capability's independent review.** [Federation public contract](../federation/capability-record.md#independent-review-contract-completeness-and-authority-18-november-2026).

Federation transports provenance, issuer/endpoint proof references, scope, audience, validity times, proof status and revocation observations; Verification evaluates specific trust evidence/credential claims where its public contract applies. Federation's local acceptance is not independent certification of organisation identity, age, issuer standing or content truth. Trust is never transitive between Hubs or Node peers. All cooperation is via public, directional host-composed contracts with scoped failure/absence semantics; preserve existing approvals and avoid package dependency cycles.


## Identity reciprocal conceptual interface — 18 November 2026

**Status: proposed Identity alignment, [draft PR #74](https://github.com/nuxt-layers/architecture-blueprint-review/pull/74), 18 November 2026; no implemented verified-owner port claimed.** Verification may provide provenance, issuer/status/subject-binding and age/corporate representation claims. Identity owns resulting local principal and digital tenant owner lifecycle, not civil identity or legal controller adjudication. A valid document/claim alone never creates principal standing, direct membership, tenant authority or legal right; stale/disputed claims hold sensitive owner transfer and recovery pending independently qualified legal review. See [Identity conceptual contract](../identity/capability-record.md#idealised-public-inbound-interfaces).

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Verification adjudicates external evidence admissibility, trust, claim qualification and freshness under permitted jurisdiction/purpose. Integrations only verifies connector/callback authenticity and transports attributed provider assertions with effective/source/observed time, revocation/staleness and unknown/conflict states. A connected national-ID, age/KYB or issuer provider never automatically verifies a person or grants domain eligibility. See [Integrations conceptual record](../integrations/capability-record.md#idealised-public-outbound-contract), PR #76; no provider selected or implementation asserted.

**Marketplace reciprocal — proposed, 19 November 2026:** [Marketplace review](../marketplace/capability-record.md#marketplace-conceptual-review--19-november-2026) consumes purpose-limited verified merchant identity, representation, KYB/eligibility claims and freshness/revocation evidence. Verification owns validity/trust of claims, Marketplace owns venue participation/approval/restriction and jurisdiction-specific application. A verified person is not automatically a legitimate seller; no universal KYC mandate or personal dossier sharing. Missing requisite assertion holds, never auto-approves. **Proposal only; VER approvals unchanged.**
