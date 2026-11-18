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

## Review notes — inventory, material flow and accounting (14 November 2026)

**Provisional conceptual notes only; not a completed Inventory specification.**

- Inventory is authoritative for **physical stock and movement**: raw materials, components, work in progress (WIP), finished goods, returned goods, consumables held for production, reservations, custody/location and quantity adjustments; whether all these states are first-class must be separately reviewed.
- Distinguish **raw stock**, **serialised unique units**, **completed assemblies**, **prepacked kits** and **virtual sales bundles**. A virtual bundle must not double count component stock; assembly/kit production consumes input units and creates traceable outputs, including scrap or yield differences.
- Inventory records acquisition/cost provenance and movements necessary for valuation; Accounting owns **financial ledger and approved valuation policy**, including cost formula, recognised inventory carrying amounts, WIP, cost of goods sold, loss and write-downs. Warehouse owns physical handling/fulfilment work, not a competing quantity ledger.
- Relevant costing questions: purchase cost, freight/duties, supplier credits, material/labour/production overhead allocation, FIFO/weighted-average/specific identification where appropriate, period cut-off, returns, write-offs and reconciliation between quantity and value.
- **A list price is not the carrying value of stock.** Financial recognition rules depend on the reporting basis and jurisdiction; IFRS IAS 2 is a useful reference, not automatically a rule for every tenant.
- **Open:** who owns valuation input evidence and landed-cost allocation? How do inventories transfer into fixed assets, and vice versa, through authorised classified movements without double recognition?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Authoritative physical units, quantities and movements, including parts, WIP and bundled stock conversions; Accounting owns financial valuations.
- **Related capability notes:** [product](../product/capability-record.md), [warehouse](../warehouse/capability-record.md), [logistics](../logistics/capability-record.md), [asset](../asset/capability-record.md), [accounting](../accounting/capability-record.md).
- **Open architectural questions:** BOM and production ownership, landed-cost evidence, inventory cost methods, and controlled transfer into or out of fixed assets.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

### Asset conceptual-review cross-reference (14 November 2026)

**Proposed:** [Asset](../asset/capability-record.md) owns operational stewardship of individually identifiable managed equipment/property, regardless of legal ownership. Inventory remains authoritative for saleable/production stock quantities and movements. Conversion of a serialised item from stock to operational use (and back) needs an authorised cross-owner handover and Accounting reconciliation, without double-counting or duplicated authority. Protocol details remain open for Inventory's own review.

## Cross-capability note — Booking final conceptual completeness (15 November 2026)

**Approved Booking scope; related capability review not completed.** [Booking's final interface review](../booking/capability-record.md#focused-reciprocal-contract-clarifications): Inventory owns stock quantity and stock-reservation commitments; Booking owns time-based reservation lifecycle and may request checked stock commitments/releases. Compound bookings remain pending/exception until all required owners confirm, with traceable compensation rather than duplicate stock commitments. No currently implemented integration contract is implied.

---

## Dedicated Inventory conceptual review — 18 November 2026

**Classification:** Proposed **Domain capability**, with authoritative stock-position and movement lifecycle; an independent implementation package is not automatically warranted. **Status:** Proposed only, not owner-approved, implemented, tested or compliant. This section develops the earlier provisional review notes without replacing or retroactively approving them.

**Opening evidence:** `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master` `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. Governing Capability Standard (normative), catalogue and accepted ADR-0001/0002/0006/0009/0012/0016/0017/0018 require bounded ownership, private stores, one-way public contracts, server authorisation, tenant authority, explicit policies and optional presentation. An organisation repository search for `inventory` found no matching accessible repository; `nuxt-layers/inventory/CONTRACT.md` was not retrievable (404). **There is no verified runtime Inventory interface.** Adjacent blueprint records and overlapping draft PRs remain proposals unless explicitly approved.

### Purpose, independent justification and exclusions

Inventory is the **single authoritative source for quantity-bearing stock**, its reservations and physical/economic stock movements within a defined stock-owning context. It supports purchasable goods, materials, components, WIP, finished products, spare parts, consigned goods, quarantined/returned goods, production consumables and individually tracked stock items where they are actually held as stock. Inventory is justified by independent concurrency, traceability, stock availability and reconciliation rules beyond Product's definitions or Warehouse's work orders.

Distinguish **stock-holding organisation** (accountable inventory book), **legal title claim**, **operational custody**, **physical site/bin**, **intended disposition**, and **accounting entity**; they are not interchangeable. Distinguish stock on hand, usable, reserved, picked/allocated, in transit, quarantine, damaged, blocked, WIP and externally held. A stock balance is a derived position from committed movements and reservations, **not** an independently editable counter. Uncertain movements are never silently counted as received or dispatched.

**Excludes:** Product/model definitions and commercial bundles (Product); prices and quotes (Pricing); customer/supplier order obligations (Order); receiving/picking/packing and physical site/bin work (Warehouse); transport and proof of delivery (Logistics); asset stewardship (Asset); financial valuation, inventory carrying amount, capitalisation, recognised COGS and general ledger (Accounting); externally binding title and legal ownership adjudication (relevant contracts/legal owner); calendar/time-booking lifecycle (Booking); identity, access decisions or external provider credentials. No generic manufacturing execution system is implied by Inventory's stock conversion.

### Owned information and lifecycle

| Owned record / state | Authority and invariant |
|---|---|
| Stock item/lot/serial identity | Inventory-specific physical stock identifier, product/version reference, batch/lot/serial provenance, tracking mode, quality/expiry evidence and unit of measure. Product owns the catalogue definition. An individual serial number cannot be concurrently active in incompatible stock positions. |
| Stock account and position | Tenant-scoped stock-owning context; site/location/custodian references, condition, hold status, stock category and revision. Aggregate available-to-promise is calculated from eligible positions minus **valid committed** reservations and applicable exclusions, never from an unrelated shopping-cart count. |
| Movement journal | Append-only provenance of accepted receipt, issue, transfer, return, correction, adjustment, loss and stock conversion; reversals/counter-movements rather than editing past entries. Record effective/recorded times, source and reason, before/after references and authorisation. |
| Reservation commitment | Immutable reservation identity with owner reference (e.g. order or booking), requested and committed quantity, expiry/hold policy, status, revision, idempotency key and release/consume history. Prevent oversubscription using authoritative atomic checks in Inventory. |
| Reconciliation / exceptions | Count evidence, variances, contradictory partner claims, provisional receipts, reconciliation cases, corrections and disposition history; cannot treat an unverified count as a completed stock movement. |
| Cost/source provenance | Reference original purchasing, freight, production, landed-cost and scrap evidence for Accounting's decisions. Preserve quantities, units, cost facts and allocation provenance; Inventory does **not** assert the financial carrying value or decide allowable capitalisation. |

**Native lifecycle:** register stock context and tracking rules → receive evidence/validate → commit stock receipt/position → place authorised holds, reservations and internal transfers → release/consume/issue/return/adjust → reconcile counts and external evidence → reverse or correct with compensating evidence → archive under retention policy. Assembly/kit conversion is an atomic or explicitly recoverable sequence of component decrements and finished-unit increments; scrap/yield remain traceable. **Virtual sales bundles are never created as extra physical stock.** Material in transit, a dispatched parcel, disputed custody or a pending external receipt must each retain an explicit non-final state.

**Native service without optional external providers:** issue and record movements, query position/history, reserve/release/consume under concurrency controls, stocktake and reconcile, track serial/lot/expiry, support simple stock transformation and handle returns/quarantine. If authoritative persistence, caller context or required access decisions are unavailable, protected operations fail closed. Operation completion is returned only once committed to Inventory's authoritative store and durable outbox; timeouts after commit yield **unknown until reconciled**, not an automatic second movement. Native mode cannot promise third-party stock changes, product catalogue creation, warehouse execution or general-ledger postings.

### Idealised public inbound contract

| Source / kind | Input facts or request and validation | Requirement and failure semantics |
|---|---|---|
| Host + IAM / trusted context | Resolved tenant/accountable group, subject, assurance, resource-scoped Authorisation decision; validate each protected action against real stock scope, never trust caller-supplied tenant/role alone. | **Required** trusted authority; missing/denied/ambiguous → refuse without stock change. |
| Inventory operator / command | Create stock context, receive/adjust/transfer/reclassify, count/reconcile, reserve/renew/release/consume, initiate/confirm return or stock conversion; supply source reference, reason, expected revision, unit/quantity, effective time, idempotency and evidence. | **Required per operation**; invalid/negative or dimensionally incompatible units, stale revision, insufficient usable quantity or unsupported transition → stable refusal; replay same key returns prior result. |
| Product / authoritative definition | Stable product/variant/version reference, units and permitted conversion, serial/lot requirements, physical/virtual bundle classification, BOM version where applicable. | **Conditional** when stocking classified product. Unknown/stale definition blocks new incompatible transactions; historical stock remains traceable. |
| Order / commitment | Versioned sale/purchase obligation, requested allocation/fulfilment, cancellation and return reference; not an instruction to manufacture Order acceptance. | **Conditional** on orders; Inventory confirms only stock commitment, never commercial acceptance. Out-of-stock/unknown → explicitly rejected/pending, no oversell. |
| Booking / commitment | Scoped time/resource booking reference and stock commitment/release request; lifecycle/time horizon supplied by Booking. | **Conditional**; a booking does not reserve stock without Inventory confirmation; compound failures remain pending compensation. |
| Warehouse / handling evidence | Receiving inspection, counted lots/serials, pick/pack/put-away, loss or return evidence, site/bin and custody handoff. | **Optional/conditional**; work-complete evidence is not a stock movement until Inventory validates and commits it; duplicate or contradictory scans → exception. |
| Logistics / custody evidence | Dispatch/receipt proof, carrier handoff, losses, delivery/refusal and returns. | **Conditional**; carrier status alone does not silently transfer title, consumption or financial value. |
| Asset / handover request | Identified serialised stock item, authorised reclassification/transfer into or out of managed-asset use, acceptance/reversal evidence. | **Conditional**; both owners acknowledge; intermediate uncertain status must prevent dual active classification. Accounting reconciles recognition separately. |
| Configuration, Clock, legal/policy | Versioned approved thresholds, safety stock, oversell prohibition, expiry/quarantine and reservation rules, effective time/timezone, applicable retention/holds and jurisdiction restrictions. | **Conditional rules**; unsafe missing policy or indeterminate expiry rejects or quarantines. Configuration stores values, Inventory interprets stock rules. |
| Integrations / external evidence | Scoped provider stock ID, source, status, version, signed/validated evidence, mapping, cursor and provider request identifiers. | **Optional**; unverified, stale, out-of-order or divergent provider evidence becomes reconciliation pending, not authority by default. |
| Accounting / reconciliation request | Request movement/cost evidence or submit approved correction classification and matched journal reference. | **Optional for operational stock**, conditional for booked finance; journal status alone cannot edit stock history. |

All inputs must distinguish **facts** from requests and untrusted evidence. Check units, precision, expiry, source ownership, stock condition, version, concurrency and allowed transitions, and reject invalid stock becoming available. No received event is itself a permission grant.

### Idealised public outbound contract

| Public surface / consumer | Meaning, authority and restrictions |
|---|---|
| Stock position / Product, Order, Shop, Warehouse, Booking, Reporting | Authoritative position by permitted tenant/stock context, product/lot/serial/location, usable/reserved/quarantined/in-transit status, as-of revision/time and freshness. Availability is **as-of**, not a durable guarantee; require reservation confirmation for commitment. |
| Commit/release/consume result / Order, Booking, Warehouse | Explicit **committed, refused, pending or unknown** status, reservation/movement IDs, quantities, owner source, expiry, revision, reason code, correlation and idempotency; source owner retains sale/booking/warehouse decisions. |
| Movements / Accounting, Audit, Reporting, Asset | Immutable fact and correction chain, physical units, source evidence, classification, effective/recorded time, quality flags; **no claim of posted finance**. Per-consumer minimisation and tenant boundary apply. |
| Stock count/reconciliation / authorised operators, Accounting | Count evidence, variance and adjudication status, correction/matched-journal references, source/version; unresolved variance is not silently reconciled. |
| Cost/provenance evidence / Accounting | Original acquisition and conversion evidence, quantities and referential allocations; Accounting independently interprets policy and recognition, including WIP, landed cost and COGS. |
| Authority/provider health / host, operations | Native/selected external source, last verified sync, lag, mapping errors, uncertain transactions, revoked connection and reconciliation status; unavailable **must not** look healthy. |
| Committed business events / subscribers | `StockReceived`, `StockMoved`, `StockAdjusted`, `StockReserved`, `ReservationReleased`, `StockIssued`, `StockReclassified`, `StockReconciled`, `StockConversionCommitted` as **illustrative conceptual names only**; emitted after authoritative commit through Inventory-owned durable outbox, transported by Message Queue. Duplicate/out-of-order delivery is possible. |

Queries support authorised scoped filtering, pagination, effective-time history, projection revision, completeness and evidence provenance. Supplier cost and serial/condition data may require separate access scope. No cross-tenant joins or access via opaque stock IDs. Historical events must retain original classifications; provider state is not automatically equal to authoritative stock state.

### Interaction guarantees, ownership and dependencies

- **Commands:** caller and domain authorisation, quantity precision and conversion, no negative available stock unless a future explicitly authorised policy permits it, atomic stock reservation/consumption, serial uniqueness, revision fencing, stable idempotency across retries, explicit compensation and outbox persistence. Returns must distinguish accepted-for-processing from committed and externally confirmed.
- **Queries:** read-only and privacy-scoped; an available quantity is a snapshot with revision/freshness, not a promise. For concurrent sales, only the commit operation is binding.
- **Events:** Inventory publishes only its committed stock facts; consumers independently validate tenant/source/ordering/replay and decide their own downstream transitions. Do not promise exactly-once cross-system delivery.
- **Shared context:** typed tenant/stock-account, product and other owner references, source operation/version, caller assurance, expected stock revision, policy version, observed/effective timestamps, correlation/idempotency, evidence and outcome. Not a mandated universal object.
- **Dependency direction:** conceptually Inventory **consumes** Product definitions, trusted IAM/Configuration/Clock/policy services and optional owner-provided evidence; Order/Booking/Warehouse/Accounting **consume Inventory outputs**. For cross-owner requests, compose published service interfaces/ports or event choreography rather than introducing circular package imports. A source event does not create automatic transaction authority.
- **External authority:** Native Inventory is default only for a context not already governed by an external stock master. If an authorised external system is designated authoritative for an explicitly bounded stock context, local data is labelled a projection and no competing writes may be committed. Connector outage cannot silently switch master to local. Provider replacement requires explicit mapping, cut-over, outstanding holds and movement reconciliation, backfill and provenance. Whether authoritative external operation is supported is a separate decision; the conceptual record does not promise it exists.

### Cross-capability reciprocal contracts

| Cooperating capability | Inventory receives | Inventory supplies / boundary |
|---|---|---|
| Product | Definitions, variants, units, component/BOM or kit classification | Positions, consumed quantities, stocked physical item IDs; Product never owns balance |
| Order / Shop / Marketplace | Commitments, cancellation/returns references and source revision | Checked reservations, issues, shortage or uncertain states; sales ownership remains with Order |
| Booking | Resource-linked stock request and release/expiry context | Stock reservation status; Booking retains booking lifecycle |
| Warehouse | Count, receiving, put-away, pick and custody evidence | Committed positions, authorised pick availability and movements; warehouse execution is separate |
| Logistics | Shipment and return handoff evidence | Released/in-transit/received stock changes; transport is separate |
| Asset | Reclassification/handover acceptance | Stock-to-asset or asset-to-stock movement and serial trace; Asset governs managed identity and stewardship |
| Accounting | Book reconciliation references/policy outcomes as needed | Movements, physical quantities, acquisition and conversion evidence; Accounting alone recognises inventory value |
| Suppliers / procurement domain (if justified) | Source receipt/order/cost evidence | Accepted receipts, shortages and returned quantities; cannot invent procurement domain contract |
| Configuration / Clock / IAM / Legal Compliance | Approved rules, time context, trusted caller, access decision and applicable legal holds | Scoped authoritative outcomes and denials; Inventory owns stock-domain rule interpretation |
| Audit / Logging / Observability / Reporting / Search | No incoming authority merely from monitoring | Purpose-limited audit events, technical health, stock read models/indexing; none owns ledger of stock |
| Scheduler / Workflow / Message Queue / Integrations | Optional task orchestration, approvals, event transport and external evidence | Inventory-owned task definitions, durable outbox and approval requests; these providers do not decide stock |

No fixed `requires` or Nuxt `extends` edges are approved by this conceptual review.

### Security, privacy and compliance

Respect accepted ADR-0017 tenant/accountable-control rules and ADR-0018 policy governance, authenticated assurance appropriate to high-risk adjustment and asset conversion, server-side Authorisation for read/write and bulk export, separation of duties and approval thresholds for material loss, restricted goods, count overrides and cross-tenant custody changes. Risk-based Audit must capture who requested/approved/corrected movements, while technical Logging must minimise commercial/personally identifiable information. Tenant isolation holds through batch reads, exports, events, provider mapping, background work and delegated operations. Protect stock and cost intelligence; encrypt secrets and provider credentials through host/Integrations controls; support retention/legal holds, subject rights where relevant, evidence integrity, rate limiting and recovery. Account for perishables, controlled goods, traceability/recalls and jurisdiction-specific legal rules **only when applicable**; do not declare blanket IFRS, IAS 2, GDPR or product-safety certification. Financial policy belongs to Accounting; statutory applicability to Legal Compliance and qualified interpretation.

### Conceptual GUI and host integration

**Optional Inventory presentation, with independently useful headless mode.** Host sidebar item **Inventory** opens a capability dashboard; host resolves tenant, site, available scopes and navigation. Dashboard: stock on hand/usable/reserved/in transit/quarantined and shortages with revision/freshness; search/filter by product, variant, serial, batch, location, custodian and status; drill into movement/audit history and source evidence. Scoped actions: receive, transfer, adjust (reason + approval), reserve/release, stocktake/reconcile, quarantine, kit conversion, authorised asset reclassification and provider reconciliation. Operator queues show discrepancies, expired holds, failed external synchronisation and unresolved handoffs. Warehouse actions appear as cross-capability links to Warehouse work, not duplicate pick/pack forms; accounting values require an authorised Accounting read model, not invented Inventory valuation. Clearly distinguish pending/unknown from committed status and restrict high-impact actions by permissions/assurance.

Use optional screens/public presentation contributions under ADR-0009; no required routes or business state in host. Follow representative `nuxt-layers-test/application-test-template` sidebar/dashboard integration, Theme Manager semantic tokens, WCAG 2.2 AA keyboard and screen-reader access, responsive tables, accessible confirmation/errors, BCP 47/Intl localisation, units and temporal display. Headless composition must expose equivalent public queries, actions, errors and events without importing private persistence. No UI is considered implemented or tested.

### Conceptual acceptance scenarios (not executable tests)

| Input | Expected behaviour / public result | Authoritative owner |
|---|---|---|
| Receive 12 verified units | Commit one receipt/movement and position revision; replay same idempotency key yields same result | Inventory |
| Two orders race for last 3 usable units | At most 3 units committed across both; other request refused or pending, no oversell | Inventory for holds; Order for sales |
| Booking requests a timed hold | Inventory confirms actual quantity/expiry or refuses; Booking remains pending until all needed owners agree | Inventory / Booking |
| Warehouse marks pick completed but stock changed | Revision/quantity check, refusal or exception; no second physical ledger | Warehouse work / Inventory movement |
| External receipt response times out after commit | Return uncertain with operation reference; query/reconcile before retry | Inventory |
| Count reveals missing stock | Evidence/variance recorded; only authorised, reasoned adjustment changes stock; audit remains | Inventory |
| Virtual bundle sold / kit physically assembled | Virtual bundle commits component reservations only; real kit conversion consumes inputs once and creates output trace | Product definition / Inventory movements |
| Serialised stock moved into service as Asset | Explicit handover and classification fencing; never simultaneously counted as active sale stock and operational asset; Accounting reconciles value | Inventory / Asset / Accounting |
| Wrong tenant, denied permission, stale product or invalid unit | Refuse without leakage or state change; stable error and logged security outcome | IAM / Inventory |
| External authority unavailable or conflicting | No silent local takeover; pending/reconciliation and provenance exposed | Designated external master / Inventory projection |
| Accounting requests stock valuation support | Movement/cost provenance returned, **no** auto-posted carrying value or journal | Inventory evidence / Accounting recognition |
| Stock record export/recall/legal hold | Authorised purpose and retention controls, with lot traceability and redaction | Inventory / Legal Compliance |

### Independent challenge and outstanding decisions

**INV-01 (proposed):** Approve Inventory as the single quantity/movement/reservation owner for stock; independent Domain lifecycle while other domains retain their own decisions.

**INV-02 (open):** Does a manufacturing/production owner govern BOM execution/work orders and yield, leaving Inventory to validate/commit stock conversion, or may minimal production execution be part of Warehouse/Process? Product remains authority for versioned product definitions, not execution.

**INV-03 (open):** Which domain owns detailed acquisition/landed-cost allocation evidence before Accounting evaluates valuation? Inventory should preserve source references, not invent costs or financial policy.

**INV-04 (open):** Define the permitted stock-master modes: local-only initially, or per-stock-context external-authoritative mode with explicit reconciliation and cut-over controls. No dual writers.

**INV-05 (open):** Confirm title/custody semantics for consignment, third-party logistics, cross-tenant transfers and loss; movement evidence does not itself convey legal ownership.

**INV-06 (proposed):** Confirm Inventory owns reservation concurrency and release/consume, whereas Order and Booking own commercial/time reservation decisions; compensate cross-owner partial completion.

**INV-07 (proposed):** Confirm bounded stock ↔ Asset reclassification handover with non-duplicated serial ownership and separate Accounting recognition.

**INV-08 (open):** Decide stock valuation support depth (quantity plus cost evidence only vs operational subledger cost layers) without duplicating Accounting's recognised financial books.

**Technical investigations:** unit-of-measure conversions, lot/serial uniqueness, expiry/DST, reservation fencing and dead-letter recovery, stocktake tolerances, multi-site transfer atomicity, provider backfill, evidence retention, recall traceability, contract drift and optimisation of indexed availability reads. These require technical research rather than owner votes unless they alter authority.

**Implementation/acceptance alignment:** publish self-contained root `CONTRACT.md` only if a package is approved; document public permissions, stable errors, ports, provider modes, read/write/event contracts, capability-owned migrations/outbox and storage register, minimal independent consumer or Nuxt host within 50 lines, CI security/concurrency/replay/tenant/GUI acceptance. None is presently claimed complete. **Conceptual sign-off awaits owner approval of INV decisions and latest-master consistency review.**


### Owner conceptual approval and implementation boundary — 18 November 2026

**Owner approval:** The owner explicitly approved the Inventory definition and instructed final documentation, architectural/Git reconciliation and squash merge in this conversation. This approves Inventory's **conceptual Domain boundary** and the documented public input/output semantics, native stock ownership, reservation concurrency, stock/Asset handover invariants, security, GUI and reciprocal principles, including INV-01, INV-06 and INV-07. It does not create a running capability, mandate a new package, claim verified integration, or approve a particular technical protocol.

**Deferred clarifications, without obstructing the approved boundary:** INV-02 (manufacturing work-order execution owner), INV-03 (landed-cost evidence allocation), INV-04 (whether/when to implement external stock-master support), INV-05 (evidenced title/custody/consignment transfer procedures) and INV-08 (whether to add operational cost layers) remain **implementation/design choices requiring separate explicit decisions**. Approved constraints still apply: no separate Product/Order/Warehouse/Accounting stock ledger, no automatic valuation, no dual active stock master, no unauthorised title assertion, no double-recognised stock versus Asset, and no unconfirmed cross-owner reservations. Existing earlier "open/proposed" labels in this historical review section describe their status at initial drafting; this approval note is authoritative for the current conceptual review status.

**Latest-baseline architectural reconciliation:** Governing `architecture-rules/master` remained `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. Blueprint baseline advanced from `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` to `cf9804f0f44cc52d996f22c273a56df1ab0bdbf6`, incorporating approved Identity, IAM, event bus/events, Attendance, Federation, Export, Help, Gallery, Gaming and other reviews. These additions do not assign stock quantity authority to another capability. Booking's newly merged Events/Attendance links must be preserved alongside Inventory's distinct **physical stock** commitment interface; neither an event attendance record nor a booking capacity commitment is a physical stock balance. Cross-capability access uses trustworthy tenant and policy context, not incidental actor or attendee identifiers. External services and transport still cannot override a domain owner's committed stock facts.


---

## Renewed conceptual design challenge — 18 November 2026 (draft PR #81)

**Status:** Proposed revision for owner consideration. The [prior Inventory conceptual approval (PR #77)](https://github.com/nuxt-layers/architecture-blueprint-review/pull/77) remains recorded and was not silently revoked. This section identifies precise additions/qualifications that would supersede ambiguous parts of the earlier design **only if expressly approved**.

**Detailed design, idealised public inbound/outbound contracts, interactions, GUI, standards, dependency matrix, safeguards, acceptance cases and decision gate:** [Inventory conceptual reassessment](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md). That dedicated document forms part of the current Inventory record; it is neither a published runtime `CONTRACT.md` nor an accepted ADR.

### Key proposed corrections

1. **Distinct stock authority:** Inventory owns stock account, movement ledger, item/lot/serial positions, available-to-promise and quantity commitments, but **does not legally adjudicate title**, own identity groups, own accounting recognition, or assume a custodian is the owner. Record stock-account authority, evidenced title assertion, custody, location, quality/hold status and accounting entity **independently**, with effective history and uncertainty.
2. **Meaningful quantities:** On-hand, available, reserved, in-transit, damaged, quarantined, customer-owned consignment and externally held positions describe different dimensions and must not be naively summed. A position is derived from committed movements and allocations, not a freely writable balance.
3. **Cross-owner handover:** Intra-account transfers differ from cross-account/cross-tenant custody and stock transfers, which require correlated release, receipt, uncertainty/reconciliation and independently evidenced rights or title assertions; completion by one actor does not imply confirmation by another.
4. **Product/production separation:** Product owns versioned BOM and kit/bundle definitions; Inventory commits quantitative input/outputs, WIP, scrap/yield genealogy but does not own the entire manufacturing work-order lifecycle. Warehouse or a future independently justified Production owner coordinates execution.
5. **Financial evidence:** Inventory publishes quantity and original cost-source references to Accounting; Accounting alone approves valuation, landed-cost allocation, period and financial entries. No competing book value or guessed capitalisation.
6. **Optional providers:** Native Inventory remains the proposed canonical stock master. Marketplace and 3PL adapters normally provide evidence or published projections; an external authoritative ledger is an explicitly optional **future** policy mode, not enabled by connection presence or outage.
7. **Public contract:** Resource-scoped, validated and idempotent commands; as-of revisioned queries; post-commit Inventory-owned outbox events. `accepted`, `committed`, `unknown`, `disputed` and `reconciled` must be differentiated. No incoming event confers access.
8. **GUI:** An optional Inventory dashboard separates available/on-hand/held/in-transit/quarantined and shows stock account, title claim, custodian, location, evidence, age/freshness, authority mode, reconciliation and authorised operations; never duplicates Order, Warehouse, Asset, Accounting or Reporting's ownership. Equivalent headless public interfaces remain mandatory.

**Proposed decision IDs:** RINV-01–RINV-08 in the [review](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#revised-conceptual-authority-and-lifecycle-proposal). All are open pending this follow-up review's owner approval. Previous INV-01/06/07 approval is retained as historical evidence. No implemented service, root public contract, independent acceptance, GUI compliance or legal certification is claimed.


### Owner approval of revised Inventory architecture and shop-floor tracking — 18 November 2026

**Owner-approved conceptual decisions:** Section 1 Option B (support owned, consigned and other third-party stock with separate stock-account, title claim, custodian, site, permitted use/sale and financial recognition relationships); Section 2 Option D (Warehouse for straightforward assembly, separate Production only when its independent operational lifecycle justifies it), **with barcode/scan-based end-to-end manufacturing material tracking**; Section 3 Option B (quantity and original cost provenance, financial valuation only in Accounting); Section 4 Option C (explicit stock-account/provider authority, native-first implementation); Section 5 (staged cross-owner and Asset handovers); Section 6 (Inventory as sole physical stock reservation authority and explicit as-of/committed states). **RINV-01–RINV-08 all approved.**

The stock account is a durable Inventory-owned quantitative accountability boundary associated with a trusted tenant and accountable organisation, allowing multiple stock accounts, sites and custodians under an organisation. Organisational membership, physical possession and title claims do **not** confer authorisation or legal ownership by implication.

**Manufacturing tracking now part of the approved scope:** Raw billet/bar stock checks out of warehouse to staging/work centre; the system tracks last **confirmed** location, quantity, condition and manufacturing stage through turning, successive milling, finishing/preparation, internal or subcontracted coating, packing and warehouse finished-goods check-in. Support individual tagged units and lot/batch/handling-unit traceability, split/merge/genealogy, conversion and yields/scrap/rework. Stock for consumables (cutting inserts, discs, cutting fluids, packaging) is separately received, issued, consumed, returned or written off, with job/station provenance; controlled reusable equipment may belong in Asset. Machine-readable barcodes/2D tags (or tagged carriers where direct marking is impractical) identify items, lots and containers; scans must be checked against server-side authority and expected state, not trusted simply for having a label. Offline/missed/out-of-sequence scans remain pending/unknown until reconciled.

**Ownership separation:** Inventory commits stock quantities, work-in-progress identities, physical position, material issues/returns and genealogy; Warehouse or future Production owns job scheduling, routing, machine operations, labour and quality process decisions. Product owns BOM and unit definitions. Accounting owns recognised financial amounts. A shop-floor screen may show process-stage evidence but must link to its authoritative operational owner rather than inventing Inventory-owned manufacturing execution.

**Published conceptual extensions:** scoped scan/identify, check-in/check-out, stage handover, material consumption, output, scrap/rework, lot split/merge, container membership/relabel and current as-of material-position/genealogy queries; committed owner events and revisioned responses. Full table definitions, workflow example and acceptance cases are recorded in [the owner-approved material-flow addendum](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026). These are *idealised contracts*, not implemented endpoints.

**Approval status:** Conceptual choices are approved; the review PR remains draft and **unmerged**. No implementation, scanner integration, automated manufacturing work orders, CI or local tests are claimed. A fresh latest-master technical/architectural check is mandatory before any separately authorised merge.


### Approved manufacturing correctness refinements and proposed operator-adoption requirement — 18 November 2026

**RINV-09–RINV-12 owner-approved:** Independently track scan/sensor observation, Production/Warehouse operation outcome, applicable quality disposition and Inventory-authorised material transition (RINV-09); multi-input/output quantity transformations, units, measured tolerances, partial WIP, genealogy and explicit scrap/loss (RINV-10); independently acknowledged and disputable inter-party custody/stock-account transfers, without inferring title from delivery (RINV-11); immutable original records, attributed observation correction and compensating committed quantity movements, with linked revisions and Audit evidence (RINV-12).

**Operator adoption — proposed RINV-13:** A distinct, **task-first, scan-first, minimal-training** operational presentation is required as a conceptual acceptance target for warehouse/shop-floor workers. It must limit routine screens to authorised current job/material/location/quantity, one clear primary action, explicit units, understandable confirmation or failure, safe retry/exception escalation and visible last-confirmed state/freshness. Scanner/mobile/touch/keyboard/manual fallbacks, glove- and noise-aware design, language/accessibility, interrupted/offline scans, shared workstation authorisation and non-deceptive pending status are part of the public-contract experience; they must not bypass the Inventory quantity ledger, operation/quality owners, tenant permissions or Audit. Supervisor reconciliation/approval and administrative policy/provider setup belong in separately authorised, progressively richer views. Measure unaided task completion, error/recovery and training burden with representative real operators before implementation sign-off; do not invent target percentages or waive safety training. Align design with ISO 9241-210 human-centred design, ISO 6385 work ergonomics and WCAG 2.2 AA without claiming certification.

**Full approved semantics, candidate RINV-13 and operator acceptance scenarios:** [Inventory reassessment — final refinements and operator adoption](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#approved-final-traceability-refinements-and-operator-adoption-design--18-november-2026). RINV-13 remains a **recommendation** pending explicit confirmation; RINV-01–12 are approved. No implementation, local tests or merge performed.


### Final conceptual approval — RINV-01–14 and Android operator application (18 November 2026)

**Owner-approved conceptual design: COMPLETE.** The owner has approved **RINV-01 through RINV-14**, including the final low-training operator-adoption obligations (RINV-13) and a single Android-compatible operator app (RINV-14) usable on affordable SIM/cellular handsets or Wi-Fi-only restricted/kiosk handsets. These decisions supersede earlier "proposed" status labels; preserve earlier review history. Operator, supervisor and administrator presentations share one trusted, authorised Inventory public contract, with progressively appropriate scope and complexity. Scan-first work, large accessible controls, minimal typing, language support, clear committed/pending/offline states, safe error recovery, workstation security and representative usability acceptance are required. Device and network selection cannot grant Inventory rights. A responsive installable PWA-capable delivery target with optional thin Android adapter is preferred, not a mandated implementation stack.

**For the complete approved decision register, Android modes, public contract, cross-capability reciprocity and final appraisal:** [Inventory reassessment and final owner approval](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#final-owner-approval-and-conceptual-closure--18-november-2026). Remaining tasks concern detailed implementation, production-provider mapping, physical devices and acceptance measurements, not unresolved conceptual scope. This does not imply a running app, available production system or measured standards compliance. **PR #81 remains draft and unmerged**, pending owner-authorised publication and latest-master/CI reconciliation.
