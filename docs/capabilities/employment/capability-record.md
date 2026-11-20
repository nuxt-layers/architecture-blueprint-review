# Capability Record — Employment

**Capability:** `employment` — proposed **Domain** capability; independent implementation/package not yet approved.
**Conceptual review:** 17 November 2026; **status: proposed for owner decision, not signed off**.
**Opening governing master:** `nuxt-layers/architecture-rules@2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
**Opening blueprint master:** `nuxt-layers/architecture-blueprint-review@b0b026931c4b66ec4bfc445489147045497db890`.
**Review PR:** [#59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59). [Baseline](../../../reviews/employment-review-baseline.md).
**Evidence:** Direct GitHub lookups of `nuxt-layers/employment` and `nuxt-layers/payroll` returned 404 to the connected account. Neither published root `CONTRACT.md` nor implementation was verified; absence from accessible repository listing is not proof that no functionality exists elsewhere. Do not claim operational readiness, provider compliance or an implemented API.

## Capability Name
Employment (`employment`).

## Status: Available, Installed, Configured, Operational, Enabled, Authorised and Proposed
**Proposed conceptual responsibility only.** Availability, installation, configuration, operation and technical enablement are not evidenced. Authorisation is a per-actor, per-resource, per-operation decision, not a globally true capability flag.

## Purpose
Hold trustworthy, dated and legally contextual evidence of **who is engaged by which employer/engaging organisation, under which agreement, in what capacity, and during what period**. Serve employees, workers, apprentices and other employment-related engagements while accurately distinguishing independent contractors and agency-supplied personnel. Support independent organisations and multiple simultaneous engagements for the same person without merging employer/tenant records.

## Classification
**Domain candidate**, because engagements, terms, changes, absences and termination have an independent authoritative lifecycle. This does not automatically justify a new repository or a mandatory Nuxt layer. Prefer a framework-independent business core with optional Nuxt presentation if implementation warrants it. A headless consumer must be supported.

## Dependencies
**Operation-essential concepts:** trusted employing/engaging legal-party evidence and tenant/organisation context; Identity subject references when an account exists; server-side Authentication/Authorisation; Clock date semantics; applicable qualified legal and Privacy constraints. These are *conceptual cooperation requirements*, not mandatory package imports. Do not equate tenant/group with legal employer.

**Conditional:** Job/position, Department/organisational unit, Profile contact data, Verification right-to-work/professional evidence, working-time source, Training/qualification, Asset assignments, Payroll, Accounting, Document/Publisher for signed instruments, Workflow and Notifications. No dependency cycle is permitted: hosts coordinate public ports, not private schemas.

## Optional integrations
External HR information systems, applicant tracking, electronic signing and payroll providers through Integrations. Each employer/engagement scope requires a versioned **authority-mode decision** (local Employment versus externally authoritative HR record), clear provider mapping, import/export, consent and transfer controls, conflict detection, reconciliation, outage/withdrawal and migration behaviour. Credentials remain in Integrations. Provider confirmation is not a legal conclusion; unknown remote completion remains unknown. Native operation must remain meaningful without a provider.

## Version
Conceptual contract version **unassigned**; revisions and event schemas would be explicitly versioned for implementation. No published compatibility promise.

## Availability
No verified Employment package, endpoint, screen or `CONTRACT.md`. Current review describes desired public behaviour only.

## Capabilities offered — ownership and exclusions

| Employment owns (proposed) | Employment does **not** own |
|---|---|
| Employer/engaging-party association and verified reference to relevant agreement | Identity's account, group, tenant, membership, authentication or legal-company registry |
| Person/worker engagement reference, engagement category, status and effective history | Profile's general biographical/contact record, civil identity or Verification claims |
| Agreed engagement conditions and effective amendments, contract evidence references | Job's position/post definition, vacancy or recruitment pipeline |
| Employer-specific workforce assignment, service commencement, suspension, leave-related engagement status, transfer and termination | Department's organisational structure or Authorisation's access grants |
| Employment-specific working pattern/leave entitlement **where legally assigned to Employment**, with evidence/approval histories | Actual time punches, rota, payroll calculations or statutory interpretation by default |
| Employment-specific case decisions and restricted personnel records, minimised event/outbox | Payroll gross/net calculations, tax deductions, payslips, wage payments and returns |
| Workforce standing and permitted eligibility signals for authorised consumers | Accounting financial ledgers, remuneration expense posting, bank settlement, generic Audit custody |

**Boundary invariant:** a group membership is not evidence of employment; Employment termination must request/reconcile access changes through Identity/Authorisation without itself deleting memberships or sessions. Job position existence does not create a worker engagement; a person may hold multiple engagements or positions, including across distinct legal entities and tenants. Worker classification is not a free-form label that establishes lawful status.

**Contractor distinction:** employment-like relationships can be represented when an engagement creates workforce governance obligations. A supplier delivering contracted services without an individual employer relationship remains under the suitable supplier/commercial agreement owner. Agency worker, consultant and contractor arrangements need an explicit engaging party, employer-of-record (if different), legal classification/evidence and agreed control boundaries. Avoid assuming jurisdiction-specific tests are universal.

## Native services, lifecycle and failure semantics
Native baseline: open an engagement from authorised and verified evidence; validate party/subject/engagement scope and effective terms; record controlled offers/acceptance and document references; activate or hold commencement; record amendments, assignment changes, suspension, approved absences, transfers, notice and termination; preserve historical snapshots; reconcile provider-owned state; supply restricted reads/exports; handle correction, appeals and dispute evidence; publish owned committed events through a durable outbox; support lawful retention and protective holds.

**Illustrative lifecycle:** proposed → offered → accepted → pending prerequisites → active → suspended/leave → ended; withdrawal/rejection/cancellation are separate evidenced exits. Amendments are dated revisions, not retrospective silent overwrites. Future-dated, backdated, disputed and overlapping engagements are explicitly validated. A single person can have multiple distinct active relationships. A delayed or rejected provider response does not mark an action complete.

An employment agreement, a person's acceptance, right-to-work evidence, a start-date instruction, payroll eligibility, actual access and final wage settlement are **separate states**. Ending engagement does not itself prove that payroll is final or equipment returned.

## Configuration
Configuration holds approved, scoped, versioned settings (workforce categories offered, default notice/approval paths, document templates, display preferences and integration mode), but Employment validates business meaning and legal floors. Different jurisdictions, employing entities, occupations and effective dates can impose different restrictions. Missing/uncertain mandatory legal constraints hold sensitive operations; company preferences cannot waive statutory minima. Profile owns personal preferences; Clock governs formatting/time semantics.

## Idealised public inbound contract

| Source / input | Meaning and authoritative source | Requirement and invalid/unknown semantics |
|---|---|---|
| Authorised employer actor and command | Requested onboarding, acceptance, amendment, leave, transfer or ending; Authentication/Authorisation supply independently checked caller/decision | Essential per operation; deny on missing/revoked authority, inadequate assurance or scope mismatch; business actions may require separate approval |
| Identity and legal-party evidence | Stable subject, tenant/group, standing; evidence identifying employer legal entity and acting authority, each from its own owner | Essential when establishing engagement; no account membership or tenant ID alone proves a legal employer or employment |
| Agreement/acceptance evidence | Terms, category, consent/acceptance, signatories, instrument version and provenance from suitable agreement/Document owner | Conditional by engagement and jurisdiction; unsigned/unverified/conflicting evidence remains pending or held |
| Job / Department | Position and authorised organisational assignment with validity/effective dates | Conditional; missing Job does not preclude engagement without a position, and no implied membership |
| Profile / Verification | Minimised, purpose-allowed contact details, right-to-work/qualification claims and expiry/status | Conditional; unavailable or stale essential verification holds commencement or applicable work |
| Legal Compliance / Privacy | Applicable jurisdiction, statutory obligations, employment/worker classification constraints, lawful purpose, retention and holds | Essential for legally constrained decisions; unknown or contradictory duty blocks unsafe conclusion; seek qualified review |
| Working time/leave source | Timesheets, work patterns, actual service, leave requests and approvals, each with source version | Conditional; no fabricated completed hours; distinguish authorised schedule from actual hours |
| Configuration / Clock | Effective employer-scoped policy versions, date/time zone, calendar and effective periods | Essential where used; ambiguous dates or superseded policy rejected/held |
| External HR provider via Integrations | Qualified remote engagement ID, source revision, status, callback, error and reconciliation evidence | Conditional; reject stale/conflicting updates, hold uncertain outcomes, preserve original provenance |
| Payroll / Accounting / Asset | Acknowledgements that payroll handoff, finance processing or returned equipment completed | Conditional; evidence never substitutes for Employment's own lifecycle decision |

Every input has attributable origin, recorded effective time and revision as relevant. Source facts, actor commands and third-party assertions are distinct; received events do not authorise changes.

## Idealised public outbound contract

| Output / consumer | Semantics, guarantees and restrictions |
|---|---|
| Authorised engagement detail / HR, subject, approved applications | Employer/party, category, effective terms, state and source/evidence references; redact remuneration, disciplinary and sensitive data by field/purpose |
| Workforce-standing decision facts / Authorisation, Identity coordination | Dated active/suspended/ended engagement and scope, never a direct grant, tenant membership mutation or unconditional legal entitlement |
| Payroll eligibility and approved remuneration basis / Payroll owner | Effective contract facts, period, work/leave entitlement references, approved pay elements and amended terms; Employment does not calculate net/gross pay or determine tax deductions |
| Labour allocation references / approved reporting/Payroll/Accounting | Approved work or cost-centre association and restricted source evidence; no raw pay/personnel file into general Accounting |
| Position/assignment status / Job, Department, Asset, Training | Minimal engaged/assignment change and effective dates; source Job/Department definitions and Asset custody remain authoritative |
| Lifecycle command results / caller | Accepted, held, rejected, pending provider, committed and reconciled are distinct statuses; stable reason codes and recovery paths |
| Queries and authorised export / HR, worker, Privacy | Time-scoped historical record, amendment lineage, redacted subject-access export and applicability/retention information, subject to independent disclosure checks |
| Events / subscribed capabilities | Committed engagement-created, offer-accepted, started, terms-amended, suspended, resumed, assignment-changed, ended, corrected and external-authority-reconciled events, with opaque refs, revision, provenance and minimal data; duplicate/replay tolerant |
| Provider reconciliation / HR administrators | Source system, authority mode, last verified revision/time, discrepancy and unknown state; never pretend a remote HR outage means local truth |

Every output is scoped by tenant, engagement, legal employing party, permitted fields, effective interval and version. An authorised consumer may learn a standing signal without being entitled to terms or pay. No exactly-once cross-system delivery guarantee.

## Commands, queries and events

**Commands:** propose, offer, record acceptance, request activation, approve/hold activation, amend agreement, assign/reassign, suspend/resume, record leave-related engagement change, give/record notice, terminate, correct historical evidence, reconcile remote state, request export/retention disposition. Validate server-side permission, assurance, controlling entity, expected revision and idempotency; use approved two-person review for high-risk amendments. Concurrent change conflicts cannot silently overwrite; retried same idempotency key returns original result or safe pending state. A legal record correction is a linked revision.

**Queries:** single engagement, worker's engagements in a specifically authorised employer scope, state-as-of, upcoming expiries, amendment history, authorised employer roster, restricted employee self-view and provenance; enforce projection freshness/completeness and field-level masking.

**Events:** publish only after authoritative commit via Employment-owned durable outbox; monotonic owner revision and identifiers support replay/deduplication. Consumer projections can lag; stale employment standing must not authorise access. Event data is minimised, with separately authorised detailed lookup.

**Shared context:** trusted tenant ID; independently evidenced employer legal-party ID; opaque person/engagement ID; actor and assurance; action/resource/authorisation; source/version; expected revision; effective time and timezone; provenance/correlation/idempotency; privacy purpose and optional provider origin. This is a semantic set, **not a mandatory universal object**.

## Privacy, security, assurance and legal constraints
Personnel records are high-risk personal data. Apply purpose limitation, minimisation, least privilege, encryption and segregation, separation of HR management and self-service, restricted medical/disciplinary/safeguarding fields, field-level disclosure and retention controls; do not publish identifiable workforce lists by default. GDPR/UK GDPR and employment duties vary by jurisdiction. Legal Compliance gives qualified constraints and legal hold context, but a code-level design does not establish legal correctness. Access review and departure revocation must reconcile promptly with IAM and preserve lawful employment evidence even after account closure. Audit owns accountable custody, Logging receives sanitised technical diagnostics; Reporting receives permission-filtered derivatives. Sensitive details should not leak into events, URLs, logs, search or notifications.

Treat hostile employer administrators, forged engagements, backdated changes, misclassification, multi-tenant inference, payroll impersonation, supplier misuse, provider replay and disputed termination as principal threat cases. High-impact actions may require recent phishing-resistant assurance, independent approval and notice with safe delay. Never let a manager unilaterally erase adverse evidence or circumvent applicable worker rights.

## Cross-capability relationships and directions

| Cooperating owner | Employment consumes | Employment supplies | Nature/absence |
|---|---|---|---|
| Identity / Authentication / Authorisation | Subject/tenant/group standing, caller assurance, decisions | Employment status signals, revocation requests | Essential for protected actions; no automatically inherited access |
| Legal party owner (unresolved), Legal Compliance, Privacy | Verified employer authority, qualified duty, processing/disclosure constraint | Agreement/standing facts and lawful records disposition | Essential for applicable regulated actions; hold uncertainty |
| Profile / Verification | Purpose-limited identity/contact/eligibility evidence | Restricted engagement context and rights outcomes | Conditional; never duplicate civil identity/verification |
| Job / Department | Position and structural references | Assignment and tenure facts | Conditional; neither owner infers work status |
| Payroll (candidate) | Payroll acknowledgement and settlement/closure confirmation | Approved pay basis, engagement status, leave/work evidence reference | Conditional; no gross/net/statutory computation in Employment |
| Accounting | Financial acknowledgement where specifically relevant | Limited employer-cost source reference via Payroll/authorised allocation | Optional; no direct private salary feed |
| Document / Publisher | Contract instrument, signature/evidence reference | Approved contract metadata and disclosure state | Conditional; signing not automatically established by publication |
| Working time / Task / Project / Training | Work and competency facts | Employment-specific eligibility/scope | Conditional; actual work evidence owned by origin |
| Asset | Assigned device/property custody, return status | Notice/start/end/reassignment signal | Optional; Employment does not close asset custody itself |
| Integrations / Workflow / Scheduler / Notifications | Provider transport, orchestration, due-work and delivery receipts | Scoped commands, state events and notices | Optional; failures recoverable, Employment remains domain owner |
| Audit / Logging / Reporting / Search | Evidence acknowledgements, diagnostics, permitted derived read models | Minimised attributable changes and authorised source views | Conditional; no generic personal data broadcast |

**Dependency discipline:** commands may be coordinated through the host, Workflow or explicit public ports; do not require Employment and Payroll/Job/Identity to import each other's private stores. Prefer single-owner state transitions plus acknowledged asynchronous handoffs; describe failures instead of inventing distributed transactions.

## Conceptual GUI / administration / headless operation
Provide optional accessible Employment dashboard from the host's capability sidebar: employer/context selector, authoritative roster with strict permission filters, engagement detail and dated timeline, offer/onboarding queue, agreement/verification status, assignments/changes, leave and notice/termination tasks, reconciliation issues, restricted remuneration terms, consent/subject access and audit evidence links. Employee self-service sees only authorised own records, corrections and requests. HR administrators, line managers, payroll operators, compliance reviewers and organisation owners have **different** scopes; being a tenant owner does not disclose every personal file.

Forms should use semantic native controls where appropriate, accessible validation/error summaries and clearly labelled pending/approved/held statuses; WCAG 2.2 AA, localisation, date/currency formatting via Clock and Theme Manager tokens. Host owns navigation and composition; presentation uses the public contract only. Fully headless operation is supported with no GUI package required. Never show confidential employment attributes in global search previews.

## Conceptual contract acceptance scenarios

| Input | Expected behaviour → output | Authority |
|---|---|---|
| Valid authorised new engagement with evidence | Draft accepted; not active until approved prerequisites; scoped engagement reference | Employment |
| Person has Identity group membership but no contract | No employment inferred or activated | Identity / Employment |
| Same person, two employers | Separate engagements and disclosure scopes; neither employer sees the other | Employment / IAM |
| Valid approved contract amendment effective next month | Dated revision; previous terms retained; downstream change signal | Employment |
| Unverified right-to-work/uncertain classification | Activation held with reason and review route; no invented legal determination | Verification / Legal Compliance / Employment |
| Duplicate command/replayed event | Same logical result, no duplicate engagement or repeated side effect | Employment |
| Stale manager grant or cross-tenant request | Denied even with known person/engagement ID | Authorisation / Employment |
| External HR provider timeout after remote submission | Explicit pending/unknown, reconciliation required before final completion | Employment / Integrations |
| Termination confirmed but asset/payroll outstanding | Engagement ended with separate outstanding handoffs, no fabricated settlement/return | Employment / Payroll / Asset |
| Retroactive disputed correction | Linked evidenced correction, preserved history and restricted exposure | Employment |
| Worker requests export/erasure | Purpose-scoped redacted export or qualified retained/held result; no blanket deletion | Employment / Privacy |
| Employment asked to compute net pay or post ledger | Unsupported/refused; refer authorised consumer to respective domain | Payroll / Accounting |

## Decisions and review gates
**Established:** governing public-boundary, acyclic dependency, headless optional UI, privacy/ASVS/WCAG, server authorisation, capability-owned storage/outbox and one-call Nuxt consumption requirements. **Provisional prior note (14 November):** workforce membership is not employment; Payroll computes pay; Accounting posts finance.

**Owner-approved conceptual decisions (17 November 2026; not yet normative or implemented):**
- **EMP-01 — Engagement breadth.** A: employees only; B (**approved**): employees, workers, apprentices and workforce-governed contractor/agency engagements with explicit legal and employer-of-record separation. Pure supplier contracts remain external.
- **EMP-02 — Payroll boundary.** A: Employment also owns payroll; B (**approved**): separate Payroll domain/public interface, independent even if bundled in same deployment; determine whether Payroll warrants its own repository after contract review.
- **EMP-03 — Working time and leave.** A: Employment owns every time entry/rota; B (**approved**): Employment owns contractual working hours, leave entitlements and applicable employment approvals. **Owner-approved refinement:** independent proposed Domain responsibility `time-attendance` owns actual time entries, clock-in/out, breaks, timesheets, corrections and the states of approval of worked-time evidence; independently defined Workforce Scheduling owns planned shifts/rosters and changes. The existing infrastructure `scheduler` owns background execution triggers, not workforce rosters. Payroll consumes qualified approved actual hours, not the raw authoritative attendance store. Time & Attendance's Domain boundary is approved conceptually; its final public contract, package and repository are unapproved.
- **EMP-04 — Personal records.** A: generic Profile stores all personnel files; B (**approved**): Profile owns general personal data, Employment owns employer-scoped confidential engagement records with restricted field disclosure and rights coordination.
- **EMP-05 — HR provider authority.** A: permanent native-first shadow copy; B (**approved**): per-employer scoped, explicit native or externally authoritative mode, no dual write authority; migration/reconciliation required.
- **EMP-06 — Employment vs Job.** A: Job owns person assignments; B (**approved**): Job owns positions/vacancies; Employment owns each person's engagement and assignment to those positions.
- **EMP-07 — Employer legal identity.** A: infer employer from Identity tenant/group; B (**approved**): require separate legal-party and evidence references, with owner of legal-party master explicitly unresolved; never invent corporate authority from group metadata.

**Technical investigations:** jurisdiction-appropriate employment status tests and lawful record categories; eligible labour classification; source of signed agreements and working-time facts; exact user-facing redaction, retention and worker-correction rights; external HR provider compatibility; cross-border transfers; legal-party authority resolution. These require qualified evidence and implementation design, not speculative platform law.

**Implementation alignment:** if Employment is built, publish an independently usable root `CONTRACT.md`, stable exports, permission/error contracts, schema/outbox, migration and native/remote modes, and demonstrate ADR-0012 host budget and actual secure consumption. No tests/builds run during this conceptual review.

**Sign-off:** EMP-01–EMP-07 Option B were explicitly owner-approved on 17 November 2026. The independent Time & Attendance ownership refinement was subsequently owner-approved; the candidate workforce rostering contract, legal-party master and implementation alignment remain open/proposed. Conceptual approval is not normative governing adoption, implementation readiness or merge approval. No merge without explicit approval.

## Owner decision record and working-hours refinement — 17 November 2026

**Approved by project owner:** EMP-01, EMP-02, EMP-03, EMP-04, EMP-05, EMP-06 and EMP-07, each Option B as set out above. This approval establishes conceptual direction; actual technical interfaces, classification and compliance evidence remain unverified.

**Working-hours refinement approved under EMP-03; separate conceptual authority:**
- Employment owns contractual hours and employer-specific work/leave entitlements, and approves outcomes under the applicable agreement.
- The separately owned **Time & Attendance** Domain candidate is the intended source of truth for recorded actual hours (clock events, submitted timesheets, breaks, adjustments, supporting evidence, approvals); distinguish submitted, disputed, approved, corrected and exported/payroll-accepted states. Avoid fabricating actual work from a roster, meeting calendar, task status or scheduler run.
- A future **Workforce Scheduling** domain may own planned shifts, rosters, availability coordination and shift swaps. Its actual status and packaging have not been established; existing platform `scheduler` manages timed task execution, **not staff rosters**.
- Payroll consumes versioned approved time/pay references, produces calculated pay results and reports discrepancies. Project/Task may hold work allocation/activity records, not an authoritative payroll timesheet by mere existence.
- Changes to submitted/approved hours require source attribution, worker/employer visibility as permitted, dispute and correction history, suitable controls against self-approval, privacy and statutory retention. Late correction must trigger Payroll reconciliation without rewriting past payslips silently.
- Time zone/DST interpretation belongs to Clock; lateness/overlapping shifts and working-time-limit policy require legal/contract qualification. External time-clock vendors provide evidence only under explicit authority and reconciliation.
- The owner approved Time & Attendance as an independent conceptual responsibility. Its [bounded candidate definition](../../../proposals/time-attendance-ownership.md) belongs in the blueprint catalogue/register; its detailed contract and implementation packaging require a dedicated later review.

## Qualification trust and employment interoperability — reciprocal proposal (18 November 2026)

**Status: QUAL-06–08 owner-agreed; QUAL-09 accepted in principle, details proposed in [Qualification PR #65](../qualification/capability-record.md).** Qualification independently owns source-qualified qualification awards, award recognition/mandate meaning and versioned trust evidence. Employment may consume narrowly disclosed verification and changes for genuine engagement prerequisites and continuing role eligibility; Job/employer defines the occupational/position requirements, and Employment/hiring authorities decide engagement consequences. An award-status change does not auto-terminate or suspend employment. Candidate-specific disclosures require lawful basis, proportionate purpose, authorisation and freshness. Qualification's proposed `evaluateQualificationRequirements` returns criterion-level met/not-met/inconclusive/pending with source and policy revisions, not a hiring decision. This note does not assert a published API or independent approval for employment.


## Job position/opening reciprocal proposal — 19 November 2026 (draft PR #84)

**Status: Proposed in [Job conceptual review](../job/capability-record.md), not Employment implementation or owner-approved Job contract.** Job proposes ownership of versioned position definitions, approved openings/headcount limits and listing intent/status; Employment alone owns worker engagement, contractual terms, appointments, position assignment and dated actual occupancy. Employment consumes authorised position/opening references and revisions and may emit/serve source-qualified assignment/occupancy evidence to Job; a missing Job reference must not automatically invalidate independently valid engagement. Job must not mark a post filled or open from stale/incomplete evidence, nor modify employment from a vacancy change. Public host-composed ports/orchestration avoid cyclic package dependencies. JOB-02 and JOB-04 remain open/proposed respectively.

## Job / Recruitment boundary supersession — 20 November 2026

**Updated reciprocal JOB-01–09 authority (20 November 2026):** The owner approved a **position-only Job** scope and favours a separate Recruitment Domain. Prior proposed Job vacancy/seat, publication, opening or derived occupancy authority in this record is **superseded as a Job allocation**. Job supplies versioned position references; Employment remains authoritative for actual contractual engagements, effective assignments and occupancy, and may supply scoped dated evidence to proposed Recruitment vacancy reconciliation. Recruitment, not Job, is the **proposed** owner of requisitions, vacancy lifecycle, advertising and applicant selection; precise vacancy funding and offer handover require Recruitment's dedicated review. No Employment engagement may be inferred from either a position or selection. [Job decision record](../job/capability-record.md) · [Recruitment proforma](../recruitment/capability-record.md).


## Recruitment reciprocal contract proposal — 20 November 2026

**Status: Proposed in [Recruitment draft PR #99](https://github.com/nuxt-layers/architecture-blueprint-review/pull/99); not owner-approved or an implemented interface.** Recruitment proposes purpose-limited, versioned offer acceptance and idempotent handover requests; Employment independently owns canonical agreement, engagement/assignment and actual occupancy, and returns accepted/rejected/unknown reconciliation receipts. Accepted offer is not an active engagement. No bulk candidate dossier transfer by default; Employment operates without Recruitment. Conceptual cooperation is through published contracts and host-supplied ports, not a new package import or a change to this capability's approved decisions. [Recruitment record](../recruitment/capability-record.md).
