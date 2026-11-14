# Capability Record — Audit

**Status:** Proposed Platform capability; conceptual review awaiting sign-off. No package, API, deployment or implementation is asserted.  
**Review date:** 14 November 2026.  
**Governing baseline:** `nuxt-layers/architecture-rules` `master` at `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.  
**Blueprint baseline:** `nuxt-layers/architecture-blueprint-review` `master` at `eeba18f12339ea67e9564c47bffae2bdba765dce`.  
**Evidence:** Governing `docs/catalogue.md` names Audit a **Platform candidate** for tamper-evident accountable business/security evidence and review, distinct from Logging and Observability. `docs/security.md` §9 requires proportionate auditable security operations. The Capability Standard and accepted ADRs establish bounded ownership, provider-neutral composition, security, privacy and tenant isolation. The initial record contained only an empty pro forma. Direct lookup of `nuxt-layers/audit` returned 404 and organisation repository search found no matching Audit repository; thus no Audit root `CONTRACT.md`, package metadata, default-branch SHA or acceptance tests were available. An organisation search is not proof that no related implementation exists elsewhere.

## Capability name, purpose and classification

**Audit** — proposed identifier `audit`; **Platform candidate**. A distinct responsibility is justified by the durable, cross-capability need to **preserve, verify and review accountable evidence of significant actions, decisions and outcomes** without reowning the facts that those actions concern. The Audit record establishes **what was asserted or observed, by which trusted source and actor/context, concerning which resource, at what times, with which outcome and evidential integrity status**. It does not make an assertion true merely because it is stored.

**Established:** The governing catalogue explicitly distinguishes Audit from technical Logging and Observability. Accepted ADR-0001 makes responsibility independent of repository, Nuxt or deployment form. **Proposed:** Audit owns the platform evidential record and verification/review lifecycle; the originator remains authoritative for domain state and event semantics. An independent repository is not yet approved.

Consumers include domain and platform capabilities (including IAM), authorised investigators, administrators and auditors, compliance processes and applications presenting authorised evidence. Normal operation needs a native evidence register and verifier, not a remote SIEM, storage vendor or connected external audit platform.

## Responsibility, records and authoritative ownership

Audit would own:

1. **Evidence envelopes**: stable audit-record identity; tenant/isolation and owning context; event class and version; action, target public identifier/type, authoritative originator and source-event identity; recording provenance; qualified actor (human, service, delegated, automated, anonymous or unknown); source assurance where verified; occurrence, observation, receipt and recording times separately; attempt/decision/outcome category; sensitivity and retention class.
2. **Evidence intake and acceptance**: authenticated producer eligibility and allowed event families; semantic validation of required provenance; deduplication and acknowledgement; quarantining or rejecting untrusted/invalid input without silently manufacturing business success.
3. **Integrity and completeness evidence**: immutable accepted revisions, detectable modification/deletion/reordering in the guaranteed scope; verification checkpoints, expected source progress where available, documented gaps, delayed delivery and disputed claims. Tamper-*evident* does not automatically mean tamper-proof, externally notarised or legally conclusive.
4. **Review and disposition**: authorised case/review references, preservation requests, annotations, findings, exceptions and review history; corrections through appended statements, never rewriting accepted evidence. A review finding is Audit-owned and must not alter the originating domain outcome.
5. **Governed lifecycle**: receipt, validation, acceptance/quarantine, protection, verification, disclosure/export, retention, lawful restriction/disposal and integrity-preserving expiry/termination evidence. Disposal must not be blocked indefinitely merely to preserve an integrity chain.
6. **Accountable access**: records of sensitive Audit viewing, exporting, investigation, policy changes, verification failures and attempted tampering, with protected controls against uncontrolled self-referential recursion.
7. **Evidence views and portability**: authorised timelines, source/actor/resource correlation, as-of evidence views, provenance and limitations, verification reports and appropriately redacted export packages.

**Does not own:** the original Accounting journal, Invoice, Asset register, Identity membership, Authentication session, Authorisation decision, Workflow approval, domain business event or owner outbox; does not grant permissions, decide legal compliance, investigate incidents as a general case-management domain, determine criminal/civil liability, implement primary metrics/traces/log processing, or become the canonical store of all document contents. Audit may retain deliberately minimised attestations and references to these facts but never replaces them.

**Source-of-truth rule:** originators own *what happened in their business domain*; Audit owns *the received evidential assertion, its custody/integrity state, review annotations and disclosure history*. If an originator changes its account of a fact, Audit appends a linked correction/reversal or discrepancy, preserving earlier assertions and provenance.

## Native functionality and invariants

A usable standalone Audit capability should:

1. Accept authorised audit submissions natively with validation, provenance, independent receipt identity and explicit accepted/pending/rejected/uncertain result; support controlled administrative submissions only with recorded authority and clear evidential classification.
2. Retain structured, minimally necessary accountable evidence and verifiable integrity metadata; distinguish attempted, denied, authorised, committed, failed, compensated, reversed, cancelled and *unconfirmed* outcomes. A denied attempt is not a successful operation; transport acknowledgement is not domain confirmation.
3. Provide trustworthy queries over tenant, originator, actor, target, event category, time range, outcome, integrity status and review status, subject to server-side access and disclosure rules.
4. Verify integrity and reported completeness across documented scopes, identify gaps and suspicious modifications, and report **unknown/unverifiable** rather than presenting gaps as success.
5. Preserve immutable accepted history while supporting linked correction, dispute, redaction/erasure or lawful disposal operations as distinct, attributable actions.
6. Apply scoped retention schedules, legal preservation restrictions and evidence-disclosure obligations; avoid collecting forbidden secrets or unnecessary personal content in the first place.
7. Provide self-contained native review and export with proof and limitations, so an optional external service is not needed to perform core evidential work.
8. Detect and recover from partial receipts, producer retries, delayed/out-of-order submissions, verifier failure, restore and split/reconciliation scenarios without silent loss or invented exactly-once semantics.

**Conceptual lifecycle:** produced/observed by originator → receipt pending/validated or quarantined/rejected → accepted and protected → periodically verified or flagged compromised/unknown → reviewed/disputed/annotated → restricted, retained, redacted where lawful or disposed under policy. Review, legal hold, integrity state and disclosure state are *orthogonal*, not one simplistic enum. Source events may arrive out of order; both source time and Audit receipt time remain visible. Archive does not imply unlimited retention. An accepted record is not edited in place; append-only claims must still admit lawful personal-data erasure or cryptographic/material redaction through explicitly validated retention mechanisms.

**Critical invariants:** tenant and resource isolation; stable source/provenance identifiers where supplied; recorded actor is neither presumed human nor automatically identified; a producer cannot attest to a stronger assurance, authorisation decision or outcome than evidence supports; replay cannot create falsely distinct business actions; lost producer events remain discoverable only when the producer provides a trustworthy completeness/checkpoint contract; records cannot be marked verified when verification cannot run; no secret, bearer token, password, session cookie or unnecessary personal profile is required in an envelope; visibility is not granted simply because a user appears as the recorded actor; independently privileged operators must not be able silently to disable or rewrite evidential controls.

**Completeness boundary:** Audit cannot prove that an event was never emitted or that an originator honestly recorded a physical event solely from an internal append-only store. Strong completeness requires a source-side expectation, sequence, reconciliation or an independent witness. The public contract must state the precise scope of each guarantee.

## Proposed conceptual public contract — seven surfaces

These are **logical contract groups**, not existing APIs, TypeScript names, packages or a mandatory universal payload.

| Surface | Inbound intention | Outbound intention and authority |
|---|---|---|
| **1. Evidence Intake** | Authenticated, scoped producer assertions; validated source event/type/version, public target refs, actor/assurance, attempt and outcome, event/observed times, correlation, retention classification | Receipt identity and accepted/pending/rejected/uncertain status, deduplication and reason; Audit confirms *receipt*, not business success |
| **2. Evidence Query** | Authorised actor, tenant/resource scope, filters, as-of criteria and disclosure purpose | Redacted chronological evidence, provenance, uncertainty, access limitation and pagination; never cross-tenant unrestricted search |
| **3. Integrity and Completeness** | Verify stated scope, source progress/watermarks where available, independent checkpoint evidence and configured assurance level | Verified/failed/incomplete/unknown result, gap and tamper signals, checked interval, proof/checkpoint references, verification time and limits |
| **4. Review and Attestation** | Open authorised review, associate records, state observations, dispute or acknowledge findings, close/reopen with grounds | Review case/reference, reviewer identity, decision history and evidence set; never changes domain business outcomes |
| **5. Retention and Preservation** | Applicable retention obligations, hold/release decisions, subject-rights requests, approved disposal or redaction requests | Policy-applied disposition, restricted/held/expired/disposed status, proof of permitted handling and unresolved conflicts; Legal Compliance/Privacy own policy constraints |
| **6. Evidence Portability** | Authorised export or external archive/sink connection, scoped time/range and disclosure profile; import of externally supplied evidence as explicitly classified assertions | Validatable export package with provenance, integrity manifest, omissions and redactions; imported evidence never silently acquires local verified-authoritative status |
| **7. Health and Control Evidence** | Query intake/verification gaps, suspend/recover channels under controlled authorisation, request reconciliation | Readiness and degraded-state indicators, receipt backlog/unknown coverage, critical audit-policy-change evidence and failure notifications through appropriate consumers |

### Input/output expectations

**Inbound:** originating capability's identified event or attempted operation, source contract/version, attribution and resource identifiers, tenant/ownership context, source outcome/confirmation evidence, independently sourced or qualified assurance claims, timestamps and correlation, sensitivity/purpose/retention category, policy constraints and authorised review instructions. Event identity and idempotency scope must be explicit; producer permission to submit does not confer permission to query others' records.

**Outbound:** durable receipt acknowledgements; audit-owned integrity/coverage status and review findings; authorised evidence timelines and exports; preservation/disposal outcome; audit-originated control alerts or verified integrity exceptions. Domain capabilities may use evidence references without Audit mutating their owned records.

**Semantic separation:** (a) *business outcome* is confirmed only by its domain owner; (b) *message delivery* by Message Queue or Integrations is not acceptance; (c) *audit acceptance* proves capture of an assertion, not its factual truth; (d) *integrity verification* proves the configured form of record continuity, not honest human intent, globally complete capture or legal admissibility.

**Failure behaviour:** required event capture for an action must specify whether a durable originator-controlled outbox satisfies the immediate obligation, whether an Audit receipt must precede committing a high-risk action, or whether the operation must fail closed. This is a risk/contract decision, **not** a blanket synchronous Audit dependency on every capability. No producer may silently claim compliance when the chosen guarantee is unavailable. Recovery reconciles expected source events/positions with accepted evidence; duplicate delivery remains distinguishable from duplicate business actions.

## Cross-capability relationship matrix

| Counterpart | Originating authoritative facts / service | Audit receives or supplies | Dependency character |
|---|---|---|---|
| **Authentication** | Authentication owns sign-in/session/MFA, step-up and revocation outcomes | Attempt, result, assurance/context and session-safe reference, not credentials; Audit stores evidential account | Risk-dependent production; no reverse domain ownership |
| **Identity** | Identity owns actors, groups, memberships, tenant and lifecycle | Opaque subject/group/tenant references and governance change assertions; display names resolved under current disclosure rules | Trust context required for relevant protected operations; no live IAM lookup required for historic interpretation if identifiers and provenance suffice |
| **Authorisation** | Authorisation owns action/resource decisions and policy grants | Authorised query/review/export decisions and policy-change/deny evidence; original decision details where safely asserted | Server-side access decision mandatory for protected actions; avoid Authorisation → Audit synchronous cycle |
| **Configuration** | Configuration owns setting declaration/precedence and governed values | Capture relevant effective policy version and approved change evidence; no Audit-owned policy editor replacing Configuration | Optional shared mechanism; Audit enforces own invariant |
| **Privacy** | Privacy owns consent/retention policy interpretation in its documented boundary | Applicable minimisation, retention and subject-rights instruction; Audit returns disposition and scoped disclosures | Mandatory applicable constraints, not necessarily mandatory package import |
| **Legal Compliance** | Legal Compliance owns jurisdictional duties, holds and legal restrictions | Receives validated applicable restrictions/hold decisions, provides custody/retention and disclosure evidence | Mandatory when applicable legal duty requires it; no universal hold indefinitely |
| **Accounting / Asset / other domains** | Each owns journals/asset lifecycle/business result and native source-event/outbox | Receives classed actions, corrections, disputed outcomes; provides evidential receipt/review references | Producer-specific optional or mandatory by risk/policy; no domain writes |
| **Workflow / Scheduler / Message Queue** | Workflow owns approval routing; Scheduler execution; Message Queue delivery, originators own outboxes | Receives attributable approvals, task triggers/executions, delivery failure evidence where necessary; can use transport without assigning it evidential ownership | Optional transport/execution mechanisms; no hidden cycles |
| **Logging / Observability** | Logging owns operational technical events and sinks; Observability owns health/metrics/traces | Correlation IDs and failure/control signals; Audit does not ingest all debug logs by default or become metrics/SIEM | Optional complementary integration |
| **Integrations** | Integrations owns external connection, credential references, provider transport and reconciliation | External evidence/provenance and provider acknowledgement versus business confirmation; optional external archive/read integration | Optional, explicit scope and non-competing authority |
| **Reporting / Search / Notifications** | Each owns presentation/derived indexes/notification delivery appropriate to its remit | Receive authorised evidence views, integrity findings and relevant alerts; no replacement evidential store | Optional projections and consumers; revocation/redaction propagated |
| **Clock** | Clock owns time semantics, not authorship or evidence | Trustworthy recorded source and receipt timestamps, time-zone interpretation and uncertainty | Shared structural clock service; no time-preference dependency |

**No mandatory package dependency is implied by this table.** Authorisation remains authoritative when access is required; origins need not import Audit synchronously. The host composes documented interfaces and preserves an acyclic graph. The responsible capability owns event definitions and transactional outboxes, not Audit or transport.

## Optional external integration and authority

**Proposed native mode:** Audit is authoritative for its accepted local evidence set, integrity checkpoints, review/disposition state and retention enforcement. Optional export to a SIEM, immutable archive, external auditor, independent timestamp authority or evidence-verification service does not transfer that authority by installation.

**Proposed connected mode:** A specifically approved external evidence repository may become authoritative for a **clearly bounded tenant, evidence class, source set and effective interval**, only after verified capabilities, lawful placement, access, retention/hold compatibility, continuity and reconciliation. During transfer, distinguish pending delivery, provider acknowledgement, confirmed external retention, verified integrity and final authority activation. Maintain source identifiers, receipts, independent checkpoints, disclosure and restore/export portability. Avoid two authoritative active repositories for the same evidence partition; do not delete locally protected originals before an approved, verifiable transfer and lawful retention decision. The exact transfer protocol, whether external authority is allowed for all evidence classes and fallback when disconnected remain **Open**.

External integrations must not claim legal admissibility, universal WORM guarantees, trusted timestamps or completeness unless independently substantiated. An imported record is a classified externally sourced claim until its provenance and verification level are established. Trusted independent anchors are useful for detecting an operator rewriting both records and internal integrity metadata, but their necessity and assurance profile are still to be approved.

## Configuration, security, privacy and compliance

- **Established:** ASVS 5.0 Level 2 minimum and relevant Level 3 security controls; server-side per-resource authorisation, explicit tenancy and group isolation, privacy by design, documented retention and erasure, tenant data region, provider independent assurance under ADR-0014, storage registers when implementation creates or causes storage.
- **Proposed mandatory audit invariants:** secure protected intake, strict producer identity/claims validation, least-privileged read/export/review/change rights, separation of evidential administration from unrestricted editing, attributable control-plane changes, rate/volume protections, secure backup/restore verification, no silent audit disablement, detection of intake outage and integrity failure. Treat Audit data as potentially high-sensitivity even without direct personal attributes.
- **Proposed policy choices:** auditable event families, severity/risk and capture assurance, redaction/minimisation schema, retention periods by lawful purpose/class, integrity checkpoint profile, independent custody, review/dual approval for exceptional disclosures and disposal, allowed external archive destinations and authority scope. Configuration may manage scoped declarations and approval; legal constraints and owning-domain meanings must not be overridden by a user preference.
- **Open tension — immutability versus data rights:** append-only evidence does not exempt personal data from purpose limitation, storage limitation, access/correction/erasure and disclosure requirements. Prefer opaque identifiers, minimal claims, separable personal metadata, selective cryptographic erasure/redaction with independently retained lawful verification evidence where justified, and explicit chain transitions on disposal. A retention hash or metadata stub may itself remain personal data; assess rather than assuming anonymisation. Actual jurisdiction-specific exceptions and legal-hold precedence need specialist validation.
- **Open assurance:** independently detect changes by compromised infrastructure administrators, multi-tenant operator collusion, lost keys, clock manipulation, hostile originators and unavailable verification anchors; declare what is and is not proved. Disaster recovery must reconcile backups with checkpoints, preserve tenant data regions and avoid silently accepting a rolled-back chain.

Relevant specialist references for later implementation review (informative, not new normative rules): OWASP Logging Cheat Sheet (separates audit/transaction trails from security logging, warns about sensitive data and tampering); NIST SP 800-92 (general security log-management guidance); UK ICO storage-limitation guidance (justified purpose-based retention rather than a universal fixed period). Applicability and legal consequences must be validated independently.

## Conceptual acceptance scenarios

1. **Native independent operation:** an application with Audit and documented host-supplied common services accepts a scoped privileged administrative change, issues a durable receipt and supports authorised verification/review without SIEM, MQ or external archive.
2. **Business outcome distinction:** Accounting emits a confirmed journal posting and later reversal. Audit preserves both linked assertions; its receipt does not create the financial posting and neither Audit nor an external sink changes Accounting balances.
3. **Denied attempt:** Authentication records a failed sign-in and Authorisation rejects a prohibited resource action. Audit records the attempts and denials without classifying them as authenticated, authorised or completed operations; no password or token is captured.
4. **Outbox and retry:** a domain action and its durable source event commit, Audit intake is unavailable, delivery retries, then succeeds. Repeated receipts are idempotently linked, source coverage gap and eventual recovery are visible. A domain unable to satisfy its chosen strict capture guarantee must refuse the risky action or report degraded status rather than assert success.
5. **Integrity attack:** a protected record is modified, deleted or reordered by a hostile operator in the declared protection scope. Verification detects the change or returns unknown if the guarantee/anchor is unavailable, never a false pass.
6. **Completeness limitation:** a producer never emitted an expected event. Audit flags a gap only if independently supplied source sequence/checkpoint evidence supports that inference; otherwise explicitly reports unverified completeness.
7. **Privacy and legal hold:** a retention/erasure request conflicts with a validated legal hold. Audit enforces the applicable decision, limits disclosure, records the disposition and resumes lawful erasure when the hold expires; neither perpetual storage nor silent deletion is assumed.
8. **Tenant isolation:** a tenant administrator cannot ingest as another tenant, search another tenant's evidence, or export evidence merely by forging tenant/group/subject identifiers. Privileged support access needs independently authorised purpose and own audit history.
9. **External repository:** a provider acknowledges an upload but has not verified retention/integrity; Audit keeps its partition locally authoritative until prescribed checks and approval. An offline provider does not silently activate, erase or replace local authority.
10. **Investigation and export:** an authorised reviewer exports a redacted timeline containing provenance, integrity result, uncertain times, missing-event warnings and disclosure restrictions; exporting itself becomes accountable without unbounded recursive logs.
11. **Recovery:** restoring an older backup creates an apparent checkpoint rollback; service is degraded until reconciled and verified, with explicit loss/uncertainty disclosed.
12. **Cross-capability corrections:** Asset corrects a disputed title claim. Audit retains the earlier and subsequent claims, attribution and evidence status, without deciding legal title or rewriting Asset's current state.

## Design challenge and unresolved decisions

| ID | Architectural question / required sign-off |
|---|---|
| AUD-01 | Confirm Audit as independent Platform responsibility and minimum coverage: security governance only, or defined business accountability event classes with risk-based obligations? |
| AUD-02 | Which actions must fail closed pending durable capture, which rely on source-owned transactional outbox, and what acknowledgement/coverage guarantee is mandatory? |
| AUD-03 | Define precise verification threat model: ordinary operator tampering, privileged infrastructure compromise, out-of-band independent anchors, and evidence of missing source events. |
| AUD-04 | Define scoped retention/hold/erasure, redaction, subject-access and cryptographic key-loss behaviour without contradicting Privacy, Legal Compliance or accepted ADRs. |
| AUD-05 | Define actor/service/delegation provenance and assurance claim trust without creating an Authorisation/Audit dependency cycle or storing unnecessary personal data. |
| AUD-06 | Decide whether a full native review-case lifecycle belongs here or whether Audit should restrict itself to evidence annotations and leave investigations to another justified domain. |
| AUD-07 | Decide permitted external authority transfer and receipt/verification requirements; what happens when external system is unavailable or evidence fails reconciliation? |
| AUD-08 | Specify retention and integrity of audit-of-audit operations, bootstrap controls, anti-recursion and dual control where justified. |
| AUD-09 | Establish bounded event schema evolution, source sequencing/idempotency, evidence import classification and cross-region/tenant correlation rules. |
| AUD-10 | Confirm whether authorised audit reporting belongs in Audit while broader analytics and dashboards remain with Reporting/Search. |
| AUD-11 | Independently validate applicable legal and industry-specific retention, admissibility, evidentiary handling and data-transfer duties; no blanket compliance claim. |

**Completeness finding:** These questions are principally *assurance-policy and authority decisions*, not missing basic functionality. Native operation and the proposed seven surfaces provide a credible conceptual boundary, but the user has **not yet approved** these choices. The record is suitable for conceptual discussion and sign-off only after the critical assurance/retention/transactional-capture questions are resolved or explicitly deferred with limits.

## Architectural consequences and review status

- **Working catalogue/register:** no change required to their provisional Audit candidate/classification or implementation-unknown status. Promote only after an approved conceptual decision; the governing catalogue remains authoritative.
- **Related capabilities:** brief reciprocal notes are appropriate in Logging, Observability and relevant business/security owners, without claiming their conceptual reviews complete.
- **Governing architecture:** no accepted ADR contradiction established at this stage. A new normative obligation on all capabilities to depend synchronously on Audit, a universal evidential schema or an altered ADR-0012 outbox shape **would** require explicit architectural approval; none is made here.
- **Implementation/repository:** not created, inspected or certified; no `CONTRACT.md` or API exists as evidence.
- **Conceptual review:** **Proposed, not signed off**. Ready for an architectural decision on risk-based capture and integrity guarantees, retention/privacy compatibility and independent-authority scope before implementation design.

**Related records:** [Accounting](../accounting/capability-record.md), [Asset](../asset/capability-record.md), [Authentication](../authentication/capability-record.md), [Authorisation](../authorisation/capability-record.md), [Identity](../identity/capability-record.md), [Privacy](../privacy/capability-record.md), [Legal Compliance](../legal_compliance/capability-record.md), [Configuration](../configuration/capability-record.md), [Logging](../logging/capability-record.md), [Observability](../observability/capability-record.md), [Message Queue](../message_queue/capability-record.md), [Reporting](../reporting/capability-record.md), [Integrations](../integrations/capability-record.md).
