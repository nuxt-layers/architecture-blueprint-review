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

## Review notes — storage, transport, fulfilment cost and accounting (14 November 2026)

**Provisional conceptual notes only.** Logistics is not yet specified as an independently implemented domain.

- Logistics may govern **movement planning and delivery execution**: shipments, carriers, freight quotations, transport legs, tracking, delivery confirmation, returns transport and actual transport charge evidence. It should not take over Order commitments, Inventory quantities, Warehouse physical storage work or Accounting postings.
- **Physical storage operations** (locations, occupancy, handling and custody) ordinarily belong to Warehouse. Storage contracts, externally billed space, detention/demurrage and charge calculation may belong to Logistics, Billing or an independently justified facilities/service responsibility; choose the owner based on the specific lifecycle, not the word “storage”.
- Potential cost evidence includes carrier charges, postage, fuel, packaging, handling, pallet/container fees, storage duration/volume, insurance, customs duties, third-party logistics (3PL) invoices, returns and damage claims. Separate **estimated/quoted** costs from **incurred/verified** costs, and record who owes or pays them.
- Costs may be allocated to **inventory acquisition/landed cost**, manufacturing/WIP, **cost of sales**, selling/distribution expense, a customer charge or a recoverable amount, depending on the actual economic event and approved accounting policy. Logistics supplies quantities, services, rates and evidence; Accounting decides recognised valuation, period, classification and journals.
- An Order may quote a customer delivery fee, Invoice may charge it, and Payment Gateway may settle it. These are **not** the same as the carrier's actual cost; reconciliation should explain margin or difference without transferring source ownership.
- Integrations could connect transport carriers and 3PL/warehouse providers. Connectors should record verified remote identifiers, checkpoints and price evidence without becoming the authoritative logistics or financial domain.
- **Open:** where do warehousing rate cards, billable occupancy, freight procurement, carrier contracts, landed-cost allocation, customs/tax, reverse logistics and third-party warehousing charges belong? Which events are authoritative for accrued versus actual costs?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Shipment, carrier and transport execution and its verified cost evidence, not accounting postings or physical warehouse stock balances.
- **Related capability notes:** [warehouse](../warehouse/capability-record.md), [inventory](../inventory/capability-record.md), [order](../order/capability-record.md), [invoice](../invoice/capability-record.md), [billing](../billing/capability-record.md), [accounting](../accounting/capability-record.md).
- **Open architectural questions:** Ownership of storage tariffs, 3PL services, actual-versus-quoted costs, allocation of inbound freight versus outbound distribution, and returns.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.


## Reciprocal interface — Inventory conceptual review (18 November 2026)

**Owner-approved Inventory conceptual reciprocity (18 November 2026; PR #77):** Logistics provides versioned dispatch, carrier handoff, delivery, return and loss evidence; Inventory alone validates and commits stock in-transit, issue, receipt and exception states. Shipment/delivery completion does not itself assert legal title transfer, a stock movement or an accounting entry. A delayed or disputed handoff remains traceable pending reconciliation. See [Inventory's proposed public contract](../inventory/capability-record.md#dedicated-inventory-conceptual-review--18-november-2026). This approves Inventory's conceptual interface only, not a neighbouring capability's unreviewed functionality or an implemented API.


## Inventory reassessment reciprocal proposal — 18 November 2026 (PR #81)

**Status: proposed, not approved or implemented.** Logistics owns shipment, carrier handoff, tracked delivery, return and custody evidence. The **proposed** Inventory revision distinguishes source-account issue, in-transit, recipient receipt, discrepancies and cross-account pending transitions. Carrier proof is evidence, not independently an Inventory stock movement, legal title transfer or Accounting posting. Record partial delivery and disputed custody with provenance. See the [Inventory reassessment contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md) and [Inventory record](../inventory/capability-record.md#renewed-conceptual-design-challenge--18-november-2026-draft-pr-81). This note preserves earlier approvals in this capability and does not complete its independent review.


### Inventory manufacturing traceability — owner-approved conceptual reciprocity (18 November 2026; PR #81)

**Approved Inventory-side conceptual requirement:** Shop-floor transfers to external coating/finishing or outside processing record dispatch, in-transit, contractor custody and verified receipt separately. Logistics provides carrier evidence; external subcontractor processing evidence must not silently transfer legal title or change the canonical stock master. Inventory retains batch/lot genealogy, material quantity and pending/disputed handover until acknowledged. This note approves the **Inventory-side requirement only**, does not change this capability's independent approval status or claim a running integration. See [shop-floor flow and public contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026).

---

## Dedicated Logistics conceptual review — 19 November 2026 (draft PR #89)

**Status: PROPOSED, not owner-approved, published or implemented.** Domain capability candidate; its autonomous domain responsibility does not dictate a separate service or Nuxt package. Opening baselines: governing `b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint `6dac83a03da8704f7945ee1bc894f2248300445a`. No accessible `nuxt-layers/logistics` repository surfaced in organisation search and its root `CONTRACT.md` could not be retrieved. The interfaces below are **idealised**, not implementation signatures. Accepted ADR-0012 and normative Capability Standard govern contracts, composition, outbox and authorisation. Related draft Location #87 is provisional.

### Purpose, authority and exclusions

Logistics owns the **shipment/consignment, transport leg, carrier handoff and delivery/return movement execution lifecycle**, including transport instructions, assigned carrier/service, shipment identifiers, tracking checkpoints, exception handling, verified proof of delivery or failed delivery, freight quotes and **transport-service cost evidence**. It serves inbound purchasing, outbound customer fulfilment, internal transfers, inter-site stock movements, repairs, third-party processing and reverse logistics; it must work for manual and self-managed vehicle/courier transport without a carrier API.

Its canonical records are: shipment intent and authorised revisions; parcels/handling units and leg plan; carrier/service appointment and provenance; custody/handover observations (reported versus confirmed); checkpoint/event chronology; exception/dispute/claim cases; transport quote/contract/rate references; charge evidence and reconciliations; delivery evidence and its verification decision. Every record is tenant scoped and revisioned. A tracking observation is not automatically a confirmed handover, delivered item, legal title transfer, Inventory receipt, Warehouse operation, Order fulfilment acceptance or Accounting posting.

**Excludes:** Order commercial commitments; Warehouse pick/pack/receive/bin and physical occupancy; Inventory quantity/reservation/movement/canonical stock custody balances; Location reference/geocoding; Asset fleet stewardship/maintenance; Booking of shared resources; Scheduling execution; Pricing's customer price rules; Billing/Invoice receivables; Payment Gateway settlement; Accounting recognition, landed-cost classification and journal entries; statutory customs/tax determinations; carrier credential storage and external synchronisation transport (Integrations). Logistics may record *evidence* of customs release, insurance, hazardous-goods clearance and temperature/condition, not independently certify those regimes or authorise a prohibited movement.

### Native service, lifecycle and recovery

Authorised request → validate serviceability, permitted destination/contents, quantities and upstream fulfilment prerequisites → create planned shipment → assign leg/service/resource and produce dispatch instructions/labels as applicable → record physical ready/handoff evidence → in transit, checkpoints, exceptions and re-routing → partial/full delivered, failed attempt, refused/lost/damaged or returned → verified closure/reconciliation, claim/dispute, retention/archive. Multi-leg and split/partial consignments are first-class; a parent is complete only when its required child units/legs have proven terminal outcomes. Statuses distinguish planned, tendered, carrier accepted, physical handoff witnessed, in transit, attempted, delivered *reported*, delivered *verified*, exception, return requested, returning, returned verified, cancelled before handoff and unresolved. Historical state changes use append-only facts/corrections with original evidence retained, not destructive overwrites.

Native mode accepts human confirmation with authorised evidence, direct transport planning and manual tracking. A human declaration is explicitly identified as such; it is not represented as carrier-certified delivery. Carrier cancellation after handoff is a return/interception request with uncertain outcome, not a successful cancellation. Disputed, missing, contradictory or stale provider confirmations remain **pending verification/exception**. Carrier timeouts after an accepted outbound request require identifier/idempotency reconciliation rather than blind retry. Failure of required persistence or trustworthy caller/decision context prevents protected state changes; optional provider outages degrade to qualified manual operation where policy allows. Durable capability-owned business events follow committed changes and may be delivered at least once, so consumers deduplicate.

### Idealised public inbound contract

| Source / kind | Input and owner | Validation / mandatory status / failure behaviour |
|---|---|---|
| Host, Identity, Authentication, Authorisation | Trusted tenant/organisation, subject, assurance and resource/action decision; host resolves context, Authorisation grants access | **Required** for protected operations; missing, ambiguous or denied context fails closed; no role escalation through carrier responses |
| Operator or domain requester / command | Shipment request, shipment scope, origin/destination references, contents classification, promised constraints, expected revision, provenance and idempotency key; Logistics owns admission | **Required per requested shipment**; reject unauthorised, invalid, inconsistent or duplicate conflicting instructions; explain pending prerequisites |
| Order, procurement or owning domain | Versioned dispatch/return/transfer obligation, recipient, service constraints, cancellation and fulfilment intent; originating domain retains obligation | **Conditional** when shipment serves a business commitment; stale or withdrawn order places work on hold, not a fabricated Order update |
| Warehouse | Authorised prepared packages, weights/dimensions, handling-unit IDs, readiness, handoff/receipt observations and discrepancy; Warehouse owns physical work | **Conditional** for warehouse-managed shipment; no asserted carrier custody from pick completion alone |
| Inventory | Authorised stock issue/receipt/reconciliation reference and quantity/lot/serial/account context; Inventory owns movement | **Conditional** for stock-bearing movement; uncertain stock state prevents claims of completed stock reconciliation |
| Location | Versioned place/address/route reference, precision and validation; Location owns place definition, not movement | **Optional/conditional**; manual contact/destination under Logistics with uncertainty if Location unavailable; never infer precise geocode from incomplete address |
| Clock + Configuration | Effective time and timezone semantics; approved tenant carrier/service, handling, retention and delegation policy | Clock semantics required; policy effective revision required; unavailable mandatory restriction blocks affected movement |
| Integrations + carrier/3PL | Provider IDs, bookings, label/tracking data, rate offers, scans, invoices, delivery signatures and timestamped source evidence; provider owns original assertion | **Optional**; verify signatures, source, freshness, mapping, charges and idempotency; contradictory/stale claims qualify evidence rather than overwrite Logistics history |
| Asset, Booking, Task/Workflow | Available authorised transport resources/slots, operator task or exception approval; owners retain resources, bookings and approvals | **Conditional** where local fleet/approval is configured; missing capacity or approval blocks allocation, not unrelated shipments |
| Legal Compliance, Privacy, Content Security | Restrictions on route/contents/retention/disclosure and evidence checks; domain and legal owners decide policies | **Conditional to risk/jurisdiction**; uncertain permission or clearance requires hold/manual qualified decision, never automatic clearance |

### Idealised public outbound contract

| Surface | Consumers and authorised meaning | Guarantees / limitations |
|---|---|---|
| Shipment and leg read model | Order, Warehouse, Inventory, operators, Reporting | Versioned authorised transport plans, parcels/legs and **Logistics** lifecycle state; not fulfilment, stock or title authority |
| Dispatch/tender and handoff result | Warehouse, Order, Inventory, carrier | Accepted versus actually handed over clearly separated; identify evidence source, actor, time and revision |
| Tracking and qualified checkpoint history | Customer tracking through authorised Order/host views, Warehouse, support | Source-qualified events and location precision; out-of-order, missing and contradictory checkpoints disclosed |
| Delivered/failed/returned evidence | Order, Inventory, Warehouse, customer service | Distinguish declared/reported from verified proof and partial quantities; downstream owners independently decide their transitions |
| Freight quotation/charge/claim evidence | Accounting, Billing, Pricing, Invoice, procurement | Quoted versus incurred versus contested amounts, currency, unit, rate/contract source, parties, period, allocations and supporting reference; **no** recognition, billable price or payable assertion |
| Exception and reconciliation queue | authorised logistics operators, Workflow/Task, Audit | Lost/damaged/delayed/disputed/unresolved with cause, correction and provenance; claim is not automatically settled |
| Authorised shipment documents/export | recipient/customer service, Audit, Reporting | Minimal shipment manifest, label, proof, export with PII masking, version, source and access checks |
| Committed domain events through own outbox | MQ relay, consuming owners | ShipmentPlanned, TenderAccepted, HandoffRecorded, CheckpointRecorded, DeliveryEvidenceReceived, DeliveryVerified, ShipmentExceptionRaised, ReturnVerified, FreightEvidenceRecorded, ShipmentCorrected; at-least-once, versioned, replayable, not other owners' transitions |

### Commands, queries, event discipline and invariants

**Commands:** request/revise/cancel shipment; split/consolidate consignments; allocate leg/service; tender/dispatch; record handoff, checkpoint, delivery attempt, proof and exception; initiate/verify return; attach quote/cost/invoice evidence; reconcile provider IDs and disputed status; correct with a reason and compensating event; archive where lawful. Each checks scoped authorisation, expected revision, validated evidence, business prerequisites and idempotency. Return `accepted`, `committed`, `pending_provider`, `pending_verification`, `rejected` or `unknown_reconcile` appropriately; never conflate acceptance with completion.

**Queries:** filtered shipments/legs, status and events, carrier tracking, cost evidence, operational tasks/exception backlog, permission-scoped recipient tracking, historical snapshots with freshness/completeness/version and provenance. A transport ETA is estimated, never a firm promise from absent evidence.

**Events:** only after Logistics commit through its own durable outbox; contain stable event ID, aggregate ID/revision, tenant, causation/correlation, qualified event/effective time, source and disclosed data. Events are facts of Logistics state only. Consumers must handle duplicate, delayed, replayed or out-of-order events; no cross-capability exactly-once or distributed transaction promise.

**Invariants:** tenant and authorised organisation scope cannot be overridden by supplied tracking IDs; shipment and handling-unit identifiers remain globally unambiguous within their declared scope; no verified completion merely from a provider status or scan without configured proof standard; leg and partial-unit completion cannot silently imply parent completion; claims/corrections preserve evidence and chronology; privacy/retention/permission apply to delivery names, addresses, signatures, location tracks and vehicle data; external updates must never execute unauthorised stock, Order or Accounting mutations.

### Cross-capability cooperation and direction

| Other owner | Logistics needs | Logistics supplies | Dependency |
|---|---|---|---|
| Order | Sale/purchase fulfilment obligation, permitted dispatch/cancel/return | Shipment progress, proof, exceptions, transport estimate/cost evidence | Conditional |
| Warehouse | Packing/handling work, readiness, physical handover/receipt | Carrier booking/labels/dispatch instruction, accepted handoff/return notice | Conditional |
| Inventory | Stock/transfer provenance, accepted issue/receipt references | Dispatch/in-transit/delivery/return/loss evidence for independent stock transitions | Conditional |
| Accounting | Approved financial classification/rate-reconciliation rules only where applicable | Actual freight/3PL/claim/landed-cost supporting facts, not journals | Optional/conditional |
| Billing, Invoice, Pricing | Customer quote and billable-term references | External service expense/quote and difference evidence, not customer charge decision | Optional |
| Location | Place reference, geocoding certainty | Movement-specific observed place/route evidence, never edits canonical places | Optional |
| Asset, Booking | Vehicle/driver/resource capability, availability | Transport assignment and use evidence, not asset ownership/bookings | Conditional |
| Integrations | Carrier/3PL provider adaptation, remote evidence & credentials handling | Domain intent/result correlation and reconciliation requests | Optional |
| Clock, Configuration, IAM | Time interpretation, operating policy, trusted authority | Domain events, status; no replacement for these owners | Essential at boundary |
| Workflow, Task, Scheduler, MQ | Approval workflow, operator assignments, scheduled retries and delivery | Approved work requests, registered task handlers, durable outbox | Optional/operational |
| Audit, Logging, Observability, Reporting | Authorised intake/diagnostics/aggregation under distinct ownership | Auditable decisions, technical correlation, operational measures and qualified domain read models | Conditional/optional |
| Legal Compliance, Privacy | Effective movement/retention restrictions | Evidence for relevant assessments and access/erasure handling | Conditional |

Dependencies are **public logical contracts**, not necessarily direct package imports; composition must remain one-way and acyclic. Order/Inventory/Warehouse independently consume Logistics evidence and apply their own domain decisions. Published contracts must negotiate reconciliation across owners without a synchronous dependency cycle.

### Providers, financial boundaries, compliance and security

Carrier/3PL integration is optional and swappable. Maintain native shipment IDs and remote-ID mappings; require scoped provider consent/credentials, verification/webhook replay protection, rate limits, quota visibility, provider downtime/retry and provider withdrawal reconciliation. Historical evidence stays labelled with provider, terms and timestamp; provider changes never rewrite historical delivery state. Freight procurement may choose tenant policy and a carrier contract reference; a legally binding carrier contract or payable may require a separate procurement/contract owner. Carrier invoices are **claims requiring checking**, not automatically Accounting recognised liabilities. Warehouse measures occupancy/handling; Logistics may hold transport-specific demurrage, detention and freight rate evidence; Billing owns customer billable calculation and Accounting owns financial recognition. Customs, sanctions, hazardous goods, dangerous routes and international shipment rules require jurisdiction/effective-date checks and qualified legal decisions when applicable. No legal compliance certification is claimed.

Security baseline: ASVS 5 L2 and higher-risk L3 where warranted; signed evidence and tamper-aware correction history; no public leakage from guessable tracking references; segregate carrier staff, dispatcher, supervisor, accountant and customer disclosure; rate-limit public tracking; encrypt and minimise recipient address/signature/phone and location; apply Privacy retention/subject requests and Legal Compliance holds without unauthorised erasure; use authoritative Audit for accountable access/overrides and Logging/Observability for technical diagnostics only. Missing policy or stale authorisation fails closed.

### GUI and headless operating mode

Optional, separable role-scoped presentation attached by host sidebar **Logistics → dashboard**, using Theme Manager/UI and localisation; no private store access. Dispatcher dashboard: shipments due, planned/in transit/delayed, carrier bookings, exceptions and action queue. Simple warehouse/driver mobile view: scan-first parcel handoff, one next action, large targets, accessible manual fallback, explicit `queued` versus `confirmed`, low-bandwidth or offline capture with server validation on reconnect (never silent execution). Supervisor: disputes, split/partial returns, overrides requiring assurance and evidence; finance user: freight evidence/reconciliation, **not** accounting postings. Customer/recipient: narrow token-scoped tracking and delivery options only when authorised, obscuring precise location/PII where unnecessary. Administrative views: carrier settings, rate/contract references, service restrictions, provider status, retention and RBAC—restricted to authorised roles. WCAG 2.2 AA, assistive technology, keyboard, CLDR/localisation, local date/time via Clock, responsive and non-colour-only status. Headless public commands/queries/events provide identical rules with `presentation: false`; host decides menu paths and composition.

### Conceptual acceptance scenarios (not executable tests)

| Input / situation | Expected behaviour and outbound meaning | Authoritative owner |
|---|---|---|
| Self-managed van, authorised handoff and signed receipt | Shipment/leg moves to verified delivery on required evidence without carrier service; Order/Inventory remain independently pending until they confirm | Logistics delivery |
| Warehouse packed 3 parcels; one uncollected | Two parcel handoffs tracked, third remains ready; parent cannot be fully dispatched | Warehouse handling; Logistics handoff |
| Inventory indicates no permissible stock issue | Stock-bearing handoff remains blocked/disputed; no Inventory quantity mutation | Inventory |
| Carrier reports delivered but recipient disputes and proof absent | Mark reported/unverified, open exception; no asserted final delivery or automatic order completion | Logistics |
| Carrier booking timeout after acceptance | Return unknown and reconcile remote ID/idempotency before second tender | Logistics |
| Provider event replay or out-of-order checkpoint | Deduplicate by identity; preserve original chronology, do not regress verified state | Logistics |
| Driver submits offline scan after revocation | Local queue not authoritative; server rejects upon sync and supplies clear recovery state | Authorisation + Logistics |
| Cross-tenant tracking identifier guessed | Deny protected detail; public view only under explicit scoped disclosure | Authorisation + Logistics |
| Freight quote £50, carrier invoice £65, customer delivery charge £40 | Preserve three independent source facts/references, report variance; no journal or customer fee modification | Logistics / Invoice / Accounting |
| Returned damaged package, partial receipt confirmed | Qualify carrier return and damage; Warehouse verifies handling and Inventory decides received/quarantine quantity | Logistics / Warehouse / Inventory |
| New carrier replaces old after withdrawal | Historic tracking remains provenance-labelled; new bookings use approved provider; unresolved old IDs enter reconciliation | Logistics + Integrations |
| Unsupported customs clearance or dangerous-goods authority | Hold or refuse and direct to qualified owner; Logistics cannot certify customs/legal acceptance | Legal Compliance |
| Cancellation after physical handoff | Interception/return pending with explicit uncertainty, not deletion of consignment | Logistics |

### Decision register and handover

- **LOG-01 — Proposed:** independently owned Logistics shipment lifecycle, native operation, and authoritative qualified handoff/delivery evidence. Recommendation: adopt.
- **LOG-02 — Proposed:** separate Order obligation, Warehouse handling, Inventory movements, Accounting recognition and Location canonical places. Recommendation: adopt.
- **LOG-03 — Proposed:** split parcels/multi-leg dispatch, partial/damaged/return outcomes and verified versus reported delivery. Recommendation: adopt.
- **LOG-04 — Proposed:** provider-neutral optional carriers/3PL with manual fallback and reconciled provider uncertainty. Recommendation: adopt.
- **LOG-05 — Proposed:** classify transport cost into quoted, incurred, disputed and supporting claim facts without performing financial recognition or billable charge computation. Recommendation: adopt.
- **LOG-06 — Open owner decision:** who contracts/procures freight and owns carrier rate cards, reserved capacity, liability and commercial disputes? Recommendation: Logistics owns transport-specific operational tariff/booking selection; a separate procurement/contract authority owns binding commercial/legal commitments when present.
- **LOG-07 — Open owner decision:** storage detention/demurrage and outsourced 3PL occupancy billing. Recommendation: Warehouse owns physical occupancy evidence, Logistics transport-associated charges, Billing customer charges, Accounting recognition; contract procurement remains distinct.
- **LOG-08 — Open owner decision:** minimum evidential standard for verified handoff/POD, delegated driver actions and public recipient visibility by risk/tenant. Recommendation: configuration subject to non-overridable legal and assurance floors; distinguish signed, witnessed, provider-reported and recipient-acknowledged proof.
- **LOG-09 — Open owner decision:** customs/controlled goods and cross-border authority ownership. Recommendation: Logistics orchestrates holds and references decisions from qualified legal/customs owners; never self-certifies.
- **LOG-10 — Technical/implementation alignment:** published root `CONTRACT.md`, provider adapters, status taxonomy, composition budget, persistence/outbox, independent consumer and CI/acceptance remain unverified. Resolve at implementation review, not by asserting readiness.

**Independent challenge:** Boundaries deliberately reject carrier statuses as stock/custody/title truth, avoid circular synchronous fulfilment coupling, preserve partial states and delayed events, prevent automatic journal posting and stop public tracking becoming an identification oracle. No recognised governing ADR changes are requested. Owner approval of LOG-01–09 and reconciliation with Location #87 and Inventory #81 is required before conceptual sign-off; later implementation and technical acceptance are separate.
