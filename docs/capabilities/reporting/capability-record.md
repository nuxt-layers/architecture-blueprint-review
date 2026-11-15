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
