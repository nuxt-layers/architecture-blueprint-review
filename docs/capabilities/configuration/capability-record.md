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

## Review notes — Accounting settings, frameworks and delegated authorities (14 November 2026)

**Status: Provisional conceptual note, not a completed Configuration specification.** The published `nuxt-layers/configuration/CONTRACT.md` provides schema-declared settings, scoped effective values and provenance, but explicitly reports its current composition limitations. Do not infer new accounting-specific settings already exist.

- **Established boundary:** Configuration stores **validated effective selections and provenance**, not posted financial journals, authoritative books, credentials or a determination that an accounting treatment is lawful.
- **Proposed accounting settings:** Per tenant or appropriate accounting-entity context, resolve the approved reporting framework/version, fiscal-year preferences where permitted, tax regime/election references, financial policy references, accounting/Invoice authority selections and relevant provider connection identifiers. Each key needs a published schema, authorisation, scope, visibility, change risk and effective-date policy.
- **Do not assume scope support:** Configuration's current contract exposes platform/tenant/group/account and its defined precedence; an *accounting entity* is a business domain object, not one of those scopes by definition. The host/Accounting must explicitly map and authorise any effective entity context or decide whether Accounting owns a domain-specific selection record.
- **Controls:** Mandatory Legal Compliance restrictions and Accounting posting invariants cannot be overridden by configurable defaults. Changing provider or framework is a controlled business transition with approval, provenance, effective dates, validation and reconciliation—not merely a preference toggle.
- **Proposed relationships:** [Accounting](../accounting/capability-record.md), [Legal Compliance](../legal_compliance/capability-record.md), [Integrations](../integrations/capability-record.md), [Invoice](../invoice/capability-record.md).
- **Open:** which settings belong in Configuration versus Accounting-owned financial-policy records; how do entity-level keys, approved elections, historical versions and migration cut-over state resolve without a new generic settings service?

### Cross-capability relationships and evidence status

- **Verified:** Configuration's public contract supports declared keys and scoped effective values with provenance; it does not establish Accounting-specific keys or accounting-entity scoping.
- **Proposed:** Domain-approved policy selections and provider references through public, host-supplied interfaces only.
- **Next review gate:** Complete Configuration's individual alphabetical conceptual review and verify current published contract before formalising new keys or service edges.

### Cross-capability note — Authentication policy configuration (15 November 2026)

**Established:** Configuration owns scoped setting values, resolution and provenance within its published contract; [Authentication](../authentication/capability-record.md) owns the validation and enforcement of sign-in, session and assurance policy. **Agreed conceptual direction (AUT-01/AUT-06):** mandatory security floors cannot be weakened by configuration; permitted stricter tenant/application/operation settings require documented precedence, version and activation. **Open:** exact registered schemas, scope compatibility, activation, rollback and active-session effects. Configuration's separate conceptual review remains incomplete.

## Cross-capability note — Authorisation policy configuration (15 November 2026)

**Established:** Configuration owns declared scoped settings and provenance; [Authorisation](../authorisation/capability-record.md) owns permission meanings, secure policy floors, role/grant models and access enforcement. **Proposed:** governed selections, revisions, effective dates and rollback may reuse published Configuration interfaces where they fit, but complex Authorisation definitions retain their owning capability's invariants. **Open:** versioned policy schema, precedence, activation, approval and absence behaviour. Configuration's review remains incomplete.

## Cross-capability note — Booking policy configuration (15 November 2026)

**Proposed reciprocal relationship; Booking has not been implemented.** [Booking](../booking/capability-record.md) will consume approved, scoped and versioned settings for booking windows, duration, holds, cancellation/attendance rules, waitlists, visibility, channel/provider selection and retention. Configuration owns declaration, scope, effective-value resolution and provenance; Booking validates its domain rules, applies effective policies and retains the decision/version reference on each affected booking. An invalid or missing mandatory setting must not allow overselling or bypass legal/authorisation constraints. Changes affecting previously confirmed commitments need explicit Booking transition rules; no second Booking preference store in Configuration.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Store only registered, approved, scoped/versioned values and provenance for permissible organisation/archetype, service selections and bounded governance rules. Do not own legal obligations, business domain decisions, Identity ownership or entitlement decisions. Security floors locked by authoritative owners cannot be weakened by custom policy. Complex governance instruments and domain rule versioning remain open; published Configuration contract is not a universal policy interpreter.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Cross-capability note — Proposed Caching policy and freshness (16 November 2026)

**Agreed conceptual boundary; no implemented adapter or new Configuration authority asserted.** [Caching](../caching/capability-record.md) consumes Configuration's approved scoped, versioned cache limits (where declared), including maximum retention, provider availability and permitted refresh preferences. Configuration owns setting declarations, scope, precedence and effective provenance; a source capability and mandatory security/privacy restrictions define stronger freshness and disclosure constraints. Caching supplies effective operational configuration, rejected/unsupported setting outcomes and sanitised health; absence or uncertainty disables unsafe caching rather than widening TTL or access. No package dependency inferred.

**Approved conceptual boundary (16 November 2026):** Host-composed backend selection and supported namespace settings are exposed through a provider-neutral caching interface. Configuration retains declared setting provenance and precedence; Caching/source security ceilings cannot be weakened by tenant preference. PostgreSQL is an evaluation preference, not a compulsory provider.


## Cross-capability note — Clock conceptual public contract (17 November 2026)

**Proposed, not yet owner-approved.** [Clock](../clock/capability-record.md#idealised-public-input-interfaces-conceptual-contract) validates temporal values, named zones, DST interpretation, formats and the host's effective presentation overrides. Configuration owns declared, approved, scoped/versioned settings and provenance; Profile owns personal locale/zoneinfo; the composition host resolves precedence and passes permitted values. No Clock preferences persistence or direct Configuration dependency is implied; invalid settings are explicitly rejected. The Clock implementation's existing six optional host-declared preferences are not built-in Configuration keys.

## Cross-capability note — Clock NTP source selection (17 November 2026)

**Conceptual direction agreed for Clock, integration not implemented.** [Clock](../clock/capability-record.md#owner-approval-and-ntp-governance-clarification-17-november-2026) keeps its injected trusted `now()` port. Configuration may govern *deployment-level*, privileged, allowlisted NTP/NTS provider selection and source-policy revisions, with approved authority/provenance; it does not manage the NTP daemon, assert synchronisation health or permit tenant/user preferences to change shared host time. Infrastructure applies approved choices; Observability reports measured status; Audit accounts for privileged changes. Whether a deploy-time only source should instead remain purely host/infrastructure configuration is a Configuration/Infrastructure integration question for their reviews.
