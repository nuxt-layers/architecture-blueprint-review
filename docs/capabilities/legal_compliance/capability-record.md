# Legal Compliance — Capability Record

**Canonical capability:** `legal-compliance` (Foundation in governing catalogue)  
**Blueprint directory:** `docs/capabilities/legal_compliance/` (actual path; do not rename)  
**Conceptual revision:** 20 November 2026 — comprehensive proposed specification, **not yet owner-approved**  
**Review:** [draft PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85)  
**Authority:** Accepted ADRs and normative standards in [architecture-rules](https://github.com/nuxt-layers/architecture-rules); this blueprint is non-normative.  
**Opening governing baseline:** `b920ce0d8b361de000a6739a16123dbdc56df7a7`; **opening blueprint baseline:** `6dac83a03da8704f7945ee1bc894f2248300445a`. Blueprint subsequently advanced to `d39df23e087cd0510c82ba2cea78996c7624850f`; final reconciliation remains required.  
**Evidence classification:** Governing responsibility **established**; LC-01–LC-13 **proposed for owner review**, including LC-08 from the prior exploratory design. Previously approved neighbouring principles are reflected only where relevant to the current interaction contracts; their source records and Git history retain their original decision evidence.

> **Implementation evidence and limits:** `nuxt-layers/legal-compliance` exists, but its inspected `master` README is only a heading and a root `CONTRACT.md` was not found. The services, schemas, ports and screens described below are an **idealised conceptual contract**, not verified implemented APIs, regulated-service coverage, legal advice, legal certification or evidence of passing acceptance tests.

## Executive definition

Legal Compliance owns the **qualified meaning, applicability, scope, provenance, temporal validity and unresolved status of legal/regulatory duties**, plus **legal-hold instruction authority**, and a governed relationship between **applicable obligations → required controls → source-domain implementation → independently verifiable evidence → monitoring and improvement**. Other capabilities own the underlying facts, operational controls, transactions, customer data, permission decisions, messages, approval processes, audit evidence and filing outcomes.

The operating principle is: **a reviewed legal interpretation is reusable; its applicability to a particular subject/activity is a separate, attributable decision; enforcement belongs to the domain owner; delivery of a message is not enforcement.** Legal Compliance does not issue a general `compliant=true` certificate. Its working modes are native/headless, synchronous decision requests, event-driven reassessment, scheduled obligation review and human-assisted qualification. The default architectural form is a bounded Foundation service composed into the modular monolith, with optional separable presentation. Independent deployment or specialised legal providers are not presumed.

### Users, jobs and successful journeys

| Person / consumer | Job to be done | How success is presented |
|---|---|---|
| Tenant / organisation administrator | Declare operating activities and see what actions or evidence are needed | Contextual onboarding, clearly scoped obligations and unresolved areas, without requiring knowledge of legislation |
| Compliance officer | Maintain obligation ownership, monitor control coverage, deadlines and exceptions | Obligation dashboard and **Legal Review Worklist** |
| Qualified legal reviewer | Validate sources and interpretation; adjudicate difficult scope, holds, conflicts and releases | Source/version comparison, privileged evidence, recorded decision, competent authority and reason |
| Business manager | Carry out allowed operations without interpreting statute | Domain-level requirements/blockers, clear next action and review route |
| Records manager / privacy officer | Preserve covered records while honouring data rights and other retention rules | Narrow hold and erasure disposition, separate legal/physical outcomes |
| Auditor / regulator liaison | Reconstruct historical assessment, control and evidence history | Authorised as-of reporting and evidence references, not fabricated completeness |
| Service capability | Determine lawful conditions for a specific action | Typed, versioned, bounded-latency applicability result with explicit unknowns |
| Platform operator | See health, missed tasks and source freshness | Operational view without unrestricted tenant legal advice or evidence |

## 1. Authority, owned information and exclusions

**Legal Compliance owns:**
1. **Legal-source register:** source reference, issuing authority, class (binding legislation / delegated instrument / regulator obligation / guidance / voluntary standard / contractual requirement), jurisdiction/territorial reach, effective dates, amendments, source provenance, licence/access limitations, verification/review and change detection.
2. **Qualified interpretation / approved rule:** immutable version, reviewer authority, approvals, legal scope and predicates, evidence, date knowledge was obtained, legal effective period, limitations and retirement/supersession; review of legal content is not merely syntactic rule approval.
3. **Coverage and applicability:** declared supported jurisdictions/activities/service categories, missing coverage, conflicts, qualified determination, factual snapshot references, source/revision, reason, expiry and historical as-of explanation.
4. **Obligation register:** law-derived responsibility, scoped accountable role, trigger, duty/required outcomes, governing source/interpretation, period, deadlines, review criteria, risk and fulfilment references. The factual filing/action remains with its owner.
5. **Control requirement mapping:** obligation → prescribed safeguards/expected outputs → implementing **domain control owner** → control evidence contract. It is a map of duties, **not** a second engine performing all domain actions.
6. **Legal-hold instruction lifecycle:** authorised basis, scope, competent requester, restrictions, records/classes, required review and release; the domain retains actual records, derivative copies, enforcement and deletion.
7. **Compliance assessment/exception:** qualified issue, risk/impact, unresolved facts, case status, review finding and improvement/corrective-action requirement. Workflow may own tasks, and Audit owns independent evidential preservation.

**Does not own:** Identity tenant/group or digital-control relationships; corporate register, ownership adjudication or legal-person master not separately established; Authentication, Authorisation, Verification; Privacy consent, subject rights and specialist privacy retention decisions; Configuration's approved user settings; Publisher's notices or policy document lifecycle; operating domain rules/records or statutory tax calculations; regulator decisions and source-domain filing content; Workflow approval choreography; Scheduler execution; Message Queue message transport; Notifications channels; Integrations credentials/transmission; Audit tamper-evident records; Logging technical logs; Observability metrics; Reporting report definitions. No universal policy service and no automatic legal interpretation by AI or provider output.

**Boundary requirement:** An authorised operation may still be legally prohibited; a legally permitted operation may still be unauthorised. Domain owners independently verify both, enforce any mandatory relevant restriction and return actual completion or failure evidence. Neither holds nor regulatory uncertainty automatically grant unrestricted platform operator access.

## 2. Canonical conceptual information model

| Object | Mandatory conceptual attributes | Authority and lifecycle |
|---|---|---|
| `LegalSource` | source ID, authority, official reference/URI, category, geographic and temporal reach, amendments, verification/known-at, provenance | Legal Compliance indexes external authority; cannot claim the text's legal validity solely from receipt |
| `InterpretationVersion` | source refs, interpretation/predicate, qualification, reviewer competence/approval, dates, scope, status, supersedes | Draft → qualified review → approved/scheduled → effective → superseded/withdrawn, no overwriting effective versions |
| `FactDefinition` | stable typed key, owner, scope, validation, trust/freshness policy, sensitivity, permissible asserted/verified states | Legal Compliance defines fact *consumption* semantics; source owner retains values |
| `FactEvidenceRef` | owner resource ID, source revision, observed/valid time, asserted/verified trust, reference/digest | Usually borrowed input; sensitive values held transiently/minimally |
| `ApplicabilityAssessment` | tenant/entity/activity/resource, jurisdiction(s), as-of/known-at, rule+fact versions, status, reasons, expiry, decision provenance | Legal Compliance owns consequence if persisted; factual origin unchanged |
| `Obligation` | legal interpretation ref, trigger/scope, duty, deadline condition/time zone, accountable party, state, review, conditions | Legal Compliance owns obligation meaning and tracking, not actual domain action |
| `ControlRequirement` | obligation ref, implementing owner, expected safeguard/outcome, evidence/verification criteria, assurance level | Legal Compliance maps duty to named public domain control; domain validates/enforces |
| `ControlEvidenceRef` | owner/operation, evidence type, applied decision version, accepted/completed/failed/unknown, timestamps, provenance | Domain owns outcome; Audit retains independent evidential record; Legal Compliance stores minimal linked status |
| `LegalHold` | competent authority, legal basis, narrow target references, scope, effective/review/release dates, approvals, propagation acknowledgements | Legal Compliance owns instruction; domain owns physical preservation/disposal |
| `ReviewCase` | reason, subject/scope, source versions, missing evidence, assigned competent reviewer, decision, timestamps, confidentiality | Legal Compliance owns legal review case; Workflow owns optional task routing |
| `Exception/ImprovementRequirement` | deviation, consequence/risk, corrective action owner, due date, evidence, independent evaluation status | Legal Compliance tracks legal requirement; domain/Workflow own remedy/action |
| `CoverageProfile` | supported jurisdiction/service/activity, source currency, validated date, exclusions, qualified responsible reviewers | Absence means unsupported/unresolved, never legal approval |

**Relationship:** `LegalSource → InterpretationVersion → ApplicabilityAssessment → Obligation → ControlRequirement → ControlEvidenceRef → Assessment/Exception/Improvement`. A hold can restrict any affected source record independently of the primary obligation chain. The graph is traceable by stable references, not shared foreign-key access to private databases. Provenance can be modelled using W3C PROV concepts (entity/activity/agent); this does not require an RDF store.

**Temporal model:** distinguish enacted/published, legally effective, observed, known-to-system, approved, applied and completed times. Historical queries specify legal **as-of** and knowledge **known-at**; retroactive changes result in linked reassessments, never silent rewriting of historical knowledge.

### Status vocabulary and certainty

- Applicability: `applicable`, `not_applicable`, `unresolved`, `unsupported`. Distinguish `stale` and `conflicting` as explicit evidence/validity qualifiers. No unknown state maps to Boolean `false`.
- Legal qualification: `draft`, `under_review`, `approved`, `scheduled`, `effective`, `superseded`, `withdrawn`.
- Enforcement: `not_requested`, `requested`, `accepted`, `completed`, `partial`, `failed`, `unknown`, `not_applicable`. Transport receipt and provider submission do not satisfy `completed`.
- Obligation: `awaiting_evidence`, `due`, `submitted`, `receipt_unconfirmed`, `fulfilled`, `overdue`, `contested`, `closed` as applicable, without assuming an external authority accepted a filing.
- Hold: `requested`, `authority_pending`, `authorised`, `effective`, `partially_enforced`, `under_review`, `released`; hold legal state and domain preservation state are orthogonal.

Every status-bearing read identifies scope, source/version, freshness/coverage, conclusion limitations and allowed next action. Account for appeals, qualified overrides permitted by law, correction, revocation and incompatible jurisdictions without a single global override flag.

## 3. Variables, flags and decision rules (LC-08 / LC-10)

**Typed variable catalogue** records stable key, type/allowed values, units, source of truth, tenant/resource scope, purpose, sensitivity, valid/fresh period, revision, provenance, validation, permitted asserted versus verified value, fallback and legal relevance. Examples:
- `tenant.id`: Identity/host-trusted isolation context; never browser authority.
- `entity.registered_country`: authoritative entity verification evidence, **not** a mere unverified Configuration assertion.
- `service.category`: Marketplace/Publisher/other source capability; authoritative actual feature taxonomy.
- `service.allows_user_content`: relevant business owner’s effective service state.
- `audience.includes_children`: sourced fact with verified/declared level, not assumed from marketing.
- `activity.effective_at`: domain owner with Clock semantics.
- `rule.version`: Legal Compliance approved decision corpus.
- `hold.active`: derived from a scoped Legal Compliance hold, not tenant-configurable.
- `control.completed`: explicit evidence from the enforcing owner, not inferred from legal applicability.

**Flags are different from legal conclusions:** Feature switches belong to Configuration/domain owners, fact flags reflect evidenced source states, legal requirement flags are derived from qualified legal results, and fulfilment flags come from enforcement evidence. No editable `legal.enabled=false` switch can waive an applicable mandatory duty. Unknown/stale sources cannot return `not_applicable` by default.

**Rule representation:** prefer a small, schema-validated, side-effect-free declarative condition/decision-table model with named variables, typed operators, explicit conflict/hit policy and output obligations. Align concepts with current OMG **DMN 1.6 (September 2026)** but do **not** promise full DMN/FEEL interchange, embed a heavy BPM suite, execute arbitrary tenant JavaScript or let rule documents call network endpoints. If later consumer requirements justify full DMN compatibility, assess import/export subset, version compatibility and deterministic evaluation separately. Rule source/qualification/approval is distinct from parse/type validation.

**Risk-aware but law-bound:** ISO 31000 can inform review criticality; organisational tolerance cannot override legal floors. Candidate automated legal interpretation and AI-assisted source extraction always require review under an appropriate competence policy and cannot self-approve.

## 4. Automation procedure and operational modes

**Shared deterministic evaluation procedure:**
1. Trigger via an authorised direct request, committed source event, Scheduler due task or qualified human review.
2. Server resolves trusted tenant, actor, assurance, resource and purpose; Authorisation checks permission before any data access or write.
3. Resolve supported jurisdiction/service/activity and legal effective/as-of and known-at periods; choose only reviewed active rule versions with source provenance.
4. Extract rule-variable dependencies; select minimal authoritative source ports; obtain scope-limited facts with source revision, observed/valid dates, trust grade and expiry (never private database reads).
5. Normalise and validate type, canonical identifiers, evidence, temporal consistency, source/tenant scope, contradictions, completeness and confidentiality. Missing/stale/unsupported/conflicting critical fact → precise unresolved/unsupported response.
6. Evaluate **all** applicable rule groups deterministically, combining obligations/conditions without allowing weaker tenant preferences to defeat statutory restrictions. Refuse to invent precedence in conflicting laws.
7. Return scoped applicability decision, obligations/controls, restrictions, supported coverage, missing facts, evidence and rule/fact version refs, evaluated and review-by times. Read-only queries need not always persist a durable decision.
8. For consequential decisions, holds and obligations, commit versioned state and capability-owned transactional outbox atomically; use optimistic concurrency and idempotency keys; distinguish accepted request from completed owner action.
9. Coordinate downstream enforcement via public ports/event subscriptions; accept domain receipts, reconcile missing/partial confirmations, publish changed status and retain accountable audit references.
10. Repeat on impacted fact/rule change, scheduled check, explicit qualified review or recovery reconciliation; never treat delivery/replay or cached result alone as final legal clearance.

**Execution channels:**
- **On demand:** bounded-latency synchronous assessment for a domain's legally gated action; source lookup timeout or unsupported scope holds only the affected unsafe act.
- **Event-driven:** source-owned durable outbox event carries source ID and revision; Message Queue transports at-least-once; Legal Compliance deduplicates, re-fetches current authoritative facts, invalidates only dependent assessments and requalifies.
- **Scheduled:** Legal Compliance specifies rule/hold review, filing/reconciliation deadlines with Clock semantics; Scheduler executes due tasks and recovery; Notifications communicates, Workflow may route approvals.
- **Human-assisted:** qualified evidence/review case with revision checks and optional dual control. Native protected reviewer commands and pending-list query work without Workflow.
- **Recovery:** durable checkpoints and periodic reconciliation identify lost/out-of-order events, expired evidence and unconfirmed holds; no impossible claim of globally exactly-once outcomes or unlimited live legal-source availability.

**Performance:** index rule dependencies and impact scope; immutable approved rule bundles and bounded derived assessments may be cached by tenant/activity/jurisdiction/fact+rule revisions/time. Cache is never authority, cannot cross tenancy/privacy boundaries, and high-risk finalisation revalidates freshness/concurrency. Prefer incremental impact matching, bounded batching and observable lag over expensive full scans. Stateful Legal Compliance owns its schemas/migrations/storage port and durable outbox; host provides infrastructure, never business tables.

## 5. Human review, worklist and message-queue boundary

**Legal Review Worklist** is a protected filtered view of Legal Compliance’s **pending legal cases**: candidate interpretations, evidence deficiencies, holds/releases, disputes, conflicts, regulatory change impacts and requalification. It is not a message queue, not a second Workflow engine and not an authority to grant business permissions.

**Workflow (optional)** provides reviewer task routing, assignment, escalation, separation-of-duty sign-off and multi-person process state; Legal Compliance checks competence, caller assurance, current case/interpretation revision and authorisation before it commits a qualified legal decision. A Workflow step marked complete is not a legal conclusion. Without Workflow, minimal `submitForReview`, `requestEvidence`, `decideReview` and `listReviewCases` remain native.
**Message Queue** transports committed domain/outbox events, controls delivery/retries/dead letters/replay and owns no human legal dossier or review approval. Event delivered ≠ review approved ≠ domain hold enforced ≠ external filing accepted.
**Scheduler** executes due-time work; **Notifications** sends communications; **Audit** receives proportionate evidential assertions; **Logging** records sanitised diagnostics; **Observability** measures service health. None becomes a legal interpretive authority.

## 6. Idealised published public input contract (not implemented)

| Interface (illustrative semantic name) | Authoritative source/input | Preconditions, validation, failure semantics |
|---|---|---|
| `evaluateApplicability` | Trusted host/domain: subject/activity, jurisdic­tion, legal entity, service facts/refs, effective/as-of time and purpose | Required for legally gated action; fact versions/provenance and tenant/permission verified; returns scope-specific typed `unresolved` or `unsupported`, never default permission |
| `describeCoverage` | Authorised tenant/host, jurisdiction/service scope | Returns coverage, review freshness, source/rule versions and limitations, not implied full legal support |
| `proposeSource`, `proposeRuleRevision` | Source curator/Integrations: official reference, amendment, jurisdiction, source dates, candidate rule and legal rationale | Untrusted feeds/AI cannot self-approve; validate licence, source trust and code-free rule grammar |
| `submitReview`, `recordReviewDecision` | Competent legal reviewer, optionally Workflow approval evidence | Protected role, recency, separation of duties if applicable; stale version conflicts or unverified competence refuse |
| `requestHold`, `reviewHold`, `releaseHold` | Authorised requester and qualified legal evidence of scope, competent basis and effective period | Reject overbroad/unsupported hold, prevent unauthorised release, preserve other independent holds and rights |
| `registerObligation`, `reassessRequirements` | Approved interpretation and trusted entity/activity trigger, source changes or scheduled event | Validate legal authority and subject facts; do not let ordinary tenant admin create “statutory” obligation by unchecked assertion |
| `recordControlReceipt`, `recordFilingOutcome` | Enforcing domain or authorised Integrations filing evidence: applied rule ID, resource, revision, completion and evidence ref | Authenticated producer, correlation/idempotency, duplicate/out-of-order handling; provider success != regulator acceptance |
| `submitException`, `recordCorrectiveOutcome` | Domain/control owner, Audit findings or authorised reviewer | Evidence and actual owner action required; risk acceptance cannot waive mandatory duty |
| `requalifyFromEvent`, `executeDueAssessment` | Source outbox, Scheduler, Workflow callback under host-composed ports | Idempotent, scoped, versioned; missing critical dependency yields pending/unresolved and recoverable task |
| Host ports | Caller/Access, Clock, owned persistence/outbox, authorised fact resolver and optional Workflow/Scheduler/Integrations | Required ports fail closed; missing optional provider uses manual/native alternative with explicit loss of functionality |

**Common context where needed:** source/tenant/actor assurance, public resource reference, source revision, correlation and idempotency, rule/effective/known-at dates, evidence provenance, disclosure class and outcome. This is a set of semantics, **not** an imposed universal request object or fixed HTTP route.

## 7. Idealised public output contract (not implemented)

| Output | Intended consumer and meaning | Non-guarantees / lifecycle |
|---|---|---|
| `ApplicabilityDecision` | Domain, Privacy, specialised service: jurisdiction- and time-qualified applicable/not-applicable/unresolved/unsupported outcome, obligations, restrictions and source versions | Not Authorisation, tax calculation, permission grant, complete legal certification or proof of domain enforcement |
| `ObligationCatalogue/Status` | Compliance staff, Scheduler, Workflow, Reporting: duty, owner, trigger, due date, required control/evidence and qualification | Due reminder, sent form and “completed workflow” do not equal regulator acceptance |
| `ControlRequirementMap` | Domain owner and Audit/Reporting: required safeguards, applicability, evidence contract and expected control outcome | Domain owns actual implementation and efficacy; Legal Compliance should not assert coverage without receipt |
| `HoldInstruction/Status` | Data owners/Privacy: precise restriction, scope/authority and review/release status | Legal instruction differs from actual preservation; domain must report partial/failed outcome |
| `Source/Qualification/Coverage` | Competent reviewer and authorised domain: approved source version, effective/known-at dates, evidence, exclusions and review-by | Unknown and stale must be visible; privileged advice redacted for ordinary users |
| `ReviewCase/Decision` | Worklist and optional Workflow adapter: case version, reviewer competence, request, approval/decline and legal decision | Task routing never grants legal validity automatically |
| `Exception/Impact/Effectiveness` | Compliance officers, Reporting, control owners: gaps, risk context, corrective requirements, evidence quality, remediation and freshness | No single “compliant” boolean or unsupported quantitative assurance |
| `HistoricalAssessment/ExportRefs` | Authorised auditors / Reporting / Export workflow: as-of and known-at provenance references | Domain originals, Audit integrity, Publisher documents and exporter bytes stay with their owners |
| `legal.*` committed events | Message Queue to authorised subscribers: source change, rule activation/withdrawal, hold, obligation, review, impact and corrective status change | At-least-once/replay; delivery receipt does not prove downstream commit or statutory acceptance |

All outputs include stable versioning and reason/message keys, tenant/purpose disclosure filtering, supported completeness and safe distinction of accepted, pending, applied and confirmed outcomes. Source operations, not a generic event, grant business permissions. Changes to contract members require independent compatibility review.

## 8. Cross-capability coordination and absence

| Capability | Inputs received by Legal Compliance | Outputs / boundary with that capability |
|---|---|---|
| Identity, Authentication, Authorisation, IAM Integration | Trusted scope, verified governance relations, human assurance/permission decisions | Legal constraints for governance/recovery; Identity changes tenant control, Authorisation decides permissions |
| Verification and legal-entity authority (open) | Attestation/provenance, credential and company authority evidence | Qualify age/KYB/recognition duties; cannot infer corporate legal standing from platform role |
| Configuration / Privacy / Profile | Approved activity/site assertions and privacy rights/retention context | Mandatory legal floors, hold exceptions; Configuration owns settings, Privacy specialist decisions, Profile personal data |
| Accounting, Billing, Invoice, Order, Payment and finance | Place of supply, transaction, entity, dates and regulated activity | Legal requirements/filing/retention conditions; financial owner calculates, records and files |
| Marketplace, Publisher, Comments, Content Security, Moderation, Search, Federation, Media | Actual service/audience/activity content and enforcement evidence | Qualified content/online safety/child protections; domain performs takedown, moderation owns case |
| Recruitment, Employment, Job, Course, Qualification, Credentials, Assets | Regulated purpose, jurisdiction, role/resource and accountable evidence | Labour/safeguarding/credential/licensing/retention requirements; operational owners enforce |
| Integrations | Source/regulator feeds, provider provenance and delivery/receipt evidence | Provider-neutral lawful transfer/filing conditions; provider delivery != regulator acceptance |
| Audit, Logging, Observability, Reporting | Audit references, secure diagnostics/health, control evidence | Risk-based evidence assertions; authorised compliance read models, never replacement of legal truth |
| Clock / Scheduler / Workflow / Message Queue / Notifications | Trusted time, due-work receipt, approval evidence, committed transport acknowledgements | Legal obligation/assessment triggers, human work requests, change events and scoped alerts |
| Storage / Caching / source domain persistence | File/class refs, retention/derivative preservation/disposal receipts | Narrow hold/legal transfer constraints; source owners control bytes, backup/derivative lifecycle |
| UI / Theme Manager / host | Presentation tokens and navigation/authorised caller context | Optional legal dashboard, filters and workflow actions using public contracts only |

**Dependency rule:** these are conceptual public information-flow edges, not reciprocal direct package imports. Hosts resolve directional ports to avoid cyclic dependencies. Only required verified infrastructure and authority ports fail closed; optional services have specified degraded/manual modes. In a modular monolith, logical separation suffices; a remote legal database, notification service or legal feed is not compulsory.

## 9. Enterprise compliance-management operation (LC-09 / LC-11 / LC-12)

Use **ISO 37301:2021** as the principal CMS design reference, not an assertion of certification. Model a lifecycle: **identify legal context and obligations → qualify and assign responsibility → map controls → implement via domains → monitor outcomes and evidence → assess effectiveness → correct/improve → requalify changes**. Each organisation can see its scoped responsibilities and control coverage while legal interpretation versions may be shared where licensed and qualified.

Use **ISO 37302:2025** to assess whether controls operate effectively. Distinguish: (i) rule understood, (ii) required control implemented by owner, (iii) evidence received, (iv) effect tested/observed, (v) deficiency remediated and independently verified. Do not count ticked tasks or “no known incidents” as evidence of legal compliance. Control effectiveness indicators may include verified coverage, review overdue rates, time to apply holds, percentage unconfirmed domain receipts, evidence staleness, recurrent control failures and effectiveness of corrective action. Reporting owns presentations/aggregates; Legal Compliance owns qualified obligation/control mappings and interpretations.

Use **ISO 31000:2018** for risk-based worklist prioritisation, likelihood/consequence and proportionate assurance. Legal significance overrides any user-tuned risk score. Use **ISO 19011:2026** to inform competence, independence, audit programme and evidence-based assessment; Audit retains evidence ownership, and professional legal interpretation remains with competent reviewers. Periodic management review and operational corrective actions are real lifecycle steps, not generic “approved” flags.

**Evidence lineage and records:** use W3C PROV-O concepts (source entity, evaluating activity, responsible agent) and **ISO 15489-1:2016** records principles for attributable creation, preservation, confidentiality, lawful disposal, supersession, historical reconstruction and controlled evidence access. No automatic RDF/triple store or immutable-forever policy; preservation restrictions remain lawfully bounded.

## 10. Security, privacy, regulatory and standards mapping

| Reference | Design use | Status/limitations |
|---|---|---|
| [ISO 37301:2021](https://www.iso.org/standard/75080.html) | Compliance system responsibilities, obligations, operational monitoring, improvement | Principal non-normative design reference; does not certify platform/tenant |
| [ISO 37302:2025](https://www.iso.org/standard/37302) | Evaluate effectiveness using independent evidence and corrective feedback | Non-normative guidance, not a boolean conformity test |
| [ISO 31000:2018](https://www.iso.org/iso-31000-risk-management.html) | Risk-driven prioritisation, escalation and review | Never reduces mandatory legal floor |
| [OMG DMN 1.6](https://www.omg.org/spec/DMN/1.6/) | Decision-table/typed rule modelling and possible interoperability | Adopt restricted concepts; no full runtime compliance claimed |
| [W3C PROV-O](https://www.w3.org/TR/prov-o/) | Source/reviewer/evaluation lineage and provenance references | No compulsory RDF store |
| [ISO 15489-1:2016](https://www.iso.org/standard/62542.html) | Evidence/records lifecycle and accountability | Not identical to statutory records-retention schedule |
| [ISO 19011:2026](https://www.iso.org/standard/19011) | Audit competence, review independence, programme design | Guidelines, not a product certification |
| [ISO/IEC 27001:2022](https://www.iso.org/standard/27001) + 2024 amendment | Confidentiality, integrity, access, change and incident assurance | Management-system reference; no ISO certificate asserted |
| [ISO/IEC 27701:2025](https://www.iso.org/standard/27701) | Privacy governance, rights/evidence coordination | Privacy capability retains specialist ownership |
| [NIST SP 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) | Appropriate AC/AU/CM/RA/SI/CP control mappings | Reference catalogue; jurisdiction/project applicability assessed separately |
| [NIST OSCAL](https://pages.nist.gov/OSCAL/) | Optional machine-readable control profiles, assessment mapping/export | No mandatory full OSCAL native data format |
| [OWASP ASVS 5](https://asvs.owasp.org/) | Authentication, access control, validation, logging, secure APIs | **Existing governing ASVS Level 2 baseline**, Level 3 where critical |
| [WCAG 2.2 AA](https://www.w3.org/TR/WCAG22/) | Review/editing dashboards, colour/keyboard/screen readers | **Existing governing accessibility baseline** |
| [ISO/IEC 42001:2023](https://www.iso.org/standard/42001) | Optional AI governance for assisted legal-source extraction and review | AI remains an untrusted assistant to competent reviewer |
| [ISO 22301:2019](https://www.iso.org/standard/75106.html) | Continuity/recovery for deadlines, holds and required controls | Host/infrastructure recovery remains independently owned |

**Legal sources are not replaced by technical standards.** For actual statutory applicability inspect effective legislation and regulators for the legal entity, nexus, service, audience and relevant time: e.g. [UK legislation.gov.uk](https://www.legislation.gov.uk/), [ICO](https://ico.org.uk/), [Ofcom](https://www.ofcom.org.uk/). Existence of an Online Safety Act feature, UK GDPR process, file scan, ISO mapping, publication of a notice, or third-party provider licence is never a universal compliance claim.

**Threats and controls:** spoofed legal sources and regulator demands, malicious legal-text prompt injection, rule poisoning, compromised reviewers, self-approval/policy capture, stale cached favourable decisions, cross-tenant legal-case disclosure, hold denial or indefinite preservation, evidence forgery, missed deadlines, provider uncertainty and cross-domain confused-deputy execution. Require strong scope/authorisation, minimum necessary disclosure, source attestation, reviewer independence, trusted time, least privilege, tamper-evident audit references, secure key/secrets boundary, backup/recovery and protected rule activation. Legal source documents are untrusted data; no arbitrary code or AI-authorised decisions.

**International operation:** support explicit jurisdictional coverage matrix rather than universal country “on/off”. Territorial scope, law types, cross-border conflicts, mandatory translations, evidence localisation, regulator relationship, authority competence, effective dates and legal-text redistribution licences require qualified verification. Unsupported markets return `unsupported`, not approval.

## 11. GUI, headless and hosted composition

An optional host-owned sidebar entry `Capabilities → Legal Compliance` opens a role-restricted dashboard. It includes: supported-jurisdiction/activity coverage, evidence freshness, obligations/deadlines, legal source register and interpretation diffs, controls/effectiveness, legal holds with **legal versus actual enforcement** state, impact/exception review, **Legal Review Worklist**, qualified approval/sign-off evidence, corrective action monitoring, regulator submission provenance, as-of historical lookup, safe audit export, and integration/provider health.

Tenant administrators get business-language activity onboarding and scoped instructions; ordinary domain operators see only contextual blocking reason/action to take. Competent reviewers see fuller legal citations and privileged evidence; host operators see operational health only. Reject unauthorised cross-tenant worklist searches and undue disclosure through autocomplete, export or notifications.

All presentation consumes published conceptual contracts (no private table import); host owns navigation/routing and server caller context; optional independent headless mode provides the same legal decision/hold/review semantics. Theme Manager semantic vocabulary, internationalisation (without changing authoritative source text), responsive layouts, keyboard operation, screen-reader labels, clear unknown/degraded states and WCAG 2.2 AA are required. `nuxt-layers-test/application-test-template` is a representative future acceptance host, not an implementation change.

## 12. Operating interactions and use cases

This section is part of the **current conceptual design**. The following relationships are deliberately expressed through authoritative public inputs and outputs, not assumed package imports. Real-world legal duties, source dates, approval competence and enforcement must be qualified for the affected jurisdiction and service. **Source event delivered**, **legal decision approved**, **domain action completed** and **external authority accepted** are separate outcomes.

### 12.1 Detailed cross-capability interactions

| Source / cooperating capability | Trigger and facts provided to Legal Compliance | Qualified Legal Compliance output | Owning action, evidence and absence behaviour |
|---|---|---|---|
| **Authentication** | Account close, session/credential deletion, security record lifecycle and scope of covered records, using public references only | Effective retention/disposal restriction and narrow hold exception with dated source/review status | Authentication owns actual credential/session records and disposal. Closure does not cancel a valid hold; confirmation includes what was deleted, retained or unresolved. No indiscriminate indefinite preservation of credentials |
| **Identity / IAM / Verification** | Tenant/group/person references, verified digital governance, assurance provenance, company-control claim and disputed authority evidence | Duties for contested governance, children/age, proof of authority, recovery safeguards and time-limited holds | Identity owns digital control and tenant relationships; Verification evidences claimed attributes, Authorisation decides access; real-world corporate entitlement requires independent qualified authority, not inferred from title, creator or parent tenant |
| **Configuration / Organisation onboarding** | Approved service assertions, operating regions, controller descriptions, tenant/site revisions, proposed governance policies and effective dates | Mandatory legal boundaries, uncertainty/coverage and rule-change impact | Configuration stores approved settings but cannot override statutory/security floors. Unverified assertions never automatically qualify the organisation |
| **Privacy / Profile / source data owners** | Purpose, right-of-access/correction/erasure request, record classes and lawful-purpose/retention assessment | Jurisdiction-qualified preservation exception, legal-hold status, disclosure/transfer duty and necessary reasons | Privacy owns data rights/consent and its specialist retention policy; source owner acts on actual data and supplies complete/partial/deferred receipts. A hold covers only justified records, not a blanket block on unrelated erasure |
| **Accounting / Billing / Invoice / Order** | Place of supply, entity/party, activity, taxable/relevant event, financial instrument/transaction and effective date, evidence references | Tax/regulatory framework and disclosure/retention/filing constraints, statutory minima, uncertainty and conflict; **not** a calculated tax amount | Accounting owns ledger and statutory return facts, Billing charge assessment, Invoice issued legal document; Integrations transports filings. Missing mandatory classification holds only impacted finalisation; successful transmission is not authority acceptance |
| **Integrations / regulator and government portals** | Official source update, provider legal/source provenance, processor/residency details, transmission/receipt and external acknowledgement | Lawful transfer/filing conditions, approved source candidate status, destination restrictions and unresolved obligations | Integrations handles connection credentials, authenticated transport and retries. External feed alone does not approve legal interpretation; acknowledgement alone is not statutory acceptance |
| **Publisher / Content Editor / Export** | Planned publication/notice, document source/version, jurisdiction, disclosure context and output purpose | Statutory notice/disclosure, licensing, preservation, accessibility and effective-date constraints | Publisher owns authored notices and publication lifecycle, Content Editor is presentation, Export statelessly renders supported output; published statement or technically valid PDF does not prove compliance |
| **Media / Comments Engine / Content Security / Moderation** | Service category, audience/age context, content/action references, moderation reports and detector provenance | Qualified online-safety/child-protection/notice/retention duties, service-specific risk and reporting requirements | Content Security owns detection evidence, Moderation cases/appeals, domains visibility/removal and enforced restrictions. Never assert universal scanning obligation, an exemption for closed groups or automatic regulator conformity |
| **Search / Federation / external index** | Public content visibility and distribution/retraction scope; actual service classification | Applicable publication, disclosure and withdrawal obligations with dates/source | Originating domains own content and restrictions; Search/Federation maintain derived indexes or replication. Takedown instruction is not proven across remote copies without acknowledgements |
| **Job / Recruitment / Employment** | Job advert, applicant processing purpose, employer jurisdiction, worker classification or verified recruitment circumstance | Applicable employment, equality, safeguarding, working-eligibility, privacy, evidential and publication restrictions | Job owns vacancy facts, Recruitment applicant lifecycle, Employment workforce records; each enforces and reports outcomes. Qualifications and local legal classifications require evidence, not generic worldwide assumptions |
| **Course / Assessment / Qualification / Credentials** | Learner age, jurisdiction, scheme, issuer/accreditor delegation, claims and award lifecycle | Safeguarding, education/accreditation, recognised award authority, retention/withdrawal and disclosure requirements | Course owns learning content, Qualification award decisions, Credentials claim issuance. Platform role is not external accreditation; external recognition must be independently evidenced and time-scoped |
| **Asset / Inventory / Storage / Caching** | Asset/custody type, record class, file/derivative/backup retention and physical enforcement progress | Narrow lifecycle, inspection, disposal/retention, legal-hold and transfer constraints | Each source owner implements restriction/disposal; Storage owns bytes and provider operations; Caching owns derived-copy eviction. Hold release is not automatic deletion; backup/provider uncertainty must remain explicit |
| **Audit / Logging / Observability / Reporting** | Source-domain completion evidence, anomaly/diagnostic metrics, authorised reporting request and scope | Legally qualified decision/obligation/control/effectiveness provenance and review outcomes | Audit preserves independent tamper-evident evidence; Logging sanitised operational diagnostics; Observability metrics/health; Reporting derived measures and exports. Neither a dashboard nor audit receipt confers legal validity |
| **Workflow / Scheduler / Message Queue / Notifications / Clock** | Approval provenance/reviewer identity, due-time receipts, committed source events, delivery acknowledgements and canonical temporal semantics | Legal review cases, obligations/deadlines, events, review triggers, safe recipient/reference notifications | Workflow coordinates human sign-off routing; Scheduler timed execution; Message Queue delivery/retries; Notifications communication; Clock temporal semantics. Legal Compliance alone commits legal review/hold state. Transport and workflow completion cannot stand in for actual enforcement |

**Dependency/authority discipline:** source owners authenticate producers, provide minimal verifiable facts and revisions, and apply their own business invariants. A Legal Compliance consumer may subscribe to an event for invalidation, but must re-fetch authoritative facts through a documented port. Cross-capability communication is host-composed to keep the dependency graph acyclic. **Missing critical legal evidence is an unresolved result for that unsafe operation, not an entire tenant shutdown by default.**

### 12.2 User-driven end-to-end journeys

**UC-01 — New online marketplace or content service.** The tenant administrator declares business activities and regions in a business-language form. The service-owning capability supplies effective content, seller and audience behaviour. Legal Compliance loads the relevant approved jurisdictional rule versions and checks qualified evidence. The result is an obligations/control list with conditions and a provenance/review date; uncertain classifications become a Legal Review Worklist case. The domain gates only relevant unsafe activation, reports its actual safeguards, and ordinary operators see an actionable reason rather than raw legal advice.

**UC-02 — New law, amendment or regulator guidance.** A curator or Integrations supplies a verified candidate primary-source citation with publication, amendment, commencement and territorial context. Legal Compliance marks it *candidate*, compares previous interpretations, maps affected variable dependencies and creates a qualified-review case. An independent reviewer approves only the supported interpretation; activation and scope-specific requalification then run by effective date. Historical known-at decisions are retained. Provider feed failure, unavailable legal text or licensing limitations remain explicit; none creates a new binding rule automatically.

**UC-03 — Regulated financial operation.** Billing/Invoice sends trusted entity, service, counterparty region, transaction and effective-time references. Legal Compliance returns relevant qualified statutory reporting, disclosure or retention constraints and uncertainty, not the tax computation or journal. Billing/Invoice/Accounting independently validate and commit their own outcomes; a missing mandatory condition blocks the affected operation rather than all financial activity. Integrations delivers any authorised filing and distinct regulator acceptance evidence is reconciled later.

**UC-04 — Legal preservation demand.** An authorised records/legal requester submits legal basis, competent authority evidence, narrow records/classes, start/review time and reason. Legal Compliance verifies scope, competence and proportionality, requires independent approval where appropriate and commits the hold. A committed hold event is transported to affected source owners, which report preservation as \`completed\`, \`partial\`, \`failed\` or \`unknown\`; worklist and incident escalation surface incomplete propagation. Release is reviewed independently and cannot silently cancel other lawful restrictions.

**UC-05 — Erasure request during a hold.** Privacy/Profile receives a rights request and identifies affected classes/owners. Legal Compliance returns narrow statutory/legal-claim preservation constraints with effective period and competence provenance. Privacy and data owners complete erasure of unaffected material and restrict/preserve covered material as lawfully justified, reporting partial completion and downstream-copy limitations. Expiry triggers reassessment, not unconditional release or indefinite retention.

**UC-06 — Disputed company or tenant control.** A claimant presents a challenged controlling-party relationship or governance instrument. Identity keeps digital tenant ownership protected; Verification supplies source authenticity but cannot adjudicate legal corporate control. Separately qualified real-world legal authority evidence is interpreted by Legal Compliance to provide restrictions, preservation and appeal safeguards. Identity, Authorisation and optionally Workflow execute any digital transfer only after independent evidence and approvals; no platform operator or Legal Compliance bypass of IAM.

**UC-07 — Upcoming filing, statutory notice or periodic obligation.** An effective qualified obligation registers trigger, due time/timezone, accountable owner, source revision and expected evidence. Scheduler raises due checks, Notifications sends reminders and Workflow routes reviews where configured. Domain owner prepares the filing or notice; Integrations transmits it if needed. Legal Compliance sees \`submitted\` versus \`receipt_unconfirmed\` versus \`fulfilled\` distinctly, records corrective needs for overdue or failed outcomes and never treats a successful MQ delivery as completion.

**UC-08 — Cross-border service and conflicting obligations.** Authoritative activity facts identify multiple jurisdictions, or a customer opens in an unsupported market. Each supported regime is qualified separately, with scope, effective law, exemptions and missing proof. Unresolved conflict or unsupported mandatory qualification causes a narrowly targeted restriction and competent legal review; there is no implicit worldwide legal support or automatic selection of the weakest requirement.

**UC-09 — Employee/learner/credential safeguarding.** Recruitment or Course sends actual service, age/eligibility, country, issuer/accreditor and purpose-relevant facts, not unnecessary personal dossiers. Legal Compliance returns employment, safeguarding, accessibility, recognition and retention conditions for that precise scenario. Recruitment/Qualification/Credentials enforce their own steps and supply completed outcomes. A platform-admin role cannot create an external professional licence or accredited award.

**UC-10 — External publication and downstream removal.** Publisher/Comments proposes public content; Moderation or a regulator later raises a restriction. Legal Compliance qualifies service-specific disclosure, takedown, retention and reporting obligations. The source owner commits a visibility/removal transition; Search/Federation and caches acknowledge their own derived-copy updates. If remote removal is unconfirmed, the review status remains partial rather than declaring universal takedown.

### 12.3 Concise example of the full interface exchange

1. A domain supplies \`tenantScope\`, \`resourceRef\`, \`activity\`, \`effectiveAt\`, source fact revisions and \`purpose\` in a server-authorised \`evaluateApplicability\` request.
2. Legal Compliance returns \`decisionId\` (if persisted), \`applicability\`, \`sourceAndRuleVersions\`, \`requiredControls\`, \`missingFacts\`, \`reviewBy\` and a minimised reason. If outside coverage or critical evidence is stale, the result is \`unsupported/unresolved\`, not \`false\`.
3. If legally gated, the domain rechecks current state and enforces the decision within its own invariant transaction; the domain owns the business result.
4. Its committed event and \`recordControlReceipt\` report applied rule version, affected resource, source revision and \`accepted / completed / partial / failed / unknown\`. Message Queue may transport events; it never becomes a human review queue.
5. Legal Compliance reconciles an obligation/control state and, when appropriate, raises a review or corrective-action requirement; Audit records independent evidence and Reporting derives authorised summaries.

## 13. Conceptual end-to-end acceptance scenarios


| ID | Input / trigger | Expected observable result and distinct owners |
|---|---|---|
| ACC-01 | Administrator creates a new marketplace activity with fully verified supporting facts | Legal Compliance evaluates approved rules, gives applicable conditions; Marketplace enforces; ordinary admin cannot approve new law |
| ACC-02 | New legal amendment imported from external feed | Candidate remains unapproved; reviewer verifies source/effective reach; impact index identifies affected tenants and services; no silent activation |
| ACC-03 | Domain asks to finalise a regulated transaction with insufficient critical facts | Typed `unresolved`, missing-fact reasons and only affected unsafe action withheld, no permissive default |
| ACC-04 | Reviewer approves source version, but underlying facts changed during sign-off | Revision/concurrency conflict forces renewed assessment; no stale approval |
| ACC-05 | Law amended retroactively | Original historical known-at decision preserved; linked current legal as-of requalification explains difference |
| ACC-06 | Legal hold approved for narrow records; event delivered but domain fails preservation | Hold is effective; physical enforcement remains partial/failed, urgent exception/evidence and retry; no false compliance |
| ACC-07 | Hold release proposed while separate lawful duty still prevents erasure | Review release; other restrictions remain; domain/Privacy decides disposal and confirms actual copies |
| ACC-08 | Subject rights request with disputed retention/legal hold | Privacy and Legal Compliance qualify narrow exceptions; unrelated data processed; no indefinite blanket retention |
| ACC-09 | Two-country service has contradictory duties | Separate scoped determinations with explicit conflict; qualified review; no weakest-rule shortcut |
| ACC-10 | External regulator gateway accepts transport but not filing | Integrations status sent; filing remains receipt-unconfirmed; legal obligation not marked fulfilled |
| ACC-11 | Message Queue duplicates/replays or delivers out of order | Event identity/revision deduplication; authoritative refetch; no duplicate reviews/holds; independent decision history |
| ACC-12 | Scheduler misses a deadline then resumes | Reconciliation flags overdue obligation, preserves original due timestamp and triggers attributable escalation |
| ACC-13 | Tenant owner, platform operator or parent tenant attempts another tenant's privileged legal dossier | Authorisation denies; redaction and audit evidence; no implicit tenant-parent access |
| ACC-14 | Optional Workflow or external legal feed unavailable | Native minimal legal review remains usable; verified local source may continue within freshness bounds; missing critical evidence returns unresolved |
| ACC-15 | Configured feature flag disables an operational control despite mandatory legal duty | Domain refuses unsafe state; Legal Compliance qualification remains effective; no tenant waiver |
| ACC-16 | Effectiveness review discovers control configured but not enforced | Distinct control implementation/evidence/observed-effectiveness states, accountable corrective requirement and independent confirmation |
| ACC-17 | Qualified interpretation reused for a second organisation | Shared rule version reused only after separate fact-supported tenant-specific applicability; no cross-tenant evidence leakage |
| ACC-18 | Optional OSCAL/DMN exchange requested outside supported subset | Explicit supported-format/version contract and rejection, not false full standards-conformance claim |
| ACC-19 | Legal text includes malicious instruction or attempts arbitrary code execution | Treat as untrusted source content; deterministic parser prevents executable side effects; reviewer examines cited text safely |
| ACC-20 | Domain attempts to infer age-assurance completed from legal requirement | Reject inference; required condition and Verification's actual completion evidence separate |

No local tests/builds were run. These are contract acceptance scenarios requiring future CI, contract tests, security assessment, minimal consumer and real-world legal qualification evidence.

## 14. Decision register and unresolved work

| ID | Proposed decision, preserved for owner approval | Approval |
|---|---|---|
| LC-01 | Qualified versioned source, interpretation, coverage and organisation-specific applicability with explicit unknowns | Proposed |
| LC-02 | Legal Compliance owns narrow legally authorised holds; source-domain owns actual preservation, release and deletion results | Proposed |
| LC-03 | Stable qualified applicability/obligation/control/receipt public contract; affected unsafe operations fail safely | Proposed |
| LC-04 | Native approved local rule corpus and manual review; external legal providers optional evidence feeds | Proposed |
| LC-05 | Separable role-aware GUI and **Legal Review Worklist**, not a technical message queue; headless parity | Proposed |
| LC-06 | Legal-person/control adjudication remains a separately justified boundary and verified evidence source, not silently reowned | Open boundary within proposal |
| LC-07 | Legal hold/statutory constraints reconcile with Privacy rights and domain preservation without duplicating Privacy authority | Proposed |
| LC-08 | Typed evidence variables, restricted deterministic policy evaluation and automatic reassessment, caching, replay-safe recovery | Proposed |
| LC-09 | ISO 37301-inspired obligation/control/evidence/improvement lifecycle and ISO 37302 effectiveness assessment | Proposed |
| LC-10 | DMN 1.6-aligned restricted decision tables/semantics, without requiring full DMN implementation | Proposed |
| LC-11 | W3C PROV-O/ISO 15489-aligned source → interpretation → applicability → control → evidence traceability | Proposed |
| LC-12 | ISO 31000 risk-based prioritisation; ISO 19011-informed independent review, competent approval and measured control assurance | Proposed |
| LC-13 | Security/privacy/records/continuity control mapping and optional OSCAL/GRC exchange; do not claim certification | Proposed |

**Needs owner decisions:** supported jurisdictions/activities at launch; legal-source rights, curation responsibility and qualified reviewer accreditation; professional counsel evidence confidentiality and appeal; minimum coverage needed before regulated operation; formal legal-entity ownership authority; mandatory review and dual-control thresholds; controlled rule language subset and compatibility policy; filing-specific statutory decision responsibility; retention/hold review law; regulator evidence/acceptance semantics; any full DMN/OSCAL interoperability obligation; relationship of risk scoring and mandatory approval. No blanket international legal validity or universal retention schedule is assumed.

**Future implementation alignment:** published independently usable root `CONTRACT.md` (there is currently none verified), threat model, versioned schemas/events/ports, evidence minimisation, storage register, permitted module/classification packaging, simple single-call Nuxt host composition or independent consumer as appropriate, CI/ASVS/WCAG acceptance, supplier/legal-source licence review, scoped legal validation and rollback/compatibility. A conceptual specification does not approve changing governing ADRs or implementing new repositories.

**Parallel-Git handover:** This review remains in **draft PR #85** until owner approval. Its original branch diverged from newer blueprint `master`; reconcile shared Job/Audit/Reporting/catalogue/register edits, check current accepted ADR changes, link validity, tests/checks/mergeability and protected master immediately before any authorised squash merge. Do not merge based on this text alone.

---

