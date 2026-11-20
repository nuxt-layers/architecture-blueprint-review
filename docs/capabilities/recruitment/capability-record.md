# **Capability Record**

## Capability Name:
`recruitment` — recruitment and candidate-selection Domain candidate.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).
**Proposed conceptual candidate; in-depth review outstanding.** Owner favours a **separate Recruitment Domain (Option A)** and approved [JOB-01–JOB-09](../job/capability-record.md) on 20 November 2026, including Job's position-only boundary. This proforma **primes later review, is not a full Recruitment conceptual approval**, public contract, implementation or legal/compliance assurance. No installation/configuration/runtime/authorisation claimed. Created as reciprocal work in [Job draft PR #84](https://github.com/nuxt-layers/architecture-blueprint-review/pull/84).

## Purpose
Potential independently governed **recruitment requisition/vacancy and applicant selection lifecycle**, consuming a versioned Job position definition when applicable, while keeping candidate evidence, application status, interview/assessment findings, employer selection outcomes, offer handover and vacancy publication separate from Job and Employment. Recruitment is a candidate Domain because applications, cases, confidentiality, dispute/appeal and vacancy state may need their own authoritative lifecycles.

## Classification
**Proposed Domain candidate; independent capability favoured by owner, detailed classification/contract not signed off.** May compose Process/Workflow/Task/Scheduler for execution, but none of these automatically owns applications or selection records. Native business authority and host integration remain for a dedicated review.

## Dependencies
**Candidate cooperation:** Job (optional, frozen position ID/revision and requirements), Identity/Authentication/Authorisation (server-side subject, tenant, permissions), Clock, Employment (dated authoritative engagement/assignment outcomes for vacancy reconciliation), Qualification/Verification (purpose-limited checked evidence), Configuration and Legal Compliance (valid policy/regulatory duties). Required versus optional ports and absence semantics are to be established; do not mandate an employment contract or a Job record for all applications.

**Potential vacancy ownership (JOB-02):** Owner favours allocating approved openings/requisitions/vacancies to Recruitment rather than Job. Detailed native objects and funding/capacity rule, authority for approval, expiry, fill/reopen and multiple adverts per opening are **open for Recruitment's own review**. Staffing budget and spend/approval evidence remain with their actual financial or policy owners; recruitment should record decisions/evidence without replacing those owners.

## Optional integrations
Publisher for publishable adverts, Search for derived listings, Integrations for job boards/ATS, Notifications/Mailer for consented communications, Process/Workflow/Task/Scheduler for staged orchestration, Audit/Logging/Observability/Reporting for their distinct responsibilities. External provider authority, confirmation, outage, reconciliation, consent, portability and withdrawal are open; external ACK must not be mistaken for confirmed publication or candidate acceptance.

## Version
Unassigned; no published Recruitment `CONTRACT.md` or API claimed.

## Availability
Candidate/proforma only. A directory does not establish an installed or approved implementation.

## Capabilities offered
**Subjects for the dedicated review, not implemented promises:** requisition/vacancy and approved seat authorisation; advertising intent, channel and publication status; candidate sourcing/application and purpose-limited dossier; stages, interview and assessment scheduling/evidence references; evaluation, conflict-of-interest and selection case; conditional offer negotiation/acceptance evidence; Recruitment-to-Employment handover with explicit receipts and unknown outcomes; withdrawal/rejection/appeal/correction, retention and restricted reporting.

**Explicit exclusions:** Job owns only position definitions; Employment owns engagements, accepted contractual conditions and effective actual assignment/occupancy; Qualification/Verification owns its own award/claim authority; Process defines processes, Workflow executes them, Task tracks assigned actions and none becomes a covert recruitment record store; Publisher owns documents; Integrations provider transport; finance/accounting owns financial decisions; Identity owns membership; Authorisation access decisions.

## Configuration
Proposed: employer/recruitment-scoped stage templates, approvals, vacancy advertising channels, equal-opportunity/purpose constraints, assessment/selection safeguards, retention, candidate communication/consent and provider modes. Configuration never establishes lawful employer status or overrides statutory floors. Final settings contract, legal/country scoping, assurance and consent require in-depth review.

## Discovery notes and outstanding findings — 20 November 2026

**Architecture:** **Job defines the position; Recruitment governs whether/when to seek and select someone; Employment governs an actual engagement.** A Job definition, a funded or approved requisition, an advertisement, a submitted application, a selection, an offer and an activated engagement are distinct events/facts, with independent owners and effective times. Do not collapse these into a `filled` boolean.

**Vacancy record questions:** one position might have multiple positions/openings; several incumbents may share assignments; internal replacements may be authorised without public adverts; a posting may represent several approved openings; one opening may appear across many boards. Determine whether the authoritative vacancy entity is a requisition, authorised opening, seat/establishment record, or several linked objects. Never equate Job's position approval or Employment's observed absence with hiring budget permission.

**Publication:** Recruitment is the proposed author of intent/approved vacancy disclosure, Publisher owns actual document, external boards own their remote listing status; Integrations coordinates provider transport. Record requested, acknowledged, confirmed, rejected, uncertain and withdrawn per channel; external confirmation requires evidence. Restrict PII and sensitive pay/role metadata, validate applicable disclosure requirements.

**Financial authority:** Recruitment records the approval source and scope for an opening/funding, but the actual budget/finance decision belongs to the identified accountable owner; neither Job editing permission nor Workflow approval action itself establishes funding. Resolve hiring-manager, HR, finance, delegated multi-party and cross-organisation authority variations.

**Recruitment-to-Employment handover:** a selection is not an accepted offer, an accepted offer is not necessarily an active employment contract, and joining does not prove right-to-work clearance or physical attendance. Define authoritative ownership of pre-engagement offer/acceptance evidence, Employment contract conditions and conditional prerequisites. Use idempotent, purpose-limited public handover with results and reconciliation; do not move candidate dossiers into Employment by default.

**Candidate evidence/security:** define lawful basis/consent when applicable, applicant access, purpose limitation, sensitive data separation, retention/deletion, adverse decisions, fairness/human review, accommodation, appeal, source provenance, automated decision safeguards, agency applicants and cross-border processing. Qualification evidence comparison is not a hiring verdict. Applicable requirements demand qualified Legal Compliance review.

**Operating without other domains:** Recruitment may handle speculative applications/talent pools without a Job position or approved vacancy if rules permit; it must distinguish those cases from authorised vacancies. Employment remains independently usable without Recruitment; Job remains independently usable without either.

**GUI (future review):** recruitment requisition/vacancy dashboard, approval and funding-evidence queue, listing status by channel, candidate/application pipeline, interview/evidence review, selection decision, offer/handover/reconciliation and compliance/retention controls; optional accessible candidate portal. Host owns navigation; headless API, WCAG 2.2 AA, BCP 47, CLDR, Theme Manager. This is a requirements seed, not approved screens.

**Later idealised public input/output contract:** define who supplies position references, applicant applications, consent, verification/qualification evidence, authorised opening requests/funding decisions, interview outcomes, external posting receipts, hire approval and accepted contractual handover; define authoritative outputs for approved vacancy/requisition, listing statuses, application and decision statuses, candidate notices, handover receipts and committed events. Specify tenant/actor/assurance/policy/revision/provenance, idempotency, time/freshness, conflict/unknown/failure, privacy and public/restricted disclosure. None is presently a published API.

**Review questions needing genuine determination:** whether Recruitment should own all vacancies including internal non-recruitment workforce establishment; funding authority boundary; initial sourcing without vacancy; candidate identity and duplicate matching; offer versus Employment agreement owner; agency/federated recruitment; employer-delegated selection rights; appeals and algorithmic decisions; archival/erasure; cross-capability contract direction and standalone minimum acceptance. Reconcile all neighbouring review records during the dedicated Recruitment PR.

**Do not prematurely mark Recruitment as reviewed/approved.** JOB-01–09 approvals settle Job's conceptual boundary and preferred Recruitment classification direction; they do not substitute for Recruitment's full mandated protocol or independent conceptual sign-off.
