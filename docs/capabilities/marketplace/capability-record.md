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

## Moderation dedicated review — reciprocal conceptual boundary (19 November 2026, draft PR #96)

**Status: Proposed, not an accepted public implementation contract.** See [Moderation's dedicated idealised input/output contract](../moderation/capability-record.md#dedicated-conceptual-review--19-november-2026-pr-96). Marketplace retains seller/listing eligibility, participation and source-specific restriction decisions. It supplies scoped source evidence and per-target actual enforcement receipts to Moderation; a case finding cannot independently suspend a seller or alter commercial/settlement outcomes. Fraud and verification evidence retain their specialist authority.

## Moderation dedicated review — reciprocal interface (19 November 2026, draft PR #96)

**Proposed, no published implementation contract.** Marketplace owns seller/listing participation, business eligibility and local enforcement. Moderation coordinates reports and decisions but may only request changes against explicit seller/listing revisions; commercial remedies and verified execution remain Marketplace-owned. See [Moderation's conceptual inbound/outbound contract](../moderation/capability-record.md#dedicated-conceptual-review--19-november-2026-pr-96). Interoperability uses public versioned host-composed ports without private-schema coupling.
