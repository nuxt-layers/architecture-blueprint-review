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

## Cross-capability note — Capability dashboard navigation (15 November 2026)

**Status: Proposed composition relationship, not a completed Application Compositions capability or generic navigation API.** The shared `nuxt-layers-test/application-test-template` uses an application-owned sidebar Capabilities entry and host-owned dashboard cards to open Theme Manager in its shared shell. **Proposed for [Audit](../audit/capability-record.md#presentation-and-application-navigation-concept-15-november-2026):** a host may add an Audit sidebar link and dashboard entry when it selects Audit's optional presentation, while the Audit headless core remains independently usable and the host retains route placement, branding and trusted user/tenant context. Visibility is not a substitute for server-side Authorisation. Audience-specific Audit screens must not mingle tenant review with privileged platform operations. No automatic discovery/menu registry, cross-capability UI dependency or changes to the shared test template are implied. Application Compositions retains its existing non-state-owning classification and incomplete conceptual review.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Host owns onboarding navigation, service-selection checkbox/tier GUI, paywall, context selector and orchestration across source capabilities. Installation is not itself a tenant; operator business tenant separately pays/receives platform transactions.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.


## Classification reconciliation — Reusable organisational administration presentation (17 November 2026)

**Transferred from the [legacy Company Console candidate](../company_console/capability-record.md), preserving its earlier conceptual requirements:** An authorised, shared-shell organisational context selector and dashboard may present tenant/group governance and owners, invitations, subscriptions and tariff tiers, licensed seats, purchased quotas and usage, approved policy documents and pending decisions, permitted reports, and owned business capabilities. These screens use the affected capability's documented public contracts. They do not store transactional/domain data, create a second hierarchy, derive owner standing from a menu label or grant resource access merely because a route is visible.

**Classification direction:** Generic host/application composition and optional capability-specific presentation are preferred to a company-only business-state service. Host owns sidebar/navigation, audience/context resolution, route placement, branding and capability assembly; Identity/Authorisation retain identity/governance/access decisions, commercial domains retain subscription/billing/usage, Publisher governs policy documents. Reuse `ui`, Theme Manager and optional presentations, respecting ADR-0009, ADR-0012 and ADR-0016. A separate reusable organisational administration *presentation kit* would require independent reuse/ownership evidence and must not gain authoritative persistence. This preserves Company Console intent without deciding to rename or create a runtime layer.

**GUI acceptance:** A person can choose among independently authorised organisation/tenant contexts; a permitted administrator sees relevant owner and service management pages, a limited member sees only their authorised activities, and a platform operator does not automatically see private child-tenant data. Host navigation controls are not server-side permission checks. The eventual interface must be accessible, localisable and work through the application test template's sidebar/dashboard approach.
