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

## Review notes — Accounting frameworks, taxation and regulatory constraints (14 November 2026)

**Status: Provisional conceptual note, not a completed Legal Compliance specification.** The governing Capability Catalogue assigns legal obligations, jurisdictional constraints and legal holds to `legal-compliance`; it expressly consolidates the former `policy-map` concept into `legal-compliance`. A root `CONTRACT.md` was not retrievable in this review, so no implemented ports are asserted.

- **Established boundary:** Legal Compliance does not own Accounting's journals or tax calculation results. It records or resolves applicable legal duties, effective-date constraints, restrictions, holds and compliance evidence for the relevant entity and activity; the actual jurisdictional rule set and determinations require qualified validation.
- **Proposed interaction:** Provide the governing obligation/restriction context for Accounting's [framework, effective-policy, tax and regulatory interfaces](../accounting/capability-record.md). Distinguish mandatory law, permitted accounting election, tenant configuration and unresolved legal uncertainty; an organisation's assertion is not automatically proof of legal validity.
- **Enforcement:** Accounting validates its own ledger invariants and applies authorised financial rules; mandatory legal refusal or unavailable necessary compliance evidence should not be silently bypassed. Legal Compliance does not directly mutate Accounting's records or substitute for Authorisation.
- **Government portals:** Accounting prepares authoritative reconciled returns and retains filing evidence. Integrations handles authenticated transmission and acknowledgement. Legal Compliance records duties and constraints, not credentials, submission transport or financial balances.
- **Open:** how is applicability determined for multi-jurisdiction entities, changes in law, tax elections, cross-border activity, effective dates, evidential review, legal holds, filing deadlines and statutory retention? Define minimal public compliance decision port before deciding any package dependency.

### Cross-capability relationships and evidence status

- **Governing evidence:** `architecture-rules/docs/catalogue.md` names Legal Compliance's obligation/constraint boundary and aliases `policy-map` to it; root implementation contract not verified.
- **Proposed relationships:** [Accounting](../accounting/capability-record.md), [Configuration](../configuration/capability-record.md), [Integrations](../integrations/capability-record.md), [Invoice](../invoice/capability-record.md).
- **Next review gate:** At the alphabetical review, inspect its repository and published root `CONTRACT.md` (if present), refine these boundaries and only then assess published service edges.

### Cross-capability note — Authentication legal restrictions (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns credentials, sessions and authentication security records; Legal Compliance owns the applicability and meaning of legal requirements and holds. **Agreed conceptual direction (AUT-11):** a valid legal hold restricts disposal only of records it covers, with attributable access, review and release; neither routine account closure nor a generic retention option silently overrides mandatory obligations. **Open:** jurisdiction-specific obligations, lawful basis, hold authority, scope and confirmed provider deletion. This does not complete Legal Compliance's separate review.

## Cross-capability note — Billing tax and statutory constraints (15 November 2026)

**Proposed reciprocal interface, not a completed Legal Compliance review or tax determination engine.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) needs applicable jurisdiction, legal-entity, tax-treatment/point, preservation, mandatory communication and permitted disclosure constraints for supported charge scenarios. Legal Compliance supplies governed legal obligations/constraints or validated references, **not** automatically tax calculations; statutory tax-decision ownership requires later explicit allocation and qualified jurisdictional validation. Billing exposes charge decision/version and required factual context to authorised consumers; Invoice owns legal documents and Accounting tax posting/returns. Missing mandatory legal/tax evidence holds relevant finalisation/handoff; no permissive default or regulatory conformity is claimed.
