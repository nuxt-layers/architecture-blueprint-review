# Credentials CRED-17 interoperability and CRED-18 jurisdiction policy closure — 18 November 2026

**Status:** CRED-01–16 owner-approved. CRED-17's *principle* owner-approved; technical profile decisions below are **evidence-backed recommendations awaiting explicit owner adoption**. CRED-18's **conceptual architecture** can be closed as a bounded policy handoff without purporting to approve every individual country's law. No implementation, certification or compliance claim. Source standard status checked 18 November 2026.

## CRED-17 — technical decision matrix

| ID | Specific decision | Rationale and constraint | Approval |
|---|---|---|---|
| CRED-17A | Canonical issued credential is a provider-neutral, versioned domain record. W3C VC Data Model **2.0** is the default **portable** model, not the private persistence schema. | Retain national/sector-specific profiles, exact transformation and source provenance. VC 2.1 is a working draft in 2026, not an automatically binding replacement. | Recommended, owner confirmation pending |
| CRED-17B | Require one explicitly versioned **cryptographic security profile** per portable format. Prefer **W3C VC JOSE/COSE**, choosing an interoperable JWS/JOSE signing profile as initial general implementation candidate, with VC Data Integrity as separate approved profile when required by relying parties. | W3C standard offers alternatives; do not call unsigned JSON verifiable; no arbitrary algorithms or unsafe fallback, and never claim all signatures verified if an unsupported suite is encountered. Cryptographic algorithm, key type, trust anchor and library chosen during implementation threat review/conformance. | Recommended baseline; exact first signing suite and key parameters to select with counterpart interoperability evidence |
| CRED-17C | Use **OpenID4VCI 1.0 Final** for wallet-compatible issuance and **OpenID4VP 1.0 Final** for compatible verification presentations when enabled. Both remain optional to native server-side lifecycle and non-wallet consumers. | Avoid embedding transport or wallet into award ownership. Verify state/nonce, audience, proof of holder/key possession where required; never assume possessing a bearer file is identity proof. | Recommended, owner confirmation pending |
| CRED-17D | Use **W3C Bitstring Status List 1.0 Recommendation** for privacy-preserving bulk VC status where the chosen credential/profile supports it; maintain source credential status and map to list publication with effective revision/freshness and outbox-driven reconciliation. | A status list is not another status master. Publish changed list or schedule with bounded lag; cached / offline proofs expose as-of/age, not false 'currently valid'. W3C 1.1 in November 2026 is draft and not auto-substituted. | Recommended, owner confirmation pending |
| CRED-17E | Layer education-specific **1EdTech Open Badges 3.0** for individual achievements and **CLR 2.0** for a multi-achievement learner record where required. EU EDC/eIDAS/EUDI and UK DVS rules are applicability-gated profiles, not mandatory platform-wide. | Qualification decides award; specific national statutory or register rules may supersede a general portable profile for a regulated claim. Certification is separately earned. | Recommended conditional; claim type / jurisdiction mapping during deployment |
| CRED-17F | Offline validator may establish signature, integrity, bounded trust/key data, holder proof if applicable and historical status evidence; **current credential/award validity remains unknown unless sufficiently fresh status/trust material is present**. No fixed globally valid '24-hour' limit. | Effective maximum status age is versioned by issuer/claim/relying party risk; hard-fail for mandatory high-assurance actions when freshness not met, else report partial/offline and ask for online verification. Prevent replay with audience-bound challenge/nonce for interactive presentations; static printed QR is not live holder proof. | Recommended, owner confirmation pending |
| CRED-17G | Privacy and trust by design: explicit issuer/award authority, cryptographic key custody, rotation and incident recovery; selective-disclosure only for **verified supported** profiles, no unsupported privacy claim. Prefer bulk status over per-holder 'phone home', enforce verifier purpose/audience and prevent credential enumeration. | Trust in a signer does not imply scope to issue regulated qualifications; local Verification makes independent third-party trust decisions. | Recommended, owner confirmation pending |
| CRED-17H | Public **profile registry** lists profile ID/edition, permitted issuer/claim types/jurisdictions, required proof and status, holder binding, expiry and freshness bounds, supported wallets/verifiers, exact error codes, migration/sunset and tests. Unsupported/revoked profile is not treated as a fraudulent credential automatically. | Independent consumer can discover compatibility and fail safely. No universal stack, forced wallet, global issuer registry or framework-specific types in the core contract. | Recommended, owner confirmation pending |

**Conformance before publication:** W3C schema and cryptographic positive/negative test vectors; invalid signature/tampered claim; unsupported algorithm/profile; stolen or retired keys; duplicate issuance/replay; revoked/expired/stale status list; online/offline comparisons; hostile verifier and cross-tenant disclosure; status list correlation; key rotation and authority withdrawal; external wallet/issuer interoperability; selected Open Badges/CLR profile if actually promised. Record exact editions, providers, trust roots, test evidence, profile limitations and renewal dates. No compliance label until independently demonstrated.

**Standards evidence**:
- W3C VC Data Model 2.0: https://www.w3.org/TR/vc-data-model/
- W3C 2025 family Recommendation announcement: https://www.w3.org/news/2025/the-verifiable-credentials-2-0-family-of-specifications-is-now-a-w3c-recommendation/
- W3C JOSE/COSE: https://www.w3.org/TR/vc-jose-cose/
- W3C Bitstring Status List 1.0: https://www.w3.org/TR/vc-bitstring-status-list/
- OpenID4VCI 1.0 Final: https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html
- OpenID4VP 1.0 Final: https://openid.net/specs/openid-4-verifiable-presentations-1_0-final.html
- 1EdTech Open Badges: https://www.1edtech.org/standards/open-badges
- 1EdTech CLR: https://standards.1edtech.org/clr/
- UK DVS v1.0: https://www.gov.uk/government/publications/uk-digital-verification-services-trust-framework-1-0
- EU eIDAS amendment: https://eur-lex.europa.eu/eli/reg/2024/1183/oj ; EU issuer format implementation: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32025R1569

## CRED-18 — resolved conceptual architecture and policy contract

**Architectural closure recommendation:** Credentials applies policy; **Legal Compliance** is authoritative for applicability of statute/regulation and lawful retention/recognition restrictions; **Privacy** is authoritative for lawful-basis and data-rights policy; **Qualification** or another claim owner remains authoritative for the underlying award and appeal; **Verification** for separately evaluated external trust; **Credentials** for issuance-specific control, disclosure, valid proof and credential status. Legal interpretation and deployment-specific country/sector approval remain distinct *tracked evidence*, not a permanently open Credentials boundary.

### Applicability and precedence

For each credential operation, resolve **issuing organisation/tenant and claim/qualification scope**, issuing jurisdiction, subject/data-protection jurisdiction when relevant, relevant **recipient/verifier location and regulated purpose**, service type, applicable time/version and external programme obligations. A single 'user country' is not enough. Multiple laws may apply; policy resolution must detect conflict/uncertainty, not silently choose a convenient country. Determine actual controlling laws/relationships through Legal Compliance and Privacy with dated source evidence and authorised review; never infer solely from IP or language.

Precedence: binding law/court/regulator requirements and mandatory protective controls; binding scheme and current issuer/delegation restrictions; lawful organisation policy; individual display/notification preferences. If a legal collision cannot be resolved, reject/hold affected operation with clear reason; do not downgrade minimum protection. Configuration selects legally permitted options, not law.

### Mandatory policy inputs to Credentials (public conceptual interface)

- Policy decision ID/edition; source organisation/approved authority; application scope (tenant, issuer, credential type/qualification scheme, country/region, regulated sector, purpose and audience); validity/effective period and reviewed-at provenance; explicit **applicable / not applicable / undetermined**.
- Authorised issuer/award mandate restrictions; lawful basis and notices; minimum age/guardian and safeguarding requirements where applicable; consent requirements **only when legally the correct basis**; disclosure/recipient/verification purposes and constraints.
- Field-level permitted attributes, selective-disclosure and verifier access limits, cross-border transfer and vendor restrictions; whether public status-only responses are allowed and how holders are protected from verifier tracking.
- Record-category-specific retention **trigger, duration or review schedule, disposal method, lawful holds, evidence retention and responsible approval** for issued records, signing proofs, subject data, access logs, Audit and distributed exports. Never pretend revocation or credential expiry mandates immediate erasure.
- Correction/appeal/revocation process, effective vs historic validity, post-revocation permissible disclosure and redress; applicable online/offline status freshness and required recertification/reproofing thresholds.
- Policy uncertainty/conflict outcome, exception authority (not unilateral waiver of law), review/expiry and notice/dispute obligations.

**Credentials public outputs:** qualified policy evaluation receipt (applied decision/version/source, allowed/held/denied/unknown, affected credential/claim and safe reason); committed issuance/status/correction actions with effective time and lineage; restricted verifier responses and as-of historical status; lawful rights/retention action receipts, erasure/anonymisation/hold exceptions and disclosure/export records; events for Audit, Reporting, Notifications and reconciliation with Qualification/Privacy. Never expose full legal opinions or sensitive case facts in public status checks.

### Resolved rights, historical status and retention

1. Maintain separate credential-local original issuance fact, historical state timeline, **current** status and **underlying award status** with observed-as-of freshness. A proof valid on a historic date may be currently revoked; an award later overturned is not silently rewritten.
2. Each rights request is validated and routed to the source owner(s). Restrict access while eligibility/hold is assessed. Retain or erase/minimise according to purpose and lawful basis, with appeal/review path; erased plaintext need not remain in an immutable Audit/event payload.
3. Assign retention schedules to **distinct categories** and event triggers, not one period. No arbitrary global 'keep indefinitely', no fabricated statutory period. Legal Compliance supplies independently reviewed schedules, Privacy applies data-rights disposition, Credentials executes within its custody.
4. Minors, guardian representation, safeguarding and special-category data require explicit verified authority and risk-scoped disclosure, not universal blanket parental consent.
5. Cross-border processing/relying-party access is a distinct decision; absence of validated transfer basis or binding local restriction blocks the affected sharing while permitting independently lawful local operation.
6. Fraud, compromised signing keys, erroneous awards, issuer withdrawal and scheme closure require attributable containment/recovery and appeal; revocation cannot be undone by replay.
7. Report uncertainty and source unavailability explicitly. No automatically permissive status, proof or disclosure when a mandatory policy is absent, stale, or disputed. A policy expiry/revision triggers targeted re-evaluation; historical policies remain attributable.

### Jurisdiction examples, not universally imposed rules

| Area | External framework and scope question | Required handling |
|---|---|---|
| UK general / employment / education | UK GDPR and Data Protection Act 2018, ICO retention/erasure guidance, applicable sector laws | Purpose- and category-specific retention; access, erasure exemptions, safeguarding, notices and transfer basis determined by Privacy/Legal Compliance, not assumed universal |
| UK regulated identity verification | UK DVS trust framework v1.0 and certification scheme **where the operator actually performs in-scope certified DVS functions** | Assess statutory applicability and certification separately; a signed credential is not a UK DVS certification |
| EU | GDPR, eIDAS as amended by EU 2024/1183, EUDI/EAA implementing rules for in-scope actors | Regulated EU credential/wallet format, qualified issuer requirements, relying-party duties and lawful recognition handled by mapped policy, not inferred from W3C conformance |
| Regulated professions / public registers / international cases | Actual competent licence body, awarding register and national/industry requirements | Verifiable original authority, recognition, retention/withdrawal and time-of-use limitations before claim presentation |

### Closure tests

- UK employee training credential at termination: retain only according to category policy; no invented UK five/seven-year default; lawful request yields explicit retain/erase/restrict decision.
- Different issuer and relying-party jurisdictions: do not conflate jurisdictions; evaluate conflicting applicable disclosure and transfer rules; fail safely if undetermined.
- Qualification revoked after issued credential: preserve time-qualified provenance; apply source decision update to credential status with accountable correction and verifier status.
- Child's achievement: verify authorised guardian where required; disclose only minimum and protect from public discovery.
- Offline proof with stale status: cryptographic authenticity may succeed; current standing unknown and high-risk acceptance denied until rechecked.
- Mandatory preservation versus erasure: apply legally supported hold and minimise all other retained material; expose rights outcome and appeal.
- External holder export and cached PDF: prevent false assumption all distributed copies can be recalled; rely on signed status references, notices and lawful export.
- Policy changes after historic decision: preserve historical applied version, evaluate new action under current policy, no automatic retroactive claim of invalidity.
- Unavailable Privacy/Legal Compliance decision: affected legally sensitive action held; other safe permitted capabilities can operate where separately authorised.

**CRED-18 closure condition:** These architectural boundaries, contracts, modes and acceptance criteria are sufficiently defined for the conceptual review. The continuing work is deployment/issuer/sector-specific legally reviewed policy schedules and provider integration, which are explicit configuration/acceptance prerequisites, **not evidence that all jurisdictions are compliant**. No new dedicated country-law engine or generic policy capability is justified.

**Authoritative legal guidance**:
- ICO retention: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-protection-principles/a-guide-to-the-data-protection-principles/storage-limitation/
- ICO erasure: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/individual-rights/right-to-erasure/
- ICO purpose limits: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-protection-principles/a-guide-to-the-data-protection-principles/purpose-limitation/
- ICO transfers: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/international-transfers/a-guide-to-international-transfers/what-are-our-other-key-uk-gdpr-obligations-in-the-context-of-international-transfers/
- EU amendment: https://eur-lex.europa.eu/eli/reg/2024/1183/oj


## Final owner decision — 18 November 2026

**Approved:** CRED-17A–H exactly as the standards-profile architecture above; CRED-18 approved and **closed at conceptual architecture level**. Earlier 'owner confirmation pending' labels in the historical decision matrix are superseded. Selected exact key algorithms/crypto suites and interop test evidence remain implementation acceptance, not a new conceptual decision. Per-jurisdiction legal mapping, schedules, scheme-specific conformance and regulatory certification remain mandatory documented deployment prerequisites, not a claim of existing compliance.
