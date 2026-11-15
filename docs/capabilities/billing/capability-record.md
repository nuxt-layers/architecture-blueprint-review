# Capability Record — Billing

**Capability:** `billing` — proposed **Domain** responsibility, not an approved standalone implementation or package.
**Review:** 15 November 2026; **BIL-01–BIL-06 and six conceptual public contract surfaces explicitly approved by the project owner**. Technical investigations, implementation and independent acceptance remain outstanding.
**Governing baseline:** [architecture-rules](https://github.com/nuxt-layers/architecture-rules/tree/2eea557fa3acbf9412fea065d2a3cdda42a764fc) `master` `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.
**Blueprint baseline:** [architecture-blueprint-review](https://github.com/nuxt-layers/architecture-blueprint-review/tree/81795d39f64842cc9cbe9a87c94920b065223a52) `master` `81795d39f64842cc9cbe9a87c94920b065223a52`.
**Representative test template:** [application-test-template](https://github.com/nuxt-layers-test/application-test-template/tree/8b7b142b84b5ec2379d4e2e727914fe344187d64) `master` `8b7b142b84b5ec2379d4e2e727914fe344187d64`; no executable acceptance performed.
**Implementation evidence:** Direct repository lookup and organisation-name search found no `nuxt-layers/billing` repository. No default branch SHA, root `CONTRACT.md`, commands, services or implemented screens are verifiable. This is **not** proof that no related functionality exists elsewhere.

## Architectural authority and evidence

**Established:** [Platform Charter](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/platform-charter.md), [Capability Standard](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/capability-standard.md), [Catalogue](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/catalogue.md), [Architecture](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/architecture.md), and applicable accepted ADRs, particularly 0001, 0002, 0006, 0008, 0009, 0012, 0014, 0015 and 0016. These establish responsibility-based classification; separate capability-owned state, schema and outbox; public-only, acyclic dependency edges; fail-closed security; one-call Nuxt composition within 50 host lines; a headless core with optional presentation; and provider neutrality. The governing catalogue calls Billing a **candidate commerce domain**, not an established deployed capability.

**Existing blueprint evidence:** The original Billing record contains provisional notes that Billing may own charge calculation and recurring charge periods; Invoice owns document semantics; Accounting owns financial postings; Payment Gateway executes payments. [Accounting](../accounting/capability-record.md) separates revenue/liabilities and ledger from billing facts. [Invoice](../invoice/capability-record.md) provisionally owns issuance, document corrections and numbering. [Audit](../audit/capability-record.md) distinguishes evidential custody from domain records; [Logging](../logging/capability-record.md) owns operational diagnostics. Current blueprint is non-normative; proposals are not approved implementation contracts. No direct architectural contradiction was established; the charge-versus-document boundary needs explicit approval.

**Evidence statuses throughout:** **Established** = accepted architectural requirement or a verified published contract; **Proposed** = this conceptual design, not yet agreed; **Open** = consequential owner decision; **Unverified** = implementation behaviour or provider capability not independently evidenced.

## Purpose and classification

**Proposed:** Billing independently manages the **commercial charge lifecycle**: when, for whom, for what, and under what commercial terms an amount is chargeable or creditable. It mediates one-off, recurring, usage-based, event-triggered, milestone and manual authorised charges, including charge assessment, periodisation, revisions, aggregation, disputes and billing runs. It can support customer receivables and commercial assessment of supplier payables without creating fictitious Orders. Its durable obligation/charge history merits a **Domain capability** rather than a stateless library or shell composition. A separate implementation repository or deployment is not implied.

**Consumers:** merchant and supplier administrators, applications, Invoice, Accounting, Order, Subscription, Pricing, Booking, usage-owning domains, customers/authorised counterparties, Reporting and external billing integrations.

## Authoritative ownership and exclusions

| Billing owns (proposed) | It does **not** own |
|---|---|
| Charge assessments, amount derivations, period boundaries and billing-cycle states | Pricing's published tariffs/quotes and approved commercial price policy |
| Billing arrangements and schedules of charge calculation, within an agreed contractual scope | Subscription's entitlement and contract/subscription lifecycle; Order's commercial acceptance |
| Charge-line records, grouped charge batches, revisions and commercial adjustment/dispute resolution | Invoice's final issued/received document, statutory number, correction document or delivery |
| Usage evidence references, consumption snapshots and rating decisions | Metering source facts, stock, fulfilment, bookings, asset custody or source service delivery |
| Charge authority mappings, provider confirmation/reconciliation of its own charges | Integrations' connections, credentials and provider transport; external supplier/customer identity |
| Billing's own authorised events, operation outcomes and durable outbox | Accounting's ledger, tax recognition, balances, accruals and payment reconciliation |
| Charge-policy application and approved discounts/credits within delegated authority | Payment Gateway's capture, refund execution, mandates and provider settlement; Audit evidential custody |

Distinguish **charge proposed**, **charge accepted**, **charge finalised**, **invoice requested**, **invoice issued**, **financially posted**, **payment authorised**, **payment settled** and **charge commercially adjusted**. None is an alias for another. Prior finalised charges remain traceable; corrections are explicit linked versions/reversals, not silent edits. A quote, purchase order, recurring commitment or usage reading is not automatically a charge.

Supplier commercial charge assessment is *proposed*; authoritative capture of incoming supplier invoices remains with Invoice and recognition of payable/accrual with Accounting, subject to **BIL-03**.

## Native self-sufficient services and state

**Proposed native baseline:** define validated billing arrangements and effective schedules; assess one-off and periodic billability; accept immutable/versioned source evidence; rate permitted usage/quantities and pro-rata periods under approved terms; calculate charge-line totals, taxes/discount inputs with provenance and rounding controls; generate and review billing runs; finalise a charge set; send an authorised invoice-generation request through Invoice's public contract when available; record invoice acknowledgement without claiming invoice issuance; support charge disputes, adjustments, reversals, credit requests and back-billing restrictions; expose authorised reads/exports; reconcile remote authority; resume after partial failures; retain attributable history.

**Conceptual model:** BillingArrangement (scope, parties, source, commercial authority, cycle), ChargePeriod (effective start/end, zone), BillableEvidence (source owner/id/version and quantity), ChargeAssessment (draft/validated/held/rejected), ChargeLine (currency, quantity/unit, rate/price reference, calculation, adjustment, policy version), BillingRun (scope, cutoff, snapshot, outcomes), ChargeBatch (finalised charge lines; issuance references), Dispute/Adjustment (reason/evidence/decision), ProviderAuthority (scope, capability mapping, verification), and Event/Outbox Record. These are business meanings, **not** persistence schema or universal request objects.

**Indicative lifecycle:** arrangement draft → approved/active → suspended/ended; assessment proposed → validated/held/rejected → approved → finalised; run scheduled → collecting → calculated → reviewing/held → finalised → handoff requested → acknowledged/failed reconciliation; dispute opened → investigated → upheld/rejected/partially upheld → adjustment approved/closed. Invalid transitions fail; a completed period is not mutable merely because a later input arrives. Clock owns time semantics, not billing period policy. A missing optional Invoice integration must not prevent internal charge assessment, but may prevent invoice issue.

**Commercial invariants:** use exact decimal amounts (no binary floating-point money), explicit currency, tax and rounding policy, effective dates and snapshot versions; no unexplained negative/repeated charges; source/version and billing-arrangement provenance; enforced cutoffs and late-evidence policy; conflict detection; tenant/entity isolation; auditable changes; deterministic re-evaluation from approved inputs and policy versions. No provider outage may silently switch the authoritative billing mode.

## Idealised public **inbound** contract

Each row identifies the required upstream fact/command/evidence, originating authority, validation and failure behaviour. `Essential` means required **for the relevant operation**, not that every listed capability is a global install dependency.

| Source and input type | Information and purpose | Originating authority; validation | Requirement; failure |
|---|---|---|---|
| Authorised actor / command | Create, approve, suspend arrangement; assess/finalise run, correct, dispute or request issue | Identity/Authentication/Authorisation server context; scope, permissions, assurance, four-eyes when prescribed | Essential; deny/hold on failed or ambiguous decision |
| Configuration and organisational business policy | Billing mode, cadence, cutoffs, permitted adjustments, currency/rounding and delegation | Configuration stores approved scoped settings; Billing validates charge-domain meaning; Legal Compliance constrains | Essential relevant policies; missing/contradictory effective setting blocks affected operation |
| Pricing / source fact | Versioned tariff, quote, price, discount eligibility and rate evidence | Pricing owns price decision; source revision, effective scope, currency must match | Conditional; unresolved prices hold charge |
| Order / source fact | Agreed items, terms, changes, cancellations, fulfilment evidence | Order owns acceptance; validate association, quantities, version and billing entitlement | Conditional; no implied charge on order creation alone |
| Subscription / source fact | Subscription/plan status, entitlements, billing interval, pause/cancel and change effective date | Subscription owns subscription rights/status; detect conflicting/superseded version | Conditional; hold disputed or inconsistent cycles |
| Booking / service / usage owner / source fact | Approved metered usage, delivery, attendance, milestone and service completion with units/timestamps | Each source owns measurement/performance; deduplicate and validate evidence quality | Conditional; missing measurement cannot be estimated as confirmed |
| Supplier/contract/asset obligation owner / source fact | Approved lease, utility, supplier service agreement or commitment, charge terms, payable eligibility | Contract/Asset/other domain retains source obligation, not Billing | Conditional, BIL-03; unverified bills held for review |
| Customer/supplier reference owner / source fact | Counterparty identity, address/tax status reference, contractual role | Identity/Profile or appropriate business-contact authority; tenant, disclosure and snapshot scope | Essential when charge is attributable; reject mismatched party |
| Clock / semantics | Date/time, calendar and time-zone interpretation for billing periods | Clock validates representation; Billing owns business cutoff meaning | Essential semantics; invalid/ambiguous periods block |
| Legal Compliance / Privacy / policy constraints | Tax/jurisdiction evidence, retention, disclosure, consumer protection, legal hold and correction restrictions | Specialist policy owner/qualified source; version/effective-date validation | Conditional by jurisdiction; fail closed for material uncertainty |
| Invoice / resulting source evidence | Invoice accepted/issued/rejected/credited and authoritative document reference | Invoice owns document state; match charge batch, scope, revision | Conditional; unknown status stays pending, no invented invoice |
| Accounting / resulting source evidence | Posting/receivable/payable status and reconciliation, with accounting period | Accounting owns ledger; never infer posting from charge completion | Conditional; expose independently pending or confirmed |
| Payment Gateway / payment evidence | Payment capture/refund/mandate result only for permitted charge status display | Payment Gateway owns execution; reconcile with Accounting for settled financial balance | Optional/conditional; pending≠paid |
| Integrations / external evidence | Verified provider charge identifiers, capabilities, accepted/rejected responses, read-back, mapping and authority status | Selected provider may be authoritative for approved Billing scope; Integrations owns connectivity | Conditional; offline/ambiguous holds, reconcile; no silent fallback |
| Workflow / approval result | Reviewed commercial adjustment, threshold exception or dispute decision | Workflow executes approval route; Billing validates business decision and actor authority | Conditional; no approval means no protected transition |
| Scheduler / task trigger and Message Queue / event transport | Due-cycle trigger and verified source-event delivery/replay | Scheduler owns trigger execution, MQ owns transport, originating domain owns facts | Optional operational providers; controlled retry, no event-as-authorisation |

## Idealised public **outbound** contract

Every output is scoped by tenant and business entity, with correlation/operation reference, owner/source identifier, revision, effective and recorded time, authority mode, completion state and permitted disclosure. Consumers must not assume all fields or personal data are readable.

| Output / service | Consumer and legitimate meaning | Authority, status, provenance and disclosure |
|---|---|---|
| Arrangement management results and authorised reads | Application/Subscription/Order: Billing arrangement and approved charging cadence | Billing-owned commercial schedule, not subscription right or executed sale; draft/active/suspended/closed |
| Charge assessment and charge-line explanation | Applicant, Invoice, Accounting, reporting: why amount and period are chargeable | Billing-owned calculation; source tariff/evidence versions, currency, rounding, policies; proposed/held/finalised |
| Billing run outcomes and exception queues | Finance/admin and Scheduler: which periods processed and which need attention | Billing-owned run state; per-line and per-batch finalisation distinct from invoicing |
| Finalised charge batch / invoice handoff instruction | Invoice: authorised snapshot of charge lines, counterparties and provenance suitable for its own validation | Billing owns charge facts; Invoice must independently accept, number and issue |
| Correction/credit or rebill recommendation | Invoice/Accounting: commercial reason and delta linked to original assessment | Billing determines commercial adjustment, not legal credit-note issuance or ledger correction |
| Billing dispute decision and evidence references | Authorised users, Invoice, Accounting, Audit | Billing's commercial decision; financial/document follow-up separate; redact sensitive dispute content |
| Charge status, history and permitted export | Customers, administrators, Reporting/Search | Authoritative Billing states and source versions; never imply payment settlement or disclose unrelated account balances |
| Provider authority and reconciliation status | Integrations, administrators and downstream consumers | Billing scope and selection; distinguish native, external, queued, accepted, confirmed, inconsistent and unavailable |
| Billing-owned domain events | MQ, Audit, Invoice, Accounting, Notifications, Reporting | Emitted after Billing-owned committed transition through durable outbox; references, versions and minimal disclosure |
| Operational diagnostics | Logging/Observability | Purpose-limited structured error/latency/correlation signals, **not** legal/commercial evidence or proof of event commitment |
| Risk-selected accountable evidence | Audit | Attributable Billing action/decision/outcome with evidential context; Audit owns custody and verification, not charges |

**Proposed event families:** `billing.arrangement.approved|suspended|ended`, `billing.charge.assessed|held|finalised`, `billing.run.finalised|partially-failed`, `billing.adjustment.approved`, `billing.dispute.resolved`, `billing.invoice-handoff.requested`, `billing.provider-authority.changed`, `billing.reconciliation.exception`. Names are conceptual, **not committed API identifiers**. Events are facts about Billing state, not commands or proof of Invoice/Accounting/Payment Gateway state. Subscribers tolerate repeats, delay and out-of-order arrivals.

## Six approved conceptual public contract surfaces

**Agreed conceptual direction (15 November 2026):** The project owner explicitly approved the following six logical surfaces. These group responsibilities for consumers; they **do not** prescribe six packages, endpoints, interfaces in source code or distinct persistence units. Every surface uses authorised, versioned, source-attributed information and clearly distinguishes requested, accepted, locally confirmed, externally confirmed, held and rejected outcomes. The inbound and outbound tables above remain the detailed dependency/data-flow matrix.

| Surface | Incoming information/commands and supplier | Operations and owned decisions | Outgoing information and consumer | Validation, absence and failure |
|---|---|---|---|---|
| **BIL-S01 — Commercial evidence intake** | Authoritative tariff/version from Pricing; contractual facts and fulfilment from Order; subscription status from Subscription; usage/booking/milestone facts from their domain owners; approved supplier commitment and counterparty references | Register, validate, classify and correlate attributable billable evidence without reowning source facts; detect stale, superseded, duplicated, incomplete and contradictory inputs | Evidence acceptance/hold/rejection, missing-evidence reasons, attributable source references and eligibility for assessment to owning sources and authorised applications | Authorise actor/tenant/entity and match source version, effective time, unit, agreement and policy. Invalid/late/absent essential evidence is held or rejected; receiving a source event alone never permits a charge |
| **BIL-S02 — Charge management** | Accepted evidence, effective tariffs, arrangement and calculation policies, authorised assess/approve/finalise/adjust commands | Own calculation, period allocation, prorating, versioned charge lines, commercial approval, finalisation and adjustment decisions | Charge assessments, explainable rate/quantity/discount/tax inputs, finalised charge batches, linked corrections, status and commercial lifecycle events to Invoice, Accounting and authorised callers | Exact decimal arithmetic; explicit currency, rounding, cutoff and tax provenance; idempotent operation identity and expected version. Missing price/authority or failed approval holds the transition; finalised history is never silently overwritten |
| **BIL-S03 — Financial handoff** | Finalised charge batch, permitted invoice request, source acknowledgement from Invoice, posting evidence from Accounting and permitted payment status from Payment Gateway | Request/document charge handoff, track per-consumer acknowledgement, surface unresolved handoffs and reconcile linked identities; **does not** issue invoices, post ledgers or execute collections | Document-ready charge snapshot and authorised adjustment request to Invoice; charge facts/source evidence to Accounting; collection reference/amount only where an independently approved payment operation exists | Request/accepted/issued/posted/settled are distinct statuses owned by their respective domains. No ack means pending/unknown, not success; retries deduplicate and investigate uncertain results |
| **BIL-S04 — Billing lifecycle and reconciliation** | Arrangement settings and effective dates, cycle trigger, customer/supplier disputes, approved correction decisions, external provider read-back and authority-change request | Own arrangement activation/suspension, run/cycle progression, disputed charge status, commercial adjustments, reconciliation exceptions and controlled native/provider cutover | Billing-run summaries, exception and dispute results, authority and migration status, adjustment events to Invoice/Accounting, operations view | Enforce authorised state transitions, time-zone-aware periods, immutable evidence and single scope authority. Partial runs remain recoverable; provider outages never silently switch mode; unsupported operations explicitly fail |
| **BIL-S05 — Queries and reporting** | Authorised queries scoped to tenant/entity/party/arrangement, date range, historical version and permitted fields | Provide filtered current/historic billing views and reproducible charge explanations, without copying other owners' records as authoritative | Arrangement state, charge breakdown/history, run totals and exceptions, dispute state, provenance, permitted exports and views to UIs, Reporting and Search | Authorise before querying; minimise personal/commercial data; disclose source versions, freshness, currency, completeness and provider uncertainty; no inference of financial settlement |
| **BIL-S06 — Events and operational integration** | Committed Billing transitions, risk-based evidence policy, optional task execution, relay transport and diagnostic sinks | Own event meaning and durable outbox; classify accountable business evidence separately from technical diagnostics; expose operational delivery/reconciliation status | Billing-owned domain events to Message Queue/consumers; selected evidence to Audit; purpose-limited diagnostics to Logging/Observability; notification intents to Notifications | Emit events only for committed Billing facts; consumers handle duplicates/out-of-order replay. A technical log does not prove an Audit receipt or charge; relay/delivery failures must remain visible and recoverable |

**Surface independence:** All six can be consumed through one self-contained public contract while preserving clear source ownership. A surface may expose commands and queries and publish events where meaningful; it must not require all interaction styles purely for symmetry. The domain-specific operations, provider capabilities and signatures remain for the eventual root `CONTRACT.md` and separately verified implementation.

**Cross-capability information exchange:** The authoritative facts flow *into* BIL-S01 from source owners. BIL-S02 produces the charge decisions that BIL-S03 supplies for Invoice/Accounting/Payment processing. BIL-S04 controls lifecycle and reconciliation, BIL-S05 exposes permitted read models and BIL-S06 publishes owned change facts, Audit evidence and diagnostics. Consumers may send independently owned acknowledgements back to BIL-S03/BIL-S04 through public boundaries; these reciprocal information flows must not create circular package dependencies.

## Commands, queries, events and shared interaction semantics

**Proposed commands:** configure/revise arrangement; record validated source evidence; assess charges; approve/hold/reject/finalise charge(s) or run; request invoice handoff; open/resolve dispute; apply credit/adjustment; suspend/resume/close arrangement; reconcile provider; request authority migration. Commands require scope, caller, operation/idempotency reference, expected version and policy context as appropriate. Results distinguish **rejected**, **accepted for processing**, **completed locally**, **accepted by external provider**, **verified externally**, **held** and **inconsistent**.

**Proposed queries:** arrangement/effective terms, billable evidence status, draft/final charge breakdown, billing run and exceptions, attributable invoice references, dispute history, provider availability and authority, source provenance and historic billing snapshots. Disclose completeness, currency, consistency point and freshness. Never expose another customer's charges or infer settlement.

**Proposed events:** above, durable, originated only following a committed Billing change. Consumer replay must not duplicate finalisation or invoice handoff. Transport cannot guarantee exactly-once delivery.

**Shared context:** trusted tenant, entity, subject/service actor, role and assurance; relevant customer/supplier; source owner and immutable/versioned reference; billing arrangement and effective policy; charge period including zone and cutoff; charge currency and precision; effective/recorded times; correlation/causation and operation IDs; authority/provider identity; evidence receipt and validation; classification and disclosure scope. These are logical contextual needs, **not** a compulsory universal request structure.

**Failure and recovery:** no success on partial issue/posting/payment; retriable versus permanent errors are distinct; failed required security/policy/authority checks fail closed. Idempotent retries return original committed result or a reconciliation-needed state; unexpected duplicates are rejected. Source updates past a cutoff create an explicit future adjustment or authorised reopening, not silent mutation. External uncertain results must be read back before replay/compensation; an absent remote response is not confirmation of failure. Preserve a durable pending/exception queue. Outbox relay failure does not erase committed Billing fact; isolate diagnostic and audit-capture failures by defined policy.

## Cross-capability relationships and graph

| Other owner | Billing consumes | Billing supplies | Relationship / absence |
|---|---|---|---|
| [Pricing](../pricing/capability-record.md) | Tariff/quote, rate, price version | Charge and consumed price provenance | Conditional public contract; missing rate holds |
| [Order](../order/capability-record.md) | Accepted terms and eligible performance | Charge status, adjustment references | Conditional; no order required for every charge |
| [Subscription](../subscription/capability-record.md) | Subscription status, plan change, entitlement period | Rated recurring charge and run status | Conditional; independent subscription lifecycle |
| [Booking](../booking/capability-record.md) and service domains | Booking/service and metered usage evidence | Source-attributed charges | Conditional; source stays authoritative |
| [Invoice](../invoice/capability-record.md) | Issue/correction results | Finalised charge snapshots and adjustment requests | Conditional; invoice issuing unavailable in its absence |
| [Accounting](../accounting/capability-record.md) | Posting and balance state | Billable facts and commercial adjustments | Conditional; Billing does not recognise revenue or liability |
| [Payment Gateway](../payment_gateway/capability-record.md) | Payment execution status when permitted | Amount/reference and reconciliation cues | Conditional; settlement stays elsewhere |
| [Asset](../asset/capability-record.md) / contractual sources | Lease/licence/service obligation reference | Charge assessment references | Conditional; no duplicate asset rights |
| [Integrations](../integrations/capability-record.md) | Provider discovery, verified payloads, transport | Authoritative business actions and mapped results | Optional mode; selected external authority requires connection |
| [Identity](../identity/capability-record.md), [Authentication](../authentication/capability-record.md), [Authorisation](../authorisation/capability-record.md) | Authoritative tenant/actor and server access decision | Scoped resource/action and risk evidence | Essential protected operations; fail closed |
| [Configuration](../configuration/capability-record.md), [Clock](../clock/capability-record.md) | Approved settings/provenance and time semantics | Domain schema/validation and periods | Essential where used; no duplicate policy ownership |
| [Legal Compliance](../legal_compliance/capability-record.md), [Privacy](../privacy/capability-record.md) | Applicable legal/disclosure/retention constraints | Processing purpose and data scope | Essential when applicable |
| [Audit](../audit/capability-record.md), [Logging](../logging/capability-record.md), Observability | Evidence policy, diagnostic delivery/status | Business evidence; separately minimised technical logs/metrics | Distinct interfaces, retention and failure semantics |
| Workflow, Scheduler, [Message Queue](../message_queue/capability-record.md), Notifications | Approval decisions, triggers, event transport, notices | Pending work, task handlers, outbox/domain events, notice intents | Optional/conditional; no transferred charge authority |
| Reporting, Search, UI, Theme Manager | Authorised views and presentation service | Typed filtered Billing read models | Optional consumers, no ownership change |

**Graph constraint:** The table is an interaction map, **not a declared package dependency graph**. Use host-connected public ports, independently-owned events and one-way source/consumer relationships to avoid Billing↔Invoice/Subscription/Accounting import cycles. If two-way integration is necessary, publish a one-way port, stable event contract or a neutral integration boundary rather than mutual runtime imports.

## Modes, provider authority and migration

**Proposed native mode:** Billing itself is authoritative for charge records and lifecycle; provider integrations absent. Invoice issuing and accounting posting may remain unavailable but charge creation, validation, adjustment and history still function.

**Proposed connected mode:** An approved external billing service can be the authoritative charging engine for a defined tenant/entity/contract scope, **only if** necessary provider operations can be discovered, validated, reconciled and safely delegated through Integrations. The native data are clearly labelled mapped projections, pending intents or historical evidence rather than simultaneously authoritative charges. Provider-specific connector does not own Billing's public business rules. Incomplete/unsupported provider operations fail explicitly; never silently issue local charges on an external-authority outage.

**Authority transfer:** Require authorised approval, scope and cutoff, historic export, identity/charge/period mapping, handling in-flight runs and invoices, reconciliation/read-back, a freeze or safe handover, rollback limits and verified no-overlap coverage. Native and external authority modes must not double bill. External tax and localisation features need independent evidence.

## Configuration, security, legal and quality

**Established baseline:** OWASP ASVS 5 L2, higher assurance for critical actions where required; access decisions server-side; WCAG 2.2 AA; i18n and Theme Manager semantics; data minimisation, purpose limitations, retention, lawful transfer and region constraints. The host supplies documented infrastructure and does not implement Billing's business rules or storage. No client-supplied amount, status or tenant claim is trusted without server validation.

**Proposed protected permissions:** manage commercial rules; assess charges; finalise charges; approve adjustments; resolve disputes; choose/migrate authority; view customer-specific charges; view all tenant billing; export; manage providers. Enforce least privilege, separation of duties/step-up for significant corrections, independently applied legal holds and tenant scope. Configuration may store policy declarations/revisions but Billing owns domain interpretation and calculation; Legal Compliance governs legal constraints, not pricing; Audit stores independent evidence, Logging stores diagnostics.

**Jurisdictional investigation:** UK VAT invoicing/tax-point and credit-note requirements, Making Tax Digital interactions, consumer/recurring-payment disclosures, unfair billing practices, statutory limitation and record retention, personal-data obligations, payment services/direct debit rules where relevant, and sector-specific billing (utilities/telecoms/health) need qualified, jurisdiction-specific validation. No universal legal or tax correctness is claimed. Billing does not calculate statutory tax without approved tax evidence/policy.

## Presentation concept — optional Billing dashboard

**Proposed integration pattern:** Application side-menu item **Billing** → capability dashboard route, configured by composition, analogous to the Theme Manager-enabled pattern in [application-test-template](https://github.com/nuxt-layers-test/application-test-template). No claim the template already contains Billing screens. Host owns menu placement, route/branding and optional overrides; Billing's headless core retains server-side rules. ADR-0009 permits optional separable screens, disabled through `presentation: false`; no required separate UI kit.

**Candidate screens:** (1) Billing overview with due runs, unbilled charges, held exceptions and provider status; (2) arrangements/cycles; (3) pending evidence and billable usage; (4) assess/run preview showing explainable calculations; (5) finalised charges and invoice handoff; (6) disputes/credits/adjustments; (7) customer-specific authorised charge view; (8) provider connection and reconciliation status; (9) commercial policy/configuration and approval history; (10) restricted audit trail and diagnostics links. Detail/edit panels must show provenance and whether displayed state is Billing-owned, Invoice-owned, Accounting-owned or provider-reported. Display remote/pending/stale status plainly.

**Accessibility and security:** roles and field-level disclosures control navigation and datasets, but hiding a menu is never authorisation; protected transitions run server-side. Accessible tables, error summaries, step-up, confirmation for irreversible actions, localised currencies and dates via Clock, and Theme Manager vocabulary. Optional screens consume *only* public Billing contracts and permitted cooperating capabilities; they must not query private schemas.

## Conceptual contract acceptance scenarios

| Scenario / input | Expected behaviour and output | Authority |
|---|---|---|
| Native monthly charge; approved active arrangement and tariff | Period assessed once, charge breakdown and finalised batch; no invoice or payment success inferred | Billing charge; Pricing source |
| Subscription changes halfway through period | Versioned source and proration policy applied; old/new rates explained; no entitlement mutation | Subscription entitlement, Billing charge |
| Order fulfilled, then invoice generated | Fulfilment evidence validated; charge finalised; Invoice separately accepts/issues; Accounting separately posts | Order, Billing, Invoice, Accounting |
| Unauthorised other-tenant adjustment | Denied before mutation and disclosure, accountable denial evidence as required | Authorisation + Billing |
| Invalid usage, currency mismatch or contradictory revisions | Hold/reject with stable reason and origin references, no financial output claimed | Source owner + Billing |
| Duplicate request/replayed source event | Deterministic prior result or explicit conflict; no duplicate charge or invoice request | Billing |
| External provider confirms charge but response times out | Uncertain/pending state; read-back and reconciliation before retry; no local fallback | Selected provider + Billing mapping |
| Late cancellation after finalisation | Original preserved; explicit adjustment/rebill under policy and linked evidence | Source owner + Billing |
| Disputed supplier utility charge | Evidence captured, hold/correction determination; supplier invoice and payable handled by Invoice/Accounting | Billing commercial assessment; others retain facts |
| Billing event delivered twice to Accounting | Accounting independently deduplicates source version and determines posting; Billing event is not journal | Billing + Accounting |
| No Invoice or Payment Gateway configured | Native charge calculations/history work; issuing/collecting clearly unavailable | Billing |
| Provider authority cutover | Freeze/reconcile old work; verified mapping and cutoff; no duplicate charged interval | Billing-selected authority |
| Diagnostic sink outage after charge commitment | Committed charge remains valid; separately expose diagnostics failure, preserve required audit policy | Billing, Logging, Audit |

## Findings, decisions, verification and sign-off

### Established requirements

- **EST-BIL-A:** Capability ownership, public-only interactions and jointly acyclic dependencies follow accepted ADR-0001/0016.
- **EST-BIL-B:** Independent state/outbox, provider-neutral host composition and fail-closed security follow ADR-0002/0012 and normative standards.
- **EST-BIL-C:** Headless services and optional separable themed screens follow ADR-0009; Billing remains a candidate, not verified implementation.
- **EST-BIL-D:** The blueprint already separates commercial charges conceptually from Invoice's documents, Accounting's postings and Payment Gateway's execution; this separation is **provisional blueprint direction**, not a newly accepted governing ADR.

### Owner-approved conceptual decisions — 15 November 2026

All six decisions below were **explicitly approved by the project owner in this review**. This approval establishes the conceptual ownership and presentation direction; it is **not** authorisation to implement a new repository, a determination of legal conformity or proof of a provider's features.

- **BIL-01 — Approved:** Billing is the independent Domain authority for commercial charge assessment, periodisation, finalisation, commercial adjustment and disputes. Pricing, Invoice, Accounting and Payment Gateway retain their respective source-of-truth boundaries.
- **BIL-02 — Approved:** Subscription owns entitlements and subscription-plan/contract lifecycle; Billing owns recurring charge rating, prorating, billing runs and charge amounts. Source effective-date/version evidence is mandatory.
- **BIL-03 — Approved:** Billing may assess attributable supplier commercial obligations; Invoice owns inbound supplier invoice capture/validation, and Accounting owns payable/accrual recognition. Billing must not invent supplier contractual authority.
- **BIL-04 — Approved:** Billing owns commercial charge disputes and adjustment decisions; Invoice owns issued credit/correction documents; Accounting owns financial reversals/postings. Cross-capability confirmations remain independently authoritative.
- **BIL-05 — Approved:** A tenant/entity/scope may select native Billing or an approved external authoritative charge engine, not concurrent competing authorities; cutover, mapping, reconciliation, provider limitations and unsupported actions are explicit.
- **BIL-06 — Approved:** Billing may supply optional standard dashboard/screens, including navigation through the host's capability menu. Its headless core and server access controls must work with presentation disabled, in accordance with ADR-0009.

**Additional approval:** **BIL-S01–BIL-S06**, the six coherent public contract surfaces defined above, were explicitly approved on 15 November 2026. They are *logical conceptual surfaces*, not final runtime APIs.

### Technical investigations (not owner decisions)

- **TI-BIL-A:** Precise tax-jurisdiction, tax-point and supplier-invoice treatment after qualified review.
- **TI-BIL-B:** Versioned price/usage snapshot boundaries, proration, daylight-saving and rounding algorithms.
- **TI-BIL-C:** Provider coverage, idempotency/read-back guarantees, partial failure, cutover and portability.
- **TI-BIL-D:** Verify how the current application template exposes navigation/Theme Manager and an eventual minimal host meets ADR-0012.
- **TI-BIL-E:** Check whether a formal business-contact or contract-owning domain already supplies needed supplier/customer/lease facts; avoid inventing one.
- **TI-BIL-F:** Reconcile tax-treatment ownership and qualified jurisdiction-specific validation with Pricing, Invoice, Accounting and Legal Compliance; do not assume Billing determines statutory tax.
- **TI-BIL-G:** Specify generic, versioned billable-usage evidence and units supplied by existing domain owners without prematurely inventing a Metering capability.
- **TI-BIL-H:** Define Billing's own missing/duplicate/unbilled-charge assurance and exception reporting while leaving Accounting reconciliation with Accounting.

### Implementation alignment (deferred, not authorised)

- **IMP-BIL-A:** When implemented, publish self-contained root `CONTRACT.md` and actual stable ports/commands/queries/events/errors; declare required/optional dependency graph and provider settings.
- **IMP-BIL-B:** Capability-owned stores, migrations, test fakes, durable outbox, provider adapter and optional presentation.
- **IMP-BIL-C:** Reconcile public contracts in Invoice, Accounting, Subscription, Pricing, Audit, Logging and Integrations through separate authorised changes.

### Acceptance and verification (future evidence)

- **ACC-BIL-A:** Independent consumer follows root `CONTRACT.md` alone, with one composition call and measured ≤50 capability-specific Nuxt host lines where applicable.
- **ACC-BIL-B:** Native, provider outage, duplicate/replay, cutover, separation-of-duties, tenant isolation, dispute/correction and round-trip reconciliation scenarios pass.
- **ACC-BIL-C:** UI presentation-off, side-navigation, authorised field-level disclosure, WCAG 2.2 AA and i18n acceptance.
- **ACC-BIL-D:** Verify no direct imports/SQL into other owners and no dependency cycles; legal applicability independently validated.

**Conceptual sign-off:** **Approved scope and six public contract surfaces (BIL-01–BIL-06, BIL-S01–BIL-S06) as at 15 November 2026.** Remaining technical investigations, implementation-contract alignment, independently verified acceptance, provider feasibility and jurisdiction-specific legal review are explicitly **outstanding**. Conceptual scope approval is **not** implementation readiness, authorisation for a new repository, operational behaviour or regulatory certification. No governing ADR, normative standard or implementation repository is changed by this review. Next alphabetical entry: [blog](../blog/capability-record.md).
