# Moderation — Capability Report (Pro-forma)

**Capability name:** `moderation`  
**Classification:** Platform candidate (subject to classification/ownership gate)  
**Status:** Proposed conceptual review; no package, API, contract or implementation verified  
**First recorded:** 17 November 2026  
**Authority:** Accepted `nuxt-layers/architecture-rules` on `master`; this report is a non-normative working document.  
**Review evidence:** [Online Safety and Content Governance review](../../../reviews/online-safety-content-governance.md) and [candidate capability record](capability-record.md).

## Capability name
`moderation`

## Status (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed)
**Proposed only.** Availability, installation, configuration, operational readiness, enablement and authorisation are **not verified**; these states are independent and must not be inferred from a catalogue entry.

## Purpose
**Proposed:** Govern reports of content and conduct, case intake/triage, qualified reviews, decisions, appeals, coordinated enforcement requests and evidence, without owning the source content, deciding criminal guilt, or replacing the data-owning capability's enforcement.

## Classification
**Candidate Platform capability.** Distinct case and appeal lifecycles may justify independent responsibility and records. Apply classification gate; do not create a separate implementation repository solely from this report.

## Dependencies
**To investigate:** trusted caller and local Authorisation decisions; source-owned item and state references from Publisher, Media, Comments Engine, Marketplace, Messaging (if introduced) and Federation; legal applicability from Legal Compliance; safety signals from Content Security; Audit evidence contract; optional Workflow, Scheduler, Notifications and Reporting. Define directional contract edges and absence semantics before approval.

## Optional integrations
Provider-neutral detection and verification services consumed mainly via Content Security; regulatory submission gateways via Integrations; specialist external abuse intelligence; age-assurance and merchant verification through owning boundaries. No mandated provider or model.

## Version
Not defined; no `CONTRACT.md` or public API version exists.

## Availability
Concept only; implementation and acceptance unverified.

## Capabilities offered
**Proposed:** Case intake; reports by affected users/automated systems; severity triage; cross-resource references; policy/version binding; protective measures; reviewer assignment and approvals; adjudication; appeal/reconsideration; authorised enforcement handoffs; regulatory reporting coordination; status/evidence reconciliation; privacy-restricted operator and end-user views.

## Configuration
**Proposed:** Service/jurisdiction risk context, risk categories, bounded approval rules, retention and access policies, reviewer scopes, provider availability/failure behaviour, notifications and appeals. Mandatory legal/security floors cannot be relaxed by tenant preference. Publishing policy text is not proof that effective controls were enforced.

## Conceptual working notes — 17 November 2026

1. **Separate detection, case decisions and authoritative enforcement:** Content Security owns scan outcomes, Moderation owns case/decision/appeal state, and source capabilities own actual publication/removal/reinstatement and business outcomes.
2. **Legal applicability matters:** Not every harm or activity is a priority offence, and not every Node/Hub has identical OSA duties. Legal Compliance supplies qualified, dated legal duties/risk obligations. An installed Moderation package cannot certify legal compliance.
3. **Case scope:** A case can link multiple comments, media, products, sellers, accounts, peer Nodes, messages or reports. Preserve cross-tenant isolation and protect reporter/reviewer privacy. Reports and scanner flags are not findings of criminal guilt.
4. **Emergency protections:** Source owners can enforce safe pre-publication holds and rapid restrictions before investigation. Moderation may coordinate but must not be a synchronous single point of failure for essential safeguards.
5. **States to examine:** received → triaged → investigating → decision pending → enforcement requested → enforcement confirmed/failed/unknown → notice/appeal/review → closed/reopened, with separate appeal and legal-reporting states; no asserted implemented enums.
6. **Trusted interfaces:** Bounded source references/revisions, reporter evidence and consent, detection assertions with uncertainty, legal/policy context and provenance, domain enforcement receipt, appeal and correction, evidence/export and authorised operator queries.
7. **Evidence:** Audit preserves accepted attributable minimal evidence and completeness/discrepancy status, not a duplicate unrestricted store of sensitive source imagery/private messages. Source owners retain their own immutable facts and outbox events.
8. **Federated Hubs:** Hub Moderation controls Hub acceptance, derived index visibility and peering; never deletes the originating Node's records. Origin withdrawal and Hub index withdrawal are separate, reconcilable facts. Shared abuse feeds are evidence, not automatic global guilt or consensus.
9. **Private communications:** E2EE threat model is distinct; user-initiated reporting, blocking and optional local filters may be examined. Do not mandate universal client-side plaintext scanning or assume every closed group is legally exempt.
10. **Commerce:** Marketplace owns seller eligibility, seller/listing suspension and participation; Payment Gateway owns payment evidence. Identity/KYB/KYC/fraud evidence comes from appropriate specialist owners/providers. Do not assume smart-contract escrow or universal KYC is a UK OSA mandate.
11. **Metrics:** Applicable-submission coverage, exposure duration, triage/enforcement latency, appeals, false positives/reversals, provider availability, backlog ageing, evidence gaps, cross-Hub withdrawal status, with denominators and scope.
12. **Operator UX:** Moderation queue, case/detail/evidence view, triage, reviews/decisions, appeals, enforcement reconciliation, escalations and reporting; source UIs retain their actions. Host controls navigation; WCAG 2.2 AA and server-side access mandatory.
13. **Unsettled questions:** statutory reporting owner and disclosure guard; emergency holds; appeal adjudication independence; retention and evidential custody; exact policy authority and safe scanner failure modes; peer reputation; safeguarding vulnerable users; multi-jurisdiction service categorisation.

## Conceptual public input/output surfaces (not implemented)

| Surface | Inputs | Outputs |
|---|---|---|
| MOD-01 Report intake | Authenticated/anonymous report permitted by policy, source IDs, evidence classification and consent | Case ID, receipt, reporter-safe follow-up route |
| MOD-02 Automated referral | Content Security verdict and confidence, source revision, detector/version, rule context | Triage decision, case or no-case result and rationale |
| MOD-03 Triage and safeguarding | Severity, service risks, legal/policy constraints, reviewer context | Priority, immediate protective request, review/expiry deadlines |
| MOD-04 Investigation and decision | Scoped reviewer evidence, authoritative source-state query, policy/version | Qualified case outcome with reasons and limits; no legal guilt determination |
| MOD-05 Enforcement coordination | Authorised decision, exact target/revision, restricted action and idempotency key | Request to domain owner and independently confirmed/failed/unknown enforcement status |
| MOD-06 Appeal / correction | Challenge, new evidence, procedural validity, review authority | Appeal outcome, revised decision and correction/reversal requests |
| MOD-07 Statutory referral | Qualified legal duty, approved facts, disclosure authority, deadlines | Prepared handoff to designated reporting process; transport acknowledgement distinct |
| MOD-08 Evidence and reporting | Significant case transitions, source events, receipt expectations | Minimised Audit submission and authorised aggregated reporting |
| MOD-09 Federation moderation | Hub-owned peer/index references and trusted external signals | Hub-local acceptance, suspension or index removal requests with appeal |
| MOD-10 Administration / presentation | Authorised operator context, queue filters, case query | Role-filtered dashboards, queues and status with headless service mode |

## Proposed conceptual acceptance evidence
- Report and scanner referral create correctly scoped cases without copying source data or treating detection as guilt.
- Emergency hold prevents public delivery without waiting for a human case.
- Cross-domain case requests domain enforcement but never writes another owner's store.
- External scanner outage yields explicit unknown/hold/escalation per applicable risk policy.
- Appeal can correct a mistaken decision and reconcile source visibility with independently auditable history.
- Hub suppresses derived index entry while origin remains authoritative; propagates withdrawal safely.
- Private evidence remains minimised and access-audited; lawful disclosure preserves appropriate restrictions.
- Regulator-facing reporting is routed only under verified applicability and independent disclosure authorisation.

## Next review
Classify Moderation independently; determine source content ownership and preservation; examine applicable Ofcom obligations as at actual deployment; define exact contracts, lifecycle and threat model; then propose any governing amendments through the normal ADR process.
