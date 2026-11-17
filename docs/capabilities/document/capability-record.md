# Capability Record — Document

## Capability Name:
`document` (directory name confirmed on blueprint `master`).

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).
**Retired as an independent capability candidate by owner decision (17 November 2026); NOT available, installed, configured, operational, enabled or authorised as a separate Document capability.** Opening review 17 November 2026, [draft PR #58](https://github.com/nuxt-layers/architecture-blueprint-review/pull/58). No `nuxt-layers/document` repository found through the connected GitHub repository lookup. This is a **conceptual conditional contract**, not a published `CONTRACT.md` or proof of a functioning service.

## Purpose

> **Final classification decision — DOC-01: Approved, 17 November 2026.** Remove `document` from the working capability catalogue and capability register. The dedicated Document capability is redundant: Publisher owns its registered document lifecycle, Content Editor provides its editorial interface, Storage owns bytes, and specialist domain owners retain domain-specific records and their meaning. Do not create an independent Document service, persistence, event stream or management GUI. The conditional custody contract and DOC-02/DOC-03 scenarios below are **superseded exploratory material**, preserved only as review history and not approved interfaces or implementation requirements. This directory remains solely as a historical review artefact pending a separate preservation-before-deletion decision; no standalone capability is implied.

Determine whether an independent **private document/records custody** responsibility exists beyond Publisher's established host-registered publishing documents. A private controlled record may need receipt/filing, originals and attachments, classification, custody, evidence of receipt, legal hold, disposition and authorised production **without publication or a public URL**. Such requirements may belong to their business-domain owner, Storage, or existing Publisher extensions; a document-shaped file alone is not proof of independent authority.

**Design recommendation (proposed, not owner-approved):** preserve `document` as an **unresolved candidate**; do **not** instantiate a separate document master, generic document database or GUI until an independently justified cross-domain custody lifecycle and its owning invariants are approved. Default editorial/publication needs stay in Publisher + Content Editor. If a cross-domain custody service is accepted, refer to it as the **conditional Document Records service** below, avoiding ambiguity with Publisher documents.

## Classification
Platform **candidate**, conditional on verified shared records-custody invariants and consumers. Alternatively retire the independent capability candidate and use source-domain records + Storage/Publisher/Export. Neither outcome is approved here.

**Authority and evidence:** governing [catalogue](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/catalogue.md), normative [Capability Standard](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/capability-standard.md), actual [Publisher root contract](https://github.com/nuxt-layers/publisher/blob/master/CONTRACT.md), and blueprint [Publisher](../publisher/capability-record.md), [Content Editor](../content_editor/capability-record.md). Baseline governing SHA `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`, blueprint SHA `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`. Publisher's published contract contains drafts, revisions, approval, publishing, addresses, rich text, import/export, personal-data erasure and committed outbox events. Do not treat a proposed records service as a second Publisher. ADR-0017/0018 files at the inspected governing baseline still label themselves proposed: their concepts are not silently promoted to accepted status.

## Dependencies
**No approved runtime dependency graph for Document.** For a conditional records service: trusted host tenant/site/subject resolution; server-side Authorisation; an owner-supplied resource/evidence authority; persistence and file-byte Storage service when actual files are retained; Clock where applicable; legal/privacy constraints. Required ports fail closed; all host wiring is through documented public contracts, never another capability's private tables. A host may compose Publisher separately, but Document must **not** require Publisher to perform a private custody operation.

## Optional integrations
Publisher (only an **explicitly authorised copy/release into publication**, not shared master); Media for images, Content Security scanning, Workflow approvals, Search authorised indexing, Metadata classification references, Export for package creation, Integrations for external DMS/office systems, Notifications, Audit, Logging, Observability and Reporting. A configured provider is neither necessarily authoritative nor available. Provider credential custody and webhooks belong to Integrations/host secrets. External authority selection, conflicting versions, withdrawal, export and portability need explicit reconciliation before enabling provider-primary mode.

## Version
Conceptual contract proposal **DOC-C01** (17 November 2026); no package version, API version or implementation version verified.

## Availability
Unknown/unverified across available, installed, configured, operational, enabled and authorised. A candidate entry is not an installed or authorised service. Provider failure or missing proof must be reported as unavailable/indeterminate rather than guessed successful.

## Capabilities offered
### Ownership, exclusions and invariant
**Conditional ownership if DOC-01 is approved:** the custody register for received/controlled private records, immutable original/version evidence references, classification, owner-source association, access/disclosure markers, receipt/transfer/hold/disposition workflow state and custody-chain receipts. Keep tenant-scoped unique record identities, content digest/size/media-type, source provenance and retention/disposition evidence; store actual bytes only through a documented Storage port. The custody record must distinguish authoritative original from derivations and independently verified provenance from a user claim.

**Explicit exclusions:** Publisher exclusively owns publishing documents, editorial revisions, approvals, scheduling, public URLs, redirects, feeds and withdrawal. Source domains (Accounting, Invoice, Asset, Employment, Course, etc.) own their transaction, evidence interpretation and domain status; Document may retain an evidential artefact without becoming a legal/financial source of truth. Storage owns byte objects/access plumbing, not custody decisions; Media owns image transformations; Content Editor only its approved Publisher presentation; Rich Text safe trees and Export file conversion are not Document responsibilities. Search owns retrieval indexes, Audit independent event evidence, Legal Compliance applicability, Privacy purpose/retention/rights, Authorisation access evaluation, Workflow approval orchestration and Integrations transport. No inferred cross-tenant access from group/tenant hierarchy or creator status.

**Potential native lifecycle:** `received → validating/scanning → registered → held/active → transfer or release → retained → disposition-requested → disposed`, with explicit `rejected`, `quarantined`, `unavailable` and `disputed` statuses. A hold can coexist with active custody; do not falsely represent it as a single ordered stage. Validation of bytes, source, tenant, permitted type, digest and required malware verdict precedes availability/disclosure. Object-write success does not equal a committed custody receipt; a committed register entry with missing bytes becomes `unavailable/repair-required`, never fabricated. Corrections append provenance; do not rewrite the original silently. Retention is governed by applicable domain/legal/privacy decisions, not an arbitrary global default. Deletion/withdrawal must honour mandatory holds and emit a confirmed disposition result; a pending request is not completion.

### Idealised inbound public contract (conditional, NOT real function names)
| ID | Source → input | Owner/validation and failure |
|---|---|---|
| DOC-I01 | Host/Identity/Authentication → trusted tenant, subject, group/resource scope, assurance and correlation | Identity/Authentication own context; verify trusted resolvers, never client claims. Missing/invalid context refuses protected operations |
| DOC-I02 | Source-domain owner → resource reference, record purpose/type, ownership attestation, evidence origin, expected revision | Domain owns meaning and eligibility; verify resource existence and current authorised scope. Missing/stale/disputed source fails closed or quarantines |
| DOC-I03 | Requesting actor/service → receive/register original, attach, classify, revise metadata, transfer custody, disclose, request release/hold/disposition | Document validates command/schema/digest/size/type, explicit permitted action, expected revision, idempotency and legal restrictions. Invalid and conflict are distinct |
| DOC-I04 | Authorisation → current scoped decision/obligations; Authentication → assurance | Authorisation owns decision; deny/step-up/indeterminate never treated as allow; recheck on fulfilment and downloads |
| DOC-I05 | Storage/Content Security → object identity, integrity readback, malware verdict and confidence, retrieval health | Storage owns bytes, Content Security assessment; unknown/timeout is not safe or complete; quarantine pending resolution |
| DOC-I06 | Privacy/Legal Compliance/Configuration/Clock → applicable purpose, retention/hold/legal restriction, validated settings/effective time | Each owner retains policy/duty/time authority. Missing mandatory determinations hold unsafe disposal/disclosure |
| DOC-I07 | Workflow/Integrations → signed approval decision bound to exact version/recipient and provider receipt or reconciliation evidence | Workflow owns approval; Integrations owns provider transport evidence, not custody authority. Pending/conflicting receipts remain unresolved |

### Idealised outbound public contract (conditional)
| ID | Authorised consumer → output | Guarantee and disclosure limitation |
|---|---|---|
| DOC-O01 | Originating domain / authorised operator → registration/transfer/disposition **receipt** | Document guarantees committed custody transition, record/revision, evidence digest, actor/provenance, effective time and correlation; not authenticity of source facts |
| DOC-O02 | Authorised source-domain and UI → scoped record list/detail, classification, status, history, integrity/hold flags | Freshness/completeness markers, no existence leakage across tenant/permission boundaries; evidence owner names remain domain-owned |
| DOC-O03 | Approved recipient / Export → bounded content read or authorised file release reference, redaction/disclosure manifest | Recheck recipient/purpose/scope/hold, issue bounded access, report unavailable/partial/expired; never an unrestricted persistent bearer link |
| DOC-O04 | Audit / authorised subscribers → committed custody, hold, disclosure and disposition events | Metadata-only, source-owned outbox, at-least-once delivery and replay-safe event identifiers; no secrets/bytes in events |
| DOC-O05 | Search/Reporting → permitted index projection and records-management metrics | Scoping/revocation and completeness supplied; these consumers cannot infer public availability or source-domain truth |
| DOC-O06 | Host/Integrations → provider health, authority mode, drift/conflict and migration/reconciliation status | Explicit source, revision and uncertainty; remote acknowledgement is not a locally completed custody transition |

### Command, query and event models
**Commands:** receive/register; update classification; append corrected metadata; transfer custody; request/release hold; request/authorise/complete disclosure; request/execute disposition; reconcile provider. Check source ownership, server Authorisation, applicable legal/privacy floor, expected revision and idempotency. Differentiate `accepted`, `pending`, `committed`, `rejected`, `conflict`, `quarantined` and `unavailable`; return a stable code/messageKey, correlation and recovery instruction. A replay with the same idempotency key and payload returns the original effect; changed payload conflicts.

**Queries:** scoped collection and item status/history; custody evidence; integrity verification result; version/provenance; export/read eligibility. Every result is explicitly tenant, purpose and recipient bounded; stale/partial index results never override authoritative checks; inaccessible and unknown resource references must not enable existence discovery.

**Events:** `document-record.registered`, `document-record.custody-transferred`, `document-record.hold-changed`, `document-record.disclosed`, `document-record.disposed`, `document-record.integrity-failed` are **illustrative only**, not published event names. Emit only after a committed own-state change via a capability-owned durable outbox; subscribers deduplicate and reconcile via authorised queries. No exactly-once distributed-delivery promise.

**Common contextual fields (not a universal envelope):** stable record/resource/tenant IDs, caller and assurance provenance, scoped permission and decision revision, source version, original digest/size and encryption metadata reference (not a key), event/transaction/correlation/idempotency IDs, applicable policy/effective time and provider origin. Unknown, contradictory, expired or unverifiable evidence is not silently treated as valid.

### Conceptual acceptance scenarios (not executable tests)
| Scenario: input | Expected behaviour and output | Authority |
|---|---|---|
| Valid private original from authorised domain | Scan and verify bytes, commit one registered custody receipt, do not create a Publisher document/public route | Domain for meaning; Document for custody; Storage for bytes |
| Same registration replay | Same committed receipt; no duplicate custody record/event effect | Document |
| Wrong tenant or revoked permission | Denied/not-found-safe outcome, no readable bytes or cross-tenant metadata | Authorisation + Document |
| Wrong digest or unavailable scan | Reject/quarantine, no authorised disclosure or completed receipt | Content Security/Storage + Document |
| Stale source revision or change conflicting with hold | Conflict/held result without changing original | Domain/Legal Compliance + Document |
| External provider times out after attempted transfer | Pending/indeterminate with reconciliation token, not success; retry safely | Integrations + Document |
| Approved release to Publisher | Separate authorised Publisher create/import, Publisher-owned revision and publication, traceable source reference; withdrawal remains Publisher-owned | Publisher and Document independently |
| Historical record under legal hold requesting disposal | Refuse irreversible disposition; record request and reasons without leaking restricted legal facts | Legal Compliance/Privacy + Document |
| File missing after registration | Explicit integrity/availability failure, repair workflow and evidence; no false downloadable response | Storage + Document |
| Unsupported conversion or purported legal certification | Explicit unsupported response; defer rendering to Export and legal judgement to relevant owner | Export/domain owner |

## Configuration
Conditional settings: admitted record classes and scope, size/format limits, retention *within mandatory floors*, hold authority, inspection requirements, disclosure policy, provider selection and resilience, secure export restrictions and accessible presentation enablement. Configuration owns registered values and precedence, not custody interpretation; secrets in approved host secret management. No user preference may weaken security/legal controls.

### Cross-capability relationship and absence matrix
| Related capability | Document would receive / supply | Dependency and absence |
|---|---|---|
| Publisher + Content Editor | Authorised publishable copy/reference / provenance back; Content Editor stays Publisher-only | Optional; no automatic shared master or GUI reuse for private files |
| Storage, Content Security | Verified bytes / scan outcomes; custody/hold and access decisions remain Document's | Required if physical files are retained; unknown verdict blocks release |
| Domain owners (Accounting, Invoice, Employment, etc.) | Source evidence and ownership / custody receipts and authorised references | Required per registered record class; no automatic source-domain mutation |
| Identity, Authentication, Authorisation | Trusted scope, assurance and decision / domain resource and action context | Required protected-operation enforcement; fail closed |
| Privacy, Legal Compliance | Retention, consent/rights, legal holds / accountable application and exceptions | Conditional applicable obligations; unsafe disposal/disclosure held on uncertainty |
| Workflow, Scheduler, Clock, Notifications | External approval/coordination/time / state confirmation and requests | Optional except configured mandatory approval; scheduling never changes domain authority alone |
| Export, Metadata, Search, Reporting | Bounded source projections / generated packages, taxonomies, indexes and metrics | Optional; stale derivatives cannot authorise disclosure |
| Audit, Logging, Observability, Message Queue | Committed custody facts / evidence, diagnostics, delivery | Outbox owned by Document if built; operational telemetry not authoritative custody proof |
| Integrations | External DMS status and mapping / host-approved actions, reconcile and revocation | Optional, explicit provider-neutral authority and portability |

**Dependency direction:** host supplies public ports; Document never calls back through a reciprocal package dependency. Source domains may request custody through the Document public contract, but records must not import their private models. Any reciprocal event is notification of a committed fact, not permission to mutate the other owner. Combined Nuxt/package extension graph must remain acyclic.

### Presentation / GUI and headless operation
**Current approved generic document editorial GUI is Content Editor for Publisher; a separate Document menu is NOT justified merely by this candidate name.** If DOC-01 is approved and custody services are implemented, a **separate optional records-management workspace** is warranted, exposed via host sidebar → authorised Documents/Records dashboard, not by extending Publisher's generic editor to privately read custody tables. Views: filtered records inbox, receive/upload/scan progress, owner/source links, version and checksum history, quarantined and missing-file queues, holds/retention schedule, authorisation-aware disclosure and export requests, disposition review/confirmation, provider reconciliation and actionable errors. Host owns menu/navigation/context; Document contract owns custody results, no browser-local sensitive cache. Separate operator controls for hold/recovery and dual approval where required. Headless commands and queries remain independently usable; UI never substitutes for server validation. WCAG 2.2 AA, keyboard and screen-reader support, high contrast, responsive layouts, BCP 47/i18n, semantic Theme Manager tokens and safe no-store previews are mandatory for any eventual presentation.

### Architectural challenge and approval ledger
- **DOC-01 — Open decision (owner approval required):** establish shared private records-custody authority as a standalone Platform capability, OR keep source-domain custody with Storage, Publisher and Export. **Recommendation:** defer new capability until independently required original-file custody, cross-domain holds/disposition, provenance and disclosure are demonstrated. This review specifies the conditional contract without prejudging existence.
- **DOC-02 — Open decision:** if DOC-01 is approved, should the Document service be the custody system of record for originals or only a non-authoritative evidence reference index? Prevent two independent hold/disposition masters; prefer authoritative custody register only with explicit domain delegation and source ownership.
- **DOC-03 — Open decision:** delineate externally hosted Microsoft 365/Google Drive/DMS originals, tenant-controlled replication, offline recovery and provider-primary authority. No external system is implicitly trusted.
- **DOC-T01 — Technical investigation:** compare existing Publisher, Storage, Export and prospective domain contracts against real private-record scenarios and avoid implementing duplicate workflows; resolve by source-contract evidence rather than speculation.
- **DOC-T02 — Technical investigation:** verify applicable original-file evidence standards, chain-of-custody, retention, privacy and legal hold requirements with qualified jurisdictional review; no compliance certification claimed.
- **DOC-A01 — Acceptance:** if authorised later, independently usable root CONTRACT, own storage register/migrations/outbox, provider-neutral composition within ADR-0012 budget, negative tenant/permission cases, retention/holds, recovery, replay and CI/minimal-host evidence.
- **DOC-A02 — Acceptance:** reconcile later Publisher/Content Editor/Storage/Export and domain reviews; verify actual adoption before changing the governing catalogue.

**Sign-off:** Draft conceptual proposal only. Neither creation of a standalone package nor merger nor implementation is approved. No local tests or builds executed.
