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


---

# Legal Compliance — dedicated conceptual review (19 November 2026)

**Status:** Proposed design for owner review; NOT conceptual sign-off, legal advice, verified statutory compliance, approved implementation contract or permission to merge. Opening baseline: governing \`b920ce0d8b361de000a6739a16123dbdc56df7a7\`, blueprint \`6dac83a03da8704f7945ee1bc894f2248300445a\`; [review PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85). Existing earlier reciprocal notes above are retained, and any uncertain approval labels in those notes remain as originally qualified.

## Identity, authority and scope

**Name/path:** \`legal_compliance\` (actual review directory); catalogue display name \`legal-compliance\`. **Class:** Foundation, established by the governing catalogue. **Form:** independently useful headless specialist policy/evidence service, optionally accompanied by separable administration presentation. A Nuxt layer, independent core or deployment choice is an implementation decision, not a new classification.

**Verified evidence:** Accepted ADR-0017 and ADR-0018; normative \`docs/capability-standard.md\`, governing catalogue and existing reciprocal conceptual records. The implementation repository \`nuxt-layers/legal-compliance\` exists, but its \`README.md\` contains only a heading and \`CONTRACT.md\` is absent on \`master\` as inspected on 19 November 2026. Accordingly **no implemented inbound/outbound API, event, store, GUI or legal-rule dataset is verified**. Related conceptual records do not establish implemented contracts.

**Purpose:** Maintain a qualified, dated and scoped account of *which legal obligations and restrictions apply* to an installation, tenant, legal entity, service, activity, audience, record class or transaction, with explicit source/professional-review provenance. Provide trusted *legal constraint and uncertainty results* to the business capabilities responsible for enforcing them, and support review, changes in law, legal holds and lawful release.

**Owns (conceptually):**
- Versioned legal-source references and interpreted obligation records (jurisdiction, territorial reach, relevant enactment/regulator, amendment/effective dates, activity/service and entity predicates, qualified reviewer/authority, confidence and verification evidence).
- Applicability assessments, conflicts, coverage gaps, legal-obligation precedence and explicit \`applicable / not-applicable / unresolved / stale / superseded\` findings; source facts are *inputs*, not certified truth merely because submitted.
- Scoped preservation/legal-hold instruction and release lifecycle: legal basis, requesting competent authority, affected record references/classes, reason, approver, commencement, review date, expiry/termination and verifiable execution acknowledgements. The *domain record* remains with its domain owner.
- Statutory deadline/requirement definitions, compliance action obligation register and fulfilment-evidence references, including missed/contested/review states. Scheduler owns execution; authoritative regulator submissions and business fulfilment remain with their producers.
- Provenance, rule-change impact assessments, legal-review queues, controlled corrections, exceptions and external verification status. Legal Compliance owns its finding/evidence-reference lifecycle, not external court/regulator determinations.

**Does not own:** Authorisation permissions; Privacy's consent/lawful-purpose/personal-data rights and specialist retention policy; Configuration's approved setting values; Identity membership, tenant tree or legal-entity record; formal corporate/beneficial ownership determinations or court adjudication; domain tax calculations, Accounting journals, Invoice issuance, credential issuance, statutory filings, source documents or domain data; Audit tamper-evident evidential history; Logging/Observability; Publisher documents; Workflow approval execution; integrations/provider transport; legal representation or professional certification. **A legally permissible operation is not automatically authorised; an authorised operation is not necessarily legally permissible.**

## Native behaviour, lifecycle and fail-safe principles

1. Register authoritative source and a candidate interpretation with territorial, temporal, regulated-activity, entity/audience and evidential predicates; distinguish enacted requirements from guidance, voluntary standards, contractual terms and internal preferences.
2. Independently review and approve high-consequence interpretations and holds with attributable human-qualified authority and conflict-of-interest/dual-control safeguards where appropriate. Machine-assisted classification may propose but must not self-certify.
3. Activate a verified version only within its scoped effective period; retain prior historical versions for as-of explanations. Future/retroactive legislation is represented with separate enactment, effective, publication/knowledge and assessment times via Clock.
4. Evaluate an authorised, fact-complete request against applicable approved legal rules; return restrictions, permitted conditional paths, notices/deadlines, verification/coverage state and source/version with an explicit consequence for unresolved mandatory requirements.
5. Maintain change-impact and requalification queues when legal sources, supported jurisdiction, regulated-service classification, tenant facts or rules change. Do not silently recompute historical decisions as though newer law applied then.
6. Issue, renew, narrow, dispute and release scoped legal holds; affected domain owners acknowledge actual restriction/preservation and report failures. Release authorisation does not itself execute deletion or erase immutable evidence.
7. Reconcile obligation fulfilment and domain enforcement receipts; distinguish \`decision issued\`, \`action requested\`, \`accepted\`, \`completed\`, \`failed\` and \`provider/regulator outcome unknown\`.
8. Native, offline-from-external-legal-provider operation uses a locally governed, explicitly limited legal-rule corpus with review provenance; without verified coverage, return unresolved rather than asserting a compliant default.

**Rule lifecycle:** sourced → drafted → under qualified review → approved (possibly scheduled) → effective → superseded/withdrawn, with corrected historical provenance. **Hold lifecycle:** requested → authority/evidence validated → authorised → effective/partially enforced → reviewed/extended/disputed → released/expired (subject to lawful authority) → owner-confirmed disposition. Rule status, hold status and actual enforcement status must remain separate.

**Invariant:** No bypass by tenant toggle, host super-admin, untrusted input, external provider outage or a missing mandatory legal rule. Scope and tenant isolation are enforced by server Authorisation and owning services. Do not infer a universal cross-jurisdiction legal answer.

## Idealised public inbound contract (proposed, not implemented)

| Input surface | Source and authoritative facts/intent | Validation; requiredness and absence outcome |
|---|---|---|
| \`qualifyApplicability\` query | Authorised domain/host supplies trusted tenant, affected entity and resource, jurisdictions, place of supply/activity, regulated service classification, audience, purpose, effective/as-of time and decision type; source owners supply underlying facts | **Required for legally gated acts**; validate entity/tenant binding, jurisdiction specificity, trusted provenance, fact revision and effective time; incomplete/contradictory/stale critical facts → \`unresolved\` and hold unsafe action |
| \`registerLegalSource\` / \`proposeInterpretation\` | Qualified curator supplies source identifier, issuing authority, actual legal text/reference, territorial scope, applicability predicates, effective/amendment dates, evidence and draft mapping | Protected write; verify source integrity and provenance, avoid arbitrary code/rule expressions; unverified source remains draft |
| \`review/approve/withdrawInterpretation\` | Separate authorised legal reviewer/approval port provides decision, reasoning, scope/version and conflict declarations | Strong Authentication/Authorisation, reviewer competence, version conflict, self-approval safeguards; missing approval cannot activate critical rule |
| \`request/renew/releaseHold\` | Authorised legal/competent process supplies legal authority, precise records/classes, subject context, restrictions, duration/review, supporting reference and disposition | Narrow scope and legal justification mandatory; requester alone cannot make a disputed or unsupported hold binding; unverifiable release holds preservation pending review |
| \`recordEnforcementOutcome\` | Data-owning capability supplies correlation, applied legal-decision version, affected reference, accepted/completed/refused/partial outcome and evidence pointers | Verify reporting owner, idempotency, relevant revision and no cross-tenant disclosure; receipt never rewrites source-domain truth |
| \`registerRequirementOutcome\` | Domain authority, regulated filing owner or Integrations supplies evidence reference, submission/receipt result, external acknowledgement and current uncertainty | Provider transport success != legal acceptance; unknown provider status stays unknown and is reconciled |
| \`reassessImpact\` / subscribed factual changes | Identity, Configuration, Privacy, site-hosting, domain owners and legal-source review supply authorised relevant updates | Source events are not permission grants; apply ordering/replay protection and re-evaluate only impacted scoped decisions |
| Host-provided ports | Caller/Access decision, Clock, persistence, event outbox, review/workflow and optionally Scheduler/Notifications/Integrations | Capability-owned storage/migrations; required persistence/access absent → fail closed; optional services have explicit manual/no-delivery fallback |

No universal input object is mandated. Each operation carries only necessary trusted context: caller/tenant, subject/resource and source revision, effective/as-of timestamp, rule version, correlation/idempotency and purpose. Avoid collecting personal/sensitive facts when narrow attestations suffice.

## Idealised public outbound contract (proposed, not implemented)

| Output | Consumers | Semantics and guarantees |
|---|---|---|
| \`LegalApplicabilityDecision\` | Accounting, Billing, Invoice, Identity, Publisher, Booking, Marketplace, Moderation, Verification, Credentials, Integrations, domain owners | Scope and time-specific applicable/non-applicable/unresolved/unsupported verdict; mandatory prohibitions/conditions, required disclosures, preservation and reporting, qualified source/reviewer/version, confidence/coverage and \`expiresOrReviewBy\`. Not a domain permission, tax amount, statutory certification or guaranteed external acceptance |
| \`LegalHoldStatus\` | Domain owners, Privacy, Audit, Storage and authorised investigators | Authoritative scoped legal instruction, status/version/review/release, affected record-class/reference; actual preservation/disposal completion belongs to domain/storage owner, evidenced by receipts |
| \`ObligationSchedule\` / \`ComplianceRequirement\` | Scheduler, Workflow, Notifications, Accounting, reporting owners | Obligation identifier, accountable role, deadline/time zone, legal source/version, evidence needed and status; *not* proof of filing or successful notification |
| \`LegalSourceAndCoverage\` | Administrators and bounded policy consumers | Qualified jurisdiction/service/period catalogue; source integrity, verification freshness, limitations, last/next review, gaps or conflicts; historical as-of result retained |
| \`LegalChangeImpact\` | Affected domain owners, Privacy, Configuration and host | Specific impacted activities/rules, future activation, re-review needs and safe transition requirements; no automatic domain mutation |
| \`ComplianceEvidenceReference\` / \`ComplianceReviewOutcome\` | Audit, Reporting, authorised regulators/inspectors via approved owner workflows | Attributable decision/evidence reference, provenance and status, privacy-filtered. Audit independently owns preserved evidence; Reporting independently owns derived reports |
| Committed \`legal.*\` events | Authorised subscribers via capability-owned durable outbox/Message Queue | Version-activated, applicability-requalified, hold-effective/released, impact-raised, requirement-changed, review-completed facts with source-event ID, actor/tenant scope and version; at-least-once consumer tolerance, no claimed global exactly-once delivery |

A query must declare freshness/coverage and not infer \`compliant\` from absence of recorded violations. Separate accepted request from completed enforcement, source knowledge from interpretation, historic judgement from current revision. Results must be authorised, minimised, versioned and safely redact privileged legal advice. Consumers receive stable errors/message keys such as \`LEGAL_SCOPE_UNKNOWN\`, \`LEGAL_EVIDENCE_STALE\`, \`LEGAL_REVIEW_REQUIRED\`, \`LEGAL_CONFLICT\`, \`LEGAL_HOLD_ACTIVE\`, \`LEGAL_AUTHORITY_UNVERIFIED\`, \`LEGAL_PROVIDER_UNCONFIRMED\`; these are conceptual codes only.

## Cooperative ownership and dependency directions

| Cooperating owner | Facts Legal Compliance needs | Legal Compliance returns; enforcement owner |
|---|---|---|
| Identity / IAM Integration / Verification | Tenant/entity identifiers and trusted scoped governance/assurance attestation, verified attributes with provenance; *not* asserted legal directorship by role | Legal authority requirements for governance, age/KYC/KYB, disputes and delegation; Identity owns digital state, Verification owns verification provenance, Authorisation all server access decisions |
| Configuration | Approved tenant/site regulated-activity assertions, location/service settings, effective revision and reviewer provenance | Mandatory scoped floors, restrictions and legal-change impacts; Configuration owns stored settings and domain owners enforce |
| Privacy / Profile | Purpose, data class, applicable processing regime and rights-request context, minimised facts | Qualified statutory constraints and preservation exceptions; Privacy owns consent, specialist rights/retention and acts on requests with source domains |
| Accounting / Billing / Invoice / Payment / Order | Entity/place-of-supply, financial activity, dates, document/class and existing tax/filing reference | Qualified statutory/tax/disclosure/preservation obligation, not tax computation, settlement or actual filing; each financial owner executes its operation |
| Publisher / Media / Comments Engine / Moderation / Content Security / Search / Federation | Service type, audience, regulated activity, jurisdiction, complaint/enforcement facts and original content references | Applicable online-safety/child-protection, accessibility, licensing and reporting constraints; service/domain owner effects takedown, Moderation owns case, detector owns signal |
| Assets / Inventory / Job / Course / Qualifications / Credentials | Relevant asset/activity/workplace/training/claim type, legal-person status and jurisdiction/time | Qualified safety, employment, accreditation, safeguarding, retention and statutory restrictions; source owner applies its own business rules; open Job PR #84 remains provisional |
| Integrations | Provider/jurisdiction, processor/residency/submission route, qualified receipts and external-rule status | Lawful-transfer/filing requirements and holds; Integrations owns connectivity/transport, external authority owns actual decision |
| Audit / Logging / Observability / Reporting | Minimised accountable evidence, diagnostics, health, authorised aggregate requirements | Legal decision and review evidence to Audit; scrubbed operational signals to Logging/Observability; authorised qualified status/reference to Reporting. None become a legal interpretation authority |
| Clock / Scheduler / Workflow / Notifications / Message Queue | Effective temporal semantics, triggers, task receipts, approval/notice delivery status and committed event transport | Deadlines, review triggers, change events and approvals to be executed; no duplicate scheduling, approval or delivery ownership |
| Storage / domain stores | Verified records/retention-class references and preservation enforcement receipts | Scoped hold/transfer/disposal constraints; each data owner owns actual record, bytes and backup deletion/disposition |

**Direct dependency caution:** all rows describe *public information exchange*, not mandatory package imports. Host/integration composition may provide ports to prevent cycles. Required: trustworthy access context, Clock semantics for temporal decisions, versioned law/evidence corpus and capability-owned persistence for qualified state. Optional: provider lookups, electronic filing, notifications and automated legal-change feeds. If a mandatory rule cannot be established, refuse the relevant high-risk operation instead of treating an unavailable optional provider as legal clearance.

## Security, legal authority and external standards

Risk: fabricated legal citations, outdated law, conflicted human approvers, forged regulator demands, cross-tenant leakage, privileged legal data disclosure, rule poisoning, overbroad indefinite holds, unlawful erasure, uncertain provider transmissions, prompt-injection through legal-source documents, and confused-deputy bypass between legal/permission decisions. Protect source supply chains; use least privilege, review separation, qualified evidence and independent audit. Legal-source ingestion is untrusted content; no automatic rule execution. Host operator cannot use a universal god-role to view tenant legal evidence.

Follow governing OWASP ASVS 5 Level 2 (appropriate Level 3 for sensitive operations), WCAG 2.2 AA, ADR-0012 composition and durable outbox, ADR-0016 acyclicity and ADR-0017/0018 protection. As applicable, consult **primary legislation and live regulator guidance**, including UK GDPR/Data Protection Act guidance from ICO, Online Safety Act and Ofcom service-specific guidance, and applicable EU/other-jurisdiction instruments. ISO 37301 (compliance management), ISO 31000 (risk), ISO 27001/27701 (security/privacy management), and W3C accessibility norms are *reference frameworks*, not an automatic compliance badge or runtime dependency. Dates and regulatory definitions must be validated per deployment; never hard-code universal effective dates or retention periods. A qualified solicitor/regulatory specialist remains accountable for professional legal determinations.

## Presentation, navigation and headless operation

**Recommended optional admin interface**, not public consumer screens or an implemented route. Host-owned sidebar \`Capabilities → Legal Compliance\` opens a capability dashboard in the application shell; only separately authorised compliance officers/legal reviewers can see relevant records. Tenant owner and operational administrator status alone does not grant legal-case or cross-tenant access. Independent host super-admin cannot silently bypass tenant confidentiality.

- **Overview:** jurisdiction/service coverage, unresolved duties, legal changes, critical holds, deadlines, review backlog, decision health and data-source freshness.
- **Applicable law:** source register, effective periods, affected services/tenants, applicability explanation, version history, reviewer/approval trail.
- **Obligation register:** deadlines, accountable owner, evidence references, status and discrepancies; links to underlying source capabilities rather than editable copies.
- **Legal holds:** narrow target and legal basis, approvals, propagation receipts, time-limited review, disputes, release and incomplete enforcement warnings.
- **Review queue:** disputed/missing evidence, change impact, draft interpretations, dual approval, legal-assistance escalation and compare historical versions.
- **Settings/integration status:** supported jurisdictions, qualification providers, source-sync health and permitted tenant assertions; no editable bypass of statutory requirements.

Use task-focused language for non-specialist operators: the affected domain presents a simple contextual \`Action blocked / review needed\` reason and safe escalation, *not* a legal-compliance dashboard. Theme Manager semantic tokens, \`ui\`, keyboard/screen-reader support, responsive presentation, localisation without losing authoritative language, WCAG 2.2 AA and clear unknown/degraded status. Separate headless mode remains fully capable of all core legal decisions/holds; host owns routing/navigation and the representative test host is \`nuxt-layers-test/application-test-template\` (no edits).

## Conceptual acceptance examples (not executed tests)

| Input | Expected behaviour/output | Authoritative owner |
|---|---|---|
| Qualified UK service, valid effective rule, approved legal facts | Versioned applicable restriction with legal source and review provenance | Legal Compliance interprets; domain owner enforces |
| Unsupported jurisdiction or missing service classification | \`unresolved\`; legally gated action held, review requested | Legal Compliance; affected domain refuses |
| Prior historical invoice date queried after rule amendment | As-of determination cites historical version, not current version by substitution | Legal Compliance; Invoice owns original document |
| Forged/overbroad regulator hold or unauthorised requester | Reject or hold pending qualified validation; no unrestricted tenant-wide seizure | Legal Compliance; Authorisation decides caller rights |
| Approved hold, domain partial preservation failure | Hold stays effective and enforcement incomplete with reconciled failure/alert | Legal Compliance owns hold; source domain owns physical disposition |
| Release of lawful hold while other retention duty persists | Release this hold only; other restrictions stay, no automatic deletion | Legal Compliance / Privacy / source owner |
| Replayed source event or duplicate enforcement receipt | Idempotent handling with original authoritative receipt and no duplicate legal effect | Legal Compliance |
| Provider confirms transmission but regulator never accepts filing | \`submitted / acceptance unknown\`; no claim of statutory completion | Integrations transport; legal requirement and domain filing owner |
| One person in two tenants requests unrelated legal dossier | Server denies cross-tenant access even if host operator or parent tenant | Authorisation; Legal Compliance scopes data |
| Change of law conflicts with tenant setting | Mandatory approved legal floor prevails; unsafe action held pending review | Legal Compliance qualifies; Configuration and domain enforce |
| Privileged advice shown to an ordinary operator | Minimal safe reason only, no underlying confidential case text | Legal Compliance output policy, Authorisation |
| Provider unavailable / source rule stale | Verified still-current local source may be used within qualification limits; else unresolved | Legal Compliance |

## Decision register and handover

**Established:** Foundation boundary; statutory applicability/effective scope; Legal Compliance distinct from Privacy, Authorisation and business enforcement; approved ADR-0017/0018; server-side permission checks, headless composition and published contract requirement.

**Agreed prior direction:** Existing reciprocal notes describing qualified constraints and per-domain enforcement are preserved as scoped historical conceptual directions; they do not constitute a completed legal-compliance contract.

**Proposed for owner approval:**
- **LC-01** Versioned, reviewer-qualified source/applicability/coverage register and explicitly unresolved jurisdiction/service results; default no universal legal conclusion.
- **LC-02** Legal Compliance owns scope/version/authority of holds, with actual preservation and disposal remaining with each owning domain; dual-controlled high-risk issuance/release and meaningful review expiry.
- **LC-03** Standardised business-meaning legal decision, hold, obligation, provenance and enforcement-receipt surfaces; domains fail closed on unresolved *mandatory* legal conditions, without blocking legally unrelated activities.
- **LC-04** Core local/offline operation with qualified source corpus; optional legal data providers are evidence feeds, never automatic authority; professional review remains necessary for high-risk determinations.
- **LC-05** Optional role-restricted GUI plus fully headless contract; host-owned navigation and server-side access; clear simple operator messaging and professional reviewer workflows.
- **LC-06** Independent owner for external formal legal-entity/control adjudication and governing-instrument lifecycle remains a **separate boundary decision**, not silently assigned to Legal Compliance. Legal Compliance consumes validated authority evidence and qualifies its legal consequences.
- **LC-07** Privacy's specialist lawful-purpose/consent/rights/retention policies and Legal Compliance's statutory qualification/holds must expose a conflict-resolution handshake without inventing a third policy authority.

**Open design/qualification questions:** exact competent-reviewer accreditation and delegation scheme per jurisdiction; legal-text licensing and authoritative source update supply; statutory reporting owners and filing-specific tax decision boundaries; conflicting multi-country laws/territorial nexus and appeal/override process; records-of-processing responsibility and jurisdictional legal-entity master; external legal counsel privileged material handling; jurisdictional minimum coverage to claim operational support. These require explicit supported-scope decisions and specialist validation rather than speculative universal laws.

**Implementation alignment:** develop/approve actual root \`CONTRACT.md\`, validated API shapes/errors, security threat model, store/outbox/retention ownership, host composition and acceptance evidence separately. **No implemented contract or legal certification claimed.** The blueprint review may be considered conceptually complete only after owner resolution of LC-01–07 and consistency review; no merge without explicit approval.
