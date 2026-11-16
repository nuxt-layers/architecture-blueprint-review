# Policy, governance, legal obligations and document boundaries

**Status:** Conceptual blueprint proposal awaiting governing adoption. **Evidence:** `architecture-rules/master` `2eea557fa3acbf9412fea065d2a3cdda42a764fc`, blueprint `master` `442b3018c580562cac7cb513dbee9e7ad5d9a707`. Accepted `docs/identity.md`, `docs/privacy.md`, Capability Standard, ADR-0003/0009/0012/0016. Configuration and Authorisation `CONTRACT.md` reviewed as implementation evidence, not proof of universal policy engine. Related: [tenancy](organisational-tenancy-and-governance.md) and [commercial onboarding](commercial-onboarding-and-entitlements.md).

## Taxonomy — do not conflate 'policy'

| Kind | Authority and mutability | Example | Record/decision owner and enforcement |
|---|---|---|---|
| Architectural invariant | Accepted ADRs/normative architecture; **not tenant configurable** | No implicit cross-tenant access, group hierarchy cycle or false operation confirmation | Every affected domain enforces its applicable invariant |
| Platform operational/security policy | Platform governance and mandatory security floors; only validated bounded overrides | Authentication assurance, owner-change cooling-off, risk-based approval | Specialist owner (Authentication/Identity/Authorisation); Configuration may carry permitted effective values |
| Organisational governance policy | Validly authorised organisation under governing instruments; versioned/approved within platform and legal floors | Two-person approval of transfer, contractor delegation, expense threshold | Identity/Authorisation/domain interprets and enforces; Configuration stores only eligible declarations/settings |
| Domain business policy | Responsible domain subject to platform and law | Booking cancellation window, billing adjustment authority | Booking/Billing/etc. own semantic validation and outcome |
| Legal/regulatory duty | Applicable law and qualified interpretation for jurisdiction/entity/activity/time; cannot be tenant-disabled | Privacy consent, statutory retention, applicable transparency obligations | Legal Compliance supplies duties/constraints; Privacy owns specialist data-protection/consent policy; domain acts on constraints |
| Published organisational policy document | Authorised publisher and document governance; text not automatically executable | Privacy notice, Modern Slavery Statement, Health and Safety Policy | Publisher owns revision/publication; Content Editor supplies GUI; underlying duty/control owner is separate |
| Governing instrument and verified authority evidence | Legally/governance-effective source, subject to independent validation | Articles of association, club constitution, council delegation | Appropriate legal-entity/governance authority; Publisher may host copy, not adjudicate its validity |

These kinds can overlap as subjects but must not share an unverified 'policy' boolean or rely on prose publication to authorise actions. Law and platform invariants can conflict; quarantine the affected operation and escalate, never quietly prioritise unsafe local settings.

## Proposed policy lifecycle and conceptual contract

**Define → validate schema/authority/applicability → approve (independently as risk dictates) → schedule effective date → activate → enforce → attest/audit → review/revise/retire.** Each stage identifies originating actor, authoritative issuer, jurisdiction, tenant/group/resource/activity, policy type, version/source, effective period, expiry, status, approver, evidence, disclosure and correlation.

| Interface | Input / owner | Output / consumer | Failure |
|---|---|---|---|
| Policy declaration/setting | Domain publishes approved schema, floor, allowed scope and change risk; authorised actor proposes value to Configuration | Scoped approved effective setting with provenance to enforcing domain | Unregistered/invalid/weakened setting refused; Configuration is not evaluator of every specialist business rule |
| Legal applicability/constraint | Authorised source facts, jurisdiction, activity, entity and source citation to Legal Compliance | Versioned applicable duty, prohibition/requirement, uncertainty and evidence reference to domain/Privacy | Unknown rule/material jurisdiction uncertainty means hold or expert review, not implied compliance |
| Privacy consent/retention decision | Processing purpose, subject choices, record class and lawful restrictions | Permitted purpose/consent/retention disposition to source owner | Missing required consent blocks optional collection; deletion cannot bypass hold |
| Access decision | Trusted subject, resource, action, group/tenant context and effective policy | Authorisation decision and assurance/approval need | Missing/contradictory critical evidence fails closed |
| Approval workflow | Protected change, policy version, nominated qualified approvers | Attributable approved/rejected/held result to owning domain | Workflow cannot itself change domain ownership or grant permissions |
| Document lifecycle | Authorised draft, governing source and approved publication version | Publisher's document/revision/publication status, through Content Editor screens | Published text does not assert operational enforcement or legal correctness |
| Evidence/notification | Authoritative changes, constraints, denial and approval references | Audit custody, Logging diagnostics, Notification notices, Reporting derived views | No fabricated source events; auditable exceptions and explicit capture guarantee by risk |

**Context is conceptual**, not a mandatory universal request envelope. Keep owner/decision scope, version, effective and record time, source and verification level, tenant/group boundaries and approved disclosure. Every critical consumer must know whether the policy is **mandatory**, **configurable within floors**, **advisory**, **not applicable**, **pending verification** or **unsupported**. A missing optional rule is distinct from provider outage.

## Example: ownership transfer

Identity owns protected owner state and lifecycle; Authorisation verifies actor's rights; Authentication provides fresh/strong assurance; Configuration supplies only permitted policy selections; appropriate verified legal/governance owner supplies company authority if claimed; Workflow coordinates approvals; Legal Compliance constrains; Audit preserves evidence. A hostile contractor cannot weaken transfer policy and immediately exploit it; protected changes to the policy itself require independent authorisation, versioning and guarded effective time. Even a digitally designated owner cannot simply abolish mandatory anti-lock-in safeguards.

## Example: organisational Modern Slavery Statement

Legal Compliance evaluates whether and which current statutory transparency duties apply to a particular organisation (jurisdiction, turnover/activity and qualified sources matter). The organisation may maintain an internal anti-slavery/supplier assurance policy even when publication is not legally mandated. Supplier/procurement and Workforce domains own actual checks/training, Workflow approvals, Publisher the statement's revisions and publication, Content Editor its GUI, Audit/Reporting approved evidence. Publication ≠ compliance; text ≠ executable control; no claim of universal automated interpretation of legislation.

## GUI / discoverability

Governance UI should separate **mandatory locked safeguards**, **configurable approved rules**, **legal obligations/uncertainty**, **policy documents** and **source evidence**. Show why a control is disabled; support requests for change, impact preview, approvals, effective dates, versions, dispute/recovery and accessibility. Host owns navigation and checks server-side; do not expose secret law-enforcement investigations or other-tenant policies.

## Architectural disposition

Do **not** create a generic `policies` capability merely to organise vocabulary. Configuration's current published contract supports declared keys, platform/tenant/group/account scopes, precedence and provenance, but not universal arbitrary policy-language evaluation. Authorisation's contract has protected policies and floors. Legal Compliance is a candidate without independently verified runtime `CONTRACT.md`. Investigate an independent structured-policy responsibility only if a lifecycle/decision authority exists that these owners cannot coherently provide.

## Governing change candidates and open items

- `docs/identity.md` / ADR-0003 for tenant hierarchy and owner guarantees; record independent authority verification and recovery without group membership duplication.
- `docs/capability-standard.md`, ADR-0009/0012/0016 for scoped policy-public interfaces, optional presentation and directional composition where necessary; **do not claim these require rewriting absent a demonstrated conflict**.
- `docs/privacy.md` and security baseline for policy/notice vs actual consent enforcement; review current law and jurisdiction with qualified specialists before asserting duties.
- Open: structured governance instruments and legal-entity authority owner; how to store complex structured policies versus ordinary Configuration keys; legally valid applicability decisions and change-of-law management; conflict/unknown and offline failure semantics; governance-policy manipulation by privileged users; who is allowed to publish a new policy version and when it takes effect.

No governing or implementation repository modified here.
