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

## Reciprocal conceptual note — Export renderer boundary (18 November 2026)

**Proposed Export review PR #68 (18 November 2026):** Reporting owns report-specific dataset/snapshot, job state, generated artefact reference, retention and authorised distribution; the governing Export Library only converts a caller-approved safe rich-text tree to PDF/DOCX-format bytes/stream and diagnostics. Reporting must retain source lineage, completeness, disclosure controls, recipient checks, revocation and recovery. Rendering completion is not report-delivery completion. See [Export conceptual contract](../export/capability-record.md). **EXP-01/09 open.**

## Approved Export boundary — reconciliation (18 November 2026)

**Owner-approved conceptual direction in [Export PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68):** Export is a headless, stateless `rich-text` rendering **Library** providing format discovery, conversion, output bytes/stream, metadata and typed technical outcomes. Any preceding proposed Export-owned durable jobs, data extraction, saved artefacts, recipients, delivery or revocation language in this record is **superseded as an Export ownership assignment**. The initiating source domain or Reporting owns its authorised export workflow and job/file reference; Authorisation supplies permission decisions, Storage stores bytes, Audit retains risk-based evidence and Logging receives scrubbed technical diagnostics according to their boundaries. CSV/XLSX are conditional on a separately approved validated tabular contract. This is not a claim of implemented interoperation, not an approval to change accepted governing rules, and not a merge authorisation.
