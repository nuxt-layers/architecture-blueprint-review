# Identity, Age and Eligibility Assurance — Cross-capability Architectural Review

**Status:** Project-owner-approved direction for conceptual documentation (17 November 2026); **not an accepted ADR or implementation contract**.  
**Authority:** Current accepted `nuxt-layers/architecture-rules` ADRs, the governing IAM separation, Security/Privacy and published owner `CONTRACT.md` contracts prevail over this working blueprint.  
**Related reviews:** [Online Safety and Content Governance](online-safety-content-governance.md), [Node–Hub Federation](node-hub-federation-architecture.md), [Moderation](../docs/capabilities/moderation/capability-record.md).  
**Decision:** Make verification and assurance a cross-capability architecture topic; do **not** automatically create a new `verification` capability or central dossier of identity documents.

## 1. Objective and terminology

Distinguish five questions that cannot be safely answered by a single `verified: true` flag:

1. **Identity proofing:** Is the person or organisation credibly linked to the identity they claim, at a specified level and time?
2. **Age assurance:** Is there sufficient qualified evidence that a person meets a specified age threshold or age band, without necessarily disclosing their name or birth date?
3. **Authentication:** Is the current actor in control of a recognised account, authenticator or credential, at the assurance and recency required for this operation?
4. **Representation/authority:** Does a particular person have valid authority to act for a specific organisation, and for what action, scope and effective period?
5. **Eligibility:** Is the actor, merchant, listing, customer or transaction allowed to use this particular service/function under applicable law, domain rules, permissions and risk controls?

**Invariants:** identity proofing ≠ authentication ≠ identity/membership ≠ legal representation ≠ permission ≠ age assurance ≠ marketplace trustworthiness. An identity-proofed person may be a scammer; a valid credential may be stolen, old or revoked; an over-18 attestation need not reveal civil identity; a director label or domain email does not itself establish authority to bind a company.

## 2. Capability ownership — proposed boundaries

| Dimension / authoritative fact | Proposed accountable owner or boundary | Distinct obligations / exclusions |
|---|---|---|
| Principal ID, tenant/group membership, organisational identity relationships and standing | **Identity** | Does not automatically certify a civil/legal identity or make access or trading decisions |
| Authentication factors, sessions, assurance level of sign-in, freshness, recovery and revocation | **Authentication** | Never infer verified legal identity, age, employer authority or permissions from sign-in alone |
| Resource permission, delegation, policy evaluation, decision-time constraints | **Authorisation** | Uses qualified evidence and domain facts, does not perform civil proofing or own domain eligibility |
| Proofing assertion and its verification lifecycle | **Open ownership question**: Identity-adjacent dedicated verifier record vs bounded specialist proofing service | Avoid a universal database of raw passports, faces, birth dates and legal documents; source/evidence rights remain constrained |
| Age-threshold/age-band attestations, provider references, validity and revocation | **Open ownership question**: a scoped age-assurance evidence boundary | May reuse proofing infrastructure but should expose minimal age claims, not require naming the subject |
| Organisation legal status and representation evidence | Identity for relationship references; **separately qualified legal/entity and representation evidence owner TBD**, potentially external registers/proofing | Mere membership/role/organisation creation is not a verified company, company officer or valid mandate |
| Merchant eligibility and seller participation decision | **Marketplace** | Owns merchant onboarding, permitted listings, suspension/reverification; proofing supplies evidence, not sale permission |
| Access to age-restricted content or services | **The relevant domain or public-service capability**, with Authorisation and qualified age claims | Gate every sensitive read/action; do not make a third-party age provider the local access-decision owner |
| Applicable UK OSA and other identity/KYB/age legal constraints and effective dates | **Legal Compliance** | Source-verified, service- and jurisdiction-specific obligations; neither proofing nor an external provider grants statutory compliance |
| Fraud, phishing, suspicious activity and reported identity abuse | Relevant security/domain owner; **Moderation** for content/conduct case governance | Authentication protects account access, Content Security assesses risky material; Moderation does not own every cyberattack |
| External provider connections, service secrets, retries, signed results and cost telemetry | **Integrations and trusted host infrastructure**, within published boundaries | Provider-specific API does not own verification truth, eligibility or access decisions |
| Accepted assurance evidence and decision provenance | **Audit** | Retain minimised attestations/references, not default unrestricted document copies; Logging is diagnostic only |
| Federation of identity/assurance assertions | **Federation** transports/validates bounded assertions subject to local trust policy | A trusted Hub's claim is not automatic tenant membership, local account creation, authorisation or global identity |

These are **proposed logical boundaries**; existing public contracts must be inspected before allocating proofing/age record custody to a specific package. No new `identity-verification`, `age-verification` or `assurance` repository is authorised by this review.

## 3. Evidence and trust model

An assurance assertion should be **purpose-limited**, signed or otherwise strongly authenticated as appropriate, and carry bounded machine-readable semantics. Proposed minimal logical fields:

- Issuer/provider identity, asserted subject binding or privacy-preserving subject pseudonym; intended audience/verifier and permitted use.
- Claim type and outcome: identity proofing level, age-band/threshold result, representation scope or eligibility evidence. No generic single `verified` property.
- Verified method and evidence class (e.g. documentary check, trusted register, approved digital credential, inferred/estimated age); assurance/accuracy limitations.
- Issuance, observation and expiry timestamps; source effective period and status/revocation mechanism; issuer policy/version and correlation/reference.
- Selective disclosure and non-linkability expectations, handling of replays, sharing across Nodes, and error/unavailable/indeterminate states.
- Audit reference and privacy-classification/retention controls; raw image/ID/birth date only if strictly justified by a separate lawful and secured workflow.

**Failure semantic:** `valid / invalid / expired / revoked / unavailable / indeterminate / unsupported` must be distinguishable. A timeout or non-responding provider cannot mean adult, proofed or permitted. Different risk and service types may require deny, hold, limited non-sensitive access or another qualified evidence path. Decisions re-evaluate freshness when necessary. A verified cryptographic signature proves provenance/key possession under a trust assumption; it does not prove truthful underlying age, authority or business conduct.

## 4. Age assurance

Age assurance comprises different techniques (age estimation, age verification and other sufficiently robust evidence). Do not equate a particular token format with the statutory standard. Evaluate service-specific **highly effective age assurance** where the law requires it, using current Ofcom guidance, actual service category, child-safety assessment, confidence/accuracy, fairness, user privacy and alternatives.

**Privacy-by-design:** request `over threshold?` or age band wherever sufficient, rather than full date of birth, scanned ID or provider account identifier. A privacy-preserving verifiable assertion or ZKP may help, but only if issuer, proofing, resistance to sharing/transfer, freshness, revocation, accessibility and real-world assurance are verified. An over-18 check does not automatically imply a user is over the minimum age for every service or that the viewer remains the checked person.

**Age-related lifecycle:** claimed/unknown → check requested → qualified evidence accepted or rejected → active within bounded scope → expired/revoked/recheck required. Account creation, age claim storage, restricted-content access and refusal/appeal are separate events. Consider under-age safeguarding, account recovery, accessibility, multi-device use, identity minimisation, child data protection and redress for misclassification.

**Cross-domain use:** Publisher, Gallery, Media, Comments Engine, Marketplace, Hub/Search and any private communication capability may enforce different rules for content submission, discovery and viewing. Age assurance evidence does not transfer ownership of content or authorisation. Avoid a globally linkable age token that lets unrelated Hubs track users.

## 5. Civil identity, organisation and representation proofing

Differentiate natural-person ID verification from organisational legal-entity verification (KYB), verification of a representative's binding authority, tax/payment eligibility, sanctions/financial crime checks and platform-specific seller standing. Source may include independent proofing vendors, company registers, bank/payment providers and corporate mandates. A recognised group, account, email domain, or membership is not evidence of legal authority alone.

**Organisation authority:** evidence can change independently of the principal's local membership and company record (mandate expires, officer leaves, organisation dissolves, access revoked). Protect against forged documents, synthetic identities, stolen identifiers, collusive proofing, provider account compromise, and malicious verification administrators. Every assertion needs scope, revision, expiry and reassessment rules.

**Marketplaces:** Marketplace owns seller eligibility and listings; Payment Gateway owns relevant payment-provider events; Order owns purchase outcome; Authorisation governs operations. Check whether particular KYB/KYC is legally required for the actual service and payment arrangement; do not universally impose civil-ID upload for a user who is only browsing a forum. No universal blockchain/smart-contract escrow assumption.

## 6. Federation and portability

A Node can accept a bounded assertion from another Node, an external credential issuer or Hub, **only after explicit audience/issuer/trust evaluation** and any required subject-binding/assurance checks. Trust relationships are not transitive by default: Hub A accepting provider X is not proof Node B must trust X. A Hub may use attestations for its own peering policy without gaining the right to create local memberships, perform domain actions or reveal a user's identity to others.

**Portability:** export or present purpose-bound reusable proofs where lawful and secure; do not export all local account membership, delegated rights, case history or third-party evidence without authority. Design revocation, de-federation, operator exit, provider rotation, issuer compromise, lost credentials, inaccessible home Nodes, replay and offline/short-lifetime claims. Keep Node standalone mode functional.

## 7. Potential public contract surfaces (not existing APIs)

| Surface | Inputs | Outputs / boundary |
|---|---|---|
| **AVA-01 Claim request** | Trusted claimant or authorised relying service, specific proofing/age/authority claim, purpose and policy/version | Scoped request, provider choice or supported method, privacy notice; not a raw ID collection by default |
| **AVA-02 Evidence intake / provider callback** | Issuer-authenticated evidence/assertion, subject binding, challenge/nonce, audience and effective validity | Validated evidence-reference and verification status or precise refusal/unknown |
| **AVA-03 Effective age assertion** | Age threshold/band, eligible subject binding, trusted issuer set, assurance and freshness | Minimal boolean/band claim with issuer quality, expiry and explicit indeterminate outcome; no automatic identity disclosure |
| **AVA-04 Proofed identity assertion** | Claimed person/organisation identity, permitted proofing pathway, purpose | Scoped proofing evidence and method/assurance, not universal local principal creation |
| **AVA-05 Representation evidence** | Entity/representative IDs, permitted act, scope, dates and trusted register/mandate | Qualified binding-authority attestation or unavailable/failed result; Authorisation and domain still decide action |
| **AVA-06 Eligibility evaluation handoff** | Domain-owned seller/service/listing facts, qualified identity/age/authority evidence, legal constraints | Evidence packet to domain owner, not an externally dictated marketplace permission |
| **AVA-07 Status, recheck and revocation** | Issuer/record status, holder request, policy expiry, risk signal | Active/expired/revoked/unknown, bounded invalidation and notifications |
| **AVA-08 Federated assertion exchange** | Signed/presented claim, issuer and audience policy, Node peer trust, local account-binding proof | Locally acceptable trust-qualified assertion or rejected/unknown; no automatic membership/transitive trust |
| **AVA-09 Evidence, data rights and costs** | Decisions, issuer/version, processing basis, authorised export/disposal, billed provider operation | Minimised Audit events, authorised rights/cost summaries; separate restricted source documents |
| **AVA-10 Administrative and subject UX** | Scope-limited administrator, parent/carer where applicable, claimant and merchant contexts | Status, why verification requested, method options, reconsideration/recovery, expiry/recheck and accessible appeal; headless service possible |

An eventual implementation needs versioned schemas, consumer-facing `CONTRACT.md`, clear required/optional ports, one-call host composition where applicable, and no cyclic local dependencies.

## 8. Failure modes, security and privacy acceptance

- Proofing provider unavailable: do not fabricate successful assurance; risk-policy controls action while offering qualified alternative paths.
- Signed token copied to another account/Node: reject unless intended audience, subject/control binding and validity are verified; prevent linkage across services beyond allowed purpose.
- Organisation officer's authority revoked: issuer or trusted source status changes, local merchant standing and access decisions re-evaluate with documented maximum staleness.
- Age estimate uncertain or biased: accessible alternative and challenge with appropriate privacy protections; avoid defaulting every uncertain child to an adult.
- Fraudulent merchant with valid ID: flag commercial risk separately; verification alone does not remove Marketplace controls.
- Malicious/compromised issuer or replayed assertion: trust revocation, key rotation, bounded validity, explicit stale outcome and Audit evidence.
- Privacy: avoid accumulating a central database of IDs/face scans/birth dates; classify and restrict any unavoidable processing, retention, onward disclosure, erasure and safeguards.
- Cross-Node: accepting a Hub-provided statement never grants access to another tenant's membership or source data.
- Audit: document false positives, refusals, provider failures, appeals, method quality and processing scope; never equate number of completed checks with proof of legal compliance.

## 9. GUI and operator experience

Potential screens: **verification status** (claimant, only minimal claim), **verify your age** (age-specific method choice without gratuitous identity collection), **merchant onboarding and representation** (Marketplace-owned UI), **verification expiry and recheck**, **appeal/recovery**, **privacy and sharing controls**, and **operator verification policy/provider diagnostics**. A Hub operator dashboard can show qualified pseudonymous eligibility of a peer/member, not raw documents or third-party social graphs.

Follow the application's host-controlled sidebar/navigation pattern and the Theme Manager/application-test-template presentation approach; no separately authorised user-facing global identity dossier. Accessible, internationalisable, low-bandwidth and privacy-respecting alternatives are essential; server-side authorisation gates source operations.

## 10. Open questions for full design review

- **AVA-Q01:** Who owns persistent proofing/age evidence and issuer status records? Is a bounded distinct verification capability justified, or do existing IAM/services suffice?
- **AVA-Q02:** Which identity and organisation proofing levels map to each specific risk and regulated service?
- **AVA-Q03:** Which provider/credential standards, subject binding and offline/federated validation are acceptable?
- **AVA-Q04:** How is highly effective age assurance demonstrated under current applicable Ofcom criteria, and what accessible alternatives exist?
- **AVA-Q05:** How are privacy-preserving proofs safely reused across unrelated Nodes without creating tracking identifiers?
- **AVA-Q06:** How are expiry, provider compromise and revocation propagated with bounded staleness?
- **AVA-Q07:** Who is authoritative for corporate representation mandates and verified business identity versus Identity's group and tenant records?
- **AVA-Q08:** Which evidence can Marketplace, Publisher, Moderation and Hubs store/disclose under relevant data protection obligations?
- **AVA-Q09:** Who governs provider licensing, availability, cost, lawful international transfers and response quality?
- **AVA-Q10:** How do an adult, a child, a wrongly rejected claimant and a merchant challenge an adverse assurance outcome?
- **AVA-Q11:** Which qualified decisions require human review and which may be automated, with independent evidence?
- **AVA-Q12:** Which minimal host/federation acceptance scenarios prove interoperability without transferring authority to external providers?

## Review disposition

Approved **for blueprint documentation and future dedicated review**, not adopted as a new bounded capability, framework, IAM responsibility amendment, selected vendor, regulatory certification, or deployed solution. Record reciprocal notes in current capability reviews and add status/decision references to working registers. Follow the established governing PR/ADR process for normative amendments after the public-contract and security/legal review.
