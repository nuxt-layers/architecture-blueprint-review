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

**Status:** Proposed design for owner review; NOT conceptual sign-off, legal advice, verified statutory compliance, approved implementation contract or permission to merge. Opening baseline: governing `b920ce0d8b361de000a6739a16123dbdc56df7a7`, blueprint `6dac83a03da8704f7945ee1bc894f2248300445a`; [review PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85). Existing earlier reciprocal notes above are retained, and any uncertain approval labels in those notes remain as originally qualified.

## Identity, authority and scope

**Name/path:** `legal_compliance` (actual review directory); catalogue display name `legal-compliance`. **Class:** Foundation, established by the governing catalogue. **Form:** independently useful headless specialist policy/evidence service, optionally accompanied by separable administration presentation. A Nuxt layer, independent core or deployment choice is an implementation decision, not a new classification.

**Verified evidence:** Accepted ADR-0017 and ADR-0018; normative `docs/capability-standard.md`, governing catalogue and existing reciprocal conceptual records. The implementation repository `nuxt-layers/legal-compliance` exists, but its `README.md` contains only a heading and `CONTRACT.md` is absent on `master` as inspected on 19 November 2026. Accordingly **no implemented inbound/outbound API, event, store, GUI or legal-rule dataset is verified**. Related conceptual records do not establish implemented contracts.

**Purpose:** Maintain a qualified, dated and scoped account of *which legal obligations and restrictions apply* to an installation, tenant, legal entity, service, activity, audience, record class or transaction, with explicit source/professional-review provenance. Provide trusted *legal constraint and uncertainty results* to the business capabilities responsible for enforcing them, and support review, changes in law, legal holds and lawful release.

**Owns (conceptually):**
- Versioned legal-source references and interpreted obligation records (jurisdiction, territorial reach, relevant enactment/regulator, amendment/effective dates, activity/service and entity predicates, qualified reviewer/authority, confidence and verification evidence).
- Applicability assessments, conflicts, coverage gaps, legal-obligation precedence and explicit `applicable / not-applicable / unresolved / stale / superseded` findings; source facts are *inputs*, not certified truth merely because submitted.
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
7. Reconcile obligation fulfilment and domain enforcement receipts; distinguish `decision issued`, `action requested`, `accepted`, `completed`, `failed` and `provider/regulator outcome unknown`.
8. Native, offline-from-external-legal-provider operation uses a locally governed, explicitly limited legal-rule corpus with review provenance; without verified coverage, return unresolved rather than asserting a compliant default.

**Rule lifecycle:** sourced → drafted → under qualified review → approved (possibly scheduled) → effective → superseded/withdrawn, with corrected historical provenance. **Hold lifecycle:** requested → authority/evidence validated → authorised → effective/partially enforced → reviewed/extended/disputed → released/expired (subject to lawful authority) → owner-confirmed disposition. Rule status, hold status and actual enforcement status must remain separate.

**Invariant:** No bypass by tenant toggle, host super-admin, untrusted input, external provider outage or a missing mandatory legal rule. Scope and tenant isolation are enforced by server Authorisation and owning services. Do not infer a universal cross-jurisdiction legal answer.

## Idealised public inbound contract (proposed, not implemented)

| Input surface | Source and authoritative facts/intent | Validation; requiredness and absence outcome |
|---|---|---|
| `qualifyApplicability` query | Authorised domain/host supplies trusted tenant, affected entity and resource, jurisdictions, place of supply/activity, regulated service classification, audience, purpose, effective/as-of time and decision type; source owners supply underlying facts | **Required for legally gated acts**; validate entity/tenant binding, jurisdiction specificity, trusted provenance, fact revision and effective time; incomplete/contradictory/stale critical facts → `unresolved` and hold unsafe action |
| `registerLegalSource` / `proposeInterpretation` | Qualified curator supplies source identifier, issuing authority, actual legal text/reference, territorial scope, applicability predicates, effective/amendment dates, evidence and draft mapping | Protected write; verify source integrity and provenance, avoid arbitrary code/rule expressions; unverified source remains draft |
| `review/approve/withdrawInterpretation` | Separate authorised legal reviewer/approval port provides decision, reasoning, scope/version and conflict declarations | Strong Authentication/Authorisation, reviewer competence, version conflict, self-approval safeguards; missing approval cannot activate critical rule |
| `request/renew/releaseHold` | Authorised legal/competent process supplies legal authority, precise records/classes, subject context, restrictions, duration/review, supporting reference and disposition | Narrow scope and legal justification mandatory; requester alone cannot make a disputed or unsupported hold binding; unverifiable release holds preservation pending review |
| `recordEnforcementOutcome` | Data-owning capability supplies correlation, applied legal-decision version, affected reference, accepted/completed/refused/partial outcome and evidence pointers | Verify reporting owner, idempotency, relevant revision and no cross-tenant disclosure; receipt never rewrites source-domain truth |
| `registerRequirementOutcome` | Domain authority, regulated filing owner or Integrations supplies evidence reference, submission/receipt result, external acknowledgement and current uncertainty | Provider transport success != legal acceptance; unknown provider status stays unknown and is reconciled |
| `reassessImpact` / subscribed factual changes | Identity, Configuration, Privacy, site-hosting, domain owners and legal-source review supply authorised relevant updates | Source events are not permission grants; apply ordering/replay protection and re-evaluate only impacted scoped decisions |
| Host-provided ports | Caller/Access decision, Clock, persistence, event outbox, review/workflow and optionally Scheduler/Notifications/Integrations | Capability-owned storage/migrations; required persistence/access absent → fail closed; optional services have explicit manual/no-delivery fallback |

No universal input object is mandated. Each operation carries only necessary trusted context: caller/tenant, subject/resource and source revision, effective/as-of timestamp, rule version, correlation/idempotency and purpose. Avoid collecting personal/sensitive facts when narrow attestations suffice.

## Idealised public outbound contract (proposed, not implemented)

| Output | Consumers | Semantics and guarantees |
|---|---|---|
| `LegalApplicabilityDecision` | Accounting, Billing, Invoice, Identity, Publisher, Booking, Marketplace, Moderation, Verification, Credentials, Integrations, domain owners | Scope and time-specific applicable/non-applicable/unresolved/unsupported verdict; mandatory prohibitions/conditions, required disclosures, preservation and reporting, qualified source/reviewer/version, confidence/coverage and `expiresOrReviewBy`. Not a domain permission, tax amount, statutory certification or guaranteed external acceptance |
| `LegalHoldStatus` | Domain owners, Privacy, Audit, Storage and authorised investigators | Authoritative scoped legal instruction, status/version/review/release, affected record-class/reference; actual preservation/disposal completion belongs to domain/storage owner, evidenced by receipts |
| `ObligationSchedule` / `ComplianceRequirement` | Scheduler, Workflow, Notifications, Accounting, reporting owners | Obligation identifier, accountable role, deadline/time zone, legal source/version, evidence needed and status; *not* proof of filing or successful notification |
| `LegalSourceAndCoverage` | Administrators and bounded policy consumers | Qualified jurisdiction/service/period catalogue; source integrity, verification freshness, limitations, last/next review, gaps or conflicts; historical as-of result retained |
| `LegalChangeImpact` | Affected domain owners, Privacy, Configuration and host | Specific impacted activities/rules, future activation, re-review needs and safe transition requirements; no automatic domain mutation |
| `ComplianceEvidenceReference` / `ComplianceReviewOutcome` | Audit, Reporting, authorised regulators/inspectors via approved owner workflows | Attributable decision/evidence reference, provenance and status, privacy-filtered. Audit independently owns preserved evidence; Reporting independently owns derived reports |
| Committed `legal.*` events | Authorised subscribers via capability-owned durable outbox/Message Queue | Version-activated, applicability-requalified, hold-effective/released, impact-raised, requirement-changed, review-completed facts with source-event ID, actor/tenant scope and version; at-least-once consumer tolerance, no claimed global exactly-once delivery |

A query must declare freshness/coverage and not infer `compliant` from absence of recorded violations. Separate accepted request from completed enforcement, source knowledge from interpretation, historic judgement from current revision. Results must be authorised, minimised, versioned and safely redact privileged legal advice. Consumers receive stable errors/message keys such as `LEGAL_SCOPE_UNKNOWN`, `LEGAL_EVIDENCE_STALE`, `LEGAL_REVIEW_REQUIRED`, `LEGAL_CONFLICT`, `LEGAL_HOLD_ACTIVE`, `LEGAL_AUTHORITY_UNVERIFIED`, `LEGAL_PROVIDER_UNCONFIRMED`; these are conceptual codes only.

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

**Recommended optional admin interface**, not public consumer screens or an implemented route. Host-owned sidebar `Capabilities → Legal Compliance` opens a capability dashboard in the application shell; only separately authorised compliance officers/legal reviewers can see relevant records. Tenant owner and operational administrator status alone does not grant legal-case or cross-tenant access. Independent host super-admin cannot silently bypass tenant confidentiality.

- **Overview:** jurisdiction/service coverage, unresolved duties, legal changes, critical holds, deadlines, review backlog, decision health and data-source freshness.
- **Applicable law:** source register, effective periods, affected services/tenants, applicability explanation, version history, reviewer/approval trail.
- **Obligation register:** deadlines, accountable owner, evidence references, status and discrepancies; links to underlying source capabilities rather than editable copies.
- **Legal holds:** narrow target and legal basis, approvals, propagation receipts, time-limited review, disputes, release and incomplete enforcement warnings.
- **Review queue:** disputed/missing evidence, change impact, draft interpretations, dual approval, legal-assistance escalation and compare historical versions.
- **Settings/integration status:** supported jurisdictions, qualification providers, source-sync health and permitted tenant assertions; no editable bypass of statutory requirements.

Use task-focused language for non-specialist operators: the affected domain presents a simple contextual `Action blocked / review needed` reason and safe escalation, *not* a legal-compliance dashboard. Theme Manager semantic tokens, `ui`, keyboard/screen-reader support, responsive presentation, localisation without losing authoritative language, WCAG 2.2 AA and clear unknown/degraded status. Separate headless mode remains fully capable of all core legal decisions/holds; host owns routing/navigation and the representative test host is `nuxt-layers-test/application-test-template` (no edits).

## Conceptual acceptance examples (not executed tests)

| Input | Expected behaviour/output | Authoritative owner |
|---|---|---|
| Qualified UK service, valid effective rule, approved legal facts | Versioned applicable restriction with legal source and review provenance | Legal Compliance interprets; domain owner enforces |
| Unsupported jurisdiction or missing service classification | `unresolved`; legally gated action held, review requested | Legal Compliance; affected domain refuses |
| Prior historical invoice date queried after rule amendment | As-of determination cites historical version, not current version by substitution | Legal Compliance; Invoice owns original document |
| Forged/overbroad regulator hold or unauthorised requester | Reject or hold pending qualified validation; no unrestricted tenant-wide seizure | Legal Compliance; Authorisation decides caller rights |
| Approved hold, domain partial preservation failure | Hold stays effective and enforcement incomplete with reconciled failure/alert | Legal Compliance owns hold; source domain owns physical disposition |
| Release of lawful hold while other retention duty persists | Release this hold only; other restrictions stay, no automatic deletion | Legal Compliance / Privacy / source owner |
| Replayed source event or duplicate enforcement receipt | Idempotent handling with original authoritative receipt and no duplicate legal effect | Legal Compliance |
| Provider confirms transmission but regulator never accepts filing | `submitted / acceptance unknown`; no claim of statutory completion | Integrations transport; legal requirement and domain filing owner |
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

**Implementation alignment:** develop/approve actual root `CONTRACT.md`, validated API shapes/errors, security threat model, store/outbox/retention ownership, host composition and acceptance evidence separately. **No implemented contract or legal certification claimed.** The blueprint review may be considered conceptually complete only after owner resolution of LC-01–07 and consistency review; no merge without explicit approval.

## User-driven operation and human approval worklists — 20 November 2026

**Status:** Proposed design exploration for LC-01–LC-07, not owner-approved or an implemented GUI/API. This section refines the preceding contract without replacing its decision status. **Current blueprint baseline checked:** `d39df23e087cd0510c82ba2cea78996c7624850f` (advanced since opening `6dac83a03da8704f7945ee1bc894f2248300445a`); changes from parallel reviews must be reconciled before merge.

### Human roles, everyday expectations and bounded access

| User/persona | Job they need to accomplish | Default interface |
|---|---|---|
| Organisation administrator | Declare accurately what the organisation does and where; see requirements and restricted activities, assign the right specialists | Context/onboarding wizard, obligations overview; cannot self-certify legal conclusions |
| Compliance officer | Maintain responsibility for requirements, review evidence, escalate uncertainty and follow up outstanding work | Obligation worklist, source register, reviews and exceptions |
| Qualified legal reviewer | Check sources, territorial/service applicability, effective dates and justification, then approve/reject or request evidence | Privileged legal review workspace, version comparison and sign-off |
| Business/domain operator | Understand what action is blocked/conditional and how to remedy it without seeing privileged legal advice | Contextual result in the source capability, not a compulsory legal console |
| Records manager | Apply appropriately scoped preservation, identify affected systems, and confirm actual completion/disposition | Hold administration, per-source enforcement receipts |
| Auditor / regulator liaison | Trace decision provenance and evidence, distinguish unverified from accepted and completed outcomes | Authorised as-of query/export through Audit/Reporting and originating domain |
| Platform operator | Diagnose rule-engine availability and safe coverage without cross-tenant access to case details | Operational status, not confidential dossiers |
| Automated business capability | Ask a precise question before a legally significant operation and apply returned constraints | Headless, versioned decision query and result/reporting contract |

**Design objective:** Ordinary users provide business facts and act on plain-language, supported outputs. Specialists qualify the legal significance. Do not require every tenant to employ its own lawyer as a platform account; allow appropriately evidenced external professional review, controlled central review or expressly unsupported regulated operations. An empty rule set is **not** a declaration of compliance.

### Worklist versus Workflow versus Message Queue

An **approval queue** is a *human-facing filtered worklist* of Legal Compliance-owned matters awaiting a legal decision: candidate rule interpretations, source challenges, holds/release requests, conflicting legal applicability, coverage gaps and periodic requalification. Prefer calling it **Legal Review Worklist** to avoid confusing it with a transport queue.

- **Legal Compliance owns** the review case/reference, legal grounds, evidence/version, review requirement, competence check, deadline, resulting decision and effective legal state; a native worklist can query pending cases without creating an additional business subsystem.
- **Workflow optionally owns** assignment, multi-stage routing, approval tasks, escalation, delegation and sign-off choreography, where a more elaborate organisational review process is selected. It returns attributable approval/decline evidence; Legal Compliance independently revalidates authority, evidence, recency and revision and *commits* its own decision. Neither a task marked done nor a workflow approval automatically creates legal validity.
- **Message Queue owns** technical routing/delivery/retries/replay/dead-letter of source-outbox events (e.g. `legal.interpretation.approved`, `legal.hold.effective`). It does not know what a legal reviewer may approve, hold a dossier as human work or decide applicable law. Delivery success never equals human approval, domain enforcement or regulator acceptance.
- **Notifications optionally owns** alerts to a reviewer or operator; delivering an alert does not count as a completed review. **Scheduler optionally owns** due-time execution and reminders; a missed run does not waive a statutory deadline. **Audit** records independent evidence.

Typical sequence: Legal Compliance creates `under_review` case → native worklist lists it → Workflow (if configured) routes tasks → reviewer checks evidence and submits sign-off → Legal Compliance checks legal scope, caller and version and commits `approved` or `rejected` → outbox event transported by Message Queue → source domain fetches current version, performs its own enforcement and reports receipt. All transitions remain attributable, and a failed message or optional workflow cannot silently convert pending into approved.

**Native absence mode:** Without Workflow, Legal Compliance provides its own minimal authorise/review/decide commands and a pending-case query; without Message Queue, its state does not depend on transport for internal correctness, but any mandatory downstream enforcement not acknowledged stays pending/incomplete. No duplicate Workflow task engine or second messaging service is built into Legal Compliance.

### User journeys / use cases across LC-01–LC-07

#### UC-LC-01 — A tenant introduces a new business activity (LC-01, LC-03, LC-05)
1. Administrator selects legal entity/tenant, country of establishment, where the activity operates and a plain-language activity classification; this is a *declaration*, not independently verified legal fact.
2. The source capability (e.g. Marketplace, Booking or Publisher) supplies the actual service features and intended audience, preferably from authoritative attributes rather than a free-text compliance assertion.
3. Legal Compliance resolves the narrow rule set by jurisdiction, territorial reach, activity, age/audience, version and effective time. It states which attributes are verified, asserted or missing.
4. Fully qualified cases yield `applicable` obligations, conditions, notices and deadlines; unsupported or contradictory critical classifications yield `unresolved`, creating a review case. The worklist explains who can complete review and which evidence is missing.
5. Operator sees actionable steps and potentially restricted features. The owning capability independently gates only activities requiring unresolved mandatory legal clearance; unrelated operations are not needlessly blocked.
6. On legally meaningful change, Legal Compliance publishes an impact event and domains revalidate before restricted execution. **Outcome:** qualified obligation list plus safe eligibility gate; not a universal `compliant=true` flag.

#### UC-LC-02 — An authoritative law or guidance change arrives (LC-01, LC-04)
1. Curator imports a source citation and amendment, through a manual source register or optional provider. Untrusted external content cannot activate a rule.
2. System identifies prior rule versions and candidate affected services; qualified reviewer verifies primary source, amendment status, commencement, transition/grace and territorial reach.
3. Proposed interpretation shows a side-by-side diff, effective/knowledge dates and affected cases. Reviewer may approve, reject, seek evidence or restrict support.
4. Approved version is scheduled/effective according to legal qualification; existing historical determinations keep their then-known source and as-of meaning. Legal Compliance emits scoped change impact; affected owners assess their own records.
5. Provider outage or unverified feed leaves source update unconfirmed, not magically obsolete or newly applicable. **Outcome:** reviewed rule revision and impact, distinct from domain remediation.

#### UC-LC-03 — A financial transaction requires a legal condition (LC-01, LC-03)
1. Billing/Invoice supplies trusted entity, customer/service geography, transaction type, tax point and document date; Accounting/other domain retains the financial calculation/record.
2. Legal Compliance returns qualified disclosure, preservation, filing or tax-treatment *requirements* and uncertainty with source/effective version—not tax amount, invoice, journal or regulator acceptance.
3. Domain applies its own calculations, permissions and finalisation rules, records the applied legal decision reference and returns completed/refused/partial receipt.
4. If a mandatory legal requirement is unresolved, only affected finalisation/handoff is held for review. **Outcome:** auditable qualified legal condition and domain-owned business decision.

#### UC-LC-04 — A preservation request arrives (LC-02, LC-07)
1. Records manager or authorised counsel requests a hold with purpose, issuing authority, evidence, entity/tenant, precise record classes/IDs, effective period and review trigger.
2. Legal Compliance checks legitimacy and competence, minimises scope and ensures independent approval where risk warrants; suspicious or overbroad demands are rejected/held for qualified review.
3. Effective hold version is made available through public contract; relevant data-owning capabilities acknowledge receipt and separately confirm real preservation of originals/derivatives, or `partial/failed/unconfirmed`.
4. Dashboard distinguishes **legal hold effective** from **preservation completed**. A failure creates urgent remediation and audit evidence, not a false success.
5. At review/release, authorised reviewer considers other duties and Privacy constraints; releasing this hold does not instruct immediate deletion. **Outcome:** lawful restriction with verifiable enforcement status and scoped review.

#### UC-LC-05 — A person requests erasure while a hold exists (LC-02, LC-07)
1. Privacy/Profile or source domain receives a data-rights request; Privacy owns purpose, data rights, lawful processing/retention context.
2. Legal Compliance qualifies whether the narrowly identified statutory preservation/legal-claim exception applies to the specific record and period.
3. Privacy/domain decides rights fulfilment within qualified law; unaffected personal data is erased/limited, affected data restricted/preserved only as justified, with response status and rights/appeal pathway.
4. Legal Compliance tracks hold expiry and review; source owner reports verified partial/complete disposition, distinguishing unavailable downstream copies. **Outcome:** neither automatic blanket erasure nor indefinite blanket retention.

#### UC-LC-06 — Business ownership or authorised control is challenged (LC-06)
1. Tenant's verified human digital owner, legal claimant or recovery operator presents a challenge with claimed company authority and independently obtainable evidence.
2. Identity protects current digital tenant control and initiates controlled recovery where warranted. Verification checks authenticity/provenance of credentials, not whether a shareholding or directorship proves company control.
3. Competent legal-entity/instrument authority (ownership still an *open architectural question*) establishes the legal standing and dispute resolution needed; Legal Compliance qualifies relevant duties, constraints and protective holds using this evidence.
4. Identity/Authorisation/Workflow execute and approve any digital-control transition under ADR-0017 safeguards; Legal Compliance never directly edits owners, joins memberships or changes permissions. **Outcome:** evidenced protected decision or held dispute, not a unilateral legal-compliance takeover.

#### UC-LC-07 — A deadline or regulator filing approaches (LC-03, LC-04, LC-05)
1. Approved legal obligation identifies responsible party, trigger, deadline, timezone, evidence needed, competent regulator and source.
2. Scheduler schedules reminders/tasks; Workflow may assign review; Notifications sends alerts. Responsible domain prepares authoritative contents, Integrations transports if configured.
3. Transport success is recorded separately from regulator filing acceptance. Legal Compliance tracks requirement `awaiting evidence / submitted / receipt unconfirmed / fulfilled / overdue / contested` according to the authoritative domain/regulator evidence.
4. No successful notification, workflow task or MQ delivery is counted as compliance completion. **Outcome:** operational obligation management with explicit evidence and uncertainty.

#### UC-LC-08 — A multi-jurisdiction conflict or unsupported new country (LC-01, LC-04, LC-05, LC-07)
1. Activity spans two jurisdictions, or a required primary source is outside supported scope.
2. Legal Compliance returns separate per-jurisdiction decisions and conflict/coverage metadata; it does not silently select the easiest regime or imply worldwide legal support.
3. Qualified reviewer seeks additional local specialist advice and documents applicable hierarchy, incompatibility and permissible business alternatives.
4. Only affected unsafe operations remain restricted pending resolution; tenant sees plain-language `review required`. **Outcome:** support boundary and explainable risk rather than fabricated completeness.

### Public use-case contract and state expectations

**Input families:** `submitActivityFacts` (usually sourced from owning domain), `proposeSourceRevision`, `requestQualification`, `submitReviewEvidence`, `decideReview`, `requestHold`, `releaseHold`, `recordEnforcementReceipt`, `recordObligationOutcome`. These are conceptual operation labels, not fixed endpoint definitions.

**Output families:** `getApplicableRequirements`, `getCoverageAndProvenance`, `listLegalReviewWork`, `getHoldAndPropagationStatus`, `listObligationsAndDeadlines`, `getDecisionAsOf`, `getChangeImpact` and related scoped outbox events. List endpoints never grant visibility into hidden legal advice or other tenants.

**Minimum result model:** `decisionId, tenantScope, activity/resourceRef, jurisdiction, effectiveAt, evaluatedAt, sourceAndRuleVersions, applicability, mandatoryConditions, missingFacts, reviewStatus, reasonCode/messageKey, freshness, provenance, confidentialityClass`. More fields are conditional per operation; avoid a universal request object. Consumers must never treat `not_applicable`, `not_checked`, `unsupported`, `stale`, `review_pending` and `no_known_obligation` as equivalent.

**Human review state (conceptual):** `draft → submitted → triaged → awaiting_evidence / awaiting_review → approved / rejected / withdrawn`, with explicit re-open/requalification and source revision handling. Workflow task status is a *different* lifecycle. High-risk review requires appropriate assurance, independent approver, non-self-approval where necessary and no stale-revision approval. A change of legal rule after a review request requires revalidation before commit.

### GUI design and accessibility acceptance

**Organisation-first entry:** choose tenant/business context, describe activities/services and applicable locations; show suggested obligations as **qualified / needs review / not supported** with source and last-reviewed time. Avoid asking administrators to classify statutes unaided.

**Compliance overview:** `What must I do?`, `What is overdue?`, `What is waiting for evidence?`, `What changed?`, `Which operations are restricted?`. Each item opens its owner-linked detail, not an editable duplicate domain record.

**Legal Review Worklist:** sort by safety/deadline, filter by tenant/subject/status/assignee, inspect evidence/version comparison, request missing facts, approve/reject/escalate with recorded rationale and qualified role. Clearly distinguish requester, assigned task, legal reviewer and decision authority. Restrict confidential attachments, prevent cross-tenant search leaks and display partially enforced holds conspicuously. Without Workflow, show native pending cases and minimal reviewer decisions; with Workflow, also show delegated approval task status.

**Operator interaction:** one concise blocker with reason, necessary next step and reference; never misleading `fully compliant` badges or unnecessary legal text.

**Acceptance:** keyboard-only complete review, screen-reader labelled statuses and errors, accessible table sorting/filtering, contrast/Theme Manager, localisation of interface but unaltered authoritative citations, responsive/mobile detail, headless parity, absence/stale/partial states and safe denial of non-authorised viewers.

### Proposed refinement to decision register (do not mark approved)

- **LC-01:** Prefer user-declared activity + domain-verified facts → qualified source/rule version → review worklist for uncertain cases. Do not make a tenant administrator the source of legal truth.
- **LC-02:** Hold authorisation and actual owner enforcement/receipt are separate states; worklist manages human scrutiny, not physical data deletion.
- **LC-03:** Public contracts return *specific conditions and unresolved reasons*, not a universal compliance boolean; domain enforcement and completion remain independent.
- **LC-04:** Manual, reviewed source ingestion is a native capability; optional providers accelerate discovery but cannot auto-approve regulations.
- **LC-05:** Rename **approval queue** in user interfaces/documentation to **Legal Review Worklist**; optional Workflow owns approval routing; Message Queue owns only committed event delivery.
- **LC-06:** Legal-entity control provenance remains a separate authority boundary; challenge journeys must not grant Legal Compliance IAM powers.
- **LC-07:** Legal qualification and Privacy rights/retention outcomes require narrow reciprocal decisions and case-by-case exception evidence.

**Open to owner resolution:** scope of jurisdictions/services supported at launch; who may act as legally qualified reviewer and how verification is maintained; mandatory review/dual-control thresholds; whether a named legal-entity authority requires a future capability; which statutory obligation/filing cases are initially supported; duration and precedence rules for conflicting holds/rights. None is answered by a generic transport queue.
