# Capability Record — Accounting

**Status:** Proposed conceptual domain capability; not an implementation specification or evidence of an existing package.  
**Review sequence:** First directory alphabetically under `docs/capabilities/`, reviewed 14 November 2026.  
**Governing authority:** `nuxt-layers/architecture-rules/docs/catalogue.md`, consulted on `master` (governing definition: Accounting owns ledger, journal, periods and reconciliations, not originating sales or warehouse transactions).  
**Related blueprint evidence:** [Multi-channel commerce and warehouse review](../../../reviews/multichannel-commerce-warehouse.md), especially the separate financial lifecycles and outstanding CW-10. The `nuxt-layers/integrations` repository exists, but its root `CONTRACT.md` was not retrievable in this inspection, so the connector contract and implementation remain **unverified**.  
**Evidence boundary:** An inspection of the `nuxt-layers` repository list found **no `nuxt-layers/accounting` repository**. A direct repository lookup returned 404; consequently no Accounting `CONTRACT.md`, package exports, manifests, tests or implementation were inspected. This is a finding about the checked repository, not a claim that no accounting solution or design exists elsewhere.

## Capability Name

**Accounting** — proposed identifier `accounting`. The public package name and interfaces are **not approved**.

## Status

- **Architecture:** Domain candidate in the governing catalogue.
- **Conceptual review:** Draft for discussion; no decision to create a capability repository.
- **Availability / Installed / Configured / Operational / Enabled:** **Not established**; no corresponding repository or application-specific evidence was found.
- **Authorised:** Not a global capability status. Any future accounting action would require a decision for the specific actor, group, resource and operation.
- **Implemented / completed / in progress:** **Not verifiable from a public Accounting contract**, because no `nuxt-layers/accounting` repository was found.

Do not treat a catalogue entry as completed software or a merged design review as implementation evidence.

## Purpose

Record and maintain a trustworthy financial account of an organisation's economic transactions over time: **what value was recognised, where it was allocated, in which accounting period, and how balances can be explained and reconciled**.

Accounting provides a stable financial capability regardless of which accounting system is authoritative. It must support both its own accounting books **and** an authorised externally authoritative accounting package connected through Integrations. This is a provider-selection and authority arrangement, not two mutually exclusive products. Accounting remains the platform-facing financial boundary and is distinct from the commercial and operational activity that generates underlying facts.

## Classification

**Domain candidate.** It has a credible independent business lifecycle, distinct from Order, Billing, Invoice, Payment Gateway and Inventory. Whether it becomes a standalone capability repository remains subject to the governing capability-start criteria and this record's open questions.

## Conceptual ownership

Accounting would be responsible for:

1. **Books and accounting entities** — a clearly identified set of books, reporting context and financial period structure. Establish explicitly how an accounting entity relates to legal entities and Identity-owned groups; they need not be identical.
2. **Chart of accounts** — account definitions, classifications, lifecycle and permitted use.
3. **Journal entries or provider mappings** — dated, attributable financial postings and a balancing invariant for locally authoritative books; when an external system is authoritative, validated mappings, source references and reconciliation evidence without claiming local postings are the authoritative ledger.
4. **Posting and correction lifecycle** — draft/validated/posted/voided or reversed as appropriate, preserving the historical record rather than silently rewriting posted facts.
5. **Accounting periods** — boundaries, opening/closing, adjustment restrictions and close controls.
6. **Reconciliation** — explaining differences between the selected authoritative books, local projections/pending actions and source records or statements, including documented resolution.
7. **Financial balances and reports** — trial balances and other authorised financial views derived from owned journals, with traceable source and period context.
8. **Financial control evidence** — approval requirements, posting restrictions, authority-mode changes and accountable actions, without substituting for a platform-wide Audit capability.
9. **Authority selection and continuity** — determine the accounting authority for each approved accounting context, use local books when no external accounting system is configured, and delegate accounting actions to a configured authoritative external system through Integrations. Do not run competing authoritative ledgers.

These are **conceptual candidate responsibilities**, not assertions about implemented schemas or API methods.

## Exclusions and boundaries

| Other responsibility | Owning concept | Accounting relationship |
|---|---|---|
| Sales commitments, quantities and order status | **Order** | Records financial consequences based on validated source facts; does not re-own orders |
| Charges and billing periods | **Billing** | Uses accepted charge/accounting facts as appropriate; does not determine the commercial charge lifecycle |
| Legally issued invoices, credit notes and their lifecycle | **Invoice** | Records financial postings attributable to issued documents; does not own invoice numbering/issuance |
| Provider payment authorisation, capture and refund operations | **Payment Gateway** | Records settlement consequences from verified payment/financial evidence; does not initiate payment-provider actions |
| Stock movements and reservation quantities | **Inventory** | May value stock under approved accounting policy; Inventory remains stock source of truth |
| Physical warehouse work | **Warehouse** | Does not own picking, receiving or dispatch operations |
| Prices, offers and promotions | **Pricing** | Does not compute commercial quotations |
| Legal-entity registration, statutory compliance rules and taxation policy | Applicable domain and **Legal Compliance** | Accounting applies approved relevant financial treatments, not an invented universal legal rule |
| Identity groups and permissions | **Identity / Authorisation** | Books must have explicit accountable ownership and server-authorised operations, with no implicit group membership grants |
| Infrastructure logs and generic audit infrastructure | **Logging / Audit**, if applicable | Financial journals are business records, not substitutes for unrelated security/audit logs |

Do not create a second financial source of truth in Integrations, Reporting, Order or Payment Gateway.

## Conceptual lifecycle

**Accounting books and periods:** establish accounting context and approved authority → accept/validate source evidence → prepare or delegate the authorised action → approve where required → post locally or obtain verified provider confirmation → reconcile → adjust/reverse through the authoritative system → close period → preserve/export financial evidence under applicable retention rules.

A finalised journal should not be silently edited or deleted. Corrections are explicit and auditable. This applies both to locally owned financial journals and the platform's records of externally confirmed actions. Whether all locally posted journals require double entry, how multiple currencies are represented, and what constitutes a legally closed period require separate accounting-policy decisions.

### Accounting authority modes

| State | Authority for accounting actions | Expected behaviour |
|---|---|---|
| **Internal accounting** | Accounting's own approved books | Default when **no authoritative external accounting connection is configured** for the accounting context. Accounting validates, posts, corrects and reconciles under its own policies. |
| **External accounting** | Selected external accounting package, such as Xero or QuickBooks | A properly configured, authorised connector through **Integrations** routes supported accounting actions to that system; local state is a mapped projection, evidence, or pending action, **not a competing authoritative ledger**. |
| **External configured but unavailable** | External system **retains authority** | Do not automatically post to local books. Mark requests pending, queue only if designed and safe, or refuse them. Expose failures and reconcile on recovery. |
| **Authority changing** | Explicitly governed transition | Activation, replacement and removal require an authorised cut-over, opening balances, mapping, outstanding-work reconciliation and provenance; an absent connector after previously being authoritative does not automatically make local books primary. |

**Authority is scoped** to an approved accounting entity/book and context, not inferred globally from the mere presence of an Integrations package. The platform must not permit two simultaneous writers to claim the same authoritative books. The public Accounting contract, if developed, should provide consistent business semantics in both modes without exposing Xero/QuickBooks SDK types or treating Integrations as the owner of financial records.

## Dependencies

**No package-level mandatory `requires` relationships are approved by this record.**

Conceptual obligations for any future implementation:

- Verify identity, tenancy/group context and **server-side Authorisation** for protected accounting operations through published composition contracts.
- Maintain trustworthy time/period semantics, potentially using **Clock** through its public contract; do not invent a direct package dependency.
- Receive verified, idempotently correlated financial source facts from relevant domains through documented public contracts and/or owner-published business events; avoid direct reads from other capabilities' persistence.
- Preserve accounting-owned data through its own persistence contract and schema; host provides infrastructure, never the accounting rules.
- Ensure a legal/accounting-entity mapping is explicitly defined rather than equating Identity group IDs to legal persons or books.

Required versus optional service ports, failure modes, event schemas and dependency DAG edges need design and owner-contract validation before any implementation specification.

## Optional integrations

Subject to independent design: invoicing, billing, payments, sales/orders, stock valuation, banking feeds, external accounting systems, reporting, audit/evidence and export. **Integrations** owns provider-connection configuration, transport and adapter concerns under its eventual verified public contract. A selected Xero, QuickBooks or other provider may be the authoritative accounting system for an approved accounting context; **Accounting** keeps responsibility for the platform-facing accounting semantics, authority selection, validation, reconciliation and protection against dual posting. The provider is not a second platform `accounting` capability, and Integrations must not become the owner of accounting business rules.

## Native Accounting — minimum self-sufficient scope

A **naked Accounting capability** means an organisation can use it **without any third-party accounting connection**. It must be useful, internally consistent and capable of maintaining authoritative books, not just a placeholder API waiting for Xero or QuickBooks.

**Minimum native accounting functions (conceptual):**

| Area | Essential native behaviour | Explicit boundary |
|---|---|---|
| Accounting context and books | Create and administer books for an explicitly identified accounting entity, ownership context and financial basis | Identity groups are access/ownership contexts, not automatically legal entities |
| Chart of accounts | Define account codes, types, active/inactive state, permitted posting and controlled changes | No forced universal chart across jurisdictions or different entities |
| Accounting periods | Define fiscal calendar, open/closed periods and governed adjustments | Clock handles time semantics; accounting policy decides eligible periods |
| Journals and double entry | Draft, validate, authorise and post balanced entries with debit/credit sides, account and currency context, source reference, date, identity and provenance | No silent mutation/deletion of posted entries; reversal and correcting entries are distinct facts |
| Balances | Calculate account balances, opening/closing balances and trial balance with a reliable as-of date/period | No unsupported inference that balances equal cleared bank funds |
| Bank and control reconciliation | Import or enter verified statement lines, match financial transactions, track unmatched items and resolve discrepancies | Accounting does not become a payment processor or bank account credential store |
| Corrections and auditability | Controlled reversal, reclassification, adjustment, posting-history evidence, period lock and authorised access | Other capability Audit/Legal Compliance duties remain independent |
| Financial outputs | General ledger, journal listing, trial balance and simple period summaries with traceable lines | Full tax returns, payroll, statutory filings and advanced consolidation are not assumed in the initial scope |
| Data portability | Export a complete supported accounting dataset with schema/semantics and provenance; validate a proposed import before authority transfer | Import is not automatic reconciliation or approval of imported balances |

The native minimum should cover a full small-organisation ledger lifecycle: opening balances → balanced journals → corrections → reconciliation → period close → verifiable reports and export. External providers may expose richer functions, but **absence of an external connector must never leave this native cycle incomplete**.

**Financial correctness principles:** postings must balance within the applicable ledger currency/basis; amounts must have defined decimal precision, currency and rounding policy (no floating-point money); distinguish transaction, posting and effective dates; identify accounting entity and period; prevent double posting on repeated requests; record source document, correction and user/system provenance; apply authorisation, separation of duties and lawful retention. Exchange rates, tax treatment and jurisdictional rules require separately governed policy and cannot be guessed.

## Conceptual public Accounting interfaces

These are **responsibility-level contract surfaces**, not TypeScript names, HTTP routes, SDK calls, an approved `CONTRACT.md` or a new manifest. They should remain recognisable whether the selected authority is native or external.

| Contract surface | Typical operations / information | Who interprets the result |
|---|---|---|
| **Accounting authority** | Identify the approved accounting context/book, authority mode, supported provider, activated version, restrictions, health and cut-over state | Accounting; operating context must be resolved before every financial mutation |
| **Books and accounts** | Create/read book, list/validate chart, propose/change account, identify currencies and fiscal basis | Native books or selected authoritative provider through adapter |
| **Periods** | List/open/close/reopen under controlled policy, determine permitted posting period | Accounting-authorised business action, not Scheduler-owned state |
| **Journal posting** | Propose, validate, approve, post, reverse, adjust, retrieve status and original/compensating references | Selected authority; distinguish accepted request from confirmed posting |
| **Balances and financial reporting** | Get trial balance, account history and period financial views with source, freshness and reconciliation status | Selected authority, optionally cached/read-projected with explicit provenance |
| **Reconciliation** | Present statement/source records, match, explain variance, approve adjustment, record result | Accounting with authorised evidence from external statement/finance owners |
| **Import/export and migration** | Describe portable dataset, validate mappings, preview import, verify reconciliation, commit cut-over, report exceptions | Accounting controls financial meaning; Integrations supplies external transport |
| **Provider capabilities and sync health** | Determine whether a provider supports a requested operation, permissions/scopes, confirmation/read-back, retry/idempotency and last verified sync | Adapter declares provider constraints; Accounting blocks or safely limits unsupported actions |
| **Financial event exchange** | Ingest owner-validated source facts; publish accounting-owned facts such as journal posted, period closed or reconciliation completed | Source owners keep original events; MQ transports events without becoming the ledger |

At a minimum, mutation requests need **accounting context, actor/authority context, source reference, correlation and idempotency key, requested business action, and expected version/concurrency evidence where relevant**. Responses must differentiate `accepted/pending`, `confirmed`, `rejected`, `unavailable`, `conflict`, and `requires reconciliation`; never report a posting as successful merely because an API request was queued or acknowledged.

**Consumer separation:** Order, Invoice, Billing and Payments use published financial operations or emit source facts for Accounting to interpret. They must not contain Xero/QuickBooks-specific branches or write Accounting's tables directly. Accounting owns its conceptual port; Integrations and optional provider adapters implement the transport-facing side under a verified, provider-neutral contract.

### Provider differences must be explicit

Do not assume every provider implements journals, periods, contacts, accounts, reporting, currencies, corrections or bank reconciliation with identical semantics. A connector must expose a **supported-operation and constraint description**, including account scope, API and permission limits, posting model, remote read-back, rate limits and non-reversible operations.

The Accounting boundary may offer a common **portable core**, but must not invent equivalent behaviour for a provider that lacks it. An unsupported operation is refused, explicitly routed to an authorised provider-specific workflow, or supported only by a separately justified local *non-authoritative* aid; never silently posted into local books while external authority is active.

### Idealised input/output contract for consumers (conceptual)

This describes **information and obligations across published capability boundaries**, not a transport protocol, TypeScript signature, route, event schema or commitment that every optional provider supports every operation. It refines — rather than replaces — the nine public contract surfaces above. The same business-facing semantics apply whether native Accounting or an approved external provider is authoritative.

#### Inbound source facts and requested actions

| Originating owner / source | Information presented to Accounting | Permitted Accounting interpretation and responsibility |
|---|---|---|
| **Order** | Approved sales and purchasing commitments, terms, amendments, cancellations, performance/fulfilment references | Evaluate whether recognition, commitment disclosure or a later financial action is warranted; **an order alone does not automatically create revenue or an expense** |
| **Invoice / Billing** | Issued invoices, supplier bills, credit notes, charges, adjustments, tax-relevant facts and document revisions | Validate sources and relevant policy; recognise and maintain receivables, payables, tax control entries and adjustments without taking ownership of the issued documents |
| **Inventory / manufacturing owner** | Purchases, receipts, consumption, production, WIP conversion, quantities, corrections, losses and verifiable cost evidence | Recognise permitted stock values, WIP, finished goods, cost of goods sold and write-downs without becoming the stock-movement ledger |
| **Asset** | Asset acquisition, commissioning, improvements, transfers, rights/custody, impairment and disposal evidence | Classify capital versus expense treatment; maintain carrying amount, depreciation and disposal postings without owning maintenance/custody |
| **Warehouse / Logistics** | Handling, storage usage, inbound freight, transport, fulfilment, returns, carrier charges, estimates and actual bills | Evaluate landed cost versus production overhead, distribution/operating expense, accrual, payable or recoverable customer charge as allowed by applicable policy |
| **Employment / approved Payroll provider** | Authorised payroll results, employment-cost liabilities, contractor costs, paid/unpaid status and qualifying labour-allocation evidence | Recognise wages, employer liabilities, contractor payables and eligible WIP/production costs; never compute employment rights or expose private payroll records through generic accounting feeds |
| **Payment Gateway / bank feed** | Payment initiation references, settlement/fees/refunds, bank statement and cleared-item evidence | Apply only confirmed financial consequences and reconcile cash, debtor/creditor balances, merchant fees and exceptions; a provider acknowledgement is not necessarily a bank settlement |
| **Business contacts / counterpart records** | Approved external counterparty references and relevant billing/settlement identifiers | Resolve the correct debtor, creditor or financing account; do not own the person, organisation profile or an Identity membership |
| **Configuration / Legal Compliance** | Permitted settings, framework selections, applicable legal restrictions, obligations, effective dates and validation outcomes | Resolve the approved accounting context, enforce mandatory constraints and apply versioned financial rules; never infer that a chosen setting proves legal validity |
| **Integrations / external accounting authority** | Verified external postings, account mappings, statements, provider capabilities, confirmation/read-back, migration and regulatory receipts | Reconcile authoritative financial status and exceptions, retaining provenance; provider connectivity must not create a second authoritative local ledger |
| **Authorised finance actor** | Journal/adjustment proposal, approval, reversal, account/period management, reconciliation or reporting request | Validate actor and separation-of-duties requirements, evidence and period rules before executing through the approved authority |

**Input distinction:** (1) an immutable or versioned *source fact* reported by an owning domain, (2) an authorised *command* requesting a financial action, and (3) *external evidence* requiring verification are different classes of input. The Accounting boundary decides their financial meaning; source owners do not pre-empt that decision through raw journal/table writes. No consumer may directly post into another capability's private ledger or override the configured accounting authority.

#### Outbound commands, queries, results and notifications

| Contract output or service | Authorised consumers | Ownership and information guarantees |
|---|---|---|
| **Financial operation result** | Initiating business capability and approved workflow | Stable operation/source reference, requested versus confirmed state, applied accounting context, journal or remote authoritative reference where confirmed, rejection/variance explanation and retry/reconciliation guidance |
| **Accounts and period status** | Approved finance staff, Invoice/Billing and other posting clients | Authoritative chart/period availability, legal posting restrictions, approval requirements and cut-over status; never imply that queued work is posted |
| **Receivables and payables views** | Authorised Invoice, Order, Billing, counterparty-facing services and finance staff | Due/outstanding balance, credits, matching settlement status, ageing or dispute flags at the permitted disclosure level; separate *invoice issued* from *financially settled* |
| **Cash/bank reconciliation** | Authorised finance administration, payment/banking owners | Authoritative cash ledger status, matched/unmatched references, bank-feed freshness, exceptions and explicit evidence of authorised adjustment |
| **Inventory carrying value / cost of sales** | Approved Inventory, Product, Warehouse and Reporting consumers | Financial values, cost allocation, book/period/currency/framework and reconciliation status; **not** a replacement for Inventory quantities or operational cost source facts |
| **Asset carrying value / depreciation** | Approved Asset and Reporting consumers | Capitalisation status, depreciation/impairment and disposal financial outcomes, with the underlying asset reference; not an operational asset state update |
| **Tax / regulatory outputs** | Approved tax reporting functions, Integrations and finance officers | Validated authoritative tax-control figures, return models, statement snapshot, reconciliation evidence, approval and government filing state; a transmitted request is not a confirmed accepted filing |
| **Financial statements and management views** | Authorised Reporting, Publisher or analytical consumers | Trial balance, profit and loss, statement of financial position, cash-flow and dimensional views with scope, framework, period, precision, source authority and completeness status |
| **Authority and provider capability view** | Host composition, authorised financial consumers | Native/external authority, supported operations, provider restrictions, connection/cut-over state, freshness and confirmed reconciliation; avoid leaking provider secrets |
| **Accounting-owned events** | Authorised subscribers, delivered via Message Queue where available | Facts such as `posting.confirmed`, `posting.reversed`, `period.closed`, `reconciliation.completed`, `authority.changed` or `return.status-changed`; labels are **illustrative**, not an approved event naming convention |

**No generalised balance leakage:** A service permitted to read *its invoice's payment status* does not thereby gain access to the customer's other invoices, bank accounts, entire ledger, unrelated legal entities or payroll. Queries require explicit tenant/entity scope, subject, action and field-level disclosure decision. Financial events should contain minimum necessary references and states, not full invoices, bank details, credentials or payroll personal data.

#### Shared financial context and provenance

A cross-boundary operation resolves the following **conceptual information**, only where applicable; this is **not one mandatory monolithic request object**:

| Dimension | Minimum conceptual requirement |
|---|---|
| **Accounting destination** | Tenant/control context, authorised accounting entity, book and authority selection; prevent one entity's data from affecting another |
| **Origin and actor** | Originating owner/capability, authenticated actor or approved service principal, authorised action, approval/assurance evidence |
| **Business source** | Stable source type/ID, owning entity, revision, related order/invoice/asset/stock/payment evidence and effective source status |
| **Temporal context** | Business occurrence/effective date, tax date where distinct, requested posting date, accounting period and relevant time-zone/calendar policy |
| **Financial measurement** | Money amounts, currency, exchange-rate source and effective date where relevant; quantity/unit/cost basis, tax and rounding provenance as needed |
| **Policy and compliance** | Applicable framework, tax regime, rule/election versions, legal constraint result and policy effective date with explanation |
| **Integrity and lifecycle** | Source uniqueness, correlation, idempotency, command/confirmation identifier, expected version, original/reversal references and audit trail |
| **Read and confirmation quality** | Native versus remote authority, as-of timestamp, read-back/sync state, completeness, reconciliation/exception status and stale-data disclosure |

The contract must separate **occurred**, **requested**, **accepted for processing**, **posted and verified**, **reversed/adjusted**, and **externally accepted or settled** meanings. Times and currencies may differ between business occurrence, invoice date, tax point, ledger period and bank settlement; they must not be conflated. Financial records and outputs retain sufficient provenance for later explanation and authorised historical reproduction.

#### Three interaction models

1. **Commands:** Authorised intent to create/adjust/reverse recognised entries, manage periods, reconcile or submit a validated return. Commands are validated against the selected accounting authority, current version, effective financial policies, authorisation, period status and provider-supported capabilities. Requests may return `accepted/pending`, `confirmed`, `rejected`, `unavailable`, `conflict`, `unsupported` or `requires reconciliation/review`, with stable identifiers and unambiguous meanings.
2. **Queries:** Read authorised accounting balances, statuses, period rules, statements, tax positions, financial valuations or operation progress. Responses disclose as-of time, entity/book, authority, freshness and whether reconciliation or external read-back remains outstanding. A cached financial read is explicitly marked as a projection, not presented as a confirmed remote balance.
3. **Events:** Publish **confirmed Accounting-owned changes** for authorised downstream reactions. A transport delivery/consumer acknowledgement does not itself establish a new financial posting or regulator acceptance. At-least-once publication requires deduplication/replay-safe consumers, without promising distributed exactly-once effects.

**Cross-domain lifecycle example:** Invoice owns a legally issued sales invoice and publishes the authoritative issue fact. Accounting validates source/version and applicable recognition rules, records or requests the receivable and returns a posting confirmation or pending state. Invoice queries the receivable's settlement status and may receive an Accounting-owned reconciliation event. Payment Gateway owns payment execution; Accounting records and reconciles the financial settlement when sufficient independent evidence exists. Reissued messages or reconnecting an external provider must not duplicate postings or create a contradictory invoice authority.

#### Conceptual contract acceptance scenarios

- **Order versus revenue:** A quotation or order is accepted without fulfilment: Accounting neither invents a sales invoice nor automatically recognises revenue. A later supported performance event can be evaluated separately.
- **Invoice versus balance:** A valid issued invoice creates a receivable where the selected framework requires it. A partial payment reduces the amount due without changing the immutable issued invoice. Only authorised callers can read the result.
- **Stock and landed cost:** Inventory supplies received quantities and procurement references; Logistics supplies qualifying transport evidence. Accounting calculates an approved stock value with explainable allocation and returns a financial value without writing Inventory quantities.
- **Asset and depreciation:** Asset records acquisition and operational custody. Accounting returns capitalisation/depreciation results and retains its own adjustments even if the equipment changes custodian.
- **Payroll confidentiality:** An approved payroll result may yield wage expense and liabilities; an Order or Warehouse consumer cannot query employee-level payroll information merely because it consumes allocated labour cost.
- **External provider uncertainty:** A connector times out after submitting a journal. Accounting reports pending/uncertain, reconciles via provider read-back/idempotent source reference and never claims confirmed posting solely from an HTTP acknowledgement or double-posts locally.
- **Cross-entity and closed-period isolation:** A request with the wrong entity, stale source revision, insufficient authority or a closed period is rejected or requires governed correction; no implicit fallback to a neighbouring entity/book.
- **Government submission:** A reconciled return is approved and transmitted; a portal acknowledgement is tracked separately from accepted, rejected and amended filing outcomes, retaining the applicable framework/policy versions.
- **Reporting consistency:** Authorised financial statements and dimensional reports reconcile to the same confirmed ledger snapshot; incomplete, stale or unallocated values are explicitly disclosed rather than silently presented as final.

**Future implementation gate:** Translate these **idealised surfaces** into a root public `CONTRACT.md` only when the corresponding repository exists and its composition interfaces, security boundaries, failure semantics and independent acceptance evidence can be verified. This section is neither an approved public API nor a mandate to implement all specialised providers at once.

## Converting and synchronising native and external accounting

**This is a governed change of authority, not merely field-format conversion.** A connector translates provider-specific structures; Accounting interprets financial meaning, decides which ledger is authoritative and validates the transition. Conversion must work in **both directions** wherever the supported provider permits usable export/import, with explicit capability limits.

### Canonical meaning and provider mappings

Define a **provider-neutral interchange model** for the agreed portable accounting core, without assuming it can express every provider feature losslessly:

- Identity of accounting entity, book, periods, account classifications, currencies and chart mapping.
- Posted journal header and balanced lines, posting/effective dates, references, corrections/reversals and period state.
- Opening/closing balances and selected reconciliation state, statement references and source provenance.
- Counterparty/customer/supplier references **only as authorised references**; do not absorb Profile, Order or Invoice data.
- Stable internal IDs and remote IDs, mapping versions, original-source IDs, origin direction, sync watermark, date/time interpretation, rounding and currency conversion rules.

**Mapping rules** must specify account-code equivalents, unsupported account types, fiscal period differences, tax-code references, currencies/exchange rates, contact/invoice references and journal correction semantics. Record unsupported or lossy mappings as **blocking exceptions requiring explicit resolution** where financial meaning or auditability would be compromised. Keep original records/source references for traceability; do not silently reinterpret historic postings.

**Where mappings live:** Accounting owns approved financial meanings and conversion policy; Integrations/connector owns connection metadata, provider DTO translations, remote identifiers and transport checkpoints. They may reference each other by documented identifiers, but cannot both become authoritative for the same mapping fact without an approved split. No connector directly modifies internal Accounting persistence.

### Controlled cut-over — internal → external

1. **Authorise and scope:** select accounting entity/book, provider connection, effective cut-over boundary, responsible approver, supported operations and applicable privacy/legal checks.
2. **Discover and preflight:** inspect connector capabilities, remote accounts/periods/currencies, schema versions, access scopes, import/export routes, provider restrictions and outstanding local postings.
3. **Map and dry run:** map chart/accounts, financial categories, source documents, tax and currency treatment; preview a candidate migration dataset and flag incompatible/lossy records.
4. **Establish a consistent boundary:** lock or coordinate financial mutations for the transitioning books, capture a definitive journal/checkpoint snapshot and decide how in-flight source events are held or replayed. No dual authoritative writers.
5. **Transfer:** create/identify target accounts and deliver only approved importable records or opening balances. Record mapping versions, receipts, rejected lines, batch and idempotency/correlation identities. Provider-specific limits determine the available migration depth.
6. **Reconcile and sign off:** independently compare trial balances by account and currency/period, opening balances, reconciled items and unresolved differences; confirm the target's posted/accepted state by provider read-back where possible. Do not treat network success as business success.
7. **Activate authority:** after explicit approval, record an immutable authority transition and enable the external route; preserve local historic books as **read-only evidence** for the pre-cut-over period. Release held new work through the selected authority without double posting.
8. **Monitor and recover:** detect missing, duplicated, late and out-of-order events; reconcile source documents to confirmed postings and track exceptions. A failed migration must keep or restore a single known authority under a documented recovery procedure, not guess that rollback succeeded.

### Controlled cut-over — external → internal or external → another provider

Use the same gates in reverse, but obtain a **provider-verified export or equivalent supported financial evidence** first. Verify period cut-off, mappings and currency treatment; reconstruct supported journals **or** establish approved opening balances with linked immutable historical archives where full ledger transfer is impossible. Load and reconcile locally **before** authorising local posting. A change from one provider to another proceeds through the same neutral validation and reconciliation boundary; it need not perform an uncontrolled double-hop through live local books.

Do not promise reversible migration, exact preservation of remote IDs, historical transaction editing or an identical feature set across providers. Provider export/API permissions and terms may prevent full transfer. In that case present the limitations, preserve accessible evidence and require a documented decision about what can legally and correctly be imported.

### Ongoing synchronisation while external is authoritative

- **Write route:** Accounting validates the business command and delegates it to the selected connector. No parallel authoritative local write.
- **Read route:** authoritative provider read or clearly identified local projection with **last-confirmed timestamp, freshness, source and completeness**, never a projection masquerading as confirmed books.
- **Delivery:** owner-owned outbox/source evidence and connector checkpoints support at-least-once processing; idempotency, remote ID matching and reconciliation prevent duplicate financial effects. Exactly-once distributed execution must not be assumed.
- **Inbound change:** verified webhook/poll response is authenticated, tenant/account scoped, de-duplicated, mapped and passed to Accounting for business validation. Record origin to prevent echo loops.
- **Conflicts:** chosen authority wins for its books, but contradictory evidence is recorded and escalated; do not silently overwrite locally initiated pending transactions.
- **Outages / deactivation:** external authority remains selected until a governed cut-over. Record pending/unknown outcomes; never silently start local posting or claim provider success.
- **History and retention:** store only the minimum permitted local projections, audit evidence and immutable references, observing access, confidentiality, provider terms, lawful retention and erasure/hold rules.

### Conversion acceptance cases

- Native-only organisation creates chart, posts balanced journals, corrects a posting, reconciles a bank statement, closes a period and exports its ledger without Integrations configured.
- Internal → external conversion with compatible chart/journal mappings produces reconciled balances and a single post-cut-over authority.
- Connector supports opening-balance import but not journal history: transition explicitly preserves the old ledger as historical evidence and records the loss of transactional portability.
- A chart mapping changes during migration: preflight and commit detect the version conflict and refuse an unreviewed transfer.
- External provider accepts a request but confirmation is lost: Accounting reports **unknown/pending**, uses idempotency/remote reference checks and reconciliation, not duplicate posting.
- A provider webhook arrives twice or out of order: deduplication and provenance prevent duplicate financial effects.
- External system becomes unavailable: Accounting does not switch to internal books; recovery or an authorised reverse cut-over is required.
- External → native transition reconstructs verified journals or approved opening balances, reconciles and activates internal authority **only after** cut-over sign-off.
- Two accounting entities under one group have different authority modes without cross-book postings or data leakage.

## Financial operations — native accounting scope and boundaries

The native core must account for complete economic lifecycles rather than only expose manually entered journals. **Accounting owns the recognised financial position and balances; originating domains retain their operational documents and business decisions.** These subfunctions are responsibilities **within Accounting**, not automatically separate Nuxt capabilities.

| Subfunction | Native Accounting responsibility | Origin / separation |
|---|---|---|
| **Receivables (AR)** | Customer balances, amounts due, due dates, part-payments, unapplied receipts, credit balances, ageing, disputes and approved write-offs/expected-credit-loss adjustments | Invoice owns issued sales invoices and credit notes; Order owns commitments; Business Contacts/Parties, if approved, owns counterpart references; Payment Gateway does not own debt |
| **Payables (AP)** | Supplier balances, due dates, part-payments, credits, accruals, approved write-offs and payable ageing | Purchase Order, Invoice/Billing and supplier evidence remain authoritative for orders and bills; banking or Payment Gateway executes payment |
| **Cash and treasury records** | Cash and bank ledger accounts, deposits, withdrawals, transfers, cleared/uncleared distinctions, bank-statement reconciliation and cash position | Financial institutions remain authoritative for bank balances and movements; Integrations supplies approved feeds, not financial meaning |
| **Equity and ownership** | Initial capital, capital contributions, owner drawings, retained earnings, distributions/dividends and owner/shareholder/director financing balances as applicable | Legal entity and approval facts originate from their authorised domain and legal/accounting context; do not misclassify capital as sales or drawings as wages |
| **Borrowings and financing** | Principal, interest, fees, repayment schedules, current/non-current classification, interest accruals and recognised financing liabilities | Contracts, lenders, interest statements and bank payments are separate source evidence |
| **Accruals, deferrals and prepayments** | Recognise income/expenses and obligations in appropriate periods; release and reverse period adjustments | Usage, employment, service delivery, purchase and invoice facts arrive from owner domains; cash timing alone is insufficient for accrual accounting |
| **Revenue and cost recognition** | Apply effective-dated financial rules to confirmed delivery/performance, discounts, returns, fulfilment, inventory costs and other source evidence | An Order, invoice issue, customer deposit and cash receipt are **not interchangeable** recognition events |
| **Tax ledger** | Tax control accounts, adjustments, liabilities/receivables, allocations and reconciled return figures | Specialist tax-rule determination and statutory submission are separate functions as defined below |
| **Period/year-end** | Trial balance, adjusting entries, period locks, financial close evidence, carried balances, retained-earnings transitions and governed re-opening/restatements | The reporting framework and legal entity context govern allowed corrections |
| **Dimensions and allocation** | Authorised references to projects, departments, product lines, warehouses, customers and cost centres, with cost-allocation provenance | Do not duplicate Project, Identity group, Product or Warehouse records; validity is checked through approved public owner contracts |

**Minimum complete native accounting cycle:** configure an accounting entity and opening balances; track and settle receivables/payables; record cash, owner funding and financing; accrue and adjust; post and reconcile taxes; close a period; produce traceable financial statements. Whether a tenant uses cash basis, accruals or another lawful basis is explicit in the chosen framework and must not cause hidden changes in recognition.

**Out of scope for the Accounting core:** generating sales or supplier invoices, payment execution, bank-credential custody, payroll computation, creating legal entities, tax-law authoring, supplier/customer contact administration and operational inventory movement. Accounting may provide controlled financial subledgers and references without owning those source records.

## Accounting contexts, frameworks and effective-dated policies

An **accounting context** represents a defined set of financial books for an **accounting/reporting entity**. It is **not automatically identical to a platform tenant, Identity group, registered company or physical site**. One tenant may govern multiple accounting entities and books with different authorities, fiscal periods and applicable rules; cross-entity entries and consolidated views require explicit review.

The context conceptually records or resolves:

- Accounting entity identifier and authorised legal/controller references, owner/group context and access decisions.
- Reporting framework and version (for example an applicable UK GAAP or IFRS framework), recognition and measurement basis, reporting and fiscal calendar, functional and presentation currencies.
- Chart of accounts, book scope and supported financial dimensions; tax registrations/schemes and financial-treatment elections when legally permitted.
- Approved **internal or external authoritative ledger** and invoice/tax provider arrangements, provider capability constraints, activation/cut-over epoch and reconciliation state.
- Financial policies with version, source, jurisdiction/territory, effective-from/effective-to, provenance, approver and applicable transitional treatment.
- Documented reporting/submission obligations and policy exceptions that require specialist approval; Configuration values cannot override mandatory law or immutable posting invariants.

**A selected framework is not enough to establish legal validity.** Legal Compliance records or supplies applicable obligation constraints and supporting evidence; Accounting owns how approved financial treatment maps transactions to postings. Qualified accountants/legal specialists must validate tenant-specific standards, elections and tax requirements before production claims. Where an external provider is authoritative, the selected framework and required reporting obligations still need an explicit compatibility check.

### Controlled extension surfaces

A framework/tax/reporting extension is a **versioned, declared, provider-neutral ruleset**, not arbitrary executable tenant code and not a new mandatory Nuxt Layer for every jurisdiction. Candidate contract surfaces:

| Extension surface | Inputs / outputs | Boundaries |
|---|---|---|
| **Describe/validate framework** | Supported reporting bases, jurisdictions, effective dates, currencies, chart/reporting requirements, policy choices and incompatibilities | Accounting rejects a missing/unsupported mandatory framework; no permissive default pretending compliance |
| **Recognition and measurement** | Validated transaction facts, entity, date/period, policy version → proposed classification, postings, valuation basis, rationale and required evidence | Core verifies balance, source uniqueness, period and authorisation before posting; rules cannot bypass ledger invariants |
| **Tax determination** | Tax-relevant facts and location/context, product/service type, dates and verified regime → proposed rates/treatments, exemptions, adjustments and traceable calculation | Tax applicability must be reviewed, including cross-border cases. Domain owners retain invoice/order facts; Accounting owns tax ledger consequences |
| **Statutory report preparation** | Accounting period, authoritative snapshot, policy versions → specified report/return model, validations, supporting reconciliation and explanation | A report is not an official filing until submission and acknowledgement |
| **Regulatory transmission** | Approved validated return, destination/account/scope and submission authority → receipt/rejection/correction status | **Integrations** owns authenticated transport, credentials and provider/API adaptation; Accounting owns authoritative return content and financial source references |

Registration must check extension identity, supported semantic contract/version, provenance, declared permissions/capabilities, integrity and compatibility. Rules execute through **constrained, deterministic and resource-bounded** interfaces; extensions cannot access other capabilities' private tables, silently edit posted records, read secrets or call arbitrary external endpoints. No raw user-defined JavaScript as a substitute for governed policy. Extension revocation/unavailability fails closed for operations that require its determinations.

### Historical reproducibility

Every confirmed accounting result needs enough **policy/version and evidence provenance** to explain why it was calculated. Updates to standards, tax rates or provider mappings must be effective-dated; they cannot silently rewrite historic journals. Corrections, retrospective adoption, prior-period adjustments and restatements are explicit, approved operations with original and revised figures linked. A closed period is not reopened simply because a ruleset was upgraded.

## Compliance, regulatory interfaces and policy ownership

The governing Capability Catalogue identifies **Legal Compliance** as owner of legal duties and applicable constraints and explicitly maps the former **policy-map** concept into **legal-compliance**. It does **not** authorise introducing a separate generic Policies domain. Current public `CONTRACT.md` for `legal-compliance` and `integrations` was **not retrievable** in this review; interactions here are **proposed ports** rather than implemented APIs.

| Owner | Proposed responsibility |
|---|---|
| **Legal Compliance** | Context-specific jurisdictional/legal obligations, evidence, legal holds, restrictions and the compliance status of required actions; may indicate uncertainty and need for review, but cannot automatically certify every tax election |
| **Configuration** | Declares validated settings, scopes, permissible values and provenance for tenant/accounting-entity choices; not the legal authority or financial source of truth |
| **Accounting** | Maintains framework/policy versions actually applied; evaluates recognition, valuation, accounts and tax consequences; prepares reconciled financial statements and return payloads; holds posting and submission evidence |
| **Integrations** | Government gateway and provider connections, secret/credential lifecycle, API adaptation, delivery retries, rate limits, submission receipts and remote references |
| **Authorisation / Identity** | Establish actor, group/entity context, authority, segregation of duties and required assurance for policy changes, posting, returns, migrations and corrections |
| **Workflow / Scheduler** | Optional approvals, preparation/reminder/deadline coordination; neither declares law nor posts accounting entries on its own |

**Conceptual policy interfaces** should answer: what requirement or restriction applies to this accounting entity/activity and effective period, how was it determined, what evidence supports it, whether human review is needed, which approved financial treatment it permits or forbids, and when it must be reconsidered. Accounting must distinguish **applicable mandatory rule**, **permitted election**, **tenant preference** and **unresolved/legal uncertainty**.

**Government submission lifecycle:** determine and verify filing obligation → prepare from an authoritative reconciled period/snapshot → apply jurisdiction-specific validation and required attestations → obtain authorised approval (and step-up/separation of duties where required) → transmit through the verified portal adapter → record received, accepted, rejected, pending, amended and finalised states with remote acknowledgement IDs → reconcile subsequent correction/refund/assessment to the books. A transport acknowledgement is **not** equivalent to regulator acceptance.

Missing legally required context, invalid credentials, uncertain jurisdiction, unsupported filing format, provider outage or unconfirmed submission must result in a clear refusal/pending or requires-review state rather than a fabricated compliant outcome. Do not hold database transactions open during remote calls.

### Legal and technical acceptance scenarios

- Two accounting entities in one tenant select different reporting frameworks and applicable tax regimes without leaking books or using the wrong policy.
- A rule changes prospectively; prior-period numbers remain reproducible, while an authorised restatement explicitly records its origin and revised outcomes.
- A tenant attempts to configure a forbidden tax treatment or bypass a legal hold: the operation is rejected even if Configuration contains the value.
- A government portal accepts an HTTP request but rejects the return: the return is **not** shown as successfully filed, and remediation is traceable.
- A regulator's submission is amended after acceptance: the platform preserves both receipts, period snapshots, approvals and financial adjustments.
- An extension is missing or cannot validate a mandatory rule: posting/reporting/filing operations requiring that decision fail closed without blocking unrelated lawful work.

## Financial statements, reporting and controls

**Accounting produces authoritative financial meaning and statement data.** The separate Reporting capability may display, compare, chart, export and distribute *authorised* views, but must not recalculate a different authoritative balance. Publisher or Template Engine may present signed-off statements; none independently posts journals.

| Financial output | Minimum conceptual information |
|---|---|
| **General ledger and trial balance** | Period/as-of date, account balances, journal provenance, controls and balancing status |
| **Profit and loss / income statement** | Recognised income, expenses, comparative periods and accounting framework reference |
| **Balance sheet / statement of financial position** | Assets, liabilities, equity and reconciliation to the underlying ledger |
| **Cash-flow information** | Cash movements and classifications appropriate to the reporting basis, with bank reconciliation provenance |
| **Receivables/payables ageing** | Outstanding counterpart balances, due dates, credits, payments and exceptions |
| **Tax reports and returns** | Supported period/tax account amounts, adjustments, liability/reclaim, schema/version and submission status |
| **Management views** | Dimensional cost/revenue allocations and margins with period, currency, allocation-method and completeness indicators |

Every output should identify the accounting entity, authoritative source (native or external), as-of/period, applied framework and policy versions, source data freshness, reconciliation state and whether it is draft, approved or issued.

**Controls to preserve:** balancing by required currency/books, decimal money precision and rounding policy; reference/correlation/idempotency; source and journal uniqueness; approval limits and segregation of duties; authorised reconciliations and adjustments; period lock; immutable reversal lineage; controlled access to potentially sensitive financial and counterparty data; retention/hold, export and recovery; and confirmation-aware external posting. No promise of distributed exactly-once delivery.

**Financial integrity scenarios:**

- A supplier bill is paid in two instalments; AP balances, bank payments and underlying invoice references reconcile without duplicate posting.
- An owner contributes funds and later makes a drawing; neither entry is silently classified as revenue or payroll.
- A bank reconciliation finds a missing transaction: evidence and permitted adjustment are explicit, not inferred from a cleared payment flag.
- A tenant views financial statements filtered by warehouse or project: the allocated figures reconcile to the authoritative whole, with unallocated costs transparent.
- A qualified framework requires different period-end treatment: the approved rules and report version determine the outcome without duplicating the source Invoice or Inventory state.
- A restored or reconnected provider returns uncertain posting results: no report is final until those uncertainties are resolved or explicitly disclosed.

**Conceptual sign-off criterion:** native Accounting can complete a defensible basic books-and-period lifecycle; connected authority has comparable core semantics with explicit supported-operation limits; legal/tax requirements can be extended through constrained versioned rules and verified provider connectors; all outstanding jurisdiction-specific decisions remain documented for qualified review. This is conceptual sign-off only, **not** evidence of regulatory certification, implementation readiness or an approved new capability.

## Version

**Conceptual record:** initial draft. **Implementation/package version:** not applicable / not verified.  
Once defined, accounting policies, chart structures, source event mappings and reporting schemes may need independently versioned representations; no concrete versioning schema is prescribed here.

## Availability

No `nuxt-layers/accounting` repository or root `CONTRACT.md` was found in the inspected organisation. The catalogue is a **candidate**, not software availability. Application installation, activation and operational health have **not been checked**.

## Capabilities offered (conceptual)

The **native core is the baseline**, not a fallback mock or a provider-only shell. The interfaces and accounting results described above should remain meaningful with no third-party connection. An external authority adds delegation and synchronisation, not a second parallel financial truth.

- Maintain accounting books and charts of accounts.
- Accept validated postings with source attribution and balancing controls.
- Enforce journal posting, reversal and period-closing rules.
- Reconcile balances against separately owned evidence and statements.
- Produce authorised, traceable ledger and period views.
- Support financial corrections and retention without erasing historical provenance.

These are possible future business functions, **not documented exported functions or endpoints**.

## Configuration (conceptual)

Potential organisational/accounting policy decisions include **authority mode per accounting context**, authorised external connection identifier, migration/cut-over state, accounting basis, fiscal year and periods, functional and transaction currencies, rounding, chart of accounts, approval thresholds, retention, reporting policies, and source-system mappings. A configured connector must be explicitly activated as an accounting authority; connection existence alone is not activation. **Configuration's** responsibility and any host-supplied policy declarations must be reviewed: business accounting policy cannot become unauthorised generic settings that override ledger invariants.

No keys, values, APIs, database type, infrastructure provider or user interface are specified here.

## Relationships to other conceptual records

- **Invoice / Billing / Payment Gateway / Subscription:** financial source evidence and separate business lifecycles.
- **Order / Inventory / Warehouse:** commercial/operational source facts without double ownership.
- **Integrations / external accounting providers:** optional configured Xero, QuickBooks or comparable connectors, with explicit authority selection and governed transition. Provider capabilities and API limits must be verified before implementation.
- **Reporting:** derived analytics and financial views should not supplant whichever ledger is authoritative for the accounting context.
- **Groups / Organisation:** groups can own and control accounting resources through authorised relationships, but a legal/accounting entity may span or differ from an Identity group.
- **Workflow / Scheduler / Message Queue:** potential approval, period-end or event-delivery mechanisms, not accounting-state owners.

## Open architectural decisions

1. **Dual-mode support is the proposed requirement:** internal books are primary when no external authority has been configured; a selected external accounting package becomes authoritative upon approved activation. Define the precise accounting-context scope, supported functions and non-overlap guarantees.
2. How do group ownership, tenant isolation, legal entities, multiple books, branches and consolidated accounts relate?
3. Which accounting basis and applicable jurisdictions are in scope? Which validations are invariants versus configurable policies?
4. Who determines and approves invoice-to-journal, refund, payout, exchange-rate, tax and stock-valuation treatments?
5. Which source facts are authoritative and how are duplicate, delayed, corrected or missing transactions reconciled?
6. Which posting and period-close operations require separation of duties, reauthentication and immutable evidence?
7. What minimum viable accounting lifecycle would establish an independent owner without prematurely building invoicing, banking or general financial ERP functionality?
8. Which actions and financial objects are covered by external authority, including unsupported provider features, and how is consistent accounting semantics preserved across connectors?
9. How is internal-to-external and external-to-internal cut-over performed: mapping, opening balances, unreconciled transactions, posted history, duplicates and rollback?
10. What happens when the external connection is degraded, revoked, paused or removed, without silent local fallback or loss of accounting evidence?

## Conceptual acceptance scenarios (not implementation tests)

- Two orders from different channels produce valid financial source evidence; Accounting creates **no duplicate journals** when events are delivered twice.
- An invoice is corrected after posting; the financial history shows an explicit compensating/reversal entry rather than a silent mutation.
- A closed period rejects or routes late changes according to an explicitly approved adjustment policy.
- A person who belongs to two groups sees and operates only on appropriately authorised books; loss of membership removes authority without erasing lawful records.
- A payment-provider payout differs from an invoice or bank statement; reconciliation exposes and resolves the difference without rewriting Order or Payment Gateway records.
- A newly configured Xero/QuickBooks-like connector is explicitly approved as authoritative; Accounting routes supported actions through Integrations and does not double-post locally.
- With **no external authority ever configured**, Accounting operates its own authoritative books.
- An authoritative external connection becomes unavailable; Accounting does **not** silently become the primary ledger, and pending/failed actions remain visible and reconcilable.
- A group deliberately migrates back from external to local authority; the cut-over reconciles balances and outstanding work before internal posting is enabled, preserving provenance and historic source references.

## Next decision gate

Review and approve the **dual-mode accounting authority model** and the scope of authority per accounting context. Then evaluate how Integrations supplies provider connections, how cut-over and outages work, and which accounting behaviours belong to the common business contract. Only then derive interfaces, persistence and operational design. This record does not amend the governing catalogue or any ADR.

## Cross-domain accounting implications — conceptual review notes (14 November 2026)

**Status:** Discussion findings for later owner-by-owner review. These are neither approved mandatory dependencies nor tax/accounting rules. Applicable financial treatment depends on the reporting entity, jurisdiction, reporting basis, contract and transaction.

### Financial consequences of non-financial domains

| Domain / source | Owns the underlying facts | Accounting would recognise, subject to policy |
|---|---|---|
| **Product / assembly / bundle** | Product definitions, versioned bills of materials, commercial sellable configurations and bundle composition (ownership of manufacturing lifecycle remains to be reviewed) | Product structure alone creates no journal. Valuation follows actual acquisitions, conversions, stock movement or sale; sales bundles require allocation and component-cost treatment without double counting |
| **Inventory / Warehouse** | Physical stock quantities, custody, locations, receipts, reservations, consumption, production and adjustments, and source evidence | Inventory carrying values, work-in-progress, finished goods, cost of goods sold, shrinkage and write-downs from verified movements/cost inputs; do **not** treat list prices as asset values |
| **Asset / equipment / buildings** | Identified assets, acquisition, custodian/location, condition, maintenance, transfer and disposal | Fixed-asset register and financial classification, capitalisation, depreciation, impairment and disposal accounting where applicable; some tools/spares are inventory/expenses rather than fixed assets |
| **Order / Invoice / Payment Gateway** | Commitments, legally issued bills/credit notes and payment-provider execution respectively | Receivables, payables, recognised revenue/cost, settlement, fees, refunds and reconciliation at appropriate recognition points; an order is not necessarily immediate revenue |
| **Employment / payroll** | Employment relationships, hours/pay entitlements and payroll calculation/payment obligations (payroll ownership not yet established) | Wage expense, employer charges, accrued liabilities, paid liabilities and allocated production labour; no employee personal profile or payroll computation ownership |
| **Contractors / utilities / overheads** | Supplier/contract terms, utility usage, purchases, service delivery and bill evidence | Operating expenses, accruals, prepayments, accounts payable; attributable production overhead may feed inventory cost where policy permits |
| **Business parties** | Tenant-scoped customer/supplier counterpart records optionally linked to Identity | Debtor/creditor account references and exposure, without owning contact records or requiring people to register |

### Required conceptual separations

- **Product ≠ inventory item ≠ saleable bundle ≠ fixed asset.** A car can be one saleable product, a versioned component assembly, a stocked serialised item, or a business-owned fixed asset depending on its role and actual use. The same underlying item must not be capitalised as fixed equipment and simultaneously counted as inventory merely because both domains reference it.
- **Assembly versus commercial bundle:** assembly/manufacture consumes components and creates output/WIP and conversion cost; a sales bundle might only group separately stocked products and allocate commercial price, without physically manufacturing another unit. If bundles are prepacked, define whether physical conversion and additional stock identity actually occur.
- **Stock versus valuation:** Inventory remains authoritative for quantity and movement. Accounting owns approved financial valuations and journal consequences. Costs, landed charges, labour, overhead, allocations and write-down policies need versioned provenance and period handling.
- **Physical asset versus financial asset register:** Asset owns the operating lifecycle (equipment, buildings, maintenance, custody). Accounting owns carrying amount, depreciation and impairment treatment, with stable references and reconciliation. Leasing, owner-versus-custodian differences and capitalisation thresholds require separate review.
- **Consumable classification is contextual:** stationery used immediately may be an expense; materials awaiting use in production may be inventory; durable equipment may be fixed assets. Classification follows authorised use, business policy and applicable accounting rules, not product naming alone.
- **Employment and payroll remain distinct:** Identity group membership is neither an employment contract nor payroll enrolment. Staff and contractors require separate terms, status, privacy and legal treatment. Payroll computation, taxes and payslips need a separately justified owner or approved external provider; Accounting records resulting financial facts.
- **Costs and commitments differ:** purchase orders, purchase invoices, accrued costs, prepayments and cash settlement have distinct dates, evidence and accounting consequences. Utilities may be recorded through recurring bills or usage; they do not require a user account for the supplier.
- **Authority modes apply consistently:** when Xero/QuickBooks or another provider is the approved accounting authority, all recognised financial postings follow that authority; operational domains remain authoritative for their own facts. No duplicate local authoritative ledger, including for stock valuation or payroll.

### Outstanding design decisions

1. What is the minimal product/assembly/bundle vocabulary and which owner controls versioned bills of materials, manufacturing work orders and actual production consumption?
2. Which domain produces reliable movement, purchase cost, landed-cost, WIP, overhead and write-down evidence for Accounting? Who sets and versions valuation policy?
3. How do asset acquisition, fixed-asset classification, disposals and depreciation reconcile across purchasing, Asset and Accounting without duplicated ownership?
4. Where do payroll calculation, employment contract, contractor billing, time recording and tax submissions belong, and which are external integrations versus independent business owners?
5. How are customer/supplier party records, legal entities, tenant/group ownership, invoice recipients and debtor/creditor accounts mapped without requiring Identity enrolment?
6. Which accounting standards and tax jurisdictions apply to each legal/accounting entity? IAS 2 (inventory), IAS 16 (property, plant and equipment) and IAS 19 (employee benefits) are **reference examples**, not universally applicable platform rules; verify local reporting frameworks before implementing policy.

**Technical references for later validation:** [IFRS IAS 2 Inventories](https://www.ifrs.org/issued-standards/list-of-standards/ias-2-inventories/); [IFRS IAS 16 Property, Plant and Equipment](https://www.ifrs.org/issued-standards/list-of-standards/ias-16-property-plant-and-equipment/); [IFRS IAS 19 Employee Benefits](https://www.ifrs.org/issued-standards/list-of-standards/ias-19-employee-benefits/). These are accounting reference materials, not accepted platform ADRs.

### Logistics, warehouse storage and delivery-cost accounting — additional review notes

- **Operational evidence:** Logistics may own shipment execution, carrier services, freight and return transport cost evidence; Warehouse normally owns actual space/occupancy, storage/handling operations and custody. Outsourced warehousing, commercial tariffs and invoicing require explicit boundary review with Billing, Order and supplier contracts.
- **Financial treatment:** Accounting alone determines whether approved costs enter inventory acquisition/landed cost, WIP/production overhead, cost of goods sold, operating storage expense, distribution expense, recoverable charge or accrued/payable balance. Avoid treating all warehouse rent or sales freight as inventory value; treatment varies by activity and accounting framework.
- **Separate quoted, billed and actual cost:** Customer-facing shipping fees in Order/Invoice, a carrier's estimate, an incurred freight cost, a supplier invoice and the eventual paid amount are distinct facts with separate dates and ownership. Reconcile them via source references; the difference may form part of margin.
- **Examples:** inbound freight on acquired goods may contribute to inventory cost when qualifying; delivery to a customer may instead be a selling/distribution expense; storage costs may normally be period expenses unless specific qualifying production/bringing-to-condition circumstances apply. Do not hard-code those examples as universally applicable policy.
- **Provider mode:** when accounting authority is external, send approved financial consequences through Integrations with idempotency and confirmation; Logistics and Warehouse continue owning the operational facts.
- **Open:** define ownership of freight/3PL agreements, storage rate cards, cost allocation by shipment/item/location, customs duties, insurance, returns, cost-estimate variance and the trigger for accrual or recognition.

## Cross-capability relationships and evidence status

- **Established evidence:** The governing Capability Catalogue identifies Accounting as a proposed domain boundary for ledger, journal, accounting periods and reconciliation, not as owner of originating commercial or warehouse transactions. No `nuxt-layers/accounting` repository or root `CONTRACT.md` was found in the prior review. This is **not** implementation or acceptance evidence.
- **Proposed scope:** Native financial books and an approved externally authoritative system connected through Integrations; financial postings and reconciliation arising from the other domains' independently owned records.
- **Related capability review notes:** [Product](../product/capability-record.md), [Inventory](../inventory/capability-record.md), [Asset](../asset/capability-record.md), [Warehouse](../warehouse/capability-record.md), [Logistics](../logistics/capability-record.md), [Order](../order/capability-record.md), [Invoice](../invoice/capability-record.md), [Billing](../billing/capability-record.md), [Employment](../employment/capability-record.md) and [Integrations](../integrations/capability-record.md). These links identify **provisional** relationships; their own pro formas remain pending alphabetical review (see separate blueprint PR #19).
- **Open architectural questions:** Native minimum and financial reporting basis; independent accounts-receivable/payable and payroll scope; capitalisation versus expense decisions; inventory and manufacturing cost inputs; revenue timing; customer/supplier party reference ownership; per-tenant authority transitions and third-party provider capabilities.
- **Review gate:** Approve Accounting's conceptual boundary before deriving an implementation contract. Other domain owners must each be assessed from their own governing responsibilities and public `CONTRACT.md`; cross-references are not approval of a dependency or transfer of ownership.

### Asset conceptual-review cross-reference (14 November 2026)

**Proposed:** [Asset](../asset/capability-record.md) owns identity, stewardship, title/rights evidence, applicable custody/assignment, condition or entitlement, obligations and lifecycle history of **tangible and intangible** managed assets, even when the legal owner, manager, beneficiary and accounting entity differ. Accounting remains authoritative for recognition of tangible, intangible and right-of-use assets, depreciation/amortisation, impairment, financial valuation and postings. Link verified operational evidence and reconcile; never infer Accounting recognition from title or physical custody alone. The fixed-asset subledger and lease-schedule design remain open for Accounting's later implementation review.

## Cross-capability note — Billing charge authority (15 November 2026)

**Agreed conceptual relationship: Billing BIL-01–BIL-06 approved by the project owner on 15 November 2026; implementation contracts remain unverified.** [Billing](../billing/capability-record.md#idealised-public-inbound-contract) owns charge assessment, rating, billing periods, finalised commercial charge facts and proposed adjustments. Accounting consumes attributable, versioned charge/invoice facts and independently owns ledger recognition, receivables/payables, accounting periods, settlement and reconciliation. Accounting may supply posting/receivable status under scoped disclosure; a Billing charge event is **not** proof of posting or payment. Failure/replay cannot double post. Supplier obligation assessment does not mean Billing owns Accounting accruals. See approved BIL-01, BIL-03 and BIL-04. Accounting's own conceptual contract remains authoritative within its agreed scope; no implementation change is proposed.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Own host-operator commercial financial postings distinct from tenant's own business books; tenant ancestry and digital owner do not automatically establish payer or ledger scope.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed for [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53), not an implemented contract.** See [Configuration conceptual public inputs](../configuration/capability-record.md#idealised-public-inbound-interfaces). Configuration owns approved schema-registered selections and provenance; Accounting owns financial policy meaning, posting, reporting entity scope and migrations. An accounting entity is not automatically a Configuration scope. Use public host-composed ports/events only; preserve all prior decisions and dependency acyclicity.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-06 (Option C):** resource/entity-specific setting contexts may be proposed through registered, domain-approved public contracts. Accounting owns accounting-entity identity, accounting policy meaning, applicability, historical transactions and migration behaviour; Configuration would own approved selection values/version/provenance only. No accounting entity silently becomes a tenant/group or gains inherited policy from tenant parentage.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.
