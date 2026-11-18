# **Capability Record**

## Capability Name:

`assessment` — Assessment definitions, assessment execution and authoritative learner assessment results.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

**Proposed — owner-requested candidate record (17 November 2026).** Not Available, Installed, Configured, Operational, Enabled or Authorised. No implementation repository, released contract, API or runtime is asserted. This is the **pro-forma for a later independent conceptual review**, not a completed capability review.

## Purpose

Own the reusable assessment instruments and the lifecycle of conducting and evaluating individual assessments. Course defines intended learning outcomes and which assessment requirements must be met; Assessment defines assessment instruments and records the individual attempts, submissions, marking, moderation, appeal and reassessment. Training independently determines verified achievements and course completion from authorised assessment evidence and other participation facts.

## Classification

**Domain candidate**. Independent domain records/lifecycle justify a dedicated future assessment review. Implementation architecture, package, storage and GUI remain undecided.

## Dependencies

**Potential contractual cooperation (not approved package dependencies):**
- [Course](../course/capability-record.md): versioned learning outcomes, required assessment references, pass/completion specifications. Course does not own learner attempts or marks.
- [Training](../training/capability-record.md): consumes authoritative, provenance-rich assessment results and determines competency/completion; must not overwrite Assessment marks.
- [Enrolment](../enrolment/capability-record.md): identifies relevant learner participation/eligibility and applicable course version, but does not assign a mark.
- Identity, Authentication, Authorisation, Profile, Privacy and Legal Compliance: verified and permission-scoped learner/assessor relationships, assurance, safeguarding, retention and restrictions. Missing mandatory policy/permission data fails closed.
- Publisher, Content Security, Media/Storage: permitted assessment content, submitted files, malware/safety gates and versioned references where applicable.
- Workflow, Clock, Audit, Logging, Reporting: moderated marking and appeal choreography, deadlines, evidence, diagnostics and reporting without reowning assessment data.

All build/runtime dependency edges must be explicit, directional and acyclic; cooperation may use public queries, host-provided ports or committed events.

## Optional integrations

External examination platforms, proctoring, marking services, approved examination boards and remote question banks through provider-neutral [Integrations](../integrations/capability-record.md). Provider results require identity, provenance, integrity, authorised scope, version and status checks before acceptance. A remote provider is not automatically an awarding authority.

## Version

**Not released.** Proposed assessment definition version, attempt/mark revision, criterion/rubric version, effective dates, source/provenance and tamper-evident correction/appeal history; exact public contract version is deferred.

## Availability

Future configuration may permit internal-only, learner-facing, assessor and operator roles. Learner attempts and results require strict server-side per-resource access, tenant separation, age/safeguarding restrictions and result-release rules. Unknown permission, issuer validity or required safety checks blocks protected action.

## Capabilities offered

**Proposed native responsibilities for review:**
1. Define versioned examination/assignment/practical assessment instruments: questions/tasks, instructions, mark schemes/rubrics, pass thresholds, outcome mappings and permitted accommodations, subject to licensing and permitted reuse.
2. Schedule/authorise an assessment attempt *in cooperation with* cohort/session and Enrolment authorities; own attempt eligibility outcome only when explicitly delegated via a trusted public decision, never infer a seat or enrolled status.
3. Accept and validate submissions/observations securely, with integrity, provenance, permitted late-submission and permitted-assistance rules.
4. Support examiner marking, second marking/moderation, review, appeal, adjustment and reassessment as explicit state transitions with evidence and separation of duties.
5. Publish authorised results, including pass/fail or score, effective rubric version, confidence/verification state, corrections, invalidation and appeals; supply results to Training and other authorised consumers.
6. Preserve lawful histories, provider statuses and idempotent/event-driven reconciliation; mark unknown, provisional, disputed, withdrawn and final results distinctly.

**Explicit exclusions:** Course curricula; learner admissions/cohort allocations; attendance or final course completion; institutional recognition/accreditation; *formal qualification awards*; credential issuance, verification, replacement or revocation; self-declared assessment success as a credential.

### Idealised public input/output (initial review notes only)

| Input and owner | Proposed expected behaviour |
|---|---|
| Course learning-outcome and assessment-requirement/version reference (Course) | Validate that an assessment instrument maps to the applicable published course criteria; do not reown the curriculum. |
| Learner participation and effective course revision (Enrolment) | Check authorised attempt eligibility, without mutating enrolment. Unknown standing blocks assessment start. |
| Assessor identity, rights and assurance (IAM) | Enforce marking/review/appeal permissions, confidentiality and separation of duties. |
| Submission or examiner observation, linked content and screening status (learner/assessor, Publisher/Media/Content Security) | Validate integrity, safety and deadlines, persist attempt state or reject; no implicit approval of unverified files. |
| External grading/proctoring evidence (Integrations) | Check source authenticity, approved provider scope, idempotency, revision and conflicts; never automatically award a qualification. |

| Output and consumer | Proposed authoritative meaning |
|---|---|
| Assessment instrument/version/criteria (Course/Training/authorised assessment clients) | Assessment-authored specification and rubric version, not a learner's accomplishment. |
| Attempt/mark/result and appeal status (Training, learner, authorised assessors) | Authoritative assessment outcome subject to finality/appeal and disclosure; not a completed course or awarded qualification. |
| Domain events/exports (Audit, Reporting, Training, approved external adapters) | Committed attempt, result, correction, invalidation and finality changes with tenant, version, effective time and provenance; duplicate/replay-safe outbox semantics, minimised disclosure. |

**Conceptual interface shape:** Commands for instrument and attempt lifecycles, queries scoped to permitted assessors/learners, and committed domain events; stable errors, expected-version checks, idempotency and no exactly-once guarantee. Contracts and GUI are to be fully specified in Assessment's separate review.

## Configuration

Candidate assessment types, marking modes, rubric versions, moderation/appeal routes, deadlines, result-release timing, retention classifications, accessibility accommodations, permitted external assessors and provider-selection policies. Organisational settings cannot override legal, safeguarding or security requirements.

## Notes requiring later independent review (17 November 2026)

**ASMT-01 — Agreed boundary from Course review (COURSE-08):** The project owner approved three distinct responsibilities: Course specifies learning outcomes and required assessment criteria; Assessment owns assessment instruments, execution and individual assessment results; Training owns verified learning achievements and final course completion. **The creation of this candidate capability record is authorised.** This does not approve all detailed design choices listed above.

**ASMT-02 — Proposed accreditation/awards boundary (COURSE-10):** Assessment should **not** own qualifications or credentials. An exam pass is evidence for an awarding decision, not automatically an award. External accrediting organisations remain authoritative for their recognition/conditions; an authorised awarding body or a properly documented delegate is authoritative for its qualification awards. A future credential/qualification authority boundary must be considered separately; do not create it as an Assessment subfeature by default.

**ASMT-03 — Credential distinction:** Award decision, credential/certificate issuance and independently verifiable credential status (replacement, expiry, suspension/revocation, correction, public verification subject to privacy) require an explicit source authority. A certificate file in Publisher/Storage is not independently an authoritative award decision. Provider-specific signed credentials and registries belong behind Integrations, with issuer provenance and current status.

**ASMT-04 — Safeguarding/retention/appeals:** Preserve legitimate minor/vulnerable learner protections, restricted submissions, special-category/health data where present, permitted accommodations, assessment integrity, retention and evidence preservation under effective legal policy. Ensure appeals never silently overwrite original marks or Qualification awards; corrections flow as explicit attributable changes.

**ASMT-05 — Conceptual GUI:** Future author/examiner workspace for rubric/instrument authoring, attempts, submission/observation, marking, moderation, appeals and permitted learner result viewing, with headless mode, WCAG 2.2 AA, i18n and Theme Manager. GUI and provider details remain to be decided.

**Open review questions:** reusable item banks and copyright; proctoring/special-category data; attempt eligibility and invigilation; external board grading trust; moderation policy; accommodation disclosure; grading and appeal finality; immutable/revised evidence and legal holds; whether and how qualifications/credentials form a separate capability.

**Evidence/authority:** `nuxt-layers/architecture-rules` accepted ADRs and normative Capability Standard take precedence. Working [Course record](../course/capability-record.md) is non-normative; no implementation contract or tests have been verified. **Do not mark the Assessment conceptual review complete.**

## Course / Assessment / Credentials reciprocal note (17 November 2026)

**Status: Course boundaries owner-agreed, Credentials and Assessment detailed designs provisional.** [Course](../course/capability-record.md), [Assessment](../assessment/capability-record.md), [Credentials](../credentials/capability-record.md): **COURSE-08 approved and COURSE-10 clarified:** Assessment owns reusable instruments, attempts, marks, moderation and appeals; Course owns required outcomes, Training owns verified learning achievement, and Credentials owns issued proofs and their lifecycle. Raw marks are not formal awards. A trusted awarding authority/delegate determines any qualification award. Assessment records must support lawful retention, safeguarding and independently authorised disclosure. This note does not complete the separate assessment review.

## COURSE-12 — Qualification authority reciprocal note (18 November 2026)

**Status: Owner-approved conceptual responsibility; detailed Qualification review and implementation pending.** [Qualification candidate](../qualification/capability-record.md): **COURSE-12 owner-approved:** Qualification owns qualification eligibility/award adjudication and qualification-level award appeals; Assessment owns assessment instruments, attempts, marks, moderation, reassessment and assessment-level appeals. Grade changes supply source evidence for a separately authorised award review; they must not automatically produce or revoke a qualification or credential. No change to previously approved assessment ownership.


## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)); COURSE-12 retained.** Assessment owns result, moderation and assessment appeal source facts; Qualification owns formal award decision and evidence combination. Credentials may reference scoped result evidence only as prescribed by an authoritative claim-decision contract. Raw passes/grades never directly authorise recognised qualification issuance; an assessment correction must be evaluated by award owner and then propagated into issued credential status via explicit public interfaces.
