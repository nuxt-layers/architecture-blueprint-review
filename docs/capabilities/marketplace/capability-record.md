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

## Cross-capability note — Marketplace commissions and multi-party charges (15 November 2026)

**Proposed reciprocal relationship, not a completed Marketplace review.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) may assess marketplace fees, seller commissions and service charges only from a versioned, authorised marketplace agreement and source transaction/fulfilment evidence. Marketplace retains buyer/seller role, fee agreement, seller entitlement and allocation facts; Billing owns calculated commercial charge lines by issuer/debtor/beneficiary and period. Payment Gateway/financial domains own capture, payouts and settlement. No automatic entitlement to levy commission, transfer funds or merge unrelated sellers' financial records follows from Marketplace participation. Disputes, fee overrides and duplicate source events require attributable adjustments and separation of duties. Actual contract shapes and supported provider modes remain for Marketplace's own review.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Commerce safety and merchant controls:** Marketplace retains seller participation, eligibility, listing rules and its own restriction/reinstatement outcomes. Identity verification, verified authority to act for an organisation, merchant standing, payment risk and transaction outcomes are separate facts. KYC/KYB/anti-fraud data should enter by properly owned verification/provider interfaces with privacy/cost controls; universal KYC and smart-contract escrow are **not** presumed OSA mandates. Content Security assesses text/images/links; proposed Moderation owns reports/cases; Marketplace enforces actual listing/seller action with receipts; Hub indexes remain derived.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Marketplace owns seller-participation/merchant eligibility, listing permissions, restrictions and reverification outcomes; it consumes purpose-limited proofs of person/company identity and authority, risk evidence, and lawful KYB/KYC requirements from appropriate owners/providers. Identity account existence is not seller legitimacy. Differentiate legal entity, authority to trade, fraud risk, permitted goods and payment evidence; do not mandate universal KYC or blockchain escrow.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Merchant proofing/representation can be provided by Verification's purpose-limited qualified assertions, but Marketplace retains seller eligibility, trade restrictions, reviews and commercial outcomes. Identity-proofed sellers can still be fraudulent, and representation mandates may expire independently. KYB provider status, cost, revocation and local legal scope remain explicit.

## Marketplace conceptual review — 19 November 2026

**Status: PROPOSED for owner review; not yet owner-approved, published as a runtime contract, implemented or legally certified.** Review branch `review/marketplace-conceptual`, [draft PR #91](https://github.com/nuxt-layers/architecture-blueprint-review/pull/91). Governing opening baseline: `architecture-rules/master` `b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint opening baseline: `architecture-blueprint-review/master` `6dac83a03da8704f7945ee1bc894f2248300445a`. The governing [catalogue](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/catalogue.md) describes Marketplace as a **Domain candidate** for multi-seller participation, listings and marketplace-specific commercial operations. No `nuxt-layers/marketplace` implementation repository was found in the organisation repository-name search; therefore there is no verified root `CONTRACT.md`, deployed API or runtime acceptance evidence. This conceptual contract is **not** an assertion that its interfaces currently exist.

### Purpose, classification and independent justification

**Proposed Domain capability:** Marketplace governs a multi-party trading venue: who may participate as buyer/seller, which seller may offer which seller-specific listing in which marketplace, under what market rules, commercial commission agreements and restrictions, with what listing publication, suspension and exit state. Multiple autonomous sellers must retain separate domain authority, tenant isolation, obligations and financial ownership. The separate lifecycle of merchant participation, marketplace publication and seller-specific agreements justifies this bounded Domain responsibility rather than a Shop composition or a search/presentation utility. A single-seller storefront can operate without Marketplace.

A Marketplace instance is a configured trading venue, not a new Identity tenant, legal entity, general-purpose Product catalogue, payments intermediary or automatic authority over its participants. An operator may host multiple independently scoped marketplaces. Sellers may trade on multiple markets; participation is not an Identity group membership, verified legal title, or authorisation grant. Buyers and sellers may be distinct tenants or external counterparties, subject to explicit scope/representation rules.

**Marketplace owns (proposed):** marketplace identities/configured operating scope; seller and buyer participation **within a specific venue**; requests/approvals/restrictions and eligibility outcomes; venue-specific seller agreement versions/commission and fee entitlements; listing **offer/publication records** binding authoritative Product/service or seller offer references to venue, seller, visibility, jurisdiction and validity; seller-specific merchandising, category/placement and market-specific policies; commission allocation **evidence**, marketplace dispute/appeal actions for its decisions, and export/exit history; its own events and durable outbox.

**Marketplace does not own:** Identity principals, tenant hierarchy or memberships; civil identity/KYB proofs; Authentication or Authorisation grants; Product's intrinsic specification/ownership; Pricing's authoritative item prices, tax or discounts; Inventory's stock; Order's accepted purchase/line allocation and fulfilment; Billing's assessed charge; Invoice's issued document; Accounting's ledger; Payment Gateway's funds authorisation/capture, split settlement, refunds or payouts; Reviews' ratings; Moderation's report/case; Content Security's safety assessment; Legal Compliance's legal determination; Search's derived index; Integrations' credentials/provider transport; Audit's evidence custody. A seller commission is contractual eligibility evidence, **not** a charge, deduction or payment instruction.

### Native operating mode and lifecycle

A self-hosted native venue needs an authoritative Marketplace store, versioned policies and agreements, seller onboarding and consent, a scoped eligibility decision, listing submission/validation, moderation/security holds via public evidence, manual/operator publication when specialised providers are absent, visibility/restrictions, read access, seller withdrawal, delisting, review/appeal, commissions evidence and durable history. It can publish listings without an external marketplace provider. Purchases, funds movement and fulfilled-order completion **require their independent capability owners**; without them the marketplace can operate in **catalogue/enquiry-only mode** and must not claim transactions or settlement.

Conceptual entities: `Venue` (operator/tenant, jurisdiction/scope and version); `Participation` (subject/role/representation, submitted→pending checks→approved/limited/rejected→suspended/revoked/closed); `MerchantEligibilityDecision` (reason, evidence reference, valid-until); `SellerAgreement` (version, commission/fee schedule reference, consent, effective interval, expiry/termination); `Listing` (venue/seller, source product/offer refs and revisions, display/territory restrictions, draft→submitted→held/approved→published→suspended/withdrawn/expired, with revision history); `MarketAllocation` (read-only attribution/commission entitlement evidence linked to Order lines and seller agreement, not a Billing line); `MarketCaseAction` (listing/participant restriction, appeal and outcome); `PublicationReceipt` (host/external channel acknowledgement distinct from authoritative listing state); and owned outbox records. These are public business concepts, **not** prescribed private database tables.

All state-changing commands validate caller/tenant scope, role and representation, current resource revision, policy and legal effective versions, prohibited-goods/safety evidence where applicable, rate and abuse controls, and an idempotency key for retryable side effects. Protected approvals and overrides require attributable reasoning and separation of duties where risk requires it. Revoked eligibility blocks new listings/transactions without silently rewriting prior Orders. Revocation, seller migration and venue closure preserve required evidence and legally permissible export. Stale external provider confirmation never upgrades a local state to completed.

### Idealised public **inbound** interfaces

The `required` designation means required **for the particular operation**, not a compulsory installation of every cooperating capability.

| Source and kind | Supplied information and purpose | Authority, validation and absence/uncertainty |
|---|---|---|
| Host/authorised operator, commands | Create venue, choose market mode, approve policy/agreement, invite/approve/restrict seller, approve listing, resolve market appeal | Marketplace owns venue decision, server Authorisation owns permission; missing/denied decision fails closed; no client-only grant; **required** |
| Identity/Authentication/Authorisation, trusted context | Tenant, actor/organisation relationship, scoped representation, current assurance and `decide` for action/resource | Identity owns relationships, Authentication session assurance, Authorisation access; require scope and fresh decision; unknown/expired/denied fails closed; **required** for protected acts |
| Product and seller offer owners, source facts | Canonical item/service identity, description/specification, permitted seller source version, availability of an offer | Product/offer owner owns item facts; Marketplace owns venue listing association; stale/unresolved source holds publication; **conditional** |
| Pricing, source facts | Seller-facing applicable price/quote/currency/discount provenance where the listing displays an amount | Pricing owns price semantics; validate version, currency, validity, jurisdiction; unknown must be marked unavailable, never invented; **conditional** |
| Inventory or fulfilment/service owner, source facts | Stock/service availability and fulfilment eligibility, freshness and limitations | Source domain owns quantity/availability; unknown is not 'in stock'; **optional/conditional** |
| Verification and qualified KYB/KYC sources, evidence | Purpose-limited identity/organisation representation, expiry, revocation, provenance and approved risk evidence | Verification owns claim lifecycle; Marketplace interprets merchant eligibility; unverified ≠ approved, expired proof triggers holds as policy requires; **risk/jurisdiction conditional** |
| Legal Compliance, Privacy, Content Security, Moderation, constraints/evidence | Applicable trading restrictions, jurisdiction, age/product rules, content safety verdicts, reports/cases/appeals and deletion/retention controls | Each specialist owns its evidence/case; Marketplace enforces market-specific listing/seller action; necessary unknown constraints hold affected operation; **conditional**, not universal KYB |
| Configuration, effective settings | Approved venue/seller policy references, markets, publication and consent rules, commission configuration, effective versions | Configuration owns setting scope/provenance; Marketplace validates domain rules against accepted ADR-0018/legal floors; **required where configured** |
| Order, source evidence | Seller-by-line purchase/acceptance, amendments, cancellations and finalised attribution | Order owns transaction truth; Marketplace computes only marketplace agreement linkage; duplicate/stale events reconcile; **conditional for commission evidence** |
| Billing, Payment Gateway, Invoice, Accounting, outcome evidence | Fee assessment, payment/settlement/payout, document and ledger status for allowed seller/operator views | Each downstream owner alone guarantees its state; pending/unknown never equals paid or posted; **conditional** |
| Integrations/external market provider, provider evidence | Approved connection/scope, verified remote listing IDs, publishing acknowledgements and read-back state | Integrations owns connection/remote authenticity; Marketplace determines local authoritative state according to approved mode; timeout yields `unknown`; **optional** |
| Clock, Scheduler, Workflow, MQ, technical context | Effective timestamp/timezone, scheduled expiry, authorised orchestration and message transport | Clock owns temporal semantics, Marketplace own expiry decision; scheduling/transport cannot assert business completion; **conditional ports** |

### Idealised public **outbound** interfaces

| Interface → consumers | Meaning, owner and guarantee | Status, scope and disclosure |
|---|---|---|
| `getVenuePolicyAndStatus`, `getMarketCapabilities` → authorised sellers, hosts, Shop/GUI | Marketplace's effective market participation/listing rules and supported venue operating mode, **not** universal legal approval | Venue, policy version/effective interval, supported/disabled/unknown and tenant/role visibility |
| `getParticipation`, `listSellerEligibility` → venue operator, authorised seller, Order/Shop | Authoritative venue participation, review/hold/restriction status and permitted marketplace seller actions; **not** civil identity validation or a server permission grant | Venue/seller/subject, decision revision/effective time, confidentiality filtered by role |
| `getListing`, `listListings`, `getListingAvailability` → Shop, Search, Federation/Hub, buyer UI | Market-authoritative listing publication/withdrawal and originating Product reference; Product/Price/Inventory facts remain attributed to source, not reowned | Source revisions, seller, jurisdiction, visibility, freshness/completeness and provenance; public result only when released |
| `getAgreement`, `getCommissionAttribution` → seller/operator, Billing, Order, Reporting | Effective seller agreement and **eligible attribution/fee basis** for specific order lines; not charge calculation, tax posting or payout | Agreement/source Order version, parties and beneficiaries, effective date, dispute flag; financial details least-privilege |
| `getMarketAction`, `getAppealStatus` → seller/operator, Moderation, Audit | Marketplace's own enforceable participation/listing action, reason/evidence reference, review and appeal result | Case/action ID, version, valid-from/until, privacy-filtered reasons and appeal visibility |
| `getPublicationReceipt`, `getProviderSyncStatus` → authorised operator, Integrations, Observability | Confirmed local state versus remote accepted/unknown/failed publication status; never invent remote completion | Provider, mapping version, attempts, checked-at, error category, reconciliation handle |
| `exportMarketRecords` and market-owned lifecycle events → authorised export, Reporting, Audit, Search, MQ subscribers | Portable non-secret participation, agreements, listings and attributable history; events only on **committed Marketplace-owned changes** through durable outbox | Tenant/venue, event ID, entity/revision, source/policy, correlation, effective time, redaction and retention policy |
| Sanitised metrics → Logging/Observability/Reporting | Operational availability, risk holds, throughput and diagnostic status; not personal dossiers, financial settlement or Audit evidence | Aggregation, provenance, restricted tenant/audience and retention |

### Conceptual commands, queries and events

**Commands (illustrative, not published signatures):** `createVenue`, `configureMarketPolicy`, `requestParticipation`, `approve/restrict/reinstate/closeParticipation`, `registerSellerAgreement`, `submit/revise/approve/publish/suspend/withdrawListing`, `recordMarketRestriction`, `resolveMarketAppeal`, `requestRemotePublication`, `reconcileRemotePublication`, `requestMarketExport`. An accepted command acknowledges a locally committed step, not necessarily completed external publication/Order/payment. Return typed statuses (accepted/completed/held/rejected/unknown) with stable reason codes, appropriate revision and recovery handle; reject invalid transitions or unsupported functions explicitly. Use optimistic concurrency and idempotent retries.

**Queries:** venue and effective-policy reads, scoped seller participation, listing discovery and detail, agreement and fee-attribution evidence, action history and appeals, export progress and external publication reconciliation. Report source timestamp, completeness and stale/unknown explicitly. Buyers never query confidential seller proofing or cross-tenant commercial arrangements by default.

**Events:** `ParticipationRequested/Approved/Restricted/Reinstated/Closed`, `SellerAgreementActivated/Terminated`, `ListingPublished/Changed/Suspended/Withdrawn`, `MarketplaceActionResolved`, `MarketplaceAttributionRecorded/Corrected`, `ExternalPublicationReconciled`. Names are provisional; only committed owned facts are emitted. At-least-once delivery may duplicate/reorder; consumers deduplicate by event identity and source revision, fetch current authorised owner state, and never treat a received event as permission or as evidence of Order/payment completion. No exactly-once distributed processing promise.

**Shared envelope is contextual, not a universal request class:** relevant tenant/venue/seller references and permission context; actor and assurance where required; resource revision; effective policy/agreement version; source Product/Order/Price revision; idempotency/correlation; Clock timestamps; provider provenance/receipt; verified-vs-unknown completion. The public surface avoids private provider SDK/persistence types. Every protected operation is server-authorised; no parent-tenant access or seller cross-market grant arises by implication (accepted ADR-0017). Policy must distinguish non-overridable security/legal floor from configurable venue rule (accepted ADR-0018). No circular package imports or private schema coupling; use host-wired ports, events or composition.

### Cross-capability cooperation and authority

| Cooperating boundary | Input Marketplace needs / output Marketplace supplies | Dependency and unavailable mode |
|---|---|---|
| Identity, Authentication, Authorisation | Actor/tenant/representation/assurance/permission → scoped participation/listing/action facts | Essential protected-operation IAM; deny/indeterminate = blocked |
| Product, Pricing, Inventory, seller-offer domain | Versioned catalogue/price/stock → published seller-venue listing ref and current venue restrictions | Product required for catalogue-backed listings; Pricing/stock conditional; stale facts held/flagged |
| Order, Shop | Order-accepted buyer/seller line/evidence → eligibility/offer visibility, agreement and attribution; Shop presents composite user journey | Order essential only to transact; Shop optional composition, cannot override Market or Order authority |
| Billing, Invoice, Payment Gateway, Accounting | Their final fee/document/payment/posting outcomes → fee entitlement/commission allocation evidence, held/disputed flags | Conditional financial cooperation; Marketplace never charges, moves funds or posts ledger |
| Verification, Legal Compliance, Content Security, Moderation | Qualified proof/constraints/verdicts/cases → local eligibility, listing/seller enforcement and action receipt | Risk- and jurisdiction-conditional; absent necessary proof/verdict = held; specialist retains own source |
| Reviews, Search, Publisher, Media, Federation | External rating/index/publication/media evidence → authoritative released listing and venue visibility/restriction | Optional reads/derived views; no Hub ownership of source records; removed listing propagates revocation |
| Integrations, Clock, Configuration, Workflow, Scheduler, MQ | Provider connectivity, time/settings and orchestration → authorised commands, owned revision/status and outbox events | Optional provider/no remote mode; critical service absence fails affected function safely |
| Audit, Logging, Observability, Reporting, Privacy | Evidential intake/diagnostics/analytics/processing constraints → attributable market actions, sanitised diagnostics, filtered report/export facts | Audit evidence not substituted by logs; minimise/disclose by lawful purpose |

**Implementation direction:** consumer-facing public Marketplace contract and host-injected upstream ports, not reciprocal static imports. Conceptual input/output relationships are not proof of a compile-time dependency. Where both domains need state, each owns its record and exchanges versioned evidence asynchronously or through injected contract ports. Existing [Billing](../billing/capability-record.md), [Verification](../verification/capability-record.md), [Moderation](../moderation/capability-record.md) and [Integrations](../integrations/capability-record.md) directions remain distinct.

### Provider, security, governance and legal constraints

**Provider modes:** native venue authority by default; optional managed external marketplace publication or synchronisation behind Integrations; a delegated/externally authoritative scoped mode needs an **explicit approved source-of-truth map per object/operation**, reconciliation, conflict strategy, provider costs/region, auth grant scope, portability, export and withdrawal. Remote listings may be pending despite local publication; remote status must distinguish last observed and confirmed. A provider outage cannot silently transfer venue ownership or confirm sales. Avoid assuming a common fee, KYC or escrow model across jurisdictions/providers.

**Threats:** seller impersonation, compromised organisation delegates, malicious listings, counterfeit/prohibited goods, manipulated ratings, commission self-dealing, fee diversion, undisclosed platform promotion, tenant/seller data leaks, stale moderation decisions, race-to-publish and provider webhook replay. Apply server-side per-resource decision and assurance, least privilege, dual approval where risk warrants, signed/validated provider assertions, anti-replay, idempotency, controlled disclosures, secure uploads through owning Media/Content Security contracts and durable auditing. Marketplace has a high-impact financial/publication surface: ASVS 5 L2 minimum, relevant L3 controls, WCAG 2.2 AA and defensible retention, minimisation, deletion/export and subject-rights handling. The statutory scope (consumer law, seller disclosures, product safety, VAT/platform reporting, sanctions, age/prohibited goods, advertising, data protection and online safety) depends on geography, product and operator role and requires Legal Compliance evidence/qualified review; **no automatic UK/EU/US compliance assertion**.

### Conceptual GUI, accessibility and adoption

**GUI justified, separable from headless domain.** The host sidebar offers **Marketplace** only to authorised users and routes to a scoped venue dashboard. Proposed views: public/buyer listing discovery and seller identification; seller onboarding and proof/representation status; seller console with guided create/edit listing, source-product selection, preview, compliance checks and submit/withdraw; seller agreement/fees visibility; marketplace operator approval queue, listings/merchant restrictions, dispute and appeal handling, provider-sync reconciliation and exports; governance/settings with venue policy version and approval trail. An unprivileged user sees only entitled controls and publicly released information; **server denies** unauthorised operations regardless of hidden UI. Simple seller/operator flows use clear statuses, plain-language reasons, accessible mobile layouts, low training burden, keyboard/screen-reader support, WCAG 2.2 AA, BCP 47/CLDR, semantic product metadata and Theme Manager tokens. Host controls menu/navigation and installation; Marketplace public contracts supply state; presentations never access private tables. Integrate with `nuxt-layers-test/application-test-template` as representative Nuxt host at implementation acceptance, including absent-optional-capability states; no executable test run in this review.

### Conceptual acceptance matrix (not executed tests)

| Input / scenario | Expected behaviour and outbound proof | Authoritative owner |
|---|---|---|
| Venue admin defines native market and seller submits verified source-linked listing | Authorised revisioned participation/listing; publication only after required checks | Marketplace; Product owns source |
| Seller changes source Product or price | Marketplace revalidates/holds stale offer, never silently substitutes wrong item/price | Product/Pricing and Marketplace independently |
| Disallowed or cross-tenant actor requests listing approval/fee view | Denied/indeterminate, no state change or confidential disclosure, attributable refusal | Authorisation and Marketplace |
| Repeat identical publish request, or conflicting resource revision | Idempotent same outcome or typed revision conflict; no duplicated listing/fee attribution | Marketplace |
| Content Security flags prohibited material; Moderation case is opened | Marketplace holds/restricts listing with own decision; moderation case remains separately owned | Content Security, Moderation, Marketplace |
| Expired KYB authority or contested representation | Marketplace holds relevant seller actions, retains limited disclosure and appeal | Verification/Identity and Marketplace |
| Order confirms seller lines against effective agreement | Marketplace exposes attributable commission basis; no charge/settlement claim | Order, Marketplace; Billing for charge |
| Billing charges, Payment Gateway reports ambiguous capture | Marketplace reports separate fee-basis and unknown financial status, does not mark paid | Billing/Payment Gateway |
| External provider accepts request then times out; duplicate webhook received | Local state remains accepted/remote unknown; verify/reconcile by receipt; no duplicated side effect | Integrations and Marketplace |
| Seller terminates participation after prior accepted purchases | Stop new market actions; preserve authoritative historical Orders, fees and retention/export | Marketplace, Order and finance owners |
| Marketplace used without Order/Payment Gateway | Enquiry/catalogue-only; purchase/settlement command explicitly unsupported | Marketplace |
| Search/Hub cache retains withdrawn listing | Marketplace revocation event and fresh authoritative visibility deny stale public presentation | Marketplace; Search/Federation derived |

### Decision register and deferred acceptance

- **Established**: Governing responsibility-based Domain classification, public-only acyclic contracts, capability-owned persistence/outbox, fail-closed IAM, ADR-0012 composition, ADR-0017 tenant isolation, ADR-0018 policy/entitlement separation and security/accessibility standards. The existing Marketplace record's 15–17 November cross-notes are **preliminary** and do not equal a published runtime contract.
- **Previously approved adjacent concepts**: Verification's VER-01–VER-12 and Online Safety/assurance directions apply as reciprocal evidence boundaries, not automatic Marketplace design sign-off.
- **Proposed for approval here**: **MKT-01** Marketplace as independent multi-seller venue Domain owner, distinct from Shop and Order; **MKT-02** authoritative venue participation, seller agreements and publication lifecycle, with no reownership of Product/Price/Inventory; **MKT-03** fee/commission basis and attribution only, separate from Billing/Payment/Accounting; **MKT-04** risk- and jurisdiction-sensitive seller eligibility and content enforcement, specialist proof/cases separate; **MKT-05** native catalogue/enquiry-only fallback and explicit optional provider authority modes; **MKT-06** versioned commands/queries/outbox, tenant isolation, failure/reconciliation semantics; **MKT-07** separable guided seller/operator/public GUI and mobile accessibility.
- **Open owner decisions**: **MKT-08** should Marketplace v1 support **both physical goods and services/digital offerings**, or initially restrict offer categories? Recommendation: generic reference-based listing supports all, with category-specific legality/fulfilment delegated to owners and unsupported combinations declared. **MKT-09** does Marketplace v1 allow **direct buyer–seller contact/enquiries** outside an Order, with bounded privacy/anti-abuse controls? Recommendation: optional consent-based enquiry via an appropriate Communications owner, never expose raw contact details by default. **MKT-10** should external delegated marketplace authority be included in the first release or staged? Recommendation: native first; document provider-neutral interfaces now, stage external authority after reconciliation/security acceptance.
- **Technical investigation**: verify actual neighbouring root `CONTRACT.md` support; source-offer identity and category semantics; regulatory obligations per actual venue jurisdiction; commission calculation/rounding in Billing; payment split/merchant-of-record and taxation; content/verification assurance coverage; resource and event contract version shapes; migration/export cost. No dependent implementation or provider capability is inferred.
- **Implementation/acceptance work**: author root `CONTRACT.md` if/when implementation is approved, record exact service ports, versioning, failure codes and storage register; choose infrastructure without leaking adapters; independently validate minimal consumer/one-call Nuxt composition within 50 lines; CI security, contract, recovery, replay, tenant-isolation, accessibility and host acceptance. **No implementation repository modified and no local tests performed**.
- **Sign-off**: the proposed design is documented for architectural review but **not conceptually approved** until the owner resolves or explicitly defers MKT-08–MKT-10 and approves MKT-01–MKT-07. No merge without explicit approval and fresh master/CI/architecture reconciliation.
