# Capability Record — Comments Engine

**Capability:** `comments-engine` (actual blueprint directory `comments_engine`).  
**Status:** Established *Platform responsibility* in the accepted governing catalogue; this detailed conceptual model is **proposed for owner review**, not an approved runtime contract.  
**Evidence date:** 17 November 2026. **Review PR:** [#52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52).  
**Governing baseline:** `architecture-rules/master@2b5c0628e88b9698c9ad6ad57cc5315c8f879953`. **Blueprint opening baseline:** `49a12948c18f35bfd58fec632f1cbd4fd67b9a25`.  
**Implementation evidence:** `nuxt-layers/comments-engine` repository exists, default `master`; root `CONTRACT.md` was not found on inspection. **No implemented interface or operational behaviour is verified.**

## Purpose and classification

Provide reusable, independently governed **user discussion attached to another capability's addressable content/resource**, including comments, replies, comment-specific visibility and moderation enforcement, abuse-resistant submission, and authorised access to discussion threads. A substantive content lifecycle, moderation/disclosure rules and independent state ownership justify retaining the **Platform** capability classification. It is neither a generic Publisher document type nor a presentation-only widget. A headless core and optional separable presentation are appropriate; separate deployment is not presumed.

## Authoritative ownership, boundaries and exclusions

**Owns (proposed):** stable comment and thread identifiers; parent/target references; authored comment text and revisions; trusted author identity reference or bounded guest provenance; thread structure and reply limits; status transitions (pending, visible, held, hidden, removed, restored, soft-deleted and where applicable terminal redacted/erased); comment-specific enforcement decisions and action receipts; local comment policy applications, edit windows, discussion locks, per-comment operational counters and durable source events. Owns only its own authoritative discussion records and lifecycle. Related safety assessments and cases remain referenced evidence.

**Does not own:** Publisher documents/pages, Media objects, target resource availability and publication; Identity or Profile records; Authentication sessions; Authorisation access policy and decisions; Content Security scanning verdicts; cross-domain Moderation reports, investigation cases, appeals and case determinations; Legal Compliance applicability/holds; Audit evidential custody; Logging technical records; Notifications delivery; Reporting aggregate reports; Search ranking/indexes; Federation peer/trust state; rich-text syntax; theme; external social-platform comment truth. Likes/reactions/votes, direct messaging, reviews and forum topics are **not silently included**. An owner-reference relation does not confer permission to alter that owner's resource.

**Principal invariant:** the comment owner can guarantee *local* persisted comment/visibility transitions, not global removal from caches, remote Hubs or search indexes. Source target deletion/withdrawal, comment removal, case completion and audit retention are different facts.

## Native responsibilities and lifecycle

1. Register or resolve approved commentable target classes through a host-supplied public target eligibility/visibility port. Preserve target owner, tenant, opaque ID, optional resource revision, discussion scope and stable reference; never import target tables. Target absence, deleted/unknown status or inaccessible target denies new comments (or uses an explicitly authorised archival/read-only policy).
2. Accept validated create, reply and edit requests. Server-side trusted caller, scopes, authorisation, audience/age/assurance where applicable, policy version, rate/spam controls, length/attachment/link restrictions, sanitised text and idempotency are required. A reply must reference a valid same-tenant, same-target parent; prevent cycles, excessive depth and races.
3. Maintain durable per-comment revisions, timestamped state changes and author-controlled edit/delete windows. Revisions and public visibility are distinct; protect historical text from unauthorised disclosure. Deletion may be soft, redaction, erasure or retention-limited depending on qualified retention/legal hold; it is not automatically an immediate hard delete.
4. Enforce publication eligibility: pending inspection, pre-moderation/quarantine, approved and visible, hidden/restricted/removed, appeal pending (case-owned), restored where authorised. Support local emergency holds without an operational Moderation service. A scanner's unknown or adverse finding cannot mean cleared.
5. Protect threads against spam, flooding, link abuse, phishing, harassment, grooming, doxxing, injection and forged source/author claims. Apply rate limiting and author/publisher actions using bounded fair-use policies; record denial reasons without leaking detector/evidence internals.
6. Serve authorised, stable paginated threads with moderation-aware placeholders, sort/order, comment counts/availability and completeness/freshness indicators. Never assume a parent or original content is visible because a reply is.
7. Handle upstream target withdrawal/ACL changes, Identity revocation, legal hold, moderation requests and provider outage through version checks, bounded retries, reconciliation and explicit `unknown`/pending outcome. Commit authoritative changes and durable outbox events atomically where persistence supports transactions.

**Persistence recommendation:** comment/thread records, bounded revision history, target mapping, moderation status/action receipts, idempotency keys, policy snapshots/references, state transitions and source-owned outbox. Keep optional derived counts separate from authoritative state. Records, schemas and migrations are capability-owned where persistence is required, with host-supplied provider; do not place these in a universal shared database layer. Formal `STORAGE-REGISTER.md` required at implementation.

## Idealised public inbound contract

These are **logical surfaces**, not endpoint names or TypeScript/API signatures.

| Source/port | Input and meaning | Owner and validation/absence semantics | Necessity |
|---|---|---|---|
| Host/Identity/Authentication/Authorisation | Trusted tenant, caller/subject and assurance, action/resource access decision, guest eligibility and delegation | IAM retains identities/session/permission facts; deny missing/ambiguous authorisation, never trust browser actor identifiers | Required security boundary |
| Publisher or other target owner | Target ID/type/revision, tenant, discussion eligibility, resource visibility/audience, target withdrawal/reinstatement | Target owner is authoritative; inaccessible, stale, revoked or unrecognised target fails closed for writes; restricted reads do not leak target | Required per target class |
| Configuration + Legal Compliance + Privacy | Versioned comment settings, effective scope/limits, required safeguards, jurisdiction, consent, retention and legal holds | Local policy must enforce legal/security floors; missing mandatory constraints deny risky operation or hold pending qualification | Required policy inputs where applicable |
| Caller via host client | Create/reply/edit/delete, thread lock/unlock, report or local protective action, expected revision and idempotency | Validate schema, safe text, target, permissions, race/conflict, abuse limits; duplicate key repeats same committed outcome | Native operations |
| Content Security | Revision-bound text/URL/attachment assessment, verdict, provenance, uncertainty, time and provider/version | Scanner owns assessment; unavailable required verdict yields pending/hold, never implicit clearance | Conditional risk-policy port |
| Moderation candidate | Qualified case-linked restriction, reinstatement, hold/release request with actor/authority, precise target/revision, action ID/expiry | Moderation owns case and decision; Comments Engine reauthorises, checks invariants and returns accepted/completed/failed/unknown independently | Optional cross-domain case port; local holds remain native |
| Media/Storage through approved ports | Attachment references and permitted availability/scan status where attachments supported | Media owns media record and file visibility; deny unapproved files and dangling refs; no unrestricted signed URLs | Optional feature |
| Scheduler/Workflow | Due work and approved workflows, expiry/release or retention instructions | Scheduling/coordination do not override domain policy; recheck on execution | Conditional orchestration |
| Federation/Integrations | Provenance-bound foreign comment/reaction or delegated publishing intent | Remote data is untrusted until audience/consent/identity/authority established; native-only default | Optional, separately approved |

**Validation:** explicit unknown/missing/stale/contradictory source facts; optimistic revision checks; bounded rate limiting; structured denial codes. Submission request *accepted for processing* is not *published*. Guest posting, anonymous pseudonyms, attachments and federated replies require separate risk/retention policy; no implicit permissive default.

## Idealised public outbound contract

| Consumer | Authoritative output and limits |
|---|---|
| Caller, host UI and target-owner presentation | Comment/reply IDs, persisted revision, self-authored update/delete receipt, scoped list/thread tree, safe text tree, effective visibility, allowed actions, counts with completeness/freshness and conditional display placeholders; never reveal private moderation data |
| Publisher/target owner | Discussion eligibility/status summary, source-owned change and lock events, thread/count references, target withdrawal acknowledgement; never a Publisher publication decision |
| Moderation | Qualified target/revision evidence reference, policy/visibility snapshot, accepted action request receipt, completed/failed/unknown outcome, local status and protected case correlation; no unapproved private reporter evidence |
| Content Security | Minimal content/reference for permitted assessment and revision, cancellation/reassessment on edit; no general export of unmoderated private text |
| Authorised reporting, search and federation subscribers | Versioned published/hidden/revised/withdrawn notifications and scoped, disclosure-safe snapshots; consumer indexes are derived and can lag. Remote publication requires separate authorisation and withdrawal reconciliation |
| Audit | Attributable, minimised evidence for creation/edit/remove, policy moderation, locks, access/retention exceptions and enforcement/reversal with identity/assurance, policy/revision, timestamps and outcome; Audit accepts custody, not comment ownership |
| Logging/Observability | Sanitised technical error codes, latency, backlog, throttling, scan timeouts, delivery/reconciliation failures, opaque correlation and permitted tenant context; no raw comment body, credentials or sensitive reports |
| Notifications | Approved recipient/action/message key and minimal references for reply, mention, moderation outcome or appeals; notification delivery is never a domain outcome |
| Export/privacy requests | Authorised portability/deletion response with completeness, redactions, lawful exceptions and evidence of applied erasure or hold; privacy owner sets constraints, Comments Engine executes own records |

**Events:** comment-created (may remain pending), revision-committed, visibility-changed, thread-locked/unlocked, enforcement-completed/failed, comment-redacted/erased, target-detached, provider/reconciliation state where meaningful. Each event contains source ID and revision, tenant, type, occurred/effective time, actor class where safe, correlation and idempotency identifiers, schema version and disclosure scope. No subscriber may infer exactly-once delivery. Duplication, reordering, expired consent and partial delivery must be tolerated; event relay is via capability-owned durable outbox and message transport, never subscriber access to tables.

## Commands, queries and shared context

**Commands:** submit, reply, revise, author-delete, report-by-reference, lock/unlock, hold/hide/reinstate, apply case request, respond to target withdrawal, redact/erase under authorised retention, import (conditional), reconcile external withdrawal. Commands require resource-scoped server-side access, expected version, validated active effective policy, per-action idempotency, and separately represent denied, accepted, committed, pending, rejected, conflict, unknown or unavailable. An administrator cannot simply erase a legal hold.

**Queries:** comment detail, thread page, replies, own-comment history, moderator queue scoped to local comment enforcement, comment status, source discussion summary, provider/assessment health and eligible export. Apply row-level authorisation and minimise read models; explain incomplete counts/lag and source availability. No API of all comments across tenants.

**Shared semantic context:** tenant/organisation and target source; trustworthy caller/assurance, subject or bounded guest; target and comment IDs/revisions; activity purpose and policy/version; request/correlation/idempotency; effective Clock time; classifier/case/provider provenance; locale; return state and disclosure bounds. **No mandatory universal envelope.** A report/scan is evidence, not authorisation; a moderation decision is not completed enforcement.

## Cross-capability relationship matrix

| Other capability | Comments Engine receives | Comments Engine provides | Authority, necessity and failure |
|---|---|---|---|
| Publisher and other target owners | Public target visibility, policy, lifecycle, revision | Discussion and withdrawal receipts | Target authority remains with source; **required** for that target type; unknown target prevents posting |
| Identity, Authentication, Authorisation | Tenant/caller, session assurance, action decision | Scoped resource/action context and attributable outcomes | **Required** trust checks, fail closed; no copied profiles or membership policy |
| Configuration, Privacy, Legal Compliance | Effective rules, retention/consent/legal constraints | Enforcement, deletion/hold receipts | Required when applicable; unknown mandatory legal safeguard cannot be bypassed |
| Rich Text + Content Editor/UI | Safe format validation and optional field editor | Sanitised tree and editable field profile | ADR-0011 library semantics; optional UI, no transfer of record ownership |
| Content Security | Revision-qualified assessments | Minimised candidate material and assessment requests | Conditional by risk; unknown is not clear |
| Moderation | Case-linked bounded action requests | Comment/revision evidence and enforced receipts | Optional cross-domain cases; essential local moderation works without it |
| Audit | Evidence intake/acknowledgement | Independent business change evidence | Safety-significant evidence; intake failure must be reported/reconciled per governing policy |
| Logging/Observability | Technical diagnostic ports | Sanitised errors/metrics and correlation | Diagnostic outages must not authorise actions or erase required evidence |
| Reporting | Authorised aggregate specification | Source counters, submission/visibility changes and coverage denominators | Reporting owns aggregates, Comments Engine owns original facts; respect missing data |
| Notifications | Delivery outcomes | Safe event and message intents | Optional; delivery failure cannot roll back committed source state silently |
| Scheduler/Workflow/Message Queue | Timed execution, optional approval, message transport | Own tasks, approval requests and durable source outbox | One-way contractual ports; unavailability recoverable without duplicating authority |
| Federation/Search/Integrations | Remote provenance/acknowledgement, permitted indexing | Public visibility changes and controlled export | Optional; no assumption of globally completed withdrawal or portable local permissions |
| Media/Storage | Approved safe attachment reference, authorised bytes port | Comment/attachment association and detachment | Optional; never exposes private media bytes through thread APIs |
| Clock, Localisation, Theme Manager | Temporal semantics, translated interfaces, semantic theme | Localised date/status metadata and message keys | Clock shared shape; localisation/Theme Manager affect presentation, not data ownership |

**Dependency direction:** Comments Engine consumes host-supplied access, target, policy, assessment and scheduling **ports**. Publisher, Moderation and other consumers may subscribe to its public events without a reciprocal package import. Treat a two-way *message exchange* as directional contracts coordinated by host composition, not cyclic Nuxt extends or mutual private imports. Record eventual delivery/unknown states.

## Moderation and content security

Maintain distinct facts: locally validated submission; Content Security assessment; review request; Moderation case decision; comment owner's enforced state; audit receipt; remote index/cache withdrawal. Distinguish illegal-risk indicators from qualified legal determination and tenant policy breach. Risk controls include rate/behaviour detection, anti-brigading, account/guest safeguards, safe links and Unicode spoofing, rich-text XSS, CSRF, SSRF on supplied URLs, injection into downstream analysis, replay/tampered evidence, stale target ACL, editing-after-scan and moderator privilege misuse. Reassess material edits against active policy. Human reviewers should see minimised evidence in a protected interface; confidential reporters and child subjects need stronger access controls. Allow protected appeals through Moderation where enabled, with no automatic restoration. No global proactive scan of encrypted private messages implied.

An immediate local protective hold must work during Moderation outage. If Content Security is mandatory and offline, create a pending/held record or reject submission according to qualified policy; never expose first and verify later by default. If the origin record is erased subject to law, a valid held/restricted evidence reference may persist under separate privacy/retention authority without republishing the content.

## Configuration, security, privacy, provider neutrality

Versioned configurable options: enabled target classes, threading/depth, comment length/profile, edit/delete windows, slow mode and anti-spam thresholds, guest/child participation policy, pre/post-moderation routing, attachment/mention permission, external federation, notification choices, retention and visibility defaults. Statutory/legal/security minima **cannot be disabled** by tenant preferences. Consent, accessibility and qualified jurisdiction/audience/age duties require Legal Compliance and Privacy authority. Do not implement universal KYC or assert Online Safety Act compliance by adding a scanner. Any provider adapter declares supported capabilities, residency/processing/terms, cost, rate limits, confidence/uncertainty, timeouts, fallback, portability and revocation; system remains useful in native mode unless a specific policy requires an external assessment.

Privacy and data rights: pseudonymity may be compatible with controlled attribution, depending on risk and service; protect IP/user-agent identifiers and avoid storing them unless necessary, bounded and justified; prevent public inference of reporter identities. Separate public comment text from private moderation notes, detection details, appeals and protected children-related evidence. Authorised export, correction/redaction, deletion and retention/hold conflict must produce explicit disposition. Technical logs must never become shadow source records.

## GUI and host integration (conceptual)

**Recommended optional, separable presentation**, with headless operation always available. Host owns sidebar, routing, trusted caller, navigation and whether screens are enabled. The representative `application-test-template` sidebar → capability dashboard pattern is illustrative, not an automatic registration contract.

- **Reader/contributor:** contextual thread below target content; safe comment/reply composer; preview, accessible edit/delete actions, pagination/collapse, pending/hidden placeholders, reporting, rate/permission feedback, moderation status, accessible guest/age restrictions if enabled.
- **Author/source administrator:** discussion settings per target, lock/unlock, visibility summary, queue of local pending comments, action history and target withdrawal reconciliation.
- **Tenant moderator:** dashboard and queue with filters, protected content preview, comments/version evidence, hold/hide/reinstate with reason and authorisation, time-limited restrictions, appeal/case link to Moderation, conflict and unknown/failure states; do not replicate Moderation's cross-domain case workspace.
- **Platform operator:** sanitised health/backlog, scanner availability, policy provenance, outbox/reconciliation and audit evidence status; no blanket reading of all tenants' content.
- **Reports/settings:** bounded aggregate links to Reporting, provider capabilities, retention and export controls, per-tenant policy; avoid duplicate Reporting domain logic.

UI renders only through public contracts, uses Theme Manager semantic vocabulary/optional `ui`, supports BCP 47/i18n, WCAG 2.2 AA, keyboard/screen reader navigation, accessible content warnings, responsive layout and clear loading/empty/permission/pending/partial failure states. Server-side enforcement is mandatory; no client-only security gate. When presentation disabled, host may compose its own views.

## Conceptual acceptance examples

| Scenario: input | Expected behaviour | Authoritative result owner |
|---|---|---|
| Allowed author submits valid reply to visible target | Validated, idempotent commit; pending if mandatory screening/review; source revision/event | Comments Engine; target eligibility from target owner |
| Invalid parent, cross-tenant reference, failed/unknown access decision | Denied without disclosing existence; no comment committed | Comments Engine enforcement; Authorisation decision |
| Same request key replayed; stale revision used for edit | Repeat original committed receipt; stale edit conflicts, not overwritten | Comments Engine |
| Target becomes private or unpublished between check and commit | Versioned eligibility is rechecked; deny/hold and reconcile already visible comments | Target owner for availability, Comments Engine for local visibility |
| Scanner unavailable while required by policy | Hold/pending or reject; no fabricated safe assessment | Content Security for unknown; Comments Engine for enforcement |
| Moderator requests hide of exact revision; target revised since decision | Revalidate authority/revision; report conflict/unknown, not a false completed action | Moderation for decision; Comments Engine for receipt |
| Local emergency hold while Moderation unavailable | Source-local visibility restricted; later case reconciliation when possible | Comments Engine |
| Audit/queue/notification sink unavailable after committed action | Business change remains committed; outbox retries and status gap surfaced; never claim downstream complete | Comments Engine source/outbox; consumer custody/delivery separately |
| Author requests erasure during legal hold | Hold/privacy constraints honoured with qualified disposition and minimised public output | Legal Compliance/Privacy constraints; Comments Engine record state |
| Federation Hub continues showing withdrawn comment | Local withdrawal emitted and reconciliation tracked; remote confirmation not assumed | Comments Engine locally; Federation/Hub for remote state |
| Presentation disabled, host uses custom UI | Same public operations, same authorisation, no screen dependency | Comments Engine core and host UI separately |
| Unsupported cross-target reparenting or reactions requested | Explicit unsupported operation until approved contract extension | Comments Engine |

## Independent challenge and unresolved decisions

**Provisional recommendation:** retain as independent Platform capability owning authoritative comment/reply records and native local enforcement; keep Moderation as candidate cross-domain case owner. No new universal discussion/forum/reactions service is proposed.

**Owner approval required (not pre-approved):**
- **CE-01:** Permitted target classes and policy: any host-registered commentable public resource versus only Publisher-managed documents; proposed extensible **registered target contract**, with opt-in per owner.
- **CE-02:** Guest/pseudonymous commenting and participation of minors: proposed **disabled by default pending risk-qualified tenant policy**; never assume signed-in identity equals age or verified civil identity.
- **CE-03:** Formatting and attachments: propose safe plain text or ADR-0011 **Inline** formatted profile by policy, with no attachments in mandatory core; extended Block/attachments only by separately reviewed configuration.
- **CE-04:** Federation: propose **local-only default** with opt-in public-export/remote-reply protocols; do not transfer origin authority or local trust.
- **CE-05:** History and deletion: propose revision-retention based on legal/privacy policy, no unconditional public edit history and no indefinite erased-text archive.
- **CE-06:** Comment ordering, counters, reactions and mentions: propose time/parent/revision stable deterministic ordering, aggregate counts with freshness, optional mentions; exclude reaction/voting domain until separately justified.
- **CE-07:** Thread anchoring after target deletion or transfer: recommend unlisted read-only archival where legally permissible, otherwise restricted/erased with provenance receipts; precise policy and reparenting require owner decision.

**Technical investigations (not owner policy questions):** evidence of target implementation maturity and actual root contract; target-registration semantics with Publisher/other owners; effective privacy and OSA service classification by jurisdiction; capacity and index/cache invalidation; no universal event schema without accepted ADR; provider data protection and false-positive controls; server-side performance/pagination/read model.

**Acceptance work:** publish actual independently usable root `CONTRACT.md`, documented one-operation composition and ≤50-line Nuxt host budget if implemented as a layer, independent fake provider/negative-path acceptance, ASVS 5 L2/L3 risk-based checks, WCAG 2.2 AA, threat model, `STORAGE-REGISTER.md`, CI/user-run tests and source-defined deployment readiness. All are future, unverified implementation activities.

## Existing approved conceptual note (preserved)

## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Comments and reports:** Comments Engine remains authoritative for comment/thread content, visibility, deletion, restoration and its comment-specific moderation states. User reports or multi-domain incidents may be referred to the proposed Moderation capability, with stable comment/version references and separate case decision. Comments Engine executes any requested restriction through its own authorised contract and provides actual outcome receipts. Abuse of reports/appeals and harassment/grooming patterns require protected reporter data and human-review channels.

