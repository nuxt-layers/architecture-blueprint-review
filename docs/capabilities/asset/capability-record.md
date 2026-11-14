# Capability Record — Asset

**Status:** Proposed Domain capability; conceptual review awaiting approval. No implemented package or public API is asserted.
**Review date:** 14 November 2026.
**Governing baseline:** `nuxt-layers/architecture-rules` `master` at `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.
**Blueprint baseline:** `nuxt-layers/architecture-blueprint-review` `master` at `e802386e256340c7cd7310398d02c30168535e17`.
**Evidence:** The governing catalogue lists `asset` as owned/controlled asset lifecycle, assignments and valuation references, excluding generic sale stock. The working catalogue calls it a Domain candidate. A lookup and organisation repository search found no `nuxt-layers/asset` repository; hence there is no Asset root `CONTRACT.md` or verified implementation to evaluate. Existing Accounting, Inventory and Product notes are provisional blueprint evidence, not accepted interfaces. Proposed design below is not normative.

## Summary and classification

**Asset** maintains the register and lifecycle of identifiable **tangible and intangible assets** an organisation owns, controls, manages, holds or is responsible for, including machinery, vehicles, buildings, software licences, intellectual property and identifiable contractual rights. It records what the asset is, its accountable management context, relationships to parties, rights and obligations, relevant condition or entitlement, availability for permitted use, and its attributable history.

Its independent responsibility is **asset identity, stewardship, rights/obligation references, applicable condition and lifecycle**, not financial ledger recognition, generic saleable stock, every commercial agreement or the authoritative execution of licences and contracts. It is a credible **Domain capability** because these records and obligations persist independently of purchasing, accounting, inventory or a particular organisation type. A separate implementation repository is not approved merely by this review. The capability can be implemented as a headless core with optional separable presentation, using the governing Capability Standard.

The scope explicitly includes manageable intangible assets: software and service-use licences, identifiable intellectual-property rights, acquired contractual rights and similar registered entitlements. It does **not** automatically turn every contract, subscription, permission, dataset or commercial relationship into an Asset; an identifiable stewardship lifecycle, rights/obligations and accountable managing context must justify inclusion. ISO 55000:2024 supplies useful asset-management terminology and lifecycle principles, not a requirement for ISO 55001 certification. Type-specific extensions must preserve a stable common identity and clearly differentiated rules.

## Ownership and relationship model

**Proposed central rule:** legal title/ownership assertions, contractual rights and obligations, operational management, physical custody (where applicable), assignment, location (where applicable) and accounting recognition are **separate dimensions**. They can concern different parties concurrently and change on different dates.

| Dimension | Conceptual meaning | Responsible source |
|---|---|---|
| Asset identity | A uniquely identified tangible unit, intangible right/licence or composite managed asset; identifier, type, provenance and any external serial/registration/reference | **Asset** |
| Legal title/ownership claim | Identified owner or owners, ownership shares where applicable, effective dates and evidence; recorded as an evidenced assertion, not a legal determination | **Asset** holds relevant relationships and provenance; applicable legal records/agreements govern disputed title |
| Operating or managing organisation | Party responsible for stewardship, maintenance, policy and operational decisions, with defined scope and effective period | **Asset** |
| Control and right of use | Lease, hire, loan, licence, concession, bailment or other documented entitlement/restriction; distinct from title | **Asset** references rights and operational constraints; authoritative contract and legal terms stay with their owning source |
| Custody | Party holding or safeguarding a tangible item, where meaningful; receipt, handover and return evidence | **Asset** owns asset custody history; Logistics/Warehouse may supply movement facts |
| Assignment | Named person, team, project, site or other permitted context using or accountable for the item; time bounded | **Asset**; Identity owns identities/groups, not asset assignments |
| Location | Physical placement when relevant; otherwise applicable digital deployment, registration territory or governed operating context as different typed references | **Asset** owns applicable placement/context references; Location owns geospatial and place definitions |
| Rights and obligations | Licence limits, permitted uses/users, seat/territory scope, transfer/renewal constraints, maintenance duties and obligations, with effective dates and authoritative evidence links | **Asset** manages operational applicability and compliance evidence; contract/licensing/legal source owns binding terms | 
| Accounting recognition | Whether, by whom and on what basis a tangible asset, intangible asset or right-of-use asset is recognised and valued | **Accounting**, not Asset |
| Operational valuation evidence | Acquisition price, appraisal, insured value, replacement estimate, condition and external valuation reference, each with type, date, currency, source and uncertainty | **Asset** stores provenance/references; Accounting owns recognised value, depreciation and postings |

Relationships must support multiple legitimate parties over time and simultaneous non-conflicting roles. No single `ownerId` or `assignedTo` field should collapse these concepts. The same party can hold several roles; the application must not infer rights or access solely from those roles. Claims about title may be contested or unknown: preserve provenance, verification and dispute status rather than falsely asserting legal certainty. A party's role may be external to the tenant and must be represented without creating a fraudulent Identity group or requiring the other party to use the application.

**Examples:** a supplier owns a leased forklift operated by a business; a charity owns a van held by a contractor; a club owns facilities maintained by a hired facilities manager; a company holds software licences with limited named-user seats; a charity holds an intellectual-property right restricted to specified territories; an organisation acquires an assignable contractual right with an expiry date. Rights can be time-bound, non-transferable or contested without requiring physical custody. None requires the owner, custodian, operator and accounting entity to be identical.

## Proposed authoritative records

Asset should own:
- **Asset register:** immutable internal identity, class/type, description, applicable physical identifiers or intellectual-property/licence/contractual reference, composite/parent-child membership and source provenance. A model, contract or catalogue entry is not automatically a managed asset.
- **Asset lifecycle:** acquisition/creation/onboarding evidence, verification, commissioning or entitlement activation, operational use, renewal or expiry where applicable, restrictions, suspension, decommissioning, disposal, surrender, transfer and archival, retaining event history. State must reflect real-world events, not erase them.
- **Operational relationships:** title claims, managing party, contractual entitlement references, assignment, custody, location, responsible persons/teams, effective periods, handover/acceptance and obligations. Track their sources, effective and recorded dates.
- **Applicable condition, entitlement and performance:** physical inspection, usage/meter readings, faults, damage, incidents, service/repair history, warranties and certificates **or**, for intangible classes, entitlement validity, allocation consumption, renewal dates, territorial restrictions, registered-right status and verified usage against limits. Specialist sources remain authoritative for their own facts. Record work orders or specialist maintenance execution only to the extent this boundary is independently justified; do not duplicate Task/Workflow execution.
- **Rights/obligations and controls:** authoritative agreement/registry references, scope, permitted usage, quantities/seats, sub-licensing and transfer restrictions, renewals, inspections, approvals, holds/releases, outstanding obligations, evidence requirements and retention under approved policy; Asset does not draft, execute or adjudicate underlying contracts.
- **Operational financial references:** acquisition/disposal consideration and cost evidence, insurance/insured values, estimates and identifiers linking to Accounting transactions, without becoming a financial subledger.
- **Provenance and export:** history and verified source references; explain material changes, corrections, reconciliation conflicts and external-authority status.

**Non-ownership:** Product owns product/model definitions and saleable offers; Inventory owns stock quantities, reservations and movements; Warehouse/Logistics own handling and transport work; Accounting owns capitalisation, recognised fixed/right-of-use assets, depreciation, impairment, financial revaluation and the journal; Invoice/Order/Billing own their financial source documents; Identity owns identifiers, groups and membership; Authorisation owns access decisions; Legal Compliance supplies applicable constraints; Configuration supplies scoped setting mechanisms; Clock supplies time semantics; Integrations manages external application connections. Asset does not decide legal title or create binding lease obligations merely by recording a relationship.

## Native functionality and invariants

A usable **native Asset** works without optional accounting, maintenance, licensing, telematics, IP-registry or external asset-management providers:
1. Register, import and identify tangible units and intangible asset rights; resolve duplicates and reconcile externally identified records without silent merging.
2. Set and verify the management scope, parties, title claims and documentary references; record that evidence can be incomplete or disputed.
3. Assign and hand over assets to people, organisations, locations or projects with clear effective periods, receipt/return and accountability.
4. Record relevant physical condition, faults, inspections, servicing, repairs, safety restrictions, warranties, usage and downtime **or** intangible entitlement, seat allocation, expiry, renewals and scope restrictions; find due/overdue obligations.
5. Control commissioning, use, movement, suspension, reinstatement, transfer, decommissioning, disposal and archival using authorised, auditable transitions.
6. Search and report by asset, location, manager, assignment, custodian, ownership claim, class, condition, compliance status, availability and history; export authorised records.
7. Associate evidence, acquisition/disposal facts and financial reference identifiers without calculating recognised depreciation or accounting balances.
8. Recover from erroneous or delayed events via explicit corrections, compensating actions and reconciliation, never history rewriting.

**Required conceptual invariants:** stable asset identity; type-specific applicability (do not require custody, physical location or repair history for intangible rights); no generic entitlement creation merely from registering an asset; no double-active incompatible exclusive-custody assignment for the same unit/time unless the asset type expressly permits shared custody; role changes have provenance and effective dates; recorded time and event time remain distinguishable; a disposal or decommission event does not automatically extinguish contractual, accounting or retention obligations; an asset cannot be represented as available while subject to an effective safety hold; external failure cannot silently authorise a prohibited action; data from one tenant cannot be read or altered through another tenant's access scope. Composite assets/parts, partial ownership and shared locations require explicit supported rules, not assumptions.

**Illustrative lifecycle:** proposed/onboarding → identified/verified → commissioned or activated → assigned/in use → restricted, suspended or temporarily unavailable → restored, renewed, decommissioned, expired, transferred, surrendered or disposed → archived. This is not one universal enum: intangible rights may renew or expire, physical assets may be inspected or repaired, and contractual obligations may outlive operational availability. These are conceptual examples, **not a mandatory single linear enum**. Title, custody, assignment, condition, financial recognition, warranty and inspection status have distinct concurrent lifecycles.

## Proposed public contract — six logical surfaces

The following are **contractual responsibility groups**, not six packages, approved TypeScript interface names, endpoints or deployed services. The core must operate natively; optional integrations may extend selected types and populations.

| Surface | Inputs and commands | Outputs, queries and events | Authority boundary |
|---|---|---|---|
| **1. Asset Registry** | Register/import, classify, identify, link asset types and parent/child relationships, verify and resolve duplicates | Asset identity and typed record; search; historical register views; registration/classification facts | Asset owns individual managed asset identity; Product owns model/commercial description; authoritative external registries retain their own registration facts |
| **2. Asset Relationships** | Record/validate claims of title, effective rights and duties, managing party, assignments, accepted custody where meaningful, territory/location and usage permissions | Party/role history; as-of ownership/management/custody/assignment; applicable rights/restrictions; handover events | Asset owns operational relationships and evidence; legal agreements/registries retain legal authority; IAM retains identity and authorisation |
| **3. Asset Operations** | Record inspections, faults, servicing, physical meters, restricted use, licence allocation/consumption, renewal obligations and class-specific observations | Condition, availability, due/overdue duties, entitlement limits, operational history; condition/restriction events | Asset owns operational assessment and evidence; external metering/licensing/specialist services keep their distinct originating facts |
| **4. Asset Lifecycle** | Verify/commission/activate, suspend/reinstate, renew, transfer, surrender, decommission, expire, dispose, correct and reconcile transitions | Lifecycle state and transition history; requested/confirmed/pending outcomes; change events | Asset owns lifecycle decisions and evidence, not financial postings, legal title adjudication or vendor-side licence execution |
| **5. Asset Evidence and References** | Attach/classify external evidence references; record valuation source, warranty, certificate, licence, legal or financial cross-reference and provenance | Auditable evidence links, dates, source, verification, as-of view, exceptions and export | Asset owns evidence associations and appraisal/reference context, not file bytes, authoritative contract terms or Accounting carrying amounts |
| **6. Asset Integration** | Receive authenticated observations/commands, request/confirm scoped synchronisation, map external IDs, perform governed authority cut-over | Owner-published business events, supported projections, reconciliation/conflict reports, authority and provider-health status | Integration providers own transport/connectors; Asset governs acceptance and its slice of authority; no automatic authority transfer |

Public interactions comprise **commands, queries, owner-published events and host-supplied ports**. A query is always subject to resource-aware access checks; an input from another capability is evidence or a requested action until validated and accepted by Asset. Owner events are emitted only for confirmed authoritative changes, via the capability-owned outbox when required. Consumers may subscribe without reading Asset storage or treating technical delivery as a completed business result.

**Contract-wide obligations:** stable typed identity and provenance; tenant and actor context; explicit server-side Authorisation; validated commands and policy; idempotency/correlation and expected-version or equivalent concurrency controls; time zones and effective-versus-recorded timestamps; type-specific applicability; errors and fail-closed behaviour; no vendor SDKs or hidden package dependencies; documented optional-port absence modes; forward-compatible extensions and export/import semantics. Related capability dependencies and Nuxt `extends` edges must remain declared, directional and jointly acyclic.

### Type differentiation and temporal rights

- **Core common model:** stable ID, asset type, managing context, source, applicable party relationships, rights/obligations, lifecycle, history and retention. Configurable **typed specialisations** validate only relevant attributes and operations (e.g. vehicle mileage, building inspection, named-user licence seats, trademark jurisdiction and renewal). Asset types do not become implicit access grants.
- **Rights and obligations:** explicit, versioned, effective-dated references and operational constraints (including territorial, quantitative, temporal, assignment, transfer and sublicensing limits). No assumption that legal owner, beneficiary, operator, holder and financial reporting entity coincide; an entitlement claim cannot prove its own validity.
- **Concurrent status dimensions:** lifecycle stage, entitlement validity, availability for permitted use, physical condition (where applicable), obligations/compliance evidence and external synchronisation/verification state remain independent. Neither `active` nor `owned` is a universal operational or accounting conclusion.
- **Historical reconstruction and portability:** support as-of queries by effective and recorded time where meaningful, explicit correction/supersession, audit-ready provenance, portable exports and governed migration; preserve retained evidence when rights expire or assets leave service. Confidentiality and retention obligations survive transfers where applicable.

Typical Asset-owned events might describe registration, assignment acceptance, condition restriction, entitlement expiry evidence, renewal confirmation or disposal. Their names and payloads remain **unapproved examples**; external claims of expiry, legal transfer or renewal require appropriate confirmation.

## External authority and integrations

The default is **native Asset authority** for operational asset records. Optional external asset/fleet/maintenance/property systems can be read as evidence, synchronised as projections or made authoritative for an **explicitly selected domain slice and asset population**, subject to approved policy. Define exactly which owner holds each record type (e.g. asset identity, inspections, meters, custody) at any time; merely installing a connector does not transfer authority.

A transfer requires authorisation, mapping, cut-over, version/identifier reconciliation, unresolved-work handling, verification and rollback policy. While an authoritative external system is unavailable, preserve its authority: queue only safe, explicitly supported requests or mark operations pending/unavailable, not silently take over or assert successful completion. Transport acknowledgements are not evidence that the business operation succeeded. Preserve source timestamps, third-party identities, idempotency and conflict resolution.

Optional domain relationships include Accounting and external accounting packages, Inventory/Product, Order/Invoice, Warehouse/Logistics, Task/Workflow/Scheduler/Notifications, Location, reporting, insurers, telematics, licensing and IP/rights registries, external maintenance providers and document/evidence storage. None is thereby a mandatory Nuxt package dependency.

## Configuration, security, compliance and presentation

Asset owns the meaning and enforcement of its **domain rules**, while Configuration can manage validated declarations, scopes, precedence and governed values through published contracts. Potential configurable policies: tangible/intangible asset categories and hierarchies, type-specific validation, identifier requirements, inspection/service and renewal intervals, authorised transfers, custody acceptance where applicable, entitlement/seat limits, status transitions, evidence requirements, approval thresholds, insurance/usage limits, retention and restricted-use conditions. No generic universal legal policy is implied.

All protected reads and changes require **server-side Authorisation** on tenant, resource, actor and action; role labels such as legal owner, manager or employee do not automatically grant permissions. Guard cross-tenant transfers with explicit authority, bilateral evidence where necessary, and tenant-isolated projections; never silently migrate an entire record between tenants. Some asset records involve personal assignment/location data, vehicle tracking, licensed-user identities, confidential intellectual property or security/access information: minimise collection and disclosure, apply Privacy/Legal Compliance restrictions, retention, subject-rights handling, safe audit and appropriate consent/lawful basis. Safety obligations, statutory inspections, regulated equipment, property title, vehicle registration, charity restrictions and tax rules vary by asset type and jurisdiction; require specialist validation where relevant, not a universal hard-coded rule.

Optional screens should expose operational status and history accessibly, with internationalisation, WCAG 2.2 AA and Theme Manager's vocabulary, while keeping the core headless. Date/time semantics should use Clock's published contract where composed. Integration must respect ADR-0012's trivial composition target and ADR-0016's jointly acyclic dependency graph.

## Cross-capability exchanges

| Relationship | Originating facts | Resulting owner and boundary |
|---|---|---|
| Product → Asset | Model/specification or unique product reference | Asset owns the identified managed tangible unit or separately managed intangible right, relationships and history |
| Inventory ↔ Asset | Stock ownership/quantity/movement; authorised release from stock | Asset receives/returns an identifiable operational unit; Inventory owns stock correction; Accounting reconciles financial classification; prevent double-counting |
| Asset → Accounting | Acquisition, improvement, impairment indicator, renewal, expiry, disposal/transfer and operational-use/right evidence | Accounting decides recognition, useful life, depreciation/amortisation, impairment, revaluation, lease treatment and journal reconciliation |
| Order/Invoice/Billing → Asset | Purchase, hire, sale or service contract evidence | Asset links lifecycle and rights to verified originating facts without reowning obligations |
| Asset ↔ Warehouse/Logistics | Physical handover, delivery/collection and location confirmation | Handling owner owns execution; Asset owns accepted custody/placement state |
| Asset → Task/Workflow/Scheduler | Inspection due, repair needed, approval requested | Execution/approval mechanisms manage their own work; Asset validates and owns resulting operational state |
| Asset ↔ Identity/Authorisation | Identity references and access decisions | Asset owns assignment; IAM owns identities, memberships and permissions |
| Asset ↔ Integrations | Provider credentials, mappings, external observations and confirmations | Provider connector handles transport; Asset's authority policy controls acceptance and reconciliation |
| Licences, IP registries and contractual sources ↔ Asset | Verified right, licence, territory, seat, renewal or legal claim evidence | Asset owns operational stewardship and expiry/usage implications, never legal validity or the authoritative agreement itself |

## Dependency and information-exchange contract

**Design principle:** Asset must remain useful with its own native register, governed relationships, type-specific obligations, lifecycle and history. A conceptual information exchange is **not** automatically a mandatory package or Nuxt `extends` dependency. Each provider/consumer uses a declared public contract, host-supplied port, validated command or owner-published event. No cross-capability private table access or cyclic dependency is permitted.

### Minimum composition obligations

- **Host-supplied persistence:** Asset defines and owns its durable schema, migrations and repository/transaction semantics; a compatible connection is supplied by the host. Required persistence unavailable means changes fail closed; there is no global Persistence capability.
- **Trusted caller and tenant context:** caller/tenant/resource scoping, authenticated or explicitly trusted service actors where relevant, and reliable identifiers from the IAM composition. Identity/Authentication own their own assertions; Asset never invents identities or grants privileges from owner/assignee labels.
- **Server-side Authorisation:** mandatory for protected reads, exports, relationships and mutations, including contractor access, cross-group delegation and transfers. A missing or inconclusive required access decision fails closed.
- **Applicable compliance and privacy constraints:** legal holds, data-handling restrictions, lawful processing and retention are observed through published policy mechanisms as applicable; Asset does not invent jurisdiction-specific legal outcomes.
- **Time:** effective/recorded timestamps, expiry/renewal and historical reconstruction are mandatory semantics. Reuse Clock's published functions where composed; choose a documented trusted clock contract/host time source without implying a direct package dependency.
- **Native absence mode:** absent Product, Accounting, Inventory, purchase/procurement, third-party legal-party directory, external licensing, workflow, notifications or external asset-management software **must not prevent** ordinary registration, evidenced party-reference entry, allocation, inspection/evaluation, asset-specific entitlement control, local renewal recording and retirement. Asset may require specific provider evidence for narrowly defined configured transitions, such as a verified Inventory transfer or external authoritative renewal.

These are conceptual host obligations, **not** a final `capability.json` dependency declaration or approved interface signatures.

### Information Asset receives

| Source / capability | Information or command supplied to Asset | Mode and authority |
|---|---|---|
| **Identity / Authentication** | Trusted actor, tenant, group and service-principal references; authentication/assurance context | Essential security context via composition; IAM owns identities, membership, credentials and sessions |
| **Authorisation** | Operation- and resource-scoped allow/deny decisions | Mandatory for protected operations; Asset enforces decision and its own state invariants |
| **Configuration** | Validated tenant/group policy values and policy change provenance | Optional settings management; Asset owns asset-domain policy meaning, defaults and enforcement |
| **Clock** | Canonical time interpretation, calendars, zones and temporal calculations | Shared function where supplied; not authority for lifecycle policy |
| **Product** | Product family/model, specifications and descriptive reference data | Optional enrichment; Product's published data is authoritative for model definition |
| **Inventory** | Identified unit, stock release/receipt, stock movement and conversion confirmation | Optional except for a governed stock-to-asset conversion; Inventory owns stock facts |
| **Order / Invoice / Billing** | Verified acquisition, sale, lease, service and disposal source-document identifiers, commercial consideration and status | Optional evidence; each originating domain remains authoritative |
| **Accounting** | Accounting entity/book reference, recognised financial record reference, financial reconciliation result or financial-control hold where applicable | Optional cooperation; Accounting exclusively owns recognition, depreciation/amortisation, impairment and postings; Asset never recalculates its books |
| **Location / organisation-facing party sources** | Place/geospatial references, external legal-party or organisational references, verified address/registration evidence | Optional; Asset stores relevant time-bounded associations, not a competing geospatial/party master |
| **Legal Compliance / Privacy** | Applicable legal constraints, holds, personal-data disclosure and retention instructions | Enforced when applicable; technical access permission alone cannot waive obligations |
| **Task / Workflow / Scheduler** | Completed or failed work evidence, approval outcomes, due execution confirmations, with correlation | Optional; these capabilities own their execution/approval processes, not Asset's operational outcome |
| **Warehouse / Logistics** | Physical handling, collection, delivery, inspection, receipt and release evidence | Optional; Asset verifies and records resulting custody/placement change |
| **Integrations / specialist sources** | External fleet/telematics readings; licence seats, usage and expiry; IP registrations; insurer, maintenance and provider confirmations | Optional and provenance-labelled; originating source authority and validation required |
| **Document / Media / Storage** | Stable evidence/file references and authorised retrieval support | Optional; Asset owns its associations, not file bytes or unrelated published documents |
| **Direct users / authorised imports** | Registration facts, verified claims, assignment, operational observations, rights evidence and lifecycle requests | Native capability input, validated against domain policy and trusted actor/resource authority |

For a given asset type, some fields are inapplicable. A software right has no physical custodian or mileage; a forklift need not have licence-seat limits. No mandatory optional-provider list may make Asset unusable merely because adjacent domain capabilities are absent.

### Information Asset supplies to consumers

| Consumer / capability | Asset-owned output | Permitted use and authority boundary |
|---|---|---|
| **Accounting** | Asset ID and type; acquisition/commissioning evidence, improvements, impairment indicators, disposal/transfer, rights/expiry and provenance | Basis for independent financial evaluation and reconciliation, **not** an Asset-generated journal or carrying value |
| **Inventory** | Identity and confirmed commissioning, decommissioning, retirement or return-to-stock evidence; linked movement correlation | Reconcile physical unit conversion without duplicate stock or unapproved dual writes |
| **Product / commercial applications** | Managed-unit association, appropriate eligibility/availability and lifecycle flags | Context for reuse or disposal sale; no alteration to Product master or stock balances |
| **Booking / Order / shared-resource applications** | Authorised operational availability, restrictions, permitted-use windows and allocation status | Validate proposed allocation/use; Asset remains authoritative for its operational restrictions, Booking owns reservations |
| **Task / Workflow** | Inspection/renewal/repair/approval obligation, due date, target asset, priority and permitted action reference | Initiate assigned work or governed approvals; Asset validates any eventual state change |
| **Scheduler / Notifications** | Upcoming/overdue servicing, licence renewal/expiry and other events with policy-approved recipients or target references | Technical scheduling and delivery; Asset owns due criteria/outcome, Notifications owns delivery |
| **Warehouse / Logistics** | Authorised transfer/release request, asset identity, condition/custody requirements and acceptance state | Carry out physical work; external acknowledgement is not accepted custody without business confirmation |
| **Reporting / Search / Audit** | Tenant-filtered asset views, rights/obligation evidence, current and as-of relationships, change/decision provenance | Indexed/aggregated/evidential projections, not competing asset records |
| **Legal Compliance / Privacy** | Referenced evidence, rights/retention obligations, personal-data association and governed export/erasure outcomes | Compliance oversight; Asset obeys authoritative holds and access constraints |
| **Integrations / external systems** | Allowed records, scoped identity mapping, validated change events and reconciliation/export data | Push/synchronise only through explicit permissions and authority assignments |
| **Authorised application screens and clients** | Asset search/detail, assignment, custody, condition or entitlement, status, lifecycle and evidence views; validated command results | Field- and resource-scoped disclosure; no direct private persistence access |

**Event publication:** publish only confirmed Asset-owned facts (for example `AssetRegistered`, `AssetRelationshipChanged`, `AssetRestricted`, `AssetRenewalRecorded`, `AssetRetired`), with tenant/asset/correlation identifiers, provenance and effective/recorded time where appropriate. These are **illustrative event names**. Durable outbox ownership stays with Asset; Message Queue transports events and does not own them. Consumers must support replay, idempotency, out-of-order arrival and revocation/retention constraints.

### Interaction patterns and dependencies

1. **Query:** a consumer reads a filtered Asset view through Asset's public service; Asset evaluates trusted actor/tenant/resource context and applicable authorisation. Do not imply that accessing Asset authorises the consumer to expose every returned field.
2. **Command:** a consumer requests an Asset transition (e.g. assign, restrict, renew, record disposal) with idempotency/correlation and expected state; Asset owns validation, acceptance, history and resulting event.
3. **Event:** Asset publishes a confirmed business fact; consumers separately decide how that fact changes their own records. The event is not an instruction to write another capability's database.
4. **Governed handover:** Inventory↔Asset transfers require explicit source and destination confirmation with a durable correlation and reconciliation plan; absent coordination must not produce competing authoritative inventory/asset state.
5. **External authority:** for an explicitly assigned record slice and population, requests remain pending or fail safely when the selected authoritative provider is unavailable; an adapter cannot create authority merely by being installed.
6. **No cyclic package imports:** an apparent two-way domain relationship is mediated by public contracts, host-supplied ports or event subscriptions, chosen so the final combined contract dependency and Nuxt extension graph stays acyclic. The eventual manifest must declare actual required/optional edges after inspecting the relevant published root contracts.

### Contract safety and response semantics

Public responses distinguish **owned facts**, **referenced external assertions**, **derived operational views**, **unverified/pending evidence**, and **provider failure**. Expose source, confidence/verification and as-of time where needed to avoid mistaking a projected value for authoritative data. Rights or ownership assertions are not legal judgements; the display of an Accounting balance remains Accounting-owned. Protected operations fail closed if required IAM or persistence is unavailable; absent optional providers degrade only their own enrichment or integrations. Business outcomes are never inferred solely from transport receipt.

## Conceptual acceptance scenarios

1. **Independent operation:** a small club records its equipment, custodians, loan/return dates, inspections and condition with no accounting connector or external asset system.
2. **Third-party ownership:** a supplier owns a forklift; a business leases and manages it; an employee uses it. Ownership, usage right, custody and assignment appear separately with effective dates. Accounting determines whether a right-of-use asset is recognised under the selected reporting basis.
3. **Third-party custody:** an organisation's machine is sent to a contractor. Ownership stays constant, custody changes with collection and receipt evidence, operational availability and inspection obligations update appropriately.
4. **Charity/club governance:** a donated asset has uncertain title/value and restricted disposal. Asset records evidence and restrictions; governance and accounting decisions are not fabricated.
5. **Inventory conversion:** a serialised item stops being sale stock and is commissioned for business use. Inventory and Asset reconcile the unit's transition, while Accounting controls financial reclassification; no duplicated stock or fixed-asset posting.
6. **Condition and safety:** failed inspection marks equipment unavailable; a later approved inspection releases the restriction, retaining history and approval provenance.
7. **Disposal:** authorised sale/scrap/loss records physical disposition, title transfer evidence, outstanding obligations and Accounting source references; no automatic erasure or invented gain/loss.
8. **External outage:** externally authoritative inspection record cannot be confirmed; pending state remains visible, duplicate retries are idempotent and no false pass is asserted.
9. **Security:** users cannot see another tenant's assets, infer personal movements through reports or self-approve asset transfers by altering submitted party identifiers.
10. **Correction:** incorrect custody or location entry is corrected with attribution and effective date while preserving original evidence, without silently modifying financial postings.
11. **Intangible rights:** a charity registers a licensed software product with named-user allocations and renewal expiry, and a separately identifiable territorial IP right; Asset records their effective entitlements, obligations, assignments and renewal evidence without acting as licence server or adjudicating legal rights.
12. **Differentiated status:** a valid software licence with all seats allocated remains legally valid but has no free allocation; a vehicle can be physically functional yet legally restricted pending inspection. No universal `active` flag conflates these conditions.
13. **Historic transfer and portability:** an expired trademark right or retired building remains traceable with applicable retention, time-bounded party relations, superseded evidence and exportable history.

## Open architectural questions

- **A1 — Scope (resolved in conceptual proposal):** Asset **includes tangible and intangible assets**, including identifiable software licences, intellectual-property rights and managed contractual rights. Inclusion is based on independent asset identity, stewardship, rights/obligations and lifecycle; not every contract, dataset or transient service entitlement automatically becomes an asset. Specialist validation applies. Any legal/financial recognition remains with its authoritative owner.
- **A2 — Title and contracts:** how to reference independently authoritative contracts/property deeds, contested ownership claims, beneficial ownership, co-ownership and liens without building a legal title registry?
- **A3 — Maintenance execution:** which inspections/repairs belong as Asset-owned history versus Task/Workflow/process work orders? Proposed: Asset owns obligations and results, execution may be delegated.
- **A4 — Financial subledger:** does Accounting own a native fixed-asset subledger and lease schedules? Proposed: yes for recognised financial records; Asset retains operational facts.
- **A5 — Stock conversion:** what exact cross-capability handover protocol guarantees one operational physical-unit authority and reconciles Inventory/Accounting without distributed dual writes?
- **A6 — External authority:** what granularity, conflict rules and cut-over guarantees are required to delegate some asset populations or record types to external systems?
- **A7 — Complex assets:** how should parent/child systems, interchangeable components, buildings/sites, shared or fractionally owned assets and mobile assets be modelled without over-designing the base?
- **A8 — Regulated specialists:** which safety/inspection, fleet, property and charity requirements must be externally configurable or delegated under applicable jurisdiction?
- **A9 — Party model:** how are verified external legal parties and contracts referenced without mistaking IAM groups for legal persons?
- **A10 — Source evidence:** how are valuations, warranty certificates, leases, photos and inspection evidence referenced without copying other capabilities' documents or storage?

## Review status and sources

**Established:** governing classification, independent ownership and security rules, separation of Inventory/Accounting and existing provisional notes.
**Proposed:** the complete operational asset responsibility, independently time-bounded party relationships, native service scope and external authority modes described above.
**Open:** A2–A10 and any specialist legal/accounting validation. A1 is resolved as a **proposed scope decision**, pending conceptual approval.
**Unverified:** an Asset repository, published API, implementation, provider capabilities and acceptance-test results.

External conceptual references (informative, not requirements automatically applicable to every tenant):
- ISO 55000:2024, *Asset management — Vocabulary, overview and principles*: https://www.iso.org/standard/83053.html
- IFRS Foundation, IAS 16 *Property, Plant and Equipment*: https://www.ifrs.org/issued-standards/list-of-standards/ias-16-property-plant-and-equipment/
- IFRS Foundation, IFRS 16 *Leases*: https://www.ifrs.org/issued-standards/list-of-standards/ifrs-16-leases/

Related candidate records: [Accounting](../accounting/capability-record.md), [Inventory](../inventory/capability-record.md), [Product](../product/capability-record.md), [Order](../order/capability-record.md), [Warehouse](../warehouse/capability-record.md), [Location](../location/capability-record.md), [Task](../task/capability-record.md), [Workflow](../workflow/capability-record.md), [Legal Compliance](../legal_compliance/capability-record.md).

**Conceptual sign-off:** ready for review of the proposed boundary; not implementation-ready and not an accepted governing contract.
