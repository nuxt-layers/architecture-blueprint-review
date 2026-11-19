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

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed contract alignment in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not a completed metadata review, normative rule or implementation change. See [Content Editor conceptual boundary](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Content Editor may present optional schema-supported taxonomy/tag pickers, but Metadata remains owner of classifications/ontology and Publisher owns document references. A missing Metadata provider disables that optional control, not Publisher's core editing.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course owns course identifiers, units, prerequisites and learning outcomes; Metadata may own shared taxonomy mappings. Metadata unavailability must not change frozen Course semantics. This note does not complete the separate metadata review.


## Dedicated conceptual review — Metadata (19 November 2026)

**Status: proposed for owner review; not conceptually approved, implemented or normative.** Governing `architecture-rules/master` opening SHA `b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint `master` opening SHA `6dac83a03da8704f7945ee1bc894f2248300445a`. [Draft PR #95](https://github.com/nuxt-layers/architecture-blueprint-review/pull/95) and [opening evidence](../../../reviews/metadata-review-baseline.md). Authority: accepted ADR-0001/0002/0009/0012/0016, normative `docs/architecture.md`, `docs/capability-standard.md` and governing catalogue. The governing catalogue already classifies `metadata` as **Platform**, owning tags, categories, taxonomies and ontologies attached to content. `nuxt-layers/metadata` exists (`master`, README only states “metadata”); root `CONTRACT.md` retrieval failed, so **no published API, operational behaviour or implementation readiness is verified**. Publisher's root `CONTRACT.md` was read (blob `6d51c98cf2fcd40e0de4f476540a63b260f76b42`); actual Publisher functions are authoritative only for Publisher, not evidence that Metadata integration exists.

### Architectural classification and ownership gate

- **Distinct outcome:** shared, governed classification vocabulary across content and participating domain resources, including terms, controlled vocabularies, hierarchies, mapping relationships and resource-to-term assignments.
- **Authority:** Metadata owns taxonomy definitions, terms, semantic links, assignments and their respective lifecycle/revisions only when made through its public boundary. A source owner remains authoritative for the resource's identity, validity, visibility, content and lifecycle. A classification may describe a resource but cannot change its business meaning, publication, policy, eligibility or access.
- **Alternatives:** generic JSON property storage in Publisher or Configuration would fragment reusable vocabularies and cross-resource invariants; a stateless tagging helper cannot own centrally curated vocabularies or audited assignments. This justifies a distinct Platform responsibility, **not** a mandatory separate service, new deployment or prescribed store. Specific purely local application labels can remain owner-local rather than require Metadata.
- **Implementation recommendation:** retain a headless independently composable Platform capability with optional separable administrative presentation; modular-monolith default, framework-independent core or Nuxt layer subject to evidence. No direct package or Nuxt extension dependency is required by these conceptual edges. Minimal owned state is versioned vocabulary/term/relationship/assignment data plus bounded provenance and reconciliation checkpoints if needed. Search indexes, cached labels and UI state are derived/non-authoritative.
- **Disposition:** **retain**, subject to owner approval and future root-contract/acceptance evidence. This review does not upgrade the repository to implemented status.

### Purpose, exclusions and domain invariants

Metadata supports reusable, scoped classifications: **tag** (typically flat keyword), **category** (controlled grouping), **taxonomy** (versioned vocabulary, term and allowed hierarchical relations), and **ontology** (explicitly typed semantic relationships where actually justified). Keep semantic inference, reasoning engines and arbitrary knowledge graphs out of the mandatory native baseline; ontology support is a separately bounded, explicit feature, not an unbounded RDF/SPARQL commitment. Term labels, descriptions, aliases and localisation references are metadata-owned classification attributes; translation workflows belong to Localisation. Resource-authored prose, Publisher document titles, canonical addresses, full-text indices, business/product type, qualifications, permissions, Identity group hierarchies, Configuration preference values and actual legal classification determinations remain with their owners.

Suggested native records: `Vocabulary` (stable scoped ID, kind, owner scope, policies, revision, lifecycle); `Term` (stable ID, vocabulary, code/slug, labels and aliases, revision, status); `Relationship` (typed, directed, versioned semantic edge); `Assignment` (owner resource reference, term, effective/provenance data, revision/status); optional `Mapping` (source-qualified external vocabulary references with confidence/review). Term code/slug uniqueness is per vocabulary and context, not globally; prevent cycles in designated hierarchical relationships; relation semantics are type-specific; never infer a security inheritance graph from taxonomy hierarchy. Constraints for cardinality, allowable target resource kinds, term status, controlled/free tagging, vocabulary scope and permitted operations are versioned and enforced by Metadata, while resource eligibility is checked against the owning domain.

Proposed lifecycle: vocabulary **draft → active → deprecated → retired**; terms **draft → active → deprecated → retired**; assignments **proposed → active → withdrawn** or rejected with reason. Revisions and effective dates are explicit. Deprecation may retain historical links; replacement mapping does not silently rewrite historical assignment meaning. Deleting vocabulary/terms is constrained by legal retention, referential use and evidence obligations; do not promise immediate physical erasure of historical records. Edits use expected revision and idempotency; invalid/cross-scope edges, retired targets, unexpected owner-revision mismatches and unknown source state fail closed. Metadata may reconcile dangling references, but must not resurrect or alter source resources.

### Idealised public inbound contract

| Source/interface | Requiredness; submitted facts, intent or evidence | Authority, validation and degraded/unknown behaviour |
|---|---|---|
| Host and trusted caller/IAM | Required for protected operations: tenant/site or group scope, caller, assurance, resource/permission context, request correlation | Identity/Authentication identify context, Authorisation decides actions; browser claims and events grant no permission; unknown/missing context denies protected changes |
| Vocabulary steward / administration command | Required for curated vocabularies: create/revise/approve/deprecate taxonomy, terms, synonyms, typed edges, allowed target kinds and revision preconditions | Metadata validates names, canonical codes, uniqueness, cycles, incompatible constraints, concurrency and actor permission; invalid state produces stable errors |
| Source capability owner via published resource contract | Conditional for assignments: resource ID, owner kind, tenant/group, eligibility/visibility, authoritative revision, life/deletion/withdrawal signals | Publisher, Product, Course, Media or another source owns existence and exposure; Metadata verifies eligibility via public owner port where required; stale/missing/contradictory evidence cannot validate a new assignment |
| Authorised classification actor or domain integration | Required for writes: attach/detach/reclassify term(s), resource reference, expected assignment/source revision, reason, idempotency | User intent is not source-authoritative; validate vocabulary policies, resource existence/ownership, scoped permissions, term status, concurrency and cardinality; no blind writes from events |
| Configuration / host policy | Optional/conditional: available vocabularies, administrative defaults, display mode, tag versus controlled classification, feature enablement | Configuration owns host settings; Metadata owns its vocabulary constraints; missing optional preference uses safe declared default, never bypasses required restrictions |
| Localisation | Optional: locale-specific rendered labels/translation results and review status | Metadata owns term identifier and source label; Localisation supplies translated presentation, not a term identity change; fall back to permitted source label with explicit locale |
| External integrations | Optional: third-party vocabularies, imported terms, mapping evidence, provider identifiers/revisions, provenance | Integrations owns connector execution; imported values are untrusted until mapped/validated/approved; unavailable or revoked provider does not delete local authority implicitly |
| Legal Compliance / Privacy / domain retention | Conditional: applicable lawful constraints, protected-category handling, retention/erasure or legal hold, effective jurisdiction/version | Owning policy services qualify constraints; Metadata enforces applicable holds/minimisation and refuses uncertain restricted disclosure/deletion; no inference of legal compliance |
| Clock / events transport | Optional infrastructure: time semantics and durable outbox relay | Clock supplies valid temporal interpretation; Metadata owns committed facts/outbox; Message Queue moves them at least once, does not decide classification |

### Idealised public outbound contract

| Consumer | Public surface and semantics | Guarantee and limitation |
|---|---|---|
| Publisher, Content Editor, Course and other authorised domain clients | `listVocabularies(scope)`, `listTerms(vocabulary, filters)`, `resolveTerm(id, revision?)`, `validateSelection(resource, terms)` (conceptual) | Metadata-attested vocabulary semantics and suitability, not proof the owner resource exists or has published |
| Authorised resource readers and editors | `listAssignments(resource)`, `listResourcesByTerm(term, constraints)` (conceptual) | Assignments and provenance are Metadata-owned; source visibility/eligibility MUST be rechecked before revealing or using source records; index-based listings may be stale/incomplete |
| Authorised stewards and domain integration | receipts from `createVocabulary`, `reviseTerm`, `changeRelationship`, `assignTerms`, `withdrawAssignment`, `deprecateTerm` | Accepted/committed state, revision, idempotency outcome and stable error; never imply publication, approval in another domain or third-party completion |
| Search, SEO, Reporting, recommendation/presentation consumers | Versioned permitted tag/category facets, term hierarchy, safe public labels, resource assignment changes | Downstream views are derived, scoped and possibly stale; Metadata must not publish draft/private source descriptors as public |
| Audit / authorised evidence consumers | actor, action, subject scope, before/after references, policy/revision/effective time and correlation | Metadata holds its operational history; Audit owns independent accepted evidence; logs are not a business audit substitute |
| Message Queue, other subscribed capabilities | Committed `VocabularyChanged`, `TermChanged`, `RelationshipChanged`, `AssignmentChanged`, `AssignmentWithdrawn` (conceptual event families) | Facts emitted from a capability-owned durable outbox; at-least-once/replay possible, event delivery neither approves another domain action nor proves current source visibility |
| Export / portability and provider management | Authorised versioned vocabulary/term/assignment export, mapping status, import result and reconciliation exceptions | Tenant-limited, provenance-rich outputs; external mappings are source-qualified and may be partial, withdrawn or unresolved |

Contract outputs include stable IDs, version/revision, source owner reference, effective timestamp, provenance, classification scope, disclosure classification and explicit `confirmed / pending / stale / unknown` where relevant. Avoid a universal request DTO. A successful classification validation only means term/vocabulary constraints passed; it does **not** grant a domain write, access right, legal compliance claim or resource-publication transition.

### Command, query, event and recovery behaviour

Commands are server-authorised, scope-bound and conditional on expected revisions; duplicate idempotency keys repeat the recorded result rather than applying a second mutation. A permitted `assignTerms` is a Metadata commitment only after target-owner eligibility and local invariants are satisfied; concurrent source withdrawal requires conservative reconciliation or rejection. Queries distinguish private editorial from public-safe terms and report completeness/freshness, never leaking hidden source counts or labels across tenants. Canonical source checks remain the domain owner's public interface. Events are emitted only after a committed Metadata change; consumer retries/deduplication required, no exactly-once distributed guarantee. If relay fails, the durable outbox retains events and operational repair/retry is available; if the provider becomes unavailable, new restricted writes fail closed while authorised cached read-only information may be explicitly marked stale where policy permits.

### Relationships, authority and absence

| Other owner | Inputs into Metadata / outputs to owner | Relationship and failure rule |
|---|---|---|
| **Publisher** | Resource identity, revision, publication/withdrawal/erasure and eligibility; returns validated taxonomy selection and assignments | Optional classification, no reciprocal mandatory import; Publisher never delegates publishing to Metadata; source withdrawal restricts derived public facets |
| **Content Editor** | Authorised schema/context and user selections via host; returns terms, picker and validation results | Optional presentation integration only; editor has no taxonomy/assignment store; missing service disables picker without blocking Publisher core |
| **Course / Product / Media / Marketplace** | Source domain resource and visibility/eligibility evidence; returns controlled vocabulary/assignments where opted in | Optional, domain owns its learning/product/media/listing meaning, classifications cannot award qualification or authorise listing |
| **Search / SEO** | Metadata-approved public facet labels and assignments, versioned changes; may receive public address eligibility from Publisher separately | Optional derived indexing, no authority transfer; stale facet/page must be repaired when source changes |
| **Configuration / Localisation / Clock** | Host defaults, locale adaptation, time interpretation | Optional/conditional, no reownership of settings, translations or time validation |
| **Identity / Authentication / Authorisation** | Trusted tenant/group/caller and decision; Metadata returns context-scoped results | Required protected-operation access contract supplied by host; denial/uncertainty fails closed; taxonomy relationships grant zero rights |
| **Legal Compliance / Privacy / Audit / Logging** | Constraints, lawful retention/erasure, evidence sinks and diagnostics; Metadata returns classification change evidence and scoped data | Conditional safeguards; separate authoritative legal/evidential decisions from technical logs |
| **Message Queue / Integrations / Reporting / Federation** | Durable committed change delivery, qualified imports/exports, derived report and cross-node projections | Optional; no direct store coupling, imported foreign meaning must remain attributed and revocable; federation is not trusted source authority |

All edges above are **logical host-wired public-contract cooperation**, not new direct imports, Nuxt `extends` or automatically required packages. Keep joint dependency graph acyclic (ADR-0016). Avoid requiring every domain to call Metadata; a domain may simply opt out. Metadata may serve fully locally with curated vocabularies and no external ontology provider. External removal requires revocation, export, last confirmed revision and reconciliation; unknown provider operation cannot be represented as committed.

### Configuration, security, privacy and compliance

Constrain taxonomy editing separately from assignment editing, publication-facing vocabulary exposure, import/mapping and ontology administration. Server-side decisions use least privilege and resource/tenant scope; sensitive tags can reveal health, protected traits, commercial secrets or vulnerable-person status and must receive heightened purpose, consent/lawful basis, disclosure, retention and access assessment. **Never** use classification hierarchy as an Authorisation role hierarchy; an unreviewed imported label cannot override access or statutory restrictions. Apply OWASP ASVS 5 L2 baseline, L3 on sensitive operations as applicable, tenant segregation, injection-safe term rendering, input length and relationship-depth limits, import quotas, cycle checks, SSRF-safe external adapters, rate limiting and audit-worthy changes. Respect subject-data rights, lawful holds and source-owner retention coordination without promising impossible global erasure. Locale labels require BCP 47 and Unicode-safe normalisation; never normalise distinct term identifiers into accidental equality.

### Presentation / GUI and headless mode

**Optional administrator/steward GUI**, not an obligatory user-facing capability or a required Publisher screen: host sidebar **Capabilities → Metadata** links to a Metadata dashboard when enabled/authorised. Screens: vocabulary list and scope/status; taxonomy/term table or hierarchical editor; term detail, labels/translations, aliases and typed relationships; assignment explorer constrained by authorised source visibility; imports/mappings with conflict and provenance review; revision/history and deprecation/replacement; settings, exceptions and reconciliation queue. Content Editor may include a contextual tag/category picker using Metadata public reads and Publisher source permissions; private drafts never leak through autocomplete. Show empty/disabled/loading/stale/unknown/conflict/access denied states clearly, and require confirmation for consequential retire/reassign operations. Host owns routing, branding, navigation and caller context; Theme Manager supplies semantic tokens, `ui` supplies generic controls. Meet WCAG 2.2 AA, keyboard-operated hierarchical selection, accessible errors, responsive tables, BCP 47/i18n; non-visual equivalent required for graph displays. Headless mode supports the same published commands/queries with no UI dependency.

### Conceptual contract acceptance (not executed tests)

| Input / scenario | Expected behaviour and output | Authoritative owner |
|---|---|---|
| Authorised steward creates a local taxonomy and terms without providers | Versioned draft/active records and stable IDs, queryable within scope | Metadata |
| User picks a current tag for an eligible Publisher document | Permission and source eligibility checked, revisioned assignment receipt, Publisher lifecycle unaffected | Metadata for assignment; Publisher for document |
| Same idempotency key replayed after lost response | One committed change, same result or recoverable authoritative receipt | Metadata |
| Concurrent stale term or resource revision | Explicit conflict; no silent overwrite or permission widening | Metadata and source owner |
| Cross-tenant term or private assignment requested | Access denied/not found without leaking existence, label or counts | IAM decision plus Metadata enforcement |
| Invalid hierarchy cycle, unmapped import or retired term | Validation/review refusal with stable error and no invalid transition | Metadata |
| Publisher withdraws/deletes referenced source | Public assignment projections removed/restricted after confirmed source evidence; lawful historical trace retained only as permitted | Publisher owns source, Metadata assignments |
| External taxonomy provider unavailable or withdrawn | Native taxonomy remains usable; imported mapping marked stale/unknown and recovery required | Metadata owns local status; Integrations transport |
| At-least-once event duplicated / relay delayed | Subscriber deduplicates; authoritative query resolves latest revision; no fictitious exactly-once promise | Metadata outbox, Message Queue transport |
| Search/SEO receives public facet | Only permitted confirmed assignment with source visibility rechecked; derived index may report lag | Metadata classification, source visibility, Search/SEO indexing |
| Unsupported grant-access or publish-document request sent to Metadata | Explicit unsupported/forbidden response, no domain side effect | Authorisation / Publisher |
| UI disabled/headless host | All authorised public service operations remain available without screens | Metadata |

### Decisions and implementation alignment

- **MET-01 (proposed):** retain independently bounded Platform classification/assignment authority, rather than merge into Publisher or Configuration.
- **MET-02 (proposed):** include controlled flat tags, taxonomies/hierarchies and typed semantic relationships; **open owner choice** whether advanced ontology reasoning/querying is in scope now or deferred (recommend defer).
- **MET-03 (proposed):** Metadata owns cross-resource assignment records, while source capability owns resource existence, disclosure and lifecycle; **open owner choice** whether some domain-specific classifications must remain exclusively owner-local (recommend yes).
- **MET-04 (proposed):** source-qualified, versioned local authority with optional external mapping/import; provider never silently becomes master.
- **MET-05 (proposed):** optional steward GUI and contextual editor selectors, with headless operation always available.
- **MET-06 (technical investigation):** reconcile source-eligibility port shapes and revision race handling with each eventual publisher/domain root contract; no invented existing endpoint.
- **MET-07 (implementation alignment):** publish complete root `CONTRACT.md`, one-operation composition, 50-line Nuxt budget if applicable, validation/error semantics, durable outbox, import/recovery and minimal-consumer evidence.
- **MET-08 (acceptance):** demonstrate isolation, permissions, term lifecycle, historical traceability, stale references, repeatable import/export, provider withdrawal, accessibility, and no duplicated Publisher/Identity authority.

Owner approval of conceptual decisions, effective deployment model, implementation, legally compliant handling and successful automated checks **remain unverified**. Before any merge reconcile concurrent PRs and latest governing/master; no implementation edits are authorised by this record.
