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
