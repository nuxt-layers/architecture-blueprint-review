# Capability Record — Invoice

**Capability:** `invoice`. **Proposed classification:** Domain candidate; independent authoritative document lifecycle, not a renderer or application composition.  
**Review:** 18 November 2026. **Owner-approved conceptual design direction to date** (explicit confirmation after the extended review); still non-normative and not implementation acceptance.  
**Opening authority:** `nuxt-layers/architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`; `nuxt-layers/architecture-blueprint-review/master@a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. ADR-0017 and ADR-0018 are accepted at the governing baseline.  
**Evidence:** Current governing `docs/catalogue.md`, `docs/architecture.md`, `docs/capability-standard.md`; current blueprint Billing, Accounting, Order and Integrations records; [opening review baseline](../../../reviews/invoice-review-baseline.md). Organisation repository search for `nuxt-layers/invoice` found no implementation repository. No root Invoice `CONTRACT.md`, runtime, migrations, tests, provider acceptance or production capability is verified. No inferred package-level dependency is approved.

## Purpose and independent justification

Invoice is the authoritative business boundary for **issued sales invoices and credit/debit/corrective documents**, received supplier invoices, their issue/receipt and verification evidence, numbering, snapshots, delivery/receipt acknowledgements, disputes and document-level settlement allocation status. These records have enforceable lifecycle, originality and history independent of Charge calculation, Order acceptance, Account postings, Payment execution and document rendering. An invoice is not merely a PDF, nor does creating a charge, journal, payment or file prove an invoice has legally been issued.

**Proposed disposition:** retain as a Domain capability candidate with a headless public contract and optional separable presentation. Independent repository/package creation remains a separate decision under the classification gate; this review neither requires nor asserts it.

## Authoritative ownership and exclusions

| Invoice owns, proposed | Excluded owner or authority |
|---|---|
| Invoice type, issuance intent, lifecycle, original approved facts and immutable issued snapshot; supplier-bill capture and receipt evidence | Billing owns billable charges, periods, commercial adjustments and calculation decisions |
| Number allocation scoped to issuing legal entity, document type, jurisdiction/series and applicable regime; collision protection | Legal Compliance provides qualified applicable obligations, not Invoice's business decisions |
| Validation of sourced amount/tax/rounding totals, document semantics and applicable approved rules; versioned line and counterparty snapshots | Pricing owns offers; source domains own agreed consideration, quantity, performed services and evidence; no independent Invoice repricing |
| Delivery/receipt attempt, immutable artefact reference/hash, recipient confirmation and outbound/inbound provider reconciliation | Notifications owns message dispatch; Storage owns bytes; Export/Template Engine own rendering mechanics |
| Correction, cancellation/void where permitted, credit/debit notes with explicit predecessor relationship; disputes and disputed status | Accounting owns financial posting, tax recognition, period close and ledger adjustments |
| Document-level amount due and settlement *allocation view* derived from verified payment and accounting evidence; unknown/pending state explicit | Payment Gateway owns initiation/capture/refund and payment-provider truth; Accounting owns general ledger reconciliation and balances |
| Provider authority scope, pending external issue/receipt, remote identifiers and reconciliation evidence for Invoice's own documents | Integrations owns connector registration, secrets, mapping, transport and checkpoints; provider can be approved external issuer/record authority |
| Invoice-owned durable outbox, versioned change provenance, command results and authorised views | Audit owns cross-domain accountable evidence; Logging and Observability own operational telemetry |

Do not infer a legal bill-to party, legal seller, taxable entity or entitlement from group/tenant hierarchy. External counterparties may lack an application Identity. Preserve the document's legal-party and contact/address/tax snapshots at issue/receipt; later contact edits do not rewrite issued records.

## Native service and lifecycle

**Native mode:** without a designated external invoice authority, an approved scope may create, validate, approve, issue, transmit, track, correct, credit, receive and reconcile invoices using capability-owned records and rules. This is a genuine usable invoice service, not a placeholder for Accounting, Publisher, a PDF generator or a third-party connector. No legally required issuance or transmission is claimed where requisite legal rules and configured resources are absent.

**Proposed model:** InvoiceAuthorityScope (issuer/receiver legal-party, tenant, jurisdiction, series, effective epoch and authority mode); InvoiceDraft; InvoiceSnapshot (source/evidence versions, parties, lines, taxes, totals, currency, terms, issue/due dates, document identifier); IssuanceAttempt; ProviderAcknowledgement; DeliveryAttempt; ReceivedBill; CorrectionLink; Dispute; SettlementAllocationProjection; OutboxEvent. These are business concepts, **not** a persistence schema.

- **Outbound sales:** draft → validated/held/rejected → approved (where needed) → issuance reserved/pending → **issued only on authoritative, uniquely evidenced completion** → delivered/undelivered/acknowledged as separate delivery states → paid/part-paid/disputed/overdue as derived state → corrected/credited via linked documents. Rejected issue attempts cannot consume a final legally issued number without the jurisdiction's approved policy; reserved or voided numbers remain traceable.
- **Inbound supplier:** received/unverified → verified or rejected/duplicate/disputed → accepted for downstream payable assessment → corrected/credited/closed with immutable source artefact and receipt trail. Receipt is not approval to pay, posting or agreement with the claim.
- **Native/connected provider authority:** exactly one designated authoritative issuer/receiver for a given entity + document scope + effective period. Connected issuance is pending until remote confirmation and read-back or equivalent trustworthy evidence. Timeout/ambiguous response means **unknown—not failed, not issued, and never safely reissued as a new invoice**. No automatic local failover. Switching authorities requires approvals, a cut-over, series and remote-ID mapping, in-flight reconciliation, historical export and duplicate prevention.
- **Correction:** preserve original issued facts and history; issue a separately identified corrective/credit/debit document when appropriate. No destructive edits to issued documents. Cancellation and invoice-number sequence treatment depend on jurisdiction and policy.
- **Failure/recovery:** required storage, source facts, applicable policy or authorisation absent/contradictory ⇒ fail closed or hold; distinguish validation rejection, provider unsupported, transport failed, remote state unknown, reconciliation required and confirmed completion. Persistent idempotency, request correlation and stable source revisions prevent duplicate issuance; retries reuse authoritative operation identity.

**Invariants:** exact decimal money, currency and rounding basis; currency conversion requires named rate/effective-date authority; totals reconcile with line/tax/discount evidence; uniqueness by issuer/series/regime with approved fiscal numbering policy; tenant and legal-entity separation; immutable provenance and historical issued presentation; explicit legal restrictions for alteration, electronic invoicing, signatures, retention and tax. Fiscal/legal regime must be qualified for each issuer and transaction context; no universal UK or cross-border rule is implied.

## Idealised public inbound contract

All inputs enter via documented public interfaces, not another capability's private storage. “Required” below means required **for that operation**, not a hard package import.

| Source and input | Meaning, owner and validation | Requirement and failure semantics |
|---|---|---|
| Actor/host, Identity, Authentication, Authorisation | Caller, tenancy, issuer/recipient scope, source resource reference, assurance, role and server-side operation decision | Essential to protected mutations/reads; reject/hold missing, stale or denied decisions; event receipt never grants authority |
| Billing finalised charge batch or approved adjustment request | Source line IDs/revisions, agreed amounts, tax inputs, currency, period and commercial approval; Billing authoritative for charge decision | Conditional for charge-backed issue; unfinalised, stale, repeated or inconsistent batches held/rejected; standalone invoice is permitted |
| Order, Subscription, service/usage/contract source | Agreed buyer/seller terms, items, deliveries, acceptance and cancellation evidence, with provenance and version | Conditional; never invent order or claim fulfilment; source change after issue triggers adjustment review |
| Counterparty/business-party source, verified contact/tax evidence | Legal seller/buyer, addresses, identifiers, routing and disclosure permissions, with issue-time snapshots | Essential to valid issue/receive; missing or disputed legal party blocks; business-party owner remains open |
| Configuration, domain approval and Legal Compliance/Privacy | Approved scope, series, taxable/e-invoicing regime, mandatory fields, retention, legal holds, delegation, provider selection and effective policy | Essential where applicable; conflict, unknown legal obligation or withdrawn authority holds issue or disclosure; optional formatting never weakens statutory floors |
| Clock | Date, zone and temporal interpretation for issue, supply period, due date, provider cutoff | Essential semantic validation; impossible/ambiguous temporal facts rejected |
| Provider via Integrations | Provider connection/operation support, remote issue/receipt identifiers, signed/verified confirmations, retries and read-back evidence | Conditional connected mode; unsupported or unknown state holds; transport response alone is not issue confirmation |
| Payment Gateway and Accounting | Independently verified payment, refunds, allocations, reversals, ledger reconciliation reference and period restrictions | Conditional to settlement view/financial correction; unknown/conflicting evidence is not “paid” |
| Authorised recipient or supplier evidence | Submitted inbound bill, original artefact, authenticity/duplicates, delivery receipt, dispute/correction request | Essential for applicable intake; suspect, conflicting and unverifiable documents quarantined for review |
| Workflow, document/rendering and delivery ports | Approval outcome, authorised template/version/render artifact, send outcome and receipt | Conditional policy/channel; template cannot change approved finance; sending != issuing, delivering != receiving |

## Idealised public outbound contract

| Surface, consumers | Output semantics, authority and permitted conclusion |
|---|---|
| Issue/receive operation result — Billing, Order, host | Accepted, rejected, pending, confirmed issued/received, unknown or needs reconciliation; immutable document/operation IDs and source revisions; **only issued/verified state** asserts authoritative status |
| Invoice detail/list and immutable snapshot — authorised user, Accounting, Reporting, Export | Legal-party and tax/amount snapshots, issue date, number/series, source evidence, currency, corrective lineage, document and provider provenance; current and historical status; scoped redaction and pagination/completeness |
| Charge handoff and correction acknowledgement — Billing | Exact originating charge batch/line revision and formal issue/rejection/correction references; never reassigns commercial charge authority |
| Financial posting source — Accounting | Confirmed invoice/credit/receipt evidence, amounts, party, tax and corrective links; does not assert that books have been posted or amounts recognised |
| Settlement view — customer, Accounting, service consumer | Document-level allocated/remaining/disputed figure tagged derived, freshness and payment/accounting evidence; not a guaranteed bank balance or provider capture |
| Provider reconciliation — operator, Integrations | Chosen authority, supported operations, remote references, last confirmed/unknown outcomes, mapping revision, scope, cutoff and unresolved mismatches; no secrets |
| Delivery and notification intent — Notifications, Workflow, authorised applications | Approved invoice document reference, minimum necessary recipient/channel and purpose, delivery result/acknowledgement; not unconditional disclosure permission |
| Committed change events — Billing, Accounting, Reporting, Audit consumer | Draft validated/held, issue requested/confirmed/rejected, bill received/verified, credit issued, dispute changed, allocation updated, provider reconciliation required/resolved; durable at-least-once via owned outbox; events do not confer authority |
| Export/render request — Export/Template Engine/Publisher when selected | Authorised immutable data snapshot/version, template locale, permitted attachments and stable proof/hash; rendered files are derivative, never the invoice source of truth |

**Required envelope semantics proportionate to each operation:** tenant and legal-accountability scope, owner resource reference and version, caller/assurance/decision evidence where relevant, correlation and idempotency identity, policy/regime version/effective time, native/provider authority and confirmation evidence, processing status and completeness, privacy/disclosure classification. Do **not** prescribe a universal request object or provider SDK types.

**Commands:** create/validate/approve/issue, record confirmed receipt, dispute, issue correction/credit, request delivery, record verified settlement allocation, reconcile, export and governed authority cut-over; every command enforces permissions, optimistic revision, valid transition, source verification and idempotency with durable result/recovery. **Queries:** authorised document/series/history/detail/status, pending provider operations, duplicate/supplier verification and correction graph; include data freshness, omitted/redacted scope and authoritative versus derived status. **Events:** emitted only for committed Invoice-owned changes; subscriber must handle duplicates, reordering and missing related events by querying public state; not exactly-once distributed delivery.

## Cross-capability relationships and dependency direction

| Relationship | Inputs to Invoice / outputs back | Critical boundary, failure and direction |
|---|---|---|
| **Billing** (approved BIL-01–06) | Finalised charge/adjustment batches → issue and credit status/document references | Billing owns charge; Invoice owns legal document; no mutual package import; event/host-port interaction |
| **Accounting** | Posting/settlement confirmation and constraints → immutable document/credit source evidence | Accounting owns books; Invoice owns issued data; asynchronous independently authorised consumption, no cross-database join |
| **Payment Gateway** | Verified capture/refund/settlement evidence → document reference/amount due for payment context | Does not execute payment, infer capture or reconcile provider itself; unavailable => settlement status unknown |
| **Order / Subscription / Pricing / Product / usage owners** | Versioned commercial source references and terms → document/adjustment references | Source remains authoritative; standalone services and supplier bills need no Order |
| **Business Contacts / Parties (owner unresolved)** | Proven legal parties, addresses, tax details and consent → referenced issued snapshot/status | Identity membership alone insufficient; anonymous external parties supported |
| **Integrations** (parallel PR #76) | Connection support, provider request/confirmation/checkpoint → domain operation intent, reconciliation results | No domain rules in connector; no double issue; design remains provisional pending PR reconciliation |
| **Legal Compliance / Privacy / Configuration / Clock** | Applicable approved legal constraints, data policy, scoped settings and temporal semantics → Invoice domain enforcement/state | Configuration doesn't override law or invariants; no inferred general policy service |
| **Authorisation / IAM** | Tenant/resource access decision, verified actor and assurance → scoped resource/status | No parent-to-child implicit access; no privacy bypass |
| **Workflow / Scheduler / Notifications / Message Queue** | Approved sign-off, due/overdue triggers, dispatch and event delivery → approved intents and owned events | Workflow does not issue invoices; scheduler doesn't own dates or issue state; queue doesn't own outbox |
| **Publisher / Content Editor / Template Engine / Export / Storage** | Optional drafting, template, render, file and delivery adjuncts → approved immutable snapshot and scoped links | No duplicate invoice lifecycle; optional rendering must not become mandatory domain authority |
| **Audit / Logging / Observability / Reporting / Search** | Audit evidence, operational telemetry and read-only authorised index/report inputs | Never confer issue status, grant access or become parallel business record |

**Dependency rule:** conceptual information exchanges are directional public calls, injected ports or outbox events. They are not automatically runtime/package imports; direct edges and Nuxt extension edges must form a **jointly acyclic** graph under ADR-0016. For a future implementation, document minimum required and optional ports; retain ADR-0012 one-operation Nuxt host integration and 50-line capability-specific budget, independent headless consumer where appropriate, and capability-owned persistence and outbox.

## GUI, configuration and security

**Proposed GUI:** optional Invoice dashboard reached through host-owned sidebar/navigation; tiles for draft/approval, pending remote confirmation, issued, received supplier bills, overdue, disputes, credits and reconciliation. List with tenant/legal-entity filters, authorised search and export; new invoice wizard with source/party lookup and draft totals; approval view; immutable issued preview with versions/number/provenance; correction/credit flow; supplier-bill upload/review and duplicate warnings; delivery and payment-allocation timeline; provider authority/cut-over/number-series controls for privileged operators. Expose unknown versus confirmed external issue prominently and disable potentially duplicative reissue. Headless mode must provide equivalent public business functions.

Use public Invoice contract, no private database access. Host composes routes, permission-filtered menus, generic UI, Theme Manager tokens and localisation; no second presentation-owned state. WCAG 2.2 AA, responsive, keyboard and screen-reader support, locale-correct decimal/currency/date display without altering canonical amounts; redaction/secure document delivery; no client-only authorisation. Financial and counterparty PII is purpose-limited, tenant-isolated, retained per applicable legal evidence and Privacy constraints, with access/export/audit controls and legal holds. OWASP ASVS 5 L2 baseline, L3 where required by risk; injection, invoice fraud, malicious attachments, forged supplier instructions, SSRF through external URLs, replay, duplicate numbers, compromised connectors and race conditions require explicit threat controls. No assertion of tax, invoice or electronic-invoicing regulatory compliance without jurisdiction-specific qualification.

## Conceptual acceptance — inputs → expected behaviour → output → owner

| Scenario / inputs | Behaviour → observable result | Owner |
|---|---|---|
| Approved standalone invoice with valid legal parties/policy | Validated issue, one number and immutable issued snapshot | Invoice |
| Billing finalised batch replayed twice | One invoice per approved idempotent intent, stable acknowledgement to Billing | Invoice; Billing retains charge |
| Issue requested without server access / wrong tenant | Denied without sensitive document disclosure or state change | Authorisation decision + Invoice enforcement |
| Expired seller/tax evidence or contradictory total | Hold/reject with field-specific safe error; no issue | Source owner + Invoice |
| External provider timeout after request | Unknown/reconcile, never claim failed or issue native duplicate | Integrations transport; Invoice status |
| Provider confirms issue after restart | Map exact remote identity to one source intent, persist provenance and emit committed event | Invoice |
| Valid credit request for issued invoice | Preserve original, link separate authorised corrective document, publish Accounting evidence | Invoice |
| Payment provider capture subsequently reversed | Invoice's derived allocation changes with provenance; no provider refund or journal invented | Payment Gateway/Accounting source, Invoice projection |
| Cross-border supplier PDF with duplicate number | Quarantine/flag scoped duplicate and preserve supplier evidence; no assumed bill approval | Invoice |
| Historical invoice party later updated | Issued snapshot unchanged; authorised current contact view may differ | Party source + Invoice snapshot |
| Client tries to erase legally retained issued invoice | Honor applicable legal hold/retention; expose restricted rights workflow | Legal Compliance + Invoice |
| Unsupported mandated e-invoice format or provider issue method | Explicit unsupported/held, not forged “issued” | Invoice |
| Provider cut-over with unresolved remote issues | Block/hold authority transfer until reconciled under approved process | Invoice + Integrations |

## Decision discipline, outstanding work and sign-off

- **Established:** governing separate ownership, headless and public contract, server authorisation, capability-owned stores/outbox, acyclic dependencies, provider neutrality, security/accessibility, ADR-0017/0018 policy/governance; governing catalogue lists Invoice as Domain candidate.
- **Owner-approved relationship:** BIL-01–BIL-06 in Billing (15 November 2026), including charge handoff versus actual issue; preserve without reopening.
- **INV-01 — APPROVED / CLOSED (18 November 2026):** Invoice owns inbound supplier-bill receipt, document capture, validation, duplicate detection, verification, disputes and document lifecycle alongside outgoing invoices. Procurement/Order/Warehouse supply purchase and receipt evidence where relevant; Accounting independently owns payable recognition/postings and Payment Gateway owns payment execution. Receiving a bill does not authorise payment or mean its claim is accepted.
- **INV-02 — APPROVED / CLOSED (18 November 2026):** Configurable jurisdiction-aware, legal-issuer/document-type scoped unique numbering series allocated atomically; preserve reservations, gaps, history and immutable issued snapshots. Credit/debit/corrective documents link explicitly to originals and are issued as separately identified documents where required. Exact series rules, VAT/e-invoicing applicability and effective-date conformance remain jurisdictional-verification work, not a reopened conceptual decision.
- **INV-03 — APPROVED / CLOSED (18 November 2026):** Invoice owns issued document amount and document status; its paid/part-paid/outstanding presentation is a provenance-tagged, freshness-qualified derivation of verified payment/allocation evidence. Accounting alone owns authoritative receivables/payables, financial postings, balances and reconciliation; Payment Gateway owns execution/capture/refund evidence. Missing or contradictory allocations must show unknown/reconciliation-required rather than invent a precise balance.
- **INV-04 — APPROVED / CLOSED (18 November 2026):** One effective authoritative issuer per legal entity/document scope/time period, either Invoice native or selected external provider reached through Integrations. No simultaneous competing issue authority and no silent local fallback on provider failure or uncertain outcome. Migration/cut-over requires approval, stable remote identifiers, in-flight request and invoice-number reconciliation, historical portability and explicit authority epochs; provider-specific adapter capability/evidence remains technical work.
- **INV-05 — APPROVED / CLOSED (18 November 2026):** Invoice consumes authoritative business customer/supplier/legal-party and verified contact/tax references from the appropriate shared business-party owner, including counterparties with no platform Identity. Identity linkage is optional and verified; Invoice snapshots legally relevant party facts on issue/receipt and never silently changes historical documents when source contacts change. Whether the shared business-party responsibility merits a separate capability remains an adjacent classification/contract investigation, not an Invoice ownership alternative.
- **INV-06 — APPROVED / CLOSED (18 November 2026):** Invoice owns its business draft, approval, issue, numbering and correction lifecycles and canonical financial/document content. Reuse Template Engine, Content Editor, Export and Storage through documented public contracts for layouts, editing controls, formats and bytes. Publisher reuse is optional only for non-authoritative generic mechanics where compatible; it must never become a second issuer/document authority or a mandatory dependency.
- **Technical investigation:** Verify real `nuxt-layers/invoice` repository/CONTRACT availability; governing jurisdictional electronic invoice/credit regimes; connector capability/read-back; exact failure codes, durable numbering and idempotency; schema ownership and retention mechanisms. These are not owner approvals.
- **Implementation alignment:** later root `CONTRACT.md`, capability metadata/exports, provider and host ports, threat model, operational runbooks and migrations. None is asserted available.
- **Acceptance evidence:** independent contract, security, race/idempotency, provider timeout/cut-over, rendering/localisation, minimal host ≤50 lines and application scenarios, to be executed by CI/user rather than this conceptual review.
- **Sign-off:** The owner subsequently approved the Invoice conceptual design to the extent documented in this record on 18 November 2026. This approval is architectural direction, not resolution of the six specifically open implementation/policy choices, published-runtime CONTRACT.md acceptance, governing adoption or merge permission.

---

## Preserved earlier conceptual and reciprocal evidence

## Review notes — invoice construction and authoritative provider mode (14 November 2026)

**Provisional conceptual notes only; not a completed Invoice specification.**

- Invoice is the **tool and business record** for construction, calculation validation, numbering, issuing, rendering, delivery, status and correction/credit-note lifecycle. It is more than a PDF; a final issued invoice must preserve the approved financial facts and provenance.
- Publisher may provide suitable document lifecycle/publication mechanics and Content Editor may provide editing/presentation; Template Engine may render from approved data. None automatically owns Invoice's statutory/business identity, amounts or adjustment rules.
- **Tenant configuration:** native Invoice when no approved external invoice authority is selected; connected Invoice through Integrations when an external provider is the approved authority for the scope. Connected mode cannot create duplicate invoice numbers or claim locally issued authority at the same time.
- Invoice and Accounting may choose different providers where supported, but must reconcile issued bills, corrections, settlements and financial postings. An external provider outage does not silently switch invoicing to native issue.
- **Order relationship:** sales or purchase order may supply terms and source evidence, but invoices may be issued for services or other legitimate charges without an Order.
- **Counterparties:** invoices snapshot needed recipient, supplier/customer and tax/address data at issue time rather than depending entirely on a mutable Business Contact or Profile.
- **Open:** who owns supplier bill ingestion, credit notes, cross-border requirements, numbering sequences, financial amounts and transfer of authority when switching provider?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Issuance, document construction and corrections; provider authority may be native or externally connected, independently from Accounting's ledger choice.
- **Related capability notes:** [order](../order/capability-record.md), [accounting](../accounting/capability-record.md), [billing](../billing/capability-record.md), [integrations](../integrations/capability-record.md), [product](../product/capability-record.md).
- **Open architectural questions:** Supplier-bill intake, statutory issue/numbering rules, party snapshots and cross-provider reconciliation.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

## Cross-capability note — Billing charge-to-document handoff (15 November 2026)

**Agreed conceptual relationship: Billing BIL-01–BIL-06 approved on 15 November 2026; Invoice implementation remains unverified.** [Billing](../billing/capability-record.md#idealised-public-outbound-contract) supplies versioned, finalised charge batches, attributed commercial calculations and approved adjustment/credit requests. Invoice independently validates, constructs, numbers, issues, records and corrects formal invoice documents; it supplies authoritative issue/rejection/credit-document status and references. A charge finalisation or handoff request must never imply a legal invoice has been issued, and replay must not duplicate issuance. Supplier invoice intake is provisionally Invoice-owned; Billing may assess commercial obligations only. See approved BIL-01, BIL-03 and BIL-04. Invoice's alphabetical review is still pending.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Own issued invoice and correction states for host-platform subscriptions and tenant business transactions in separately authorised scopes; never deduce legal bill-to party from tenant parentage alone.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.

## Extended conceptual review — contract, interoperability, GUI and reuse (18 November 2026)

**Owner direction:** On 18 November 2026 the owner approved the prior recommendations as conceptual direction and requested deeper explanation. This does **not** mark INV-01–INV-06 individually resolved or an unverified `CONTRACT.md` as published. The contractual surfaces below are **idealised proposals** until specified and independently accepted by an actual Invoice implementation.

### Plain-English issues and public-contract commitments

An invoice is a uniquely identifiable *legal and commercial document*, not the same as the charge that caused it, a rendered PDF, an accounting journal, a payment request or money actually received. Issuing, transmitting, acknowledging delivery, receiving a supplier bill, approving, posting, paying and correcting are distinct states and often distinct owners. Protect immutable issued content; maintain source revision, legal-party and tax facts as-at issue; use exact decimals and explicit rounding and currency policies. Native mode must be independently useful. External issue needs a single authority for each entity/document-scope/period; a timeout cannot justify reissue through another provider. Invalid supplier invoices, disputed facts, numbering collision, authorisation loss and missing required legal obligations must fail safe.

**Input contract families:** (1) authorised actor plus operation and document revision; (2) versioned commercial/charge source (optional Order, approved Billing batch or independent legitimate charge); (3) legally attributable issuer/recipient, contact and relevant tax evidence; (4) approval, effective rules, legal/privacy constraints, locale and clock semantics; (5) incoming supplier document/original artefact; (6) external provider capability/read-back evidence; (7) independently confirmed payment/allocation and financial evidence; (8) delivery/approval results. Each input carries source authority, permitted scope, provenance, applicable version, absence/staleness/contradiction semantics and explicit idempotency for mutations.

**Output contract families:** (1) accepted/pending/rejected/unknown versus **confirmed** issued/received result; (2) immutable number, legal-party and financial snapshot plus correction lineage; (3) authorised queries, revision/history and redacted document access; (4) Billing issue/credit acknowledgements; (5) Accounting posting-source references without claiming posting; (6) derived allocation/outstanding state with freshness and uncertainty; (7) delivery and provider-reconciliation status; (8) durable versioned Invoice-owned events and scoped report/export facts. All protected surfaces are separately authorised; receiving an event is not authorisation.

### Reciprocal contract with Logging, Audit and Reporting

| Partner / nature | Invoice publishes to partner (partner inbound) | Partner sends to Invoice / supplies to consumers | Owner and critical guarantee |
|---|---|---|---|
| **Logging** — optional operational diagnostics | Typed, bounded, sanitised errors and timings for numbering conflicts, validation, retries, delivery/connector timeouts, reconciliation, outbox backlog; opaque correlation and operation references | Diagnostic sink outcome, correlation/health/retention/sink-failure signals (not domain facts); ops access to restricted diagnostics | Logging owns technical records and sinks. Never log full invoices, tax/bank/contact details, payment secrets or unfiltered supplier uploads. Log success/failure **cannot** prove issue or substitute for Audit |
| **Audit** — accountable evidence | Risk-classified committed invoice issue/credit/void/correction, approval/denial, authority cut-over, high-risk access/export, dispute resolution, retention override and provider reconciliation events with actor/decision scope, source sequence/revision, outcome and evidence references; protected producer provenance | Accepted/pending/rejected/uncertain evidence receipt, integrity/coverage gap/review notices and authorised evidence-query/export references; no automatic change to Invoice's business state | Invoice owns document and outbox, Audit owns evidential intake, custody and verification. No claim of exactly-once delivery or complete coverage without source-side reconciliation; no bulk raw logging as Audit evidence |
| **Reporting** — optional analytical consumer | Authorised tenant/legal-entity/party-scoped invoice and credit summaries, issue/delivery/receipts, ageing inputs, disputed/partially allocated figures, currency/tax category, provider backlog, as-issued/as-corrected revisions, source event checkpoints and completeness | Report definitions/results, scoped cross-source comparisons, execution/freshness/completeness/lineage, safe report/export links; analytics cannot instruct issuance | Reporting owns derived reporting only; Accounting owns ledger/recognised revenue and payable/receivable balances. Reports must label unmatched sources, partial periods, unknown provider states and access-scoped omissions; no direct Invoice table access |

**Critical interactions:** Invoice can issue without Logging or Reporting. Mandatory selected security/financial evidence must remain captureable through an Invoice-owned durable outbox even if Audit transport is unavailable; if durable evidential guarantees cannot be met, affected high-risk actions may be held according to approved risk policy. Reporting re-authorises source reads and its generated exports; revocation and cross-tenant/small-cohort inference must be handled even for cached reports. Logging, Audit and Reporting are separate public contracts, not reciprocal package imports that form cycles.

**Specialist acceptance:** log sink outage while issuing; mandatory Audit receipt delayed/replayed, failed or incomplete; duplicate emitted credit event; invoice issued while a report refresh is down; report reconciliation across Billing/Invoice/Accounting/Payment Gateway with unposted invoices, part payments, credit reversals, stale external confirmation and multi-currency boundaries; report export denied after authority revocation; Audit report shows evidential uncertainty rather than mislabelling issue state.

### Established standards and changing legal rules

| Standard or source | What to reuse, not reinvent | Adoption boundary |
|---|---|---|
| **EN 16931** | Structured semantic European electronic-invoice business fields and validation principles | Qualification by country, transaction, supplier/buyer and effective dates |
| **OASIS UBL 2.1**, **UN/CEFACT CII**, **Peppol BIS Billing 3.0** | Standard machine-readable invoice/credit-note formats and network interoperability rules | Peppol BIS is a profile; standards conformance does not itself confer network access or legal issue |
| **ISO 4217**, **ISO 3166**, **UN/ECE unit/code lists** | Currency, country and quantity/unit classification codes | Version and issuer-country constraints must be recorded |
| **ISO 8601**, **Clock**, **ISO 20022** (where payment/remittance flows apply) | Date semantics and payment/remittance references | Business due-date rules remain in Invoice, payment facts with Payment Gateway |
| **HMRC VAT Notices 700, 700/63 and 700/21** | UK invoice content, electronic authenticity/integrity/legibility and recordkeeping | Apply only where relevant; obtain qualified legal treatment and valid effective regulations |
| **UK e-invoicing roadmap (published October 2026)** | Anticipate UK structured VAT e-invoicing from **1 April 2029** as announced, with detail subject to legislation/regulation | Treat as a planned statutory change, not proof that a particular format/provider is already mandatory or sufficient |
| **OWASP ASVS 5 L2**, **WCAG 2.2 AA**, **UK GDPR**, accepted ADR-0012/0016/0017/0018 | Authorisation, evidence, privacy, accessible UI and disciplined ports/host integration | Security baseline and effective legal duties must be validated independently |

Sources checked: [Peppol BIS Billing](https://docs.peppol.eu/poacc/billing/3.0/bis/), [UK VAT Notice 700](https://www.gov.uk/guidance/vat-guide-notice-700), [VAT Notice 700/63](https://www.gov.uk/guidance/electronic-invoicing-notice-70063), [UK e-invoicing roadmap](https://www.gov.uk/government/publications/e-invoicing-implementation-roadmap/roadmap-for-e-invoicing-implementation).

### Commercially permissive OSS candidates — discovery, not dependency approval

| Candidate | Licence / role | Recommendation and qualifications |
|---|---|---|
| [decimal.js](https://github.com/MikeMcl/decimal.js) | **MIT**, exact-arithmetic decimal library | Strong candidate for amounts and controlled rounding, with explicit canonical serialisation and policy-owned precision |
| [Zod](https://github.com/colinhacks/zod) | **MIT**, TypeScript runtime schema validation | Useful for commands, forms and provider boundary data; avoid duplicate business rule engines |
| [Ajv](https://github.com/ajv-validator/ajv) | **MIT**, standards-based JSON Schema validation | Useful when machine-readable public schemas and interoperable payload validation are needed; prefer a coherent validation strategy |
| [fast-xml-parser](https://github.com/NaturalIntelligence/fast-xml-parser) | **MIT**, XML parse/build | Useful for UBL/XML mechanics, **not** EN 16931/Schematron semantic conformance alone; secure XML processing and size bounds required |
| [KoSIT XML Validator](https://github.com/itplr-kosit/validator) | **Apache-2.0**, independent structured invoice validator | Mature reference/conformance option for applicable German/European rule packs, but Java/runtime and external rule artefacts carry operational/licensing obligations; use as optional adapter, not a required SaaS |
| [pdf-lib](https://github.com/Hopding/pdf-lib) | **MIT**, PDF editing/generation | Potential Export-layer implementation detail; assess maintenance and PDF/A, archival/signing/accessibility requirements before adoption |
| [bwip-js](https://github.com/metafloor/bwip-js) | **MIT**, barcodes/QR representations | Optional payment references/print artefacts, not a payment authority or a mandated invoice feature |
| [Pino](https://github.com/pinojs/pino) | **MIT**, structured Node logging | Prefer reuse in Logging rather than a second Invoice-owned log platform |

All listed *core software* carries a genuine permissive source licence in its checked public material, rather than depending on a proprietary-hosted API. This is **not** a certification of every transitive dependency, trademark, standard ruleset or third-party provider; verify licence notices, maintenance, vulnerability state, current version and dependency tree at implementation selection. Do not adopt a purported all-in-one e-invoice SaaS or a commercial add-on as the authoritative invoicing engine. Prefer small, replaceable format/validation adapters. Existing platform Clock, Export, Template Engine, Logging, Storage, Integrations and infrastructure services should be reused instead of duplicated.

### GUI and host composition — reference application evidence

Read-only reference: [`nuxt-layers-test/application-test-template`](https://github.com/nuxt-layers-test/application-test-template) current `README.md`: host homepage `/`, development dashboard `/admin`, responsive collapsible capability navigation, themed shell/top bar and a `/theme-manager` capability entry. A composed application owns navigation and branding; each capability owns its protected business screens and contracts. [Theme Manager `CONTRACT.md`](https://github.com/nuxt-layers/theme-manager/blob/master/CONTRACT.md) confirms its library/index and editor route model but also documents that its **current** integration remains short of full ADR-0012 composition compliance; do not copy that deficiency.

**Proposed Invoice sidebar entry:** labelled **Invoices** with an optional capability-owned icon, visible only for the caller's authorised scope; host routing can target `/invoice` (illustrative, not prescribed endpoint). Clicking opens the capability dashboard inside the shared host shell, not a new application or navigation layout. The hostname/app owns shell and routes; Invoice screens consume its own public services and Theme Manager tokens. No unauthenticated test fixture is deployable.

| Screen | Purpose / key actions | Audience and controls |
|---|---|---|
| **Invoice dashboard** | Drafts to approve, issue failures/unknown, issued/overdue, received supplier bills, unpaid/part-paid, credits, disputes, reconciliation; counts include cutoff and scope | Authorised finance users, concise role-scoped widgets; drill-down into lists |
| **Sales invoice list / detail** | Search, filter, review issued snapshots, source lineage and delivery/payment timeline, authorised export | Finance and scoped customer/self-service; state and provider uncertainty always distinct |
| **Create / edit draft** | Choose approved charges or standalone sources, legally valid counterparties, lines, totals, currency, tax evidence, preview and submit | Staff with create authority; server validation and protected approvals |
| **Approval and issue queue** | Compare source versions, four-eyes approval where required, authorised issue; prevent duplicate clicks | Approvers/issuers; step-up assurance according to risk |
| **Received supplier invoices** | Ingest, verify, deduplicate, match commercial evidence, dispute/accept for downstream assessment | Payables clerks and approvers, privacy-controlled attachments |
| **Credit / dispute / correction** | Select original issued record, explain adjustment, approve and issue separate linked corrective document | Delegated financial staff; never silently edit issued historical facts |
| **Provider reconciliation** | Pending/unknown remote issue, mismatched numbers/identifiers, read-back and recovery | Privileged finance operators; prevent automatic provider failover |
| **Settings and numbering** | Legal issuer, scoped series, approval policy, allowed document types, template and external authority/cut-over | Approved tenant/legal-entity administrators, not ordinary customers |
| **Reports / export** | Links into Reporting-owned invoice ageing, document counts, exceptions and authorised output | Scoped read access plus separate Reporting export/aggregate controls |

**Navigation proposal:** `Home → Admin/test dashboard → Invoices → Invoice dashboard → list → detail/draft/approval`; the top bar and appearance controls remain from the shared application shell, and the host can hide the entire Invoice UI while using its headless contract. Reporting retains its own screens and merely accepts Invoice references/filters; Invoice does not duplicate a reporting framework. All views meet WCAG 2.2 AA, keyboard focus and screen-reader semantics, responsive/mobile behaviour, i18n and locale-appropriate formatting while storing canonical numbers unchanged.

### Open design decisions and further acceptance

**Follow-up approval (18 November 2026):** the owner explicitly approved all six recommended resolutions **INV-01–INV-06**. Their conceptual decision status is **closed**. The specific jurisdictional rules, provider adapters, adjacent shared business-party owner contract, published runtime interfaces and acceptance remain separate technical/implementation/legal verification work. Additional technical evidence is needed on tax/e-invoice validators, legal record retention, import/export and provider conformance, non-repudiation/receipt semantics and minimal-host composition. A new `CONTRACT.md` must eventually declare concrete function signatures, permissions, error codes, idempotency and failure handling, not claim these conceptual tables are implemented.


## Owner conceptual approval and handover — 18 November 2026

**Decision:** The project owner explicitly approved the `invoice` conceptual design **to this point**, including the expanded explanations, idealised inbound/outbound public contract, named cooperating capability boundaries, reciprocal Logging/Audit/Reporting integration, standards-based and permissively licensed library selection principles, and optional GUI using the application-test-template sidebar/dashboard approach.

**Approved direction:** Invoice is a Domain candidate and the sole platform-facing owner of issuance/receipt, numbering, original document evidence, corrective documents and its own external-authority reconciliation; it is independently useful in native mode. Billing owns charges, Accounting owns books, Payment Gateway owns payment execution, Integrations owns connectors, Audit owns evidential custody, Logging owns diagnostics and Reporting owns derived reports. Invoice uses source contracts rather than private storage; changes require authorised commands, idempotent issue semantics, immutable issued snapshots, tenant/legal-entity isolation, recoverable owned outbox and explicit provider uncertainty. Headless operation and optional themed, accessible screens are required conceptual options. Standards and open-source candidates are **evaluation choices**, not mandatory package dependencies or proof of legal compliance.

**Conceptual decisions now closed:** INV-01–INV-06 were subsequently expressly approved with the recommended standards-based resolutions on 18 November 2026. Retain only separate follow-up investigations for national/international fiscal and electronic-invoice conformance, provider-specific interoperability/cut-over evidence, definitive shared business-party public contract and classification, concrete published Invoice `CONTRACT.md`, and independent implementation/security/acceptance evidence. These do not reopen INV-01–06. The root Invoice contract and deployed capability have not been independently established.

**Git and adoption boundary:** This approval authorises documentation of the design but **not a merge**. Keep all changes in [draft PR #78](https://github.com/nuxt-layers/architecture-blueprint-review/pull/78). Reconcile against latest governing and blueprint `master` and overlapping concurrent PRs; complete the mandatory technical and architectural consistency review and obtain a separate explicit merge instruction before merging.


## Decision closure — INV-01 through INV-06 (owner approval, 18 November 2026)

**Decision status:** All six conceptual decision IDs **APPROVED / CLOSED** by explicit owner instruction, adopting the six standards-based recommendations recorded above. Do not reopen these conceptual ownership choices without a new, explicit architectural change decision. The closing record does not imply legal conformance, implementation readiness, or permission to merge.

| Decision | Approved resolution | Separate remaining evidence / follow-up |
|---|---|---|
| INV-01 | Invoice owns inbound supplier invoices as well as outgoing invoices; receipt, commercial acceptance, ledger posting and payment remain distinct | Detailed incoming validation/matching rules and supplier fraud threat model |
| INV-02 | Atomic, unique, jurisdiction/issuer/doc-type scoped series; immutable documents and separately linked credits/corrections | Qualified local VAT/e-invoicing, numbering/gap and retention conformity per effective jurisdiction |
| INV-03 | Invoice owns document status and a clearly derived settlement view; Accounting owns authoritative books and balances; Payment Gateway executes | Public allocation evidence/recency contract and cross-provider reconciliation acceptance |
| INV-04 | One native or external issuer authority per explicit scope/effective epoch; governed migration, no silent fallback | Provider support matrix, unknown-outcome/read-back, mapping, cut-over and import/export acceptance |
| INV-05 | Shared authoritative business-party source including nonmember counterparties; issue-time immutable Invoice party snapshot | Adjacent business-party owner/classification and public contract verification |
| INV-06 | Reuse generic rendering/editor/export/storage tools, with Invoice retaining legal document authority and business lifecycle | Adapter/format compatibility, archival/accessibility and minimal-host composition evidence |

**Separated follow-up workstreams:**

1. **Jurisdictional and standards verification:** qualified jurisdiction/effective-date legal analysis, EN 16931/UBL/CII/Peppol and national profiles, statutory invoice identifiers, tax/credit content, electronic delivery/signature/retention requirements.
2. **Published contract specification:** draft and later validate actual `invoice/CONTRACT.md` with typed commands/queries/events, error codes, IAM rights, authority scopes, provider protocols, cross-capability data contracts and explicit missing/uncertain outcomes; reconcile the shared business-party source with its future owning contract.
3. **Implementation and independent acceptance:** provider conformance and migration/recovery, transactional numbering/idempotency/outbox, canonical document integrity, privacy/audit/financial checks, GUI/headless/minimal-host compatibility, independent CI and operational evidence. Tests are performed by the user/CI, not this review.

**PR gate:** preserve all changes in draft PR #78. Reconcile current governing/blueprint master and other active reviews; run the mandatory pre-merge architectural/technical status review and obtain explicit approval before any protected-branch squash merge.
