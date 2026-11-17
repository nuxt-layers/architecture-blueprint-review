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

## Review notes — contacts, financial providers and ownership (14 November 2026)

**Provisional conceptual notes only; verify root public contract before detailed Integrations specification.**

- Provider connectors (e.g. Xero/QuickBooks, payroll, procurement, banking, CRM) manage connections, provider-specific identity and field mapping, transport, checkpoints, provider limitations and status; they never silently become the owner of Product, Inventory, Asset, Order or Accounting domain facts.
- Accounting and Invoice independently select an approved authority per tenant/accounting context and supported service. Provider scope and compatibility must be verified; no assumption a connected product implements every accounting or invoicing operation.
- A connected customer/supplier directory may be externally authoritative under a specific approved mapping, but **Identity** and **Profile** remain authoritative for platform identities and personal-data disclosure.
- Provider outage does not silently switch authority. Changeover requires approved mapping, reconciled balances and outstanding work, source/remote IDs, versioned checkpoints and explicit cut-over.
- Imported financial transactions, asset registers, stock costs, supplier records and contacts must be validated and authorised by their owning domain, with provenance and replay/deduplication handling.

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Provider-neutral connection and transport mechanisms; never own commercial, physical-stock or financial domain records.
- **Related capability notes:** [accounting](../accounting/capability-record.md), [invoice](../invoice/capability-record.md), [order](../order/capability-record.md), [product](../product/capability-record.md), [inventory](../inventory/capability-record.md), [logistics](../logistics/capability-record.md).
- **Open architectural questions:** Per-tenant authority/connector selection, provider compatibility, external party-directory mappings and reconciled changeover.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

### Government, accounting-framework and financial-provider interface notes

- **Accounting frameworks and tax rules** are not ordinary connector payload transforms. [Accounting](../accounting/capability-record.md) owns financial posting meaning and approved framework/rule application; [Legal Compliance](../legal_compliance/capability-record.md) owns obligation/constraint determination. Integrations owns provider connection, credentials, schema adaptation and transport/checkpoint evidence.
- **Government portal adapters** may handle authenticated tax/financial submissions, acknowledgements, status checks, amendments and delivery errors for a tenant/accounting entity. Accounting remains owner of the authoritative reconciled return and its business state; a successful HTTP transport does not prove a filing was accepted.
- **Provider capability discovery** must declare supported operations, geographical/period/API restrictions, scope and permissions, synchronisation semantics, read-back and mapping capabilities. Missing regulated functions or required rules must surface as unsupported/requires-review, not silent local fallback.
- **Change control:** tax-framework updates, remote schema revisions, connector credential changes and provider migration require versioned mapping, evidenced effective dates, safe retries/idempotency and explicit authorisation. Connector code cannot bypass Accounting's immutable posting/period controls.
- **Open:** which provider registration/attestation, sandbox certification, government gateway security, legal acceptance evidence and integration-country constraints require Legal Compliance review before enablement?

## Cross-capability note — External Billing authority and provider interoperability (15 November 2026)

**Agreed conceptual relationship: BIL-05 approved on 15 November 2026; provider functionality remains unverified.** [Billing](../billing/capability-record.md#modes-provider-authority-and-migration) selects a single authoritative commercial-charge mode per approved scope (native or verified provider), validates commercial semantics, controls cutover and reconciles charge status. Integrations owns provider connection, credential-reference management, capability discovery, mapping, transport, webhook provenance, retries and revocation, not the charges. Missing provider acknowledgement means pending/uncertain, not success or failure; no silent native fallback, duplicate periods or competing charge authority. No connector implementation or provider operation is asserted.

## Cross-capability note — External Booking provider authority (15 November 2026)

**Proposed reciprocal relationship, not verified provider support.** [Booking](../booking/capability-record.md) controls selection of one effective authoritative capacity owner per resource/scope/period, reservation business lifecycle, local mappings and reconciliation state. Integrations owns configured connections/credentials, provider operation discovery, authenticated webhook/transport and technical sync checkpoints. Booking supplies authorised hold/confirm/amend/cancel intent and idempotent identity; Integrations returns authenticated, provenance-rich external operation evidence, capability limitations and failure/uncertainty. Provider timeout or webhook receipt does not prove successful booking. Authority transfer needs reconciled checkpoint/cutover, no dual-writer capacity guarantees and explicit unsupported-operation handling.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Provide verified external company registry, payment and authority evidence transport and provider status, not adjudication of legal authority, commercial settlement or domain ownership. Preserve mapping/provenance, tenant isolation and provider uncertainty.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Review-approved documentation direction, not an implemented interface or governing ADR. See [safety review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

Provider-neutral external adapters may support specialist image/NCII detection, URL intelligence, KYB/KYC, age assurance, fraud signals and regulatory submission transport where appropriate; respective specialists/domain owners own semantics and use. Record lawful sharing, processing location, provider/version, costs, timeout, idempotency, unknown outcomes and exit. An external acknowledgement does not establish authoritative legal filing truth.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

External proofing, age-assurance and merchant-verification adapters should be provider-neutral where approved by public contracts: trusted callbacks/nonces/audience, lawful provider processing and data minimisation, claim quality, expiration/revocation, errors, billing, retries and outages. Integrations transports qualified assertions, not independent legal identity, merchant permission or content access decisions.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Proposed Verification capability consumes national ID, age/KYB, document-proofing or credential issuers through provider-neutral Integrations/host adapters where contract-appropriate. Integrations owns transport and connection lifecycle, never the attested truth or local eligibility; country-specific APIs need lawful provider access, data-residency and usage-right checks.
