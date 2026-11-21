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

## Cross-capability note — Authorisation and aggregate disclosure (15 November 2026)

**Status:** Proposed reciprocal interaction; not an established Reporting adapter. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) can provide current visible-group filters and per-resource permission decisions. Reporting owns report generation and derived output but must enforce context-specific access to filters, underlying rows, totals, small-cohort aggregates, exports and retained report snapshots. Query scoping alone cannot certify disclosure safety or persist rights after revocation. Reporting's conceptual review remains incomplete.

## Cross-capability note — Billing report-source and derived-report contract (15 November 2026)

**Status:** Agreed conceptual direction for Billing BIL-S05 integration, not a completed Reporting capability review, a verified Reporting root `CONTRACT.md` or an implemented adapter. See [Billing's reporting interface](../billing/capability-record.md#billingreporting-contract-boundary--bil-s05-elaboration-15-november-2026) and the existing Authorisation aggregate-disclosure note above.

**Reporting consumes from Billing (conditional public-contract relationship):** tenant/entity/party-scoped authorised charge and charge-line queries; states of assessments, finalised charges, disputed/waived/reversed amounts; arrangement, billing-cycle and run status; invoice handoff and provider reconciliation exceptions; source/reference revisions and effective periods; original currency, tax/discount/rate facts where permitted; Billing-owned versioned events for projection invalidation. Billing owns those business facts, rules, durable outbox and authority scope. Billing may expose its own native operational summaries even without Reporting installed. No Reporting service may access Billing's tables or implement competing commercial-charge calculations.

**Reporting supplies to Billing:** permitted report catalogue/definition versions; execution request/status and report reference; snapshot timestamp, data lineage, source revision/cutoff, freshness/completeness and explicitly unknown coverage; authorised visualisation/export/distribution outcome; report invalidation and refresh status. Reporting owns report definition, orchestration and derived artefact lifecycle, not charge corrections or downstream financial confirmations. A queued report is not a completed file; a created file is not proof of delivery.

**Other owning sources:** Invoice alone owns issued/received invoice and credit-document status; Accounting alone owns ledger postings, recognised revenue, receivables/payables and financial statement meaning; Payment Gateway owns payment execution. Reports comparing these sources must preserve each source's status, period, currency and provenance and label unmatched records, delayed evidence and partial coverage. Reporting may derive comparisons, aggregates and alert indicators but cannot promote such results into authoritative financial facts or independently remediate Billing/Accounting/Invoice records.

**Security and history:** Billing authorises each data query; Reporting independently controls filters, aggregates, small-cohort inference risks, report generation, saved result reads, scheduled delivery and exports, re-checking rights after revocation. Tenant/entity cross-scope reports require explicit authorisation, not just a valid group filter. Reporting must distinguish original historic source snapshots from current corrected/restated projections and report unavailable historical revisions rather than invent reproducibility. Preserve report-definition version, parameters, data source/authority references, effective and observation times, currency/FX policy provenance, missing source coverage and legal retention/disclosure constraints.

**Failure/absence and performance:** Reporting unavailable or behind does not block Billing's core transactions; expose projection age, missing periods, provider uncertainty, failed refresh and report execution status. Replayed Billing events must be idempotent and never double-count; update derived views through authorised source reads. Large analytics should not degrade Billing charge-finalisation operations. Logging handles technical report diagnostics; Audit handles risk-selected attributable export/privileged access evidence. Reporting owns no Audit evidence.

**Presentation:** Billing's optional dashboard may link to a Reporting-owned catalogue and report results with bounded scoped filters; the menu is not an access grant. Reporting's later UI review must establish accessible, themed, internationalised report views and appropriate permission-specific navigation.

**Acceptance direction:** Native Billing without Reporting; incomplete run; retroactive adjustments/as-was versus as-now; multi-currency reporting; cross-tenant and small-cohort disclosure denial; revocation after report generation; stale external-provider data; Billing/Invoice/Accounting reconciled versus unmatched totals; duplicate/out-of-order events; failed scheduled report delivery. This note does not predetermine Reporting's full functional scope or package/API architecture.

## Cross-capability note — Booking analytics source facts (15 November 2026)

**Proposed reciprocal relationship only.** [Booking](../booking/capability-record.md) supplies authorised, minimised, versioned reservation, occupancy, lead time, cancellations, attendance/no-show **where Booking owns evidence**, provider reconciliation and availability freshness for scoped reporting. Reporting owns report definitions, execution and derived presentation; Billing/Accounting own financial outcomes, Asset owns asset condition, and external resources retain their source facts. A report snapshot cannot create/cancel reservations or infer attended service from confirmation alone. Sensitive attendance/location inference, tenant aggregation and disclosure require explicit server-side policy.

**Booking approval clarification (15 November 2026):** Booking BK-01–BK-05 are approved in principle. [Booking's specialist Reporting interface](../booking/capability-record.md#booking--reporting--scoped-operational-and-historical-analysis) provides protected, revisioned booking and available-capacity source facts with status, effective time/zone, freshness, provenance and coverage for utilisation, demand, cancellation, lead time, no-show (when Booking-owned), booking-channel/provider exceptions and authorised exports. Reporting alone owns analytical definitions, snapshots, execution, derived visualisation and delivery. Tenant enablement is not permission: per-user, group, resource, department and action scoping must be rechecked on source reads and report viewing/export, including revocation after saved report creation and cross-tenant/small-group inference. Reporting absence never blocks native reservations; snapshots cannot be promoted into booking or Billing/Accounting authority. Reporting's own full review remains open.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Provide authorised derived tenancy, provisioning, payments, quota, governance and policy-attestation reporting over published source contracts; never inherit child private data simply via parentage.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.

## Cross-capability note — Proposed Caching operational aggregates (16 November 2026)

**Agreed conceptual boundary; implementation unverified.** [Caching](../caching/capability-record.md) may supply purpose-limited, authorised cache efficiency, capacity, freshness and failure aggregates with reporting period, source scope, completeness and provenance. Reporting owns report definitions and generated results, not cache provider validity, IAM policy or original business records; it must prevent cross-tenant and small-cohort inference. Reporting outage never blocks normal source operation or cache invalidation. No package dependency inferred.

**Approved conceptual boundary (16 November 2026):** Reporting can offer historical performance/efficiency analysis using authorised, source-identified and time-qualified aggregates from Caching/Observability, not cached content or cache backend tables. Missing measurements must remain visible; retention and aggregate grain are later policy/technical decisions.



## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Review-approved documentation direction, not an implemented interface or governing ADR. See [safety review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

Reporting consumes authorised source, Moderation, Content Security, Audit and Federation outcomes to derive scoped indicators: submission assessment coverage with denominator, exposure and enforcement latency, case backlog, appeals/reversals, provider failures, reporting and Hub/cache withdrawal gaps. It does not own case or domain facts; full scanning coverage does not prove accuracy or compliance.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine supplies authorised comment submissions (including pending/rejected), exposure and visibility transitions, edit/erase/restore outcomes, thread volume and qualified coverage denominators, policy/version, freshness/completeness, tenant and target granularity. Reporting calculates cross-source aggregates and compliance indicators using Moderation, Content Security and Audit evidence, without becoming comment owner. Distinguish hidden from deleted, request from actual enforcement, missing measurements, Hub withdrawals and false-positive reversals.

### Comments Engine CE-06 — owner-approved ethical boundary (17 November 2026)

**Status:** Owner-approved conceptual direction in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), not an implemented API or governing ADR. Comments Engine supplies authorised, scope-aware comment/reply counts and chronological/thread status measures, **not** social likes, public reaction popularity, engagement scores or engagement-driven ranking. Reporting may analyse operational quality, safety and response effectiveness with valid purpose and privacy constraints, but must not silently reintroduce a public social-scoring system as a derived report or leaderboard. Separately justified professional evaluation or formal voting remains with the appropriate domain owner and needs ethical/security review.


### Comments Engine CE-06 — approved private appreciation exception (17 November 2026)

**Status:** Owner-approved conceptual refinement in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), not implemented. Comments Engine may hold essential individually scoped acknowledgement records to prevent duplicates, permit withdrawal and support privacy and misuse enforcement. It may present a private qualitative appreciation notice to an authorised recipient, but **never an accumulating count**. Reporting must not repurpose these records into popularity metrics, public reaction counts, leaderboards, engagement optimisation or individual reputation scores. Aggregate abuse diagnostics require distinct justified purposes and disclosure restrictions.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Reporting may consume authorised minimised aggregates of Content Security scan completion, category detection, incompleteness and quality metrics, with uncertainty/provenance. Do not use raw detector scores to rank people or infer popularity; Content Security owns individual verdict evidence and source owners own enforcement.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course supplies authorised versioned course catalogue, curriculum and lifecycle facts; Reporting owns derived analytics. Learner admission and completion measures must come from Enrolment/Training with independent disclosure checks, not from Course. This note does not complete the separate reporting review.

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-09/11 agreed:** cohort capacity, attendance and completion reports source authoritative facts from Enrolment/Events/Booking and Training/Assessment, not the Course catalogue. Credentials supplies credential issue/revocation facts, but no report can confer an award. Ensure historical version, small-cohort and safeguarding disclosure constraints. This note does not complete the separate reporting review.


## Reciprocal conceptual contract — Credentials (18 November 2026)

**Status: CRED-01–16 owner-approved conceptual boundary; CRED-17 framework selection pending (18 November 2026, PR #62).** Credentials publishes authorised tenant/issuer/time-scoped issued credential, expiry, suspension, revocation, replacement, issuance backlog and verification-outcome source facts via scoped reads plus committed status events, including source revision, effective/as-of times, coverage and staleness. Reporting owns report definitions, aggregations, snapshots, exports, delivery and refresh lifecycle; returns report reference/status, completeness, lineage and disclosure controls. Distinguish qualification awards (Qualification-owned) from issued credentials (Credentials-owned); do not double-count corrections/replacements or convert partial coverage into valid totals. Recheck saved-report disclosure and small-cohort privacy independently. Reporting outage must not block issuance; no private tables or claimed implemented adapter.

## Reciprocal note — Events conceptual review (18 November 2026)

**Events review reciprocal (18 November 2026; EVT-01–10/12–15 owner-approved; implementation unverified):** [Events](../events/capability-record.md) supplies authorised versioned event/session read models, schedule and cancellation state and privacy-limited source change events. Reporting owns report definitions, aggregation and exports; any joined participation, reservation or learning metrics require respective Booking/Enrolment/Training authorities and disclosure checks. Event creation is not proof of attendance or bookings.

## Events interface reciprocity — 18 November 2026

**Events approval and attendance boundary (18 November 2026):** [Events](../events/capability-record.md) supplies versioned, authorised event/occurrence programme/status, change/cancellation timelines and event-specific restrictions; *if EVT-15 is approved*, purpose-limited attendee and observed attendance counts with confidence, coverage and redaction. Reporting owns definitions, aggregation, reports, delivery and freshness; it must not infer attendance from RSVP or Booking alone, leak a participant roster through small-group statistics, or modify Events facts. [Contract detail](../../../reviews/events-contract-attendance-and-handover.md).

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** Reporting owns report-specific dataset/snapshot, job state, generated artefact reference, retention and authorised distribution; the governing Export Library only converts a caller-approved safe rich-text tree to PDF/DOCX-format bytes/stream and diagnostics. Reporting must retain source lineage, completeness, disclosure controls, recipient checks, revocation and recovery. Rendering completion is not report-delivery completion. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.

## Federation — reciprocal conceptual note (18 November 2026)

**Status:** Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69), not a published implementation contract or completed independent review. See [Federation conceptual contract](../federation/capability-record.md).

Reporting consumes authorised Federation participation, delivery, freshness, rejection and withdrawal read models/events, with source/peer scopes and incomplete/unknown counts. Reporting owns aggregates only and must never infer verified deliveries from attempts or mutate underlying exchange state. Public directional ports, explicit absence modes and acyclic package dependencies apply.


## Reciprocal conceptual note — Help capability (18 November 2026)

**Status:** HELP-01–04 owner-approved conceptual direction; this specific intake/GUI elaboration is proposed in [Help PR #72](https://github.com/nuxt-layers/architecture-blueprint-review/pull/72), not an implemented adapter or replacement for this capability's future full review. [Help public contract](../help/capability-record.md#approved-direction-elaboration--published-contracts-standards-libraries-and-gui-18-november-2026).

Help may publish public-contract, permission-scoped coverage/freshness views: documented versus mapped contexts, outdated or broken topics, locale gaps and safe aggregate operations. Reporting owns report definition, execution, snapshots, derived measures, suppression and disclosure enforcement, not source mappings or documents. Raw queries, identified reading histories and small-cohort inferences are excluded by default; absence of Reporting never blocks Help.

## Cross-capability note — Gaming conceptual review (18 November 2026)

**Gaming (18 November 2026; proposed, not owner-approved):** [Gaming](../gaming/capability-record.md) supplies authorised game instances, participants, provisional/final/corrected results and rankings with ruleset, competition scope, effective revision, coverage and privacy restrictions. Reporting may own cross-game aggregates and derivative reports but never edits official scores, standings or source records. On corrections, invalidate/recompute with replay-safe handling; protect small-cohort and child-identity inference.

### Gaming portal scope correction — 18 November 2026

**Gaming scope clarification (18 November 2026, owner-provided; detailed decisions proposed):** [Gaming](../gaming/capability-record.md) is a shared game catalogue, launch portal and accepted-score/leaderboard owner, **not** a generic game engine. Independently composed game layers own their own gameplay, session/move/physics state, game rules and original results. Earlier gaming reciprocal wording implying that Gaming owns gameplay, game rounds, adjudication of moves or original raw results is superseded. This owner-supplied distinction takes precedence within this working review; no implementation or published game contract is asserted.



## Reciprocal conceptual interface — IAM Integration (18 November 2026)

**Status: Owner-approved conceptual direction in IAM Integration review PR #73; not a verified Reporting implementation contract.** IAM Integration can expose authorised tenant-scoped operation-stage, revocation/reconciliation, readiness and approval-processing summaries with per-member source status/provenance. Reporting consumes these via published authorised query/read-model interfaces and owns report definitions, aggregations and exports; each query, filter, snapshot and export must independently respect current IAM access and Privacy limits. Reporting never reowns identities, sessions, role changes or Profile data, and correlation/aggregate values cannot bypass small-cohort disclosure restrictions. See [IAM Integration idealised public contract](../iam_integration/capability-record.md). Do not add a direct package dependency on IAM Integration merely for these event/read-model relationships.


## Identity reciprocal input/output — 18 November 2026

**Status: recommended Identity reciprocal elaboration, 18 November 2026, [draft PR #74](https://github.com/nuxt-layers/architecture-blueprint-review/pull/74); not a verified Reporting connector.** Identity offers authorised, minimal and revision/freshness-qualified principal, tenant, group, direct membership, invitation and digital governance status and lifecycle events. Reporting owns report templates, execution, derived aggregates, snapshots, lineage, distribution and scoped export; it may return execution/freshness/disclosure outcomes but cannot mutate Identity or become its directory. Ensure cross-tenant and small-cohort non-inference, reauthorisation of saved exports after revocation, and clear unknown/stale coverage. Reporting absence must not disable Identity's native directory. See [Identity extended review](../identity/capability-record.md#extended-review--published-interfaces-observability-standards-library-suitability-and-gui-18-november-2026).


## Infrastructure reciprocal reporting relationship — 18 November 2026 (owner-approved Infrastructure direction; Reporting review remains independent)

[Infrastructure's approved conceptual contract and companion review](../../../reviews/infrastructure-approved-contract-standards-gui.md) supplies qualified, sanitised infrastructure readiness, change status, backup/recovery verification and incident/UTC synchronisation summaries with provenance and freshness. Reporting may aggregate these for authorised platform operators but **does not own provider truth or raw control-plane resources**, must preserve unknown/degraded/partial states, and must not expose credentials or private tenant data. Reporting retains report definition, execution and permitted disclosure authority. This is a reciprocal proposal for Reporting's separate conceptual/implementation alignment, not an assertion of published runtime API.

## Integrations reciprocal interface — 18 November 2026

**Status: owner-approved conceptual Integrations direction INT-01–06 in [draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76), not a verified published API or approval of this capability's independent review.** Integrations provides authorised tenant/purpose-scoped, versioned operational provider/connection/synchronisation/reconciliation facts (volume, request statuses including unknown, costs/rate limits, lag, supported operations, evidence provenance and coverage) through public read models and committed change events. Reporting owns report definitions, derived aggregates/snapshots, refresh, export and disclosure; it returns report run/reference/completion/status to legitimate consumers. A provider receipt is not a domain business result, and Reporting must not read Integrations private stores. Reporting absence does not block native Integrations health queries. [Integrations proposed contract](../integrations/capability-record.md#reciprocal-logging-audit-and-reporting-public-interfaces); conceptual owner approval of INT-01–06 only.


## Inventory reassessment reciprocal proposal — 18 November 2026 (PR #81)

**Status: proposed, not approved or implemented.** Inventory's proposed versioned, authorised stock movement/position and reconciliation read models include stock-account, lot/serial where permitted, physical/usable/reserved/in-transit/restricted dimensions, as-of revision, provenance and uncertainty. Reporting computes presentations and aggregates, not stock balance, availability commitments or financial valuation. Avoid summing overlapping dimensions or exposing consignment/tenant costs across scopes. See the [Inventory reassessment contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md) and [Inventory record](../inventory/capability-record.md#renewed-conceptual-design-challenge--18-november-2026-draft-pr-81). This note preserves earlier approvals in this capability and does not complete its independent review.


### Inventory manufacturing traceability — owner-approved conceptual reciprocity (18 November 2026; PR #81)

**Approved Inventory-side conceptual requirement:** Reporting consumes versioned Inventory positions, stage/custody history, lot genealogy, WIP ageing, material yield/scrap, tool/consumable quantity usage, late handovers and reconciled/unknown scan states for authorised reports. Show confirmed-as-of time, not invented continuous physical presence; avoid counting the same lot across warehouse/staging/machine/coater/finished bins. Reporting owns analytics, not movements. This note approves the **Inventory-side requirement only**, does not change this capability's independent approval status or claim a running integration. See [shop-floor flow and public contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026).


### Inventory operator usability and correction reciprocity — 18 November 2026 (PR #81)

**Inventory owner-approved RINV-09–12; RINV-13 proposed, not separately approved:** RINV-09–12 are Inventory-owner approved. Proposed Inventory UX RINV-13 requires evaluation with representative shop-floor operators, measuring task completion, critical errors, retry/recovery and training effort without invented thresholds. Reporting may consume permitted aggregate operational/usability outcomes and revisioned WIP/movement facts, subject to purpose and worker privacy; not claim continuous location tracking or reconstruct sensitive individual performance reports without authority. See [Inventory operator adoption contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#approved-final-traceability-refinements-and-operator-adoption-design--18-november-2026). This does not revise independent approvals or claim an implemented UI.

## Invoice reciprocal public interface — 18 November 2026

**Status:** Invoice conceptual design approved, INV-01–06 closed (18 November 2026); Reporting's full review and implementation remain unverified. [Invoice](../invoice/capability-record.md#reciprocal-contract-with-logging-audit-and-reporting) supplies authorised tenant/legal-entity/party-scoped invoice and credit status, issuance periods, currency/tax breakdowns, correction lineage, source revision, payment allocation projection with freshness/uncertainty, provider-confirmation exceptions and completeness/checkpoints. Reporting owns definition, derived results, distribution/export and cross-source comparisons with Accounting, Billing and Payment Gateway; it cannot claim posting, payment or tax recognition on Invoice's behalf. Recheck source permissions and disclosure of aggregates, snapshots and exports, including revoked access and tenant isolation; missing provider evidence must remain unknown, never treated as zero.


## Job vacancy/headcount reporting reciprocal proposal — 19 November 2026 (draft PR #84)

**Status: Proposed in [Job review](../job/capability-record.md).** Reporting may consume purpose- and tenant-authorised Job position/opening revisions, permitted vacancy counts and publication statuses. Employment, not Job, remains source of actual engagement/occupancy; any fill ratio/available-seat report must carry source, completeness, as-of time and uncertainty, and must not equate absent Employment data with zero employees. Reporting owns report assembly, not underlying post, engagement or candidate records. No unrestricted sensitive personnel export is implied.

## Job / Recruitment boundary supersession — 20 November 2026

**Updated reciprocal JOB-01–09 authority (20 November 2026):** Prior Job-derived vacancy, approved-seat and occupancy projections are superseded as a **Job-owned** interface. Job supplies authorised position definitions and revisions. Proposed Recruitment will supply vacancy/requisition and application/selection facts after its own review; Employment remains authoritative for effective assignments and actual occupancy. Reporting composes authorised qualified source projections with as-of, completeness and unknown semantics; it does not treat missing occupancy as zero or gain applicant dossier access by default. [Job](../job/capability-record.md) · [Recruitment proforma](../recruitment/capability-record.md).

## Job position-only reciprocal interface — 20 November 2026

**Status: Conceptual, following owner-approved JOB-01–09, not an existing adapter.** **Job reciprocal public data clarification:** Job provides only authorised position descriptions, categories, grades where disclosed, effective revisions and status/history; Reporting owns report definitions, snapshots, aggregates and permitted exports. Recruitment is the proposed vacancy/application source; Employment is the actual workforce/assignment source. Reports must not count positions as open vacancies or incumbents. Preserve source revision, as-of time, missing-data and disclosure limits. [Plain-English contract review](../../../reviews/job-public-contract-standards-and-gui.md); no published Reporting root contract was verified.


## Recruitment reciprocal contract proposal — 20 November 2026

**Status: Proposed in [Recruitment draft PR #99](https://github.com/nuxt-layers/architecture-blueprint-review/pull/99), not owner-approved or implemented.** Recruitment supplies scoped, versioned vacancy/application/decision measures and corrections; Reporting owns aggregates, not underlying hiring determinations; apply small-cohort privacy safeguards. Cooperation uses published contracts/host ports, without private state or mandatory cyclic imports. [Recruitment record](../recruitment/capability-record.md).


## Legal Compliance reciprocal conceptual contract — 19 November 2026 (draft PR #85)

**Status: proposed, pending owner approval; not an implemented or published interface.** [Legal Compliance dedicated conceptual contract](../legal_compliance/capability-record.md) proposes scoped, time/version/source-qualified legal applicability, mandatory restrictions, holds, deadlines and uncertainty. **reporting** supplies only authoritative, minimally necessary resource/service/activity/tenant context and completion/refusal evidence through documented public contracts; Legal Compliance does not take ownership of reporting's records, business decisions or enforcement. Statutory interpretation is not personal Authorisation, Privacy's specialist consent/rights rules, or proof of regulator acceptance. Missing or conflicting mandatory legal qualification holds only the affected unsafe action; authorised source owners report applied decision version and partial/failed enforcement. Cross-capability cooperation is host-composed, not an implicit direct package dependency. Existing neighbouring decisions and active PR proposals retain their own status.


## Legal Compliance control effectiveness reporting — 20 November 2026

**Approved conceptual reciprocity under draft [PR #85](https://github.com/nuxt-layers/architecture-blueprint-review/pull/85), not implemented.** [Legal Compliance canonical contract](../legal_compliance/capability-record.md) offers authorised obligation-to-control mappings, qualified applicability/coverage, receipt/exception status, effectiveness criteria and provenance/known-at dates, informed by ISO 37301/37302. Reporting owns derived dashboards, report definitions/aggregates/exports, and must distinguish requirement known, control implemented, evidence received, control effective, corrective action verified and legal support unknown. No global `compliant` flag, reporting-owned legal interpretation, or regulator acceptance inferred from transport.
