# Capability Record — Organisation Console

**Proposed name:** `organisation-console`  
**Previous classification label:** `company-console`  
**Status:** Agreed conceptual name and purpose (17 November 2026); provisional **Presentation / Application Composition**. Not a confirmed independent runtime capability, repository or implemented contract.

## Purpose

Provide a **reusable, role-aware organisational administration interface** for managing an organisation's digital presence, governance, members, subscriptions, enabled capabilities and operational information **through the authoritative public contracts of the responsible capabilities**.

`organisation-console` is preferable to `company-console` because organisations on the platform may be companies, sole traders, partnerships, clubs, charities, committees, councils or other configured organisational types. A company-specific name would incorrectly restrict the intended audience and composition. The word *console* describes a coherent management experience: dashboards, context selection, administration and applicable operational views.

## Classification and boundaries

- **Presentation / Application Composition**, not an independent business-data owner.
- The console may collect and organise views and authorised commands from capabilities; it does **not** own Identity tenants, groups or memberships, legal-entity authority, digital owners, Authorisation grants, Subscription entitlements, Billing charges, Policy documents or other domain source records.
- **Organisation and tenant are distinct.** A person may manage multiple organisational contexts and tenants. An application's host remains responsible for routing, branding, composition and audience selection; tenant parentage never automatically grants child-record access.
- The console remains distinct from a **platform-operator console** used for deployment/infrastructure administration or protected platform recovery. Routine operator authority must not imply access to customer records.
- A menu item, visible action or disabled button never substitutes for a server-side permission/assurance/policy decision.
- Its reuse may be achieved through host-owned application composition and existing capability-supplied optional presentation. A **separate `organisation-console` package** requires an independently demonstrated reuse/lifecycle justification, a published public contract and ADR-0012/0016 conformance; the name does not authorise one.

## Conceptual GUI scope

The host may offer a common organisational landing dashboard with audience-specific views and navigation for:

1. **Organisation and context selection:** authorised tenant/group switcher, organisation overview, current context and permitted capabilities.
2. **Identity and governance:** human digital owners, delegation, invitations, scoped group/member management, ownership-transfer requests, independent approvals, disputes and recovery status via IAM contracts.
3. **Commercial management:** selected service tiers, Subscription entitlements, seat allowance and actual usage, Billing/Invoice information, upgrades, cancellations and provision/enablement statuses from their respective owners.
4. **Resources and operations:** purchased storage quotas and measured use, operational summaries, permitted reporting and links into the appropriate capability's own dashboards.
5. **Policies and published documents:** approved organisational settings/decisions, legal-compliance status as qualified, and Publisher-managed approved policy documents; publishing a statement does not establish legal or operational compliance.
6. **Notifications and evidence:** authorised workflow requests, pending tasks, status/error messages and permitted Audit/Reporting views without inventing source data.

Specific screens are optional and depend on the assembled application, organisation archetype, enabled services, authorised actor and policies. The console must not become a central controller implementing every other capability's decisions.

## Idealised interaction boundary (preliminary, not a complete public contract)

| Inbound authority | Console consumes | Console supplies to the host/user |
|---|---|---|
| Authentication, Identity and Authorisation | Trusted caller/context, verified tenant/group facts and scoped access/assurance decisions | Authorised context choices, navigation, guarded action requests; no impersonation or membership grant |
| Configuration and organisation archetype metadata | Approved scope, presentation choices and permitted feature selections | Organisational settings and appropriate feature views; no independent domain policy decision |
| Subscription, Pricing, Billing, Invoice and Payment Gateway | Authoritative entitlements, tariffs, charges, invoices and payment/provisioning states | Scoped management screens and requests to the relevant owner, clearly distinguishing pending, paid, entitled, enabled and authorised |
| Storage and operational resource owners | Allowed quota, usage and authorised operational results | Scoped resource dashboard; no promise that a usage read enforces quota |
| Workflow, Notifications, Audit and Reporting | Pending approvals, notices, source-provenanced evidence and authorised aggregates | Review, decision-routing and reporting experiences; no duplicate evidence master |
| Publisher, Privacy and Legal Compliance | Approved policy documents, privacy/consent restrictions and qualified applicability constraints | Authorised document navigation and status; never legal-compliance certification |
| Application composition / host | Route placement, enabled screens, branding, locale, tenant context and user audience | Optional sidebar/dashboard presentation and link/navigation contract; no business persistence |

### Contract and failure expectations

Protected actions must go through the owning capability's server-authorised public contract. Absence of permission, missing entitlement, stale context, unknown external confirmation or unavailable required upstream service must not render a successful business operation or reveal restricted information. Respect SSR/client hydration, cache invalidation on context/revocation, WCAG 2.2 AA, internationalisation and Theme Manager's semantic vocabulary. Source-owned events and audit trail remain with their respective owners.

## Naming rationale and alternatives

| Name | Disposition |
|---|---|
| **`organisation-console`** | **Selected:** broad, meaningful, recognised and neutral across organisation types |
| `organisation-admin` | Describes administrators but inadequately covers dashboards and permitted non-administrative views |
| `management-console` | Too broad; could be confused with platform or infrastructure management |
| `tenant-console` | Too technical and misleading: an organisation need not equal a tenant |
| `administration-ui` | Describes presentation technology rather than organisational scope |
| `company-console` | Superseded: artificially company-specific |

## Relationship to existing architectural evidence

This name and conceptual responsibility supersede the earlier `company_console` label. The earlier requirements for tenant context selection, ownership and governance, invitations, tier and quota information, organisational policy documents and authorised reporting were **already preserved** in [Application Compositions](../application_compositions/capability-record.md) during [blueprint PR #42](https://github.com/nuxt-layers/architecture-blueprint-review/pull/42).

See [tenancy and governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md) and [organisational recovery](../../reviews/organisational-ownership-and-recovery.md).

**Open for later classification:** Is there an independently reusable, maintained presentation contract warranting a separately packaged console, or is the requirement fully satisfied by Application Compositions, `ui`, and existing capability-specific optional presentation? Until resolved, keep `organisation-console` a **provisional presentation/composition entry**, not a completed domain capability or implementation specification.
