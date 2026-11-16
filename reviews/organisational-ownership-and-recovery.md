# Review — Organisational ownership, hostile administrator recovery and portability

**Status:** Review evidence, not accepted governing authority. **Baseline:** governing `2eea557fa3acbf9412fea065d2a3cdda42a764fc`, blueprint `442b3018c580562cac7cb513dbee9e7ad5d9a707`. Related proposals: [tenancy](../proposals/organisational-tenancy-and-governance.md), [policy](../proposals/policy-and-governance-boundaries.md), [onboarding](../proposals/commercial-onboarding-and-entitlements.md).

## Problem and security objective

A founder, employee or external IT contractor may create a company's account, organise its digital assets and then withhold access, change credentials, remove owners or make portability contingent on their cooperation. Conversely, a fraudulent third party may pose as the lawful company controller and seek to seize its tenant. Both abuse cases must be prevented while preserving independently attributable digital creator provenance.

Creation != digital owner != real-world controlling entity != delegated administrator != commercial payer. Company director, shareholder, person with significant control and digital owner are distinct. No legal title is automatically verified by platform role label.

## Threat/abuse scenario matrix

| Scenario | Required response | Failure to avoid |
|---|---|---|
| Contractor sets up company tenant and refuses handover | Verified controller can submit independently reviewed recovery with high assurance, audit, scope-limited revocation and export | Creator has permanent irrevocable control |
| Fraudster claims to be company director | Verify authority and counter-evidence; hold contested change and provide notice/appeal | Automatic title-derived takeover |
| Last human owner leaves/dies or loses credentials | Restrict sensitive changes and use controlled succession/recovery, preserve source business data | Silent orphan-to-any-admin promotion; irrevocable lock |
| Owner changes policy to 'no approvals' before hostile transfer | Mandatory floor, separate authorisation for policy change, versioning/effective delay | One actor weakens and exploits same rule |
| Parent tenant admin requests subsidiary customer data | Independently authorised resource permissions; parent-only maintenance may remain possible | Parent relationship bypasses child privacy |
| Subscription lapses during ownership dispute | Controlled commercial restrictions and retention; access to eligible recovery/export stays governed | Automatic destructive erasure or ransom-like lock |
| Company switches provider/IT contractor | Portable authorised export of domain-owned records/configuration with provenance | Provider-vetoed export or leaking third-party data |

## Cross-capability tests

Identity maintains source records, Authentication step-up, Authorisation decisions, Legal Compliance/legal authority specialist supplies qualified obligation/evidence, Workflow approvals, Configuration valid versions, Audit independent custody, Notifications affected-party alerts, domain owners export, Reporting authorised evidence and Logging sanitised diagnostics. Each domain remains source of truth. Policy requirements are not silently copied into the Identity group model.

## Contract acceptance scenarios

- Attempt to remove last active owner: block/hold per approved governance; recovery is separate protected pathway.
- A rightful controller requests tenant recovery: hold original owner control only to the extent legally and operationally justified; retain non-repudiation, hearing/appeal and no presumption of claimant truth.
- Retry completed recovery: original result/idempotent status; no extra ownership mutations or repeated notifications misrepresented as separate change.
- Contractor access revoked: all dependent grants and fresh sensitive operations denied; audit retained, historical documents untouched.
- Customer requests export: source-specific authorised and complete/partial status, privacy/hold exclusions disclosed; ownership of bytes/records not silently reassigned.
- Legal conflict or unavailable evidence: operation held with explicit uncertainty and independently reviewable process, not interpreted as permission.

## Outstanding governance and engineering investigations

Precisely who adjudicates contested real-world legal authority (possible specialist legal-entity domain); qualified human review capacity; evidence collection/minimisation and duration; interim business continuity; tamper-resistance, notification timing, cooling-off and appeal; external identity-verification integrations and availability; policy precedence and locked floors; recovery under provider outage; portability contract per domain. Evidence requires professional jurisdiction-specific legal validation; this blueprint is not a legal opinion.
