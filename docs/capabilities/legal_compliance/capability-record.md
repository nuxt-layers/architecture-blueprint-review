# Legal Compliance — Capability Record

**Canonical capability:** `legal-compliance` (Foundation in governing catalogue)  
**Blueprint directory:** `docs/capabilities/legal_compliance/` (actual path; do not rename)  
**Conceptual revision:** 20 November 2026 — comprehensive proposed specification, **not yet owner-approved**  
**Review:** [draft PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85)  
**Authority:** Accepted ADRs and normative standards in [architecture-rules](https://github.com/nuxt-layers/architecture-rules); this blueprint is non-normative.  
**Opening governing baseline:** `b920ce0d8b361de000a6739a16123dbdc56df7a7`; **opening blueprint baseline:** `6dac83a03da8704f7945ee1bc894f2248300445a`. Blueprint subsequently advanced to `d39df23e087cd0510c82ba2cea78996c7624850f`; final reconciliation remains required.  
**Evidence classification:** Governing responsibility **established**; LC-01–LC-13 **proposed for owner review**, including LC-08 from the prior exploratory design. Historical separately owner-approved *neighbouring* decisions are preserved below, without implying approval of this complete specification.

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

## 12. Conceptual end-to-end acceptance scenarios

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

## 13. Decision register and unresolved work

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

## Appendix — Previously recorded conceptual review and reciprocal history

The following material is retained unchanged as provenance of previous proposals, owner-labelled decisions and adjacent-capability notes. **The comprehensive model above is the latest proposed synthesis**; historical provisional wording does not supersede accepted governance or silently become implemented contract evidence.

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

## Declarative variables, flags and automation execution — 20 November 2026

**Status: proposed LC-08 detailed design; awaiting owner approval, no implemented public contract.** This builds on the [user-driven use cases](#user-driven-operation-and-human-approval-worklists--20-november-2026). Existing ADR-0018 grants Legal Compliance legal applicability/constraint authority, not Configuration/domain state ownership.

### Information categories, ownership and trust

| Category | Meaning / example | Source and safeguards |
|---|---|---|
| Trusted context | `tenant.id`, caller assurance, request time, resource | Host/IAM/Clock trusted context; browser cannot nominate another tenant to obtain access |
| Source fact | `service.category`, `entity.registered_country`, `activity.starts_at` | Owning domain, Identity/Configuration or separately evidenced legal-entity authority; source revision/validity required |
| Declaration | `audience.includes_children`, intended jurisdiction | User assertion through Configuration or source domain, tagged `asserted` rather than automatically `verified` |
| Qualified legal knowledge | source, approved rule, applicability predicates, legal effective interval | Legal Compliance-owned reviewed version; cannot be changed by a tenant feature flag |
| Derived assessment | applicable/not-applicable/unresolved/unsupported, rule version and coverage | Legal Compliance computes from validated fact snapshot and effective approved rules |
| Operational fulfilment | `age_assurance.completed`, `hold.applied`, `filing.accepted` | Verification, record owner, regulator/filing owner respectively; Legal Compliance may reference evidence, not reown state |
| Work orchestration | review task state, scheduled due trigger, event transport | Workflow, Scheduler, Message Queue; none owns legal verdict |

**Variables are typed and registered** with stable semantic identifier, allowed values/units, source owner, purpose, scope, privacy classification, trust grade, freshness/TTL, canonical time, version, validation, missing-data handling, and whether user-editable. A Boolean is never a sufficient encoding for legal applicability. Use `applicable | not_applicable | unresolved | unsupported` and separate source knowledge/approval/enforcement status; `false` is not inferred from missing evidence. Flags may be derived *from* qualified outcomes by the consuming domain, but cannot replace the source decision.

### Exact conceptual load/evaluate/commit procedure

1. **Trigger:** synchronous authorised command/query, source-owned committed outbox event, schedule trigger or authorised human reassessment. Every trigger has source/event ID, correlation, subject/resource, change version and effective time; do not trust browser-supplied tenant identifiers or outbox delivery as authorisation.
2. **Scope/authorise:** server resolves caller, tenant and resource, permission and risk/assurance. Legal Compliance checks declared decision purpose and authorised supported jurisdictions/services.
3. **Select rules:** choose reviewed, active legal-rule versions by jurisdiction, territorial reach, regulated activity/entity/audience and legal-effective/as-of time. Distinguish `knownAt` from `legallyEffectiveAt`; do not apply today's law silently to a historic decision.
4. **Plan dependencies:** extract the referenced variable keys from selected rules' validated expression trees/decision tables; deduplicate fetches, and use stable public contracts and composition-supplied fact-resolver ports. Do not query another capability's tables.
5. **Load fact snapshot:** gather narrow authoritative facts plus source owner, revision/ETag, observation time, expiry, provenance and verification state. User settings are validated assertions; checked source facts and independent legal authority take precedence in their defined scopes. Prefer snapshot/revision consistency or re-read critical facts if they changed during evaluation.
6. **Normalise and validate:** schema check, canonical identifiers, known jurisdiction codes, units and Clock time zones, source/tenant binding, type, expiry, contradictory evidence and sensitive-data minimisation. Missing, invalid, stale, conflicted or unsupported critical fact is a typed `unresolved` outcome, never default `false`.
7. **Evaluate deterministically:** use a restricted typed operator set (equality, set membership, comparison, logical all/any/not, range/date operations) with documented null/unknown handling; no `eval`, arbitrary JavaScript, network access or externally authored side-effect code. Evaluate **all** applicable rules and combine mandatory conditions without permitting a weaker tenant rule to override statutory/security floors. Conflicts escalate rather than assume priority.
8. **Return result:** `decisionId` (when persisted), tenant/resource scope, fact snapshot digest/references, applicable rule IDs/versions, per-jurisdiction coverage, as-of/knowledge dates, required/forbidden/conditional operations, obligations/hold instructions, unresolved reasons, freshness/review deadline and privacy-limited explanation. A read-only query need not generate a new durable record for every attempt.
9. **Commit consequential state:** for approval/hold/obligation/important assessed action, use capability-owned persistence and atomic outbox writes to record idempotent decision/result with optimistic concurrency over source/rule revisions. Accept pending/committed/failed/unknown separately. New fact/rule revision makes prior prospective assessment stale for affected activity rather than rewriting historic evidence.
10. **Act and reconcile:** domain owner enforces, Workflow routes human reviews, Scheduler runs due tasks, Message Queue transports committed events, Notifications alerts and Audit independently accepts evidence. Record source-domain acceptance/completion receipts; message delivery does not imply actual application or regulator confirmation.

### Rules representation and versioned lifecycle

Prefer **schema-validated declarative rule/decision table**, with `ruleId`, `version`, `status`, `sourceCitation`, `sourceEffectiveInterval`, `qualificationVersion`, `jurisdictions`, `activityPredicates`, `requiredVariableKeys`, `typedConditions`, `outcomes`, `reviewerProvenance`, `approvedAt` and `supportedCoverage`. Expressions may select facts and generate qualified requirements, but have no arbitrary scripting, network or domain-write privileges. A qualified reviewer approves legal meaning, not merely JSON syntax. Parse/schema/type checks, impossible-branch and contradiction checks, sample scenarios and independent approval precede activation. Rule versions are immutable once effective; supersede by new versions with future/retroactive date semantics recorded. Unverified external law feeds create *candidates* only.

Do **not** represent an obligatory legal requirement as a tenant-editable Boolean: `legal.safeguard.enabled=false` cannot waive a statute. Domain-owned operational flags like `age_assurance.completed` require the domain's verified evidence and cannot be asserted by Legal Compliance alone.

### Loading modes and refresh/invalidation

- **Immediate synchronous query** for legally gated transactions: resolve bounded authoritative facts and qualified rules within explicit latency/timeout budgets; if critical data cannot be established, return scoped `unresolved` and hold only the affected unsafe operation.
- **Event-driven:** a source's committed fact/policy/hold change invalidates affected cached decisions by declared variable dependency and version; MQ delivers at-least-once, so handlers deduplicate, tolerate out-of-order events, re-fetch authoritative facts, and preserve independent source history.
- **Scheduled:** Scheduler invokes review/expiry/obligation checks at Clock-qualified dates and time zones; apply idempotency and overdue recovery. A missed timer is not a waiver.
- **Manual review:** privileged authorised correction or legal source update enters Legal Compliance worklist, optionally Workflow routing; revalidate against latest evidence/version before legal commit.
- **Recovery:** durable per-scope requalification/checkpoint and eventual reconciliation discover missed/replayed events and stale owner-enforcement receipts; no full tenant scans for every insignificant change. Legal Compliance owns assessment index/cache invalidation semantics where needed, not general Caching/MQ infrastructure.

**Caching:** cache only approved immutable rule bundles and sufficiently bounded derived assessments by tenant/activity/jurisdiction/fact versions/rule versions/time slice; respect retention/Privacy. For high-risk checks, revalidate freshness at commit; stale cache never proves permissibility. Optional cache provider does not change legal authority.

### Automation safety, testable conceptual scenarios

- Same `requestId` + same facts/rule versions retries → same committed state without duplicate holds/reviews; changed content with same idempotency key → conflict.
- Partial fact-provider outage → typed unresolved result; unrelated low-risk operations remain functional.
- Tenant switches a feature off → domain functionality changes; legal duty does not magically disappear if underlying regulated activity persists.
- Contradictory two-country rule outcomes → jurisdiction-specific requirements plus review/hold for affected act, not automatic choice of weaker obligation.
- Law amended retroactively → preserve past provenance and distinguish present-day legal re-evaluation from what was known at the original time.
- MQ event replay → re-fetch current authoritative revision and avoid duplicated review cases.
- Hold notification delivered but source owner preservation fails → hold effective, preservation incomplete, urgent remediation not fabricated success.
- No Workflow → native legal review state remains usable; no Message Queue → local legal decisions remain correct but required downstream enforcement cannot be considered confirmed.

### Decision recommendation

**LC-08 — Deterministic, event-driven legal applicability automation (proposed):** Define typed/provenance-scoped variables and trusted source resolvers, restricted qualified declarative rules, explicit four-state applicability, versioned decision snapshots and dependency-triggered requalification. Automate safe routine qualification, monitoring and receipt reconciliation while retaining human legal interpretation/approval and domain-owned enforcement; reuse Scheduler, Workflow, MQ and Notifications instead of creating duplicated engines. Subject to owner approval and future root CONTRACT.md/acceptance evidence.
