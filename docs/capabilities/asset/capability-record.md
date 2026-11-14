# Capability Record — Asset

**Status:** Proposed Domain capability; conceptual review awaiting approval. No implemented package or public API is asserted.
**Review date:** 14 November 2026.
**Governing baseline:** `nuxt-layers/architecture-rules` `master` at `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.
**Blueprint baseline:** `nuxt-layers/architecture-blueprint-review` `master` at `e802386e256340c7cd7310398d02c30168535e17`.
**Evidence:** The governing catalogue lists `asset` as owned/controlled asset lifecycle, assignments and valuation references, excluding generic sale stock. The working catalogue calls it a Domain candidate. A lookup and organisation repository search found no `nuxt-layers/asset` repository; hence there is no Asset root `CONTRACT.md` or verified implementation to evaluate. Existing Accounting, Inventory and Product notes are provisional blueprint evidence, not accepted interfaces. Proposed design below is not normative.

## Summary and classification

**Asset** maintains the operational register and lifecycle of individually identifiable assets an organisation **owns, controls, manages, holds or is responsible for**, including equipment, machinery, tools, vehicles, fixtures, facilities and buildings. It records what the asset is, its accountable management context, its relationships to other parties, where it is, who has custody, whether it is safe and available for use, and what has happened to it.

Its independent responsibility is **operational asset identity, stewardship, condition and lifecycle**, not the financial ledger or generic saleable stock. It is a credible **Domain capability** because these records and obligations persist independently of purchasing, accounting, inventory or a particular organisation type. A separate implementation repository is not approved merely by this review. The capability can be implemented as a headless core with optional separable presentation, using the governing Capability Standard.

The intended scope is deliberately broader than owned fixed assets but narrower than everything that might have economic value. ISO 55000:2024 supplies useful asset-management terminology and lifecycle principles, not a requirement to build an ISO 55001-certified management system or a generic intangible-asset registry. Specialist asset classes may use validated extensions without transferring authoritative responsibility.

## Ownership and relationship model

**Proposed central rule:** physical/legal ownership, contractual rights, operational responsibility, custody, assignment, location and accounting recognition are **separate dimensions**. They can concern different parties concurrently and change on different dates.

| Dimension | Conceptual meaning | Responsible source |
|---|---|---|
| Asset identity | A particular physical unit, complex asset or managed asset system; unique identifier, classification, serial/registration references and traceability | **Asset** |
| Legal title/ownership claim | Identified owner or owners, ownership shares where applicable, effective dates and evidence; recorded as an evidenced assertion, not a legal determination | **Asset** holds relevant relationships and provenance; applicable legal records/agreements govern disputed title |
| Operating or managing organisation | Party responsible for stewardship, maintenance, policy and operational decisions, with defined scope and effective period | **Asset** |
| Control and right of use | Lease, hire, loan, licence, concession, bailment or other documented entitlement/restriction; distinct from title | **Asset** references rights and operational constraints; authoritative contract and legal terms stay with their owning source |
| Custody | Party currently holding, transporting or safeguarding the item; receipt, handover and return evidence | **Asset** owns the asset custody history; Logistics/Warehouse may supply movement facts |
| Assignment | Named person, team, project, site or other permitted context using or accountable for the item; time bounded | **Asset**; Identity owns identities/groups, not asset assignments |
| Location | Current declared/confirmed location and history, with optional geographic or premises reference | **Asset** owns asset placement; Location owns reusable place/geospatial references |
| Accounting recognition | Whether, by whom and on what basis an owned asset or right-of-use asset is recognised and valued | **Accounting**, not Asset |
| Operational valuation evidence | Acquisition price, appraisal, insured value, replacement estimate, condition and external valuation reference, each with type, date, currency, source and uncertainty | **Asset** stores provenance/references; Accounting owns recognised value, depreciation and postings |

Relationships must support multiple legitimate parties over time and simultaneous non-conflicting roles. No single `ownerId` or `assignedTo` field should collapse these concepts. The same party can hold several roles; the application must not infer rights or access solely from those roles. Claims about title may be contested or unknown: preserve provenance, verification and dispute status rather than falsely asserting legal certainty. A party's role may be external to the tenant and must be represented without creating a fraudulent Identity group or requiring the other party to use the application.

**Examples:** a supplier owns a leased forklift operated by a business; a charity owns a van held by a contractor; a club owns facilities maintained by a hired facilities manager; an organisation holds a loaned instrument; a company owns equipment deployed at a customer's premises. None requires the owner, custodian, operator and accounting entity to be identical.

## Proposed authoritative records

Asset should own:
- **Asset register:** immutable internal identity, class/type, description, identifying markings, manufacturer/model references, serial number/registration as applicable, composite/parent-child membership and source provenance. A model or catalogue item is not automatically a physical asset.
- **Asset lifecycle:** acquisition/onboarding evidence, verification, commissioning, operational use, temporary unavailability, maintenance, suspension, decommissioning, disposal, transfer and archival, retaining event history. State must reflect real-world events, not erase them.
- **Operational relationships:** title claims, managing party, contractual entitlement references, assignment, custody, location, responsible persons/teams, effective periods, handover/acceptance and obligations. Track their sources, effective and recorded dates.
- **Condition and performance:** inspections, assessments, usage/meter readings, faults, damage, incidents, maintenance/service/repair history, warranties, certificates and restricted-use decisions with supporting evidence. Record work orders or specialist maintenance execution only to the extent this boundary is independently justified; do not duplicate Task/Workflow execution.
- **Operational controls:** lifecycle approvals, permitted transitions, inspection schedules/rules, hold and release flags, overdue and unavailable states, evidence requirements and retention applied from approved policy.
- **Operational financial references:** acquisition/disposal consideration and cost evidence, insurance/insured values, estimates and identifiers linking to Accounting transactions, without becoming a financial subledger.
- **Provenance and export:** history and verified source references; explain material changes, corrections, reconciliation conflicts and external-authority status.

**Non-ownership:** Product owns product/model definitions and saleable offers; Inventory owns stock quantities, reservations and movements; Warehouse/Logistics own handling and transport work; Accounting owns capitalisation, recognised fixed/right-of-use assets, depreciation, impairment, financial revaluation and the journal; Invoice/Order/Billing own their financial source documents; Identity owns identifiers, groups and membership; Authorisation owns access decisions; Legal Compliance supplies applicable constraints; Configuration supplies scoped setting mechanisms; Clock supplies time semantics; Integrations manages external application connections. Asset does not decide legal title or create binding lease obligations merely by recording a relationship.

## Native functionality and invariants

A usable **native Asset** works without optional accounting, maintenance, telematics or equipment-management providers:
1. Register, import and identify individual assets; resolve duplicates and reconcile serialised records without silent merging.
2. Set and verify the management scope, parties, title claims and documentary references; record that evidence can be incomplete or disputed.
3. Assign and hand over assets to people, organisations, locations or projects with clear effective periods, receipt/return and accountability.
4. Record condition, faults, inspections, servicing, repairs, safety restrictions, warranties, usage and downtime; find due/overdue obligations.
5. Control commissioning, use, movement, suspension, reinstatement, transfer, decommissioning, disposal and archival using authorised, auditable transitions.
6. Search and report by asset, location, manager, assignment, custodian, ownership claim, class, condition, compliance status, availability and history; export authorised records.
7. Associate evidence, acquisition/disposal facts and financial reference identifiers without calculating recognised depreciation or accounting balances.
8. Recover from erroneous or delayed events via explicit corrections, compensating actions and reconciliation, never history rewriting.

**Required conceptual invariants:** stable asset identity; no double-active incompatible exclusive-custody assignment for the same unit/time unless the asset type expressly permits shared custody; role changes have provenance and effective dates; recorded time and event time remain distinguishable; a disposal or decommission event does not automatically extinguish contractual, accounting or retention obligations; an asset cannot be represented as available while subject to an effective safety hold; external failure cannot silently authorise a prohibited action; data from one tenant cannot be read or altered through another tenant's access scope. Composite assets/parts, partial ownership and shared locations require explicit supported rules, not assumptions.

**Illustrative lifecycle:** proposed/onboarding → identified/verified → commissioned/available → assigned/in use ↔ returned/available → restricted, under maintenance or out of service → reinstated or decommissioned → transferred, disposed or retired → archived. These are conceptual examples, **not a mandatory single linear enum**. Title, custody, assignment, condition, financial recognition, warranty and inspection status have distinct concurrent lifecycles.

## Conceptual services (proposals, not existing APIs)

- Asset registration/identity, classification, evidence attachment and duplicate resolution.
- Owner/right/manager/custodian/assignment/location relationship queries and governed changes, including as-of historical views.
- Asset acceptance/receipt, custody transfer, allocation and return commands with acceptance evidence.
- Condition, inspection, defect, maintenance, warranty, meter and availability recording and queries.
- Lifecycle transition validation, exceptional hold/release, loss/theft, disposal and transfer recording.
- Operational valuation/reference evidence, Accounting linkage, reconciliation and exception reporting.
- Import/export, synchronisation and event publication **after** authoritative asset changes.

Any future public contract must document stable data shapes, error codes, permissions, idempotency, expected dates/time zones, missing-provider behaviour and appropriately scoped event identifiers. Do not impose provider SDK types or application-specific organisation structures.

## External authority and integrations

The default is **native Asset authority** for operational asset records. Optional external asset/fleet/maintenance/property systems can be read as evidence, synchronised as projections or made authoritative for an **explicitly selected domain slice and asset population**, subject to approved policy. Define exactly which owner holds each record type (e.g. asset identity, inspections, meters, custody) at any time; merely installing a connector does not transfer authority.

A transfer requires authorisation, mapping, cut-over, version/identifier reconciliation, unresolved-work handling, verification and rollback policy. While an authoritative external system is unavailable, preserve its authority: queue only safe, explicitly supported requests or mark operations pending/unavailable, not silently take over or assert successful completion. Transport acknowledgements are not evidence that the business operation succeeded. Preserve source timestamps, third-party identities, idempotency and conflict resolution.

Optional domain relationships include Accounting and external accounting packages, Inventory/Product, Order/Invoice, Warehouse/Logistics, Task/Workflow/Scheduler/Notifications, Location, reporting, insurers, telematics, external maintenance providers and document/evidence storage. None is thereby a mandatory Nuxt package dependency.

## Configuration, security, compliance and presentation

Asset owns the meaning and enforcement of its **domain rules**, while Configuration can manage validated declarations, scopes, precedence and governed values through published contracts. Potential configurable policies: asset categories and hierarchies, identifier requirements, inspection/service intervals, authorised transfers, custody acceptance, status transitions, evidence requirements, approval thresholds, insurance/usage limits, retention and restricted-use conditions. No generic universal legal policy is implied.

All protected reads and changes require **server-side Authorisation** on tenant, resource, actor and action; role labels such as legal owner, manager or employee do not automatically grant permissions. Guard cross-tenant transfers with explicit authority, bilateral evidence where necessary, and tenant-isolated projections; never silently migrate an entire record between tenants. Some asset records involve personal assignment/location data, vehicle tracking or confidential security/access information: minimise collection and disclosure, apply Privacy/Legal Compliance restrictions, retention, subject-rights handling, safe audit and appropriate consent/lawful basis. Safety obligations, statutory inspections, regulated equipment, property title, vehicle registration, charity restrictions and tax rules vary by asset type and jurisdiction; require specialist validation where relevant, not a universal hard-coded rule.

Optional screens should expose operational status and history accessibly, with internationalisation, WCAG 2.2 AA and Theme Manager's vocabulary, while keeping the core headless. Date/time semantics should use Clock's published contract where composed. Integration must respect ADR-0012's trivial composition target and ADR-0016's jointly acyclic dependency graph.

## Cross-capability exchanges

| Relationship | Originating facts | Resulting owner and boundary |
|---|---|---|
| Product → Asset | Model/specification or unique product reference | Asset owns the actual managed unit, operational identity and history |
| Inventory ↔ Asset | Stock ownership/quantity/movement; authorised release from stock | Asset receives/returns an identifiable operational unit; Inventory owns stock correction; Accounting reconciles financial classification; prevent double-counting |
| Asset → Accounting | Acquisition, improvement, impairment indicator, disposal/transfer and operational-use evidence | Accounting decides recognition, useful life, depreciation, impairment, revaluation, lease treatment and journal reconciliation |
| Order/Invoice/Billing → Asset | Purchase, hire, sale or service contract evidence | Asset links lifecycle and rights to verified originating facts without reowning obligations |
| Asset ↔ Warehouse/Logistics | Physical handover, delivery/collection and location confirmation | Handling owner owns execution; Asset owns accepted custody/placement state |
| Asset → Task/Workflow/Scheduler | Inspection due, repair needed, approval requested | Execution/approval mechanisms manage their own work; Asset validates and owns resulting operational state |
| Asset ↔ Identity/Authorisation | Identity references and access decisions | Asset owns assignment; IAM owns identities, memberships and permissions |
| Asset ↔ Integrations | Provider credentials, mappings, external observations and confirmations | Provider connector handles transport; Asset's authority policy controls acceptance and reconciliation |

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

## Open architectural questions

- **A1 — Scope:** should non-physical assets (software licences, intellectual property, contractual rights, data assets) fall outside the initial operational Asset boundary, with future specialists? Proposed: initially physical/tangible operational assets; allow typed references to recognised rights without universal intangible management.
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
**Open:** A1–A10 and any specialist legal/accounting validation.
**Unverified:** an Asset repository, published API, implementation, provider capabilities and acceptance-test results.

External conceptual references (informative, not requirements automatically applicable to every tenant):
- ISO 55000:2024, *Asset management — Vocabulary, overview and principles*: https://www.iso.org/standard/83053.html
- IFRS Foundation, IAS 16 *Property, Plant and Equipment*: https://www.ifrs.org/issued-standards/list-of-standards/ias-16-property-plant-and-equipment/
- IFRS Foundation, IFRS 16 *Leases*: https://www.ifrs.org/issued-standards/list-of-standards/ifrs-16-leases/

Related candidate records: [Accounting](../accounting/capability-record.md), [Inventory](../inventory/capability-record.md), [Product](../product/capability-record.md), [Order](../order/capability-record.md), [Warehouse](../warehouse/capability-record.md), [Location](../location/capability-record.md), [Task](../task/capability-record.md), [Workflow](../workflow/capability-record.md), [Legal Compliance](../legal_compliance/capability-record.md).

**Conceptual sign-off:** ready for review of the proposed boundary; not implementation-ready and not an accepted governing contract.
