# Recruitment — control traceability register

**Status:** Conceptual design traceability, consolidated 21 November 2026. REC-01–15 and STD-A–F were owner-approved 20 November 2026. This register maps *design obligations* to evidence and **does not assert external legal applicability, implementation completion, independent conformity assessment or certification**. [Canonical Recruitment capability](../docs/capabilities/recruitment/capability-record.md) · [Standards assessment](recruitment-standards-assessment.md) · [Conceptual acceptance review](recruitment-acceptance-and-consistency-review.md).

## Interpretation and applicability

- **G** = governing platform baseline (accepted ADR/Capability Standard).
- **L** = jurisdiction-/activity-/effective-date-dependent law or regulator duty. Legal Compliance must resolve applicability and law version before enforcement.
- **D** = owner-adopted conceptual design principle supported by voluntary standard or professional guidance; voluntary source is not itself mandatory law.
- **C** = conditional integration/AI interoperability profile; applicable when enabled and selected.
- Each row explicitly specifies owner, input/public output surface, guard/evidence and observable conceptual acceptance. Source version and law effective dates belong in Legal Compliance policy references; do not duplicate legal interpretation as Recruitment master data.
- `R-IN-` and `R-OUT-` refer to **idealised business interfaces**, not deployed endpoints; reference `S-` acceptance scenarios in the companion review.

## End-to-end control mapping

| ID / adopted decision | Standard / law and status | Source owner → Recruitment interface → consumer | Guard, evidence and negative/uncertain result | Acceptance |
|---|---|---|---|---|
| T-01 REC-01/02 | ADR-0001/0002; Capability Standard **G** | Job/Finance → R-IN-01/02 → R-OUT-01 | Separate requisition, opening, campaign, application and position identifiers and revisions; no fictitious vacancy authority | S-01, S-03 |
| T-02 REC-11 | ISO 30409:2016 **D**; delegated mandate rules **L** | Establishment/Finance → R-IN-01 → R-OUT-01 | Scope-limited, unexpired opening authorisation with actual funding/seat owner; deny absent mandate | S-01, S-02 |
| T-03 REC-03 | ADR-0009/0012 **G**; ISO 30405:2023 **D** | Native recruiter/applicant → R-IN-03 → R-OUT-03 | Manual intake and recorded selection without external ATS, Job or board; no auto-authorised vacancy | S-01, S-04 |
| T-04 REC-04/14 | UK/EU GDPR as applicable **L**; ISO/IEC 27701:2025 **D** | Candidate/Privacy → R-IN-03/09 → R-OUT-03/07 | Purpose, controller, restricted tenant grants, provenance and sharing authority; deny unrelated employer access | S-05, S-06 |
| T-05 REC-05/12 | Employment agreement law **L**; ADR-0012 **G** | Recruitment offer → R-IN-08/R-OUT-05 → Employment | Separate selection, offer, acceptance and independently evidenced agreement/engagement; unknown handover not active | S-07 |
| T-06 REC-06 | schema.org/JobPosting **C**; ISO 30405 **D** | Recruitment R-OUT-02 → Publisher/Integrations/board → R-IN-07 | Approved disclosure and pay fields as applicable; provider ACK ≠ confirmed publication | S-08 |
| T-07 REC-07 | ADR-0012/Capability Standard **G** | Recruitment R-OUT-08 → Message Queue/subscribers | Own committed durable outbox, idempotency, replay-safe subscriber, versioned events with restricted identifiers | S-09 |
| T-08 REC-08 | Equality Act 2010/territorial equivalents **L**; ISO 30415 **D** | Legal Compliance/Assessment → R-IN-04/05 → R-OUT-04 | Job-related, fair, accessible and reviewable criteria; unsupported discriminatory criterion blocked | S-10 |
| T-09 REC-09 | ADR-0012/ASVS **G**; ISO 27001 **D** | Recruitment → R-OUT-04/07/08 → Audit/Logging/Reporting | Audit evidence vs sanitised diagnostics vs authorised aggregate corrections; never log dossier | S-11 |
| T-10 REC-10/STD-C | WCAG 2.2 AA/BCP 47/CLDR/ECMA-402 **G** | Candidate/recruiter GUI → R-IN-03/09 → R-OUT-03/07 | Keyboard/screenreader/error recovery/accessibility alternative and zone-correct dates | S-12 |
| T-11 REC-13 | HR Open Standards interchange **C** | ATS via Integrations → R-IN-03/07 → R-OUT-03/09 | One designated authority per fact and scope, mapping revision, signed origin, conflicting remote data remains disputed | S-13 |
| T-12 REC-15/STD-B | UK GDPR amended by DUAA 2025 / EU GDPR / EU AI Act where applicable **L** | Legal Compliance/Configuration/assessment provider → R-IN-04/05 → R-OUT-04 | No universal automation prohibition; explicit lawful basis/conditions, intervention and contest safeguards; default human control | S-14 |
| T-13 STD-A | ISO 37301:2021 **D**, applicable employment/privacy law **L** | Legal Compliance → R-IN-04/09 → guarded commands | Effective-time, jurisdiction, role and legal-source version, deny/indeterminate if mandatory source unavailable | S-02, S-15 |
| T-14 STD-A | OWASP ASVS 5.0 L2 / heightened L3 **G** | Identity/Authentication/Authorisation → R-IN-04 → all R-OUT | Resource/field-level permission, assurance and delegation; event never grants access | S-05, S-16 |
| T-15 STD-A | ISO 30408:2016 **D** | HR/Finance approvers → R-IN-01 → R-OUT-01 | Separation of duties, approval provenance, recusal, revision/effective validity; reject self-approved invalid mandate | S-02 |
| T-16 STD-B | ISO 10667-1/-2:2020 **D** | Assessment/qualified provider → R-IN-05 → R-OUT-04 | Method relevance/validity/limitations, qualified evaluator and assessment source revision; stale evidence review | S-10, S-17 |
| T-17 STD-B | ISO 30415:2021; SIOP/APA Principles (2018) **D** | Job criteria/panel → R-IN-02/05 → R-OUT-04 | Approved structured rubric, reasons, conflicts, corrections, non-comparable scores not collapsed | S-10, S-18 |
| T-18 STD-B/REC-15 | ISO/IEC 42001:2023/23894:2023; NIST AI RMF **C** | AI provider/model registry → R-IN-05 → R-OUT-04 | Model/dataset version, fairness validation, human oversight, re-evaluation and appeal evidence | S-14 |
| T-19 STD-C | ISO 30405:2023; ISO/IEC 30071-1:2019 **D** | Candidate → R-IN-03/06 → R-OUT-03/06 | Accessible CV alternative, appropriate notices, communication preference and independent delivery receipt | S-12, S-19 |
| T-20 STD-C | Equality Act 2010 and equivalents **L** | Candidate accessibility request → R-IN-06/09 → case-visible restricted action | Adjustments separate from panel scoring and special-category data; reasonable route and confidential disclosure | S-12 |
| T-21 STD-C | UK/EU GDPR candidate rights **L** | Candidate/Privacy → R-IN-09 → R-OUT-07 | Authorised access, correction, withdrawal, contest, appeal and statutory timelines; no automatic erasure promises | S-06, S-20 |
| T-22 STD-D | ISO 15489-1:2016 **D** | Recruitment/Storage → R-IN-03/05/09 → R-OUT-07 | Provenance, integrity, case chronology, revisions, disposition evidence and bounded retention | S-21 |
| T-23 STD-D | UK/EU GDPR/ICO recruitment retention where applicable **L** | Privacy/Legal Compliance → R-IN-09 → R-OUT-07/08 | Data-category purpose/legal basis, deadline, storage and sharing, hold precedence; record deferred deletion | S-21 |
| T-24 STD-D | ISO/IEC 27001/27002; ASVS **D/G** | Files/Storage/Content Security → R-IN-03/05 → authorised case reads | Safe attachment intake, content scanning, encrypted storage ports, access logs, malicious upload quarantine | S-22 |
| T-25 STD-E | HR Open Standards approved version at integration time **C** | ATS/Integrations → R-IN-03/07 → R-OUT-09 | Explicit source-to-canonical field map and schema version, invalid mapping rejected/quarantined | S-13 |
| T-26 STD-E | schema.org/JobPosting **C** | Recruitment R-OUT-02 → Publisher/Search | Redacted approved advert version, pay/transparency check, lifecycle withdrawal/expiry propagation | S-08 |
| T-27 STD-E | OpenAPI/JSON Schema where HTTP selected **C** | Public host adapters → R-IN-01…10/R-OUT-01…09 | Validated versioned request/result, backwards compatibility, no leaked provider SDK or private schema | S-23 |
| T-28 STD-E | W3C VC Data Model / OpenID4VP where selected **C** | Verification/Qualification → R-IN-05 → R-OUT-04 | Scope/issuer/subject, validity/expiry/revocation/unknown; credential alone not employment eligibility | S-17 |
| T-29 STD-F | ADR-0012 and Capability Standard **G** | Capability owner → all public surfaces | Every standard requirement linked to owner, validation, evidence and acceptance; no invented runtime proofs | S-23 |
| T-30 STD-F | ISO/IEC 25010:2023 **D** | Host/GUI/Reporting → authorised read projections | Performance, resilience, accessibility, maintainability and freshness envelope; measured at later acceptance | S-12, S-24 |
| T-31 UK right-to-work | Home Office employer guidance, immigration law **L** | Verification/right-to-work source → R-IN-05/08 → Employment | Applicable role/employee check evidence and time; conditional or unknown cannot become cleared | S-07, S-17 |
| T-32 EU pay transparency | Directive 2023/970 and national implementation **L** | Legal Compliance/Job/Finance → R-IN-02/04 → R-OUT-02 | Applicable pay/range disclosure, neutral advert and salary-history restrictions; avoid hard-coded cross-border rule | S-08, S-15 |
| T-33 US hiring law | EEOC Title VII/ADA/ADEA and relevant state law **L** | Legal Compliance/Assessment → R-IN-04/05 → R-OUT-04 | Job-related selection validation and local disparate-impact/accommodation requirements | S-10, S-14 |
| T-34 Sector checks | Local safeguarding, DBS, vetting, regulated occupations **L** | Legal Compliance/Verification → R-IN-04/05 → R-OUT-04/05 | Role- and country-scoped checks, no speculative blanket health/criminal history collection | S-17 |
| T-35 Cross-border/agency | UK/EU GDPR transfers and controller arrangements as applicable **L** | Agency/Federation/Privacy → R-IN-03/04/09 → R-OUT-03/07 | Explicit mandate, destination, transfer controls, purpose and data subject rights; deny absent lawful disclosure | S-06 |
| T-36 Recovery and time | ADR-0012; Clock standards **G** | Clock/Workflow/Scheduler/Message Queue → R-IN-06/07 → R-OUT-08/09 | Effective/observed timestamps, monotonic revisions, retries, safe replay, dead letters and manually reconcilable unknown | S-09, S-25 |
| T-37 Event security | OWASP ASVS / secure webhook guidance **G/C** | Signed third-party provider events via Integrations → R-IN-07 | Trusted provider identity, nonce/idempotency, payload validation, signature, replay expiry, refusal of forgery | S-13, S-22 |
| T-38 Candidate metrics | ISO 30414:2025 **D**; data protection **L** | Recruitment R-OUT-01/03/04 → Reporting | Clearly defined funnel metrics with correction/version and disclosure suppression for small cohorts | S-11, S-24 |

## Traceability completeness and change control

This matrix covers all **15 REC** decisions and all **six STD** areas through T-01–T-38 (some controls intentionally cover multiple decisions). It is comprehensive for the **identified core design requirement classes**, not an assertion that every national/sector law has been catalogued. A new jurisdiction, sector, ATS provider, AI model, statutory change, material ADR change or new candidate-data category triggers a scoped Legal Compliance and domain-control review and appended or revised matrix rows. A law-dependent row is **conditionally binding only once its applicability has been determined by the accountable policy authority**. ISO adoption has not been equated with certification.

Unresolved implementation evidence is tracked separately: actual source licences/versions/SDKs, source-level contract tests, threat modelling, localisation testing, security assessments, legal opinions, deployment and external provider attestations. None are conceptual domain-ownership decisions or reasons to claim implementation already exists.
