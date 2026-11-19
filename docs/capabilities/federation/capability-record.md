# Capability Record — Federation

**Status:** Candidate Platform capability; conceptual direction approved for blueprint documentation on 17 November 2026. Classification and implementation require independent review; no repository, implementation or public API is asserted.  
**Review date:** 17 November 2026.  
**Architectural authority:** `nuxt-layers/architecture-rules` accepted ADRs and normative documents on `master`; this working record is non-normative.  
**Evidence:** Node–Hub conceptual architecture discussion (17 November 2026); [Node–Hub architecture review](../../../reviews/node-hub-federation-architecture.md). Existing `search`, `identity`, `authentication`, `authorisation`, `publisher`, `message-queue`, `content-security`, `audit`, `logging` and `site-hosting` responsibilities were compared at architectural level. No federation implementation `CONTRACT.md` has been verified.

## Summary, purpose and classification

**Federation** is a *candidate* bounded Platform responsibility for optional, interoperable publication and consumption of authorised records between independently governed installations. It coordinates peer relationships, publication subscriptions, protocol exchange, synchronisation cursors, delivery/reconciliation and withdrawal evidence. It neither owns originating business records nor operates a universal search engine.

**Node** denotes an independent installation and network participant, not a new business capability. **Hub** denotes an optional *operating role/application composition* that combines Federation with Search and applicable trust, moderation and presentation services. Every Hub operates as a Node; any appropriately configured and authorised Node may operate Hub services. An installation can operate multiple separately governed Hub services, subject to explicit isolation and policy. A Node need not participate in federation, and federation-capable Nodes need not index remote records.

**Initial classification recommendation:** retain `federation` as a proposed Platform capability with independently meaningful coordination state, but apply the capability classification gate before creating a package. Retain `hub` as application-composition vocabulary, not a standalone stateful capability. Proposed federation service may be implemented framework-independently with an optional Nuxt adapter; no new manifest, repository or separate deployment is approved by this record.

## Authority, ownership and explicit exclusions

| Dimension | Federation candidate owns | Owned elsewhere / excluded |
|---|---|---|
| Peer relationships | Registration, subscription intent, verified endpoint associations, negotiated capabilities, suspension and withdrawal state | Identity owns local principals/tenants/groups; Authentication owns local credentials/session assurance |
| Exchange subscriptions | Collection and peer subscription state, approved feeds and destinations | Publisher/Job/Marketplace/other sources own underlying published resources and publication policy |
| Synchronisation | Delivery attempts, cursor/checkpoint state, retries, reconciliation and tombstone acknowledgement where supported | Message Queue transports capability-owned events; Temporal Gateway integrates infrastructure execution; Scheduler owns scheduled work |
| Inter-node protocol | Validation, version/capability negotiation, bounded remote fetch and provenance for exchange | Host manages network endpoints/secrets; Site Hosting manages addresses/domains; Integrations owns provider-specific external application adapters |
| Trust coordination | Peer trust signals and accepted publisher/collection decisions in scope, with evidence and appeal route | Authorisation owns access decisions; Content Security owns safety scanning; Legal Compliance supplies legal constraints; Audit owns evidence custody |
| Index handoff | Canonical, signed/verified where supported, authorised indexable record envelopes and update/withdrawal signals | Search owns derived indexes, ranking and query execution; Reporting owns authorised aggregates |
| Application experience | Optional operator-facing peer/subscription diagnostics and status | Hub composition chooses search experiences, navigation, marketplace/forum/jobs presentation and host routes |

**Invariants:** local capability data remains authoritative; remote index content is derived and may be stale; an index entry is not authoritative price, availability, permission or entitlement. Participation grants no cross-tenant membership, resource access or control of the origin Node. A Hub cannot compel publication, suppress local operation or become a required central registry. An operator must be able to leave a Hub and use another, with appropriate withdrawal semantics. No blanket cross-node replication of private data.

## Conceptual operating modes and lifecycle

- **Standalone Node:** all local applications remain functional with federation disabled or offline; no federation dependency.
- **Publishing Node:** selects approved public collections, advertises them to one or more Hubs, and publishes changes/withdrawals under local policy.
- **Discovering Node:** queries selected Hub indexes; may publish nothing.
- **Hub Node:** runs the Hub application composition, receives permitted remote publications and offers indexes/discovery; may also publish its own collections.
- **Multiple Hubs:** direct Node-to-Hub subscriptions first. Hub-to-Hub exchange is optional future work; no mandatory global directory or distributed consensus layer.

**Peer lifecycle (proposed):** discovered/requested → verified/policy checked → active → paused/suspended → withdrawn/revoked; include incompatible/unreachable/unknown outcome explicitly. **Collection lifecycle:** declared → approved → published → updated → withdrawn/expired. **Delivery lifecycle:** pending → attempted → accepted/duplicate/rejected/indeterminate → retried/reconciled. **Index freshness:** fresh/last-confirmed/stale/withdrawn/unknown, with TTL and source revision where available.

**Failure and recovery:** network outage may delay discovery but must not alter the originating transaction. Notifications can be missed, duplicated or reordered; pull snapshot/checkpoint reconciliation repairs state. Retrying and reprocessing must be idempotent. Unknown delivery and unknown remote policy outcome never imply acceptance or authorisation. Deletion notices/tombstones are propagated according to lawful retention and documented propagation guarantees; no claim of instant deletion from every remote cache.

## Conceptual public contract — inputs and outputs

These are *idealised logical surfaces*, not implemented methods or a prescribed universal wire schema.

| Surface | Inputs received | Outputs, guarantees and failures |
|---|---|---|
| **FED-01 Node and protocol capability discovery** | Explicit configured peer URL or independently discovered record, supported protocol/version and trusted host context | Verified endpoint, supported collections/protocols, freshness and incompatible/unknown/untrusted status; no single compulsory directory |
| **FED-02 Peer and Hub participation** | Authorised operator, peer identity/evidence, scoped subscription/publishing intent, policies | Registration, active/suspended/withdrawn state, reason, effective scope and auditable decision; participation does not grant resource access |
| **FED-03 Collection declaration** | Source-owned public collection descriptor, canonical origin, schema/version, access and visibility policy | Validated publication declaration, canonical discovery reference and explicit exclusions; no read of source private tables |
| **FED-04 Change publication** | Source-issued durable change fact/reference, version, canonical record ID, publication permission and causal ID | Idempotent delivery attempt/status, bounded metadata, accepted/unknown/retry/rejected result; remote acceptance is not origin transaction completion |
| **FED-05 Remote record retrieval** | Peer request, trusted caller/peer identity, collection/item reference, allowable representation | Authorised, validated source envelope, revision and provenance or deny/not found/unavailable; no direct domain storage exposure |
| **FED-06 Inbound validation** | Untrusted remote publication envelope, proof/signature metadata, schema and source location | Accepted/rejected/quarantined decision, validated metadata and source provenance; no direct index write without checks |
| **FED-07 Synchronisation and withdrawal** | Signed or otherwise authenticated update/deletion signals, checkpoint/snapshot request, version and retention context | Resume cursor, reconciliation result, staleness and withdrawal acknowledgement where supported; bounded eventual convergence |
| **FED-08 Index/search integration port** | Accepted, public, validated indexable records and withdrawal events | Derived-index update request and status from Search; Federation does not own query syntax or ranking |
| **FED-09 Operational governance and evidence** | Operator policy changes, abuse reports, peer health, legal/privacy restrictions and audit correlation | Scoped trust decisions, actionable health/errors, minimised audit evidence and sanitised diagnostics; explicit appeal/review workflows |
| **FED-10 Federation management presentation** | Authorised admin or publisher context and scoped status queries | Peer/Hub subscriptions, collection visibility, freshness, sync history, controls and accessible status states; headless mode supported |

A provisional envelope needs stable canonical resource ID, originating publisher/Node identity, collection/type, schema version, source version, update timestamp, canonical retrieval address, visibility, provenance and withdrawal marker. Cryptographic verification and exact signature mechanisms require protocol selection and threat modelling. Do not equate a cryptographic signature with proof that a listing is true.

## Inputs, outputs and cross-capability relationships

| Cooperating capability or composition | Federation receives | Federation supplies / boundary |
|---|---|---|
| Publisher and domain owners (Product, Jobs, Events, Forum/Comments, Marketplace) | Explicitly approved public representations, authoritative updates and withdrawals | Subscription/publication transport; never writes their records or makes their domain decisions |
| Authentication / Identity | Trusted local actor and service-principal evidence; candidate remote trust mapping | Verified *claims* only; remote peer identity never automatically becomes a local principal/member |
| Authorisation | Trusted decision for publication, retrieval and admin operations | Resource/operation context for server-side access decisions; no permission inheritance from Hub subscription |
| Privacy / Legal Compliance | Disclosure, retention, lawful removal and jurisdiction constraints | Transfer/withdrawal evidence and bounded coordination; no bypass of legal obligations |
| Search | Supported derived indexing and query port | Validated indexable records, provenance, source revisions, expiry/withdrawal updates; Search owns index and result query |
| Site Hosting / host configuration | Domains, verified endpoints, networking and secret references | Discovery endpoints and diagnostics; no ownership of TLS/proxy or vendor credentials |
| Message Queue / Scheduler / Workflow / Temporal Gateway | Transport and task orchestration via documented public boundaries | Retry/reconciliation jobs, moderation review requests; no duplicated generic queue, scheduler or workflow engine |
| Content Security / Audit / Logging / Observability | Scan decisions, accepted evidence contracts, technical telemetry | Candidate quarantine/moderation events, provenance, failures and health without leaking private content |
| Hub application composition | Publisher/peer policy, selected discovery experiences, navigation settings | Federation coordination operations; Hub composes Search and other services without becoming an additional domain owner |

**Contract integration:** all interactions use published, one-way contract/port dependencies and capability-owned outboxes as applicable; remote bidirectional exchange is not a licence for cyclical local package dependencies. A Nuxt adapter would still obey ADR-0012 single-call/50-line integration and ADR-0016. Use optional dependencies with explicit absence modes.

## Persistence and information lifecycle

If independently justified, Federation owns the minimum durable state for peer associations, subscriptions, approved collection declarations, cursor/checkpoint progress, delivery/idempotency keys, scoped trust outcomes and retirement/withdrawal coordination. It does **not** store source business records as authoritative data or duplicate Search's derived index. Data retention, tenant/publisher isolation, export, erasure, lawful holds, network metadata privacy, replay resistance and secure transport must be documented before implementation. Its own `STORAGE-REGISTER.md` would be required when storage exists. No specific database, bucket, consensus algorithm or shared persistence platform is imposed.

## Conceptual GUI, navigation and presentation

**Possible optional screens:** a Federation dashboard (enabled/disabled state, peers, delivery and sync health); published collections and visibility; subscribed Hubs and participation status; peer trust/acceptance and suspension controls; sync history, stale data, retry and withdrawal details; review/appeal queues and privacy disclosures. A dedicated Hub composition could add index statistics, category feeds, search presentation and operator accounting, but these are not Federation's business records.

**Audiences:** authorised Node administrators, publishers, Hub operators, moderators/auditors and permitted support operators with distinct scopes. Server-side decisions enforce every action. The host controls the sidebar/navigation entry and routes; enabled capability dashboards can follow `nuxt-layers-test/application-test-template`'s conceptual pattern without implying automatic menu registration. Theme Manager vocabulary, WCAG 2.2 AA, internationalisation, low bandwidth and clear empty/offline/stale/error states apply. The core must work headlessly, with presentation switched off.

## Threats, standards and design alternatives

- Threats: malicious/impersonating publishers, forged updates, replay, unsafe remote URL retrieval/SSRF, DNS rebinding, metadata leakage, unauthorised publication, spam, index poisoning, huge records, denial-of-service, stale/inaccurate commerce, abusive defederation, concentration of Hub control, non-removal of withdrawn data, and amplification through Hub-to-Hub loops.
- Apply current security, privacy, authorisation and audit floors. Inbound remote requests and outbound fetches are untrusted, require bounded rates/payloads, safe allowed schemes/hosts, verification and independent moderation policy. Do not mandate client-side scanning of private E2EE communications as an architectural prerequisite.
- Evaluate existing standards before inventing a protocol: WebSub (publication notification), ActivityPub (social activity federation), AT Protocol's PDS/relay/app-view separation (architectural precedent), HTTP/JSON Schema and HTTP Message Signatures where appropriate. None individually establishes the whole Hub application, trusted business listings or query semantics.
- Prefer **direct Node–Hub subscription and independent Hub indexes** first. Hub-to-Hub exchange and a distributed replicated index remain separate, later decisions; do not assume consensus, blockchain, token economics or global directories.

## Conceptual acceptance scenarios

1. Standalone Node runs its local marketplace/forum/jobs with no federation enabled; offline/disconnected operation continues.
2. Node A advertises and publishes an authorised vacancy; Hub Node B indexes it; Node C searches B and follows the canonical link to A. Application and authoritative transaction stay on A.
3. Node A changes or withdraws a listing; duplicate/reordered updates and missed notifications reconcile from checkpoints; stale entries are flagged and withdrawn under stated eventual-consistency guarantees.
4. A Node publishes to two independently governed Hubs and withdraws from one without losing its original data or membership elsewhere.
5. One Node enables Hub operation while retaining its original local apps; another Hub Node operates without any local shop/forum. Multiple separately scoped Hub services cannot cross-leak data.
6. Hub or Node outage yields bounded degraded discovery without permitting unauthorised reads, invented successful deliveries or improper domain writes.
7. Untrusted remote publication attempts SSRF, impersonation, replay, oversized payloads or cross-tenant leakage: refuse safely and create appropriately scoped evidence.
8. A Hub rejects or suspends a peer under versioned policy, with provenance and review/appeal pathways; rejection cannot prevent independent Node operation.
9. Headless consumption and optional capability management screens both satisfy server-side access, clear visibility, privacy and accessibility requirements.

## Open decisions and handover

- **FED-Q01:** What qualifies an installation as a Node on the public network and who controls discoverable identity/key rotation?
- **FED-Q02:** Is there one federation contract for different collection types, or protocol adapters per use case?
- **FED-Q03:** Which publication schemas are canonical and how are third-party/non-Nuxt producers handled?
- **FED-Q04:** Which peer trust evidence, signature and credential standards are appropriate for remote publications?
- **FED-Q05:** Are private/member-only cross-node collections in scope later, and how is consent/revocation handled?
- **FED-Q06:** What query/discovery contract sits between Hub composition and Search?
- **FED-Q07:** What are the guaranteed staleness, TTL, tombstone and retry bounds?
- **FED-Q08:** How are independent Hub directories found without recreating mandatory central control?
- **FED-Q09:** Which operational obligations, moderation governance and financial transparency apply to optional Hub operators?
- **FED-Q10:** Under what measured need would Hub-to-Hub federation or distributed index replication be justified?

**Disposition:** record `federation` as a candidate, `hub` as composition, and `node` as deployment/participant role. Proceed to independent contract/protocol/security evaluation before proposing a governing ADR, creating an implementation repository, altering IAM or installing new network services.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Hub moderation boundary:** An originating Node owns its source publication, and a Hub Node independently owns peering/acceptance and its derived index visibility through Federation and Search. Proposed Moderation may coordinate Hub-local reports, appeals and enforcement requests, but cannot delete source records or make global criminal determinations. Signed external abuse/block feeds are scoped, attributable and appealable evidence, not mandatory global consensus. Propagate source withdrawals with version/checkpoint, report stale/unconfirmed Hub removals, and qualify Hub-specific OSA duties separately.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Federated Node/Hub assurance accepts third-party age, identity or authority assertions only through scoped issuer/audience, subject binding, expiry and local trust policy. Trust is not transitive; a Hub endorsement cannot mint a local Identity membership, authority or merchant standing. Support Node exit, peer revocation and privacy-preserving age thresholds without globally linkable tracking tokens.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Federation can transport Verification's bounded age/identity/organisation evidence across Nodes or Hubs but must not adopt a global verified status or make local trust transitive. Each receiving Node validates issuer, purpose, subject binding, audience, quality, expiry/status and local authorisation independently; avoid linkable global identifiers and support issuer/key revocation.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine owns origin-Node comment/revision visibility and withdrawal events. Any outbound public discussion/feed or inbound remote reply is opt-in and subject to origin/publication rights, provenance, local trust, eligibility, audience, expiry, replay and conflict protection. Federation owns peer/subscription/transmission receipts; Hub Search owns derived index state. A local comment withdrawal is not proof of remote Hub/cache removal; reconcile acknowledgements without granting remote peers local authorisation.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed for [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53), not an implemented contract.** See [Configuration conceptual public inputs](../configuration/capability-record.md#idealised-public-inbound-interfaces). Configuration may supply registered, scoped federation selections; Federation owns peer trust, exchange/reconciliation and withdrawal. Source domains and Authorisation govern actual disclosure. Use public host-composed ports/events only; preserve all prior decisions and dependency acyclicity.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

A Hub/Node may request authorised technical assessment of externally supplied material or links, but remote scan claims are untrusted until provenance and scope validated. Content Security supplies detection evidence only; origin Node controls original publication while receiving Hub controls own listing/index restrictions and withdrawal reconciliation. Do not indiscriminately share private bytes with foreign scanners.

## Reciprocal conceptual note — Course (17 November 2026)

**Status: Proposed, pending owner approval.** [Course review](../course/capability-record.md), draft PR #56: Course may expose authorised, attributed, versioned catalogue descriptors and withdrawal facts for optional federation. Federation owns transport, peer subscriptions and reconciliation, not curriculum source authority or enrolment; remote copies can be stale and must respect disclosure. This does not complete federation's own review.

## Assessment cross-institution evidence transfer — 18 November 2026

**Status: Assessment ASMT-14 owner-approved conceptual relationship; Federation contract detail provisional.** [Assessment](../assessment/capability-record.md): Federation may coordinate authenticated, permissioned, purpose-restricted record exchange between installations, preserving origin, source revision, disclosure rights and withdrawal/recheck. Federation transports and validates peer exchange; it neither confers trust in an examination issuer nor determines assessment admissibility. Verification evaluates source/issuer proof and scoped trust; receiving Assessment decides evidence acceptance, Training/Qualification decide dependent outcomes. Hub or peer trust is not transitive, and no blanket transfer of scripts, learner identities or accommodations is permitted.


## Independent review: contract completeness and authority (18 November 2026)

**Status:** Independent conceptual review *proposal*, pending owner sign-off; this section refines (and does not silently supersede) FED-01–FED-10 and FED-Q01–FED-Q10 above. Governing opening master: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint opening master: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. The capability exists as a working blueprint candidate, **not** as a verified implementation contract, repository, running protocol or adopted governing classification. The 17 November Node–Hub architecture direction was approved for documentation, not implementation. No federation runtime `CONTRACT.md` was found or verified.

### Independent justification and source of authority

A replaceable cross-installation exchange service requires its own governed peer/subscription lifecycle, durable delivery checkpoints, proof and policy-evaluation outcomes, and withdrawal coordination even when Search, Publisher, Message Queue and domain owners exist. This justifies **retaining Federation as a candidate Platform capability**, subject to conceptual approval, not creating a new repository by assumption. Federation is *source of truth only for its local peer relationships, declared participation/subscriptions, exchange attempts, validation decisions, checkpoints and acknowledgements*. The originating capability alone owns published business facts and origin withdrawal. The receiving Hub owns its local decision to carry a derived index entry; Search owns its indexed representation, not the legitimacy of the origin's business assertion.

**No transitive trust:** proof of peer endpoint control is not proof of legal identity, content truth, professional standing or entitlement. A signature verifies integrity and key possession subject to established binding and revocation; Verification may assess specific claims. Receiving policy and Authorisation still apply for each action.

### Published idealised inbound contract: consumer-facing operations

All inputs are independently runtime-validated; caller, organisation/tenant, audience, source reference/revision, effective policy, key/proof evidence and request correlation accompany operations *where relevant*, rather than a mandatory universal request object. Stable error identifiers include `invalid`, `unauthorised`, `untrusted-peer`, `incompatible-version`, `disallowed-disclosure`, `conflict`, `stale-source`, `rate-limited`, `unavailable`, `unknown-outcome`; UI messages use localisable keys.

| Public input | Supplied by / essentiality | Validation and absent/invalid/contradictory behaviour |
|---|---|---|
| **Register, verify, pause, resume, revoke or exit peer relationship** | Authorised local operator and approved peer discovery/service identity; required for network participation, absent in standalone mode | Enforce local admin rights, tenant scope, endpoint/key control, network restrictions, version compatibility, policy and proof freshness; deny unknown/mismatched trust; revocation blocks future transfer and initiates bounded withdrawal, without deleting origin data |
| **Declare, amend, stop or withdraw an exchange collection** | Publisher or any authorised source owner provides canonical public view, schema/version, revision, disclosure decision and withdrawal facts; required to publish | Only origin owner authorises content/visibility; Federation rejects absent explicit publication permission, contradictory revision, unsupported representation or ambiguous audience; never reads private tables |
| **Subscribe/unsubscribe to approved collection or Hub** | Local operator/consumer with scoped request and peer consent or policy, where applicable | Validate both sides' approval, collection type, scope, policy and expiry; absence of approval means pending/denied, not implicit consent; discontinuation leaves local source intact |
| **Publish change notification, fetch snapshot, resume/reconcile cursor** | Origin event/public fetch surface and remote subscriber, as appropriate; optional while offline | Stable item and origin ID, monotonically comparable source revision or opaque version token, collection, idempotency and schema; reject older updates, bound batch size/TTL, record indeterminate receipts and reconcile by origin snapshot; transport receipt never signifies business acceptance |
| **Accept and validate inbound remote item/update/withdrawal** | Untrusted remote Node/Hub with signed/authenticated or appropriately trusted representation, source link and proof | Verify source binding, audience, integrity, freshness, replay, allowed type, safe URL, payload limit and local acceptance policy; quarantine/reject invalid or unsupported data; remote assertions alone never authorise access |
| **Apply scoped local participation/trust policy and review evidence** | Configuration supplies configured choices, Authorisation validates operator, Verification/Legal Compliance/Moderation may provide scoped proof or decisions; conditional | Record policy version and reasons; missing mandatory trust/consent/safety/legal evidence fails closed; optional scanner unavailability uses configured safe policy, never implicit trust; appeals cannot override statutory controls |
| **Request peer health, delivery history and disclosure/withdrawal status** | Authorised administrator, auditor or source owner; essential read model for operators | Enforce least privilege, redact identifiers/content and return explicit last-observed time, incomplete/unknown states; do not claim that a remote Hub has actually deleted a record without proof |

### Published idealised outbound contract: permissible conclusions

| Public output | Consumers | Authority and precise promise |
|---|---|---|
| **Peer/participation record** (peer reference, authenticated endpoint claim, scopes, statuses, policy version and effective times) | Operators, host, Audit, authorised Integrations | Authoritative *local* association and acceptance only; does not certify global identity or grant source-resource privileges |
| **Collection advertisement and retrieval descriptor** (origin, type, schema, canonical URL, visibility, revision, expiry, allowed use) | Authorised peers/Hub/Search adapter | Federation conveys source-owned and explicitly permitted facts with provenance; *not* authoritative source content or rights beyond declared scope |
| **Delivery receipt/checkpoint** (source change ID, recipient, attempted/accepted/rejected/unknown, reason, cursor, last reconciliation) | Publisher, originating owner, operators, Audit, Observability | Authoritative local attempt and verified remote acknowledgement *only if evidenced*; cannot promise exactly-once processing or remote final visibility |
| **Validated inbound indexable envelope / withdrawal signal** | Search via public port, Hub composition, optionally moderation/security workflow | Federation attests its own validation and local acceptance; source facts remain attributed to origin, potentially stale. Search decides index application and query semantics |
| **Verification/policy disposition** (accepted, refused, suspended, quarantined, awaiting review, evidence references) | Operators, Moderation, Audit, affected peers where disclosure appropriate | Explains *local* participation or receipt decision, including appeal/recheck route; never substitutes for Verification's issuer assurance or Authorisation's resource decision |
| **Federation lifecycle events** | Message Queue consumers, Search, Audit/Reporting through documented ports | Committed local facts such as `PeerParticipationChanged`, `CollectionAdvertisementChanged`, `FederatedChangeAccepted`, `FederatedWithdrawalObserved`, `DeliveryStateChanged`, `SyncCheckpointAdvanced`; delivered at least once where supported, with deduplication and outbox sequencing; no synthetic domain-business event |
| **Authorised management read models and diagnostics** | Optional GUI, operators, Logging/Observability/Reporting | Accurate scoped status and freshness/unknown information, sanitised technical errors and aggregated telemetry; no private raw content or cross-tenant dashboards |

**Command semantics:** validate caller and purpose at point of execution, require source-owner approval, enforce state transitions, use idempotency keys with bounded retention, return accepted-vs-completed and recoverable unknown outcomes separately. **Query semantics:** return tenant-filtered, policy-bound, versioned views with last-observed time, source provenance and completeness/freshness indicator. **Event semantics:** emit after owned state commits through a capability-owned durable outbox; Message Queue delivers without adopting event authority. Remote HTTP interaction or a transport ack does not become a business event until the local owning state commits.

### Working collaboration and dependency direction

| Provider / consumer | Input to Federation; output from Federation | Dependence and source-of-truth boundary |
|---|---|---|
| **Identity, Authentication, Authorisation** | Local tenant/principal and validated assurance; request-time allow/deny for administration/publication/retrieval; scoped federation context to those decision ports | Required for protected local actions; remote Node never becomes a local member by association. Authn credentials and local grants stay with IAM |
| **Verification** | Scoped issuer/key/organisation/eligibility proof and expiry/revocation signals; Federation passes provenance and proof references | Conditional trust input, no blanket trust; receiving domain decides substantive evidence admissibility |
| **Publisher and domain owners (Job, Events, Marketplace, Product, Course, Assessment, Comments Engine)** | Approved public projection, source revision and authorised withdrawal; Federation supplies external reach, delivery/acknowledgement/failure status | Conditional on an enabled source/public view; source remains authoritative for business state and disclosure |
| **Configuration, Legal Compliance and Privacy obligations** | Operator preference, retention/disclosure/transfer constraints, policy effective period; Federation supplies exchange status and evidence | Configuration stores settings, not Federation peer lifecycle; legality must be assessed per jurisdiction/purpose; missing mandatory permission denies |
| **Search and Hub composition** | Search provides public index ingestion/results; Federation provides validated remote descriptors, provenance, source staleness and withdrawals | Conditional for Hub indexing; no Search required for publishing-only Node; Hub host owns search GUI and navigation |
| **Content Security and Moderation** | Safety assessment and locally authorised review/adjudication; Federation supplies suspect transmission context, quarantine state and action receipts | Conditional to exposure/risk; origin controls own content, receiver decides its local propagation; moderation does not grant remote authority |
| **Message Queue, Scheduler, Workflow and Temporal Gateway** | Host-composed delivery transport and scheduled retry/reconcile or human review when enabled; Federation supplies committed events, retry intents and outcome observations | No duplicated queue, timer or workflow engine; Temporal Gateway is infrastructure adapter; background orchestration can be replaced with equivalent host-supplied ports |
| **Audit, Logging, Observability, Reporting** | Evidence-capture and technical telemetry ports; Federation outputs versioned participation changes, operator decisions, proof references, failures, attempts and metrics | Audit owns accountable evidence; Logging owns operational logs; Observability owns runtime telemetry; Reporting owns views; Federation owns its own factual status |
| **Site Hosting, Integrations and host secrets/network** | Verified local addresses, safe outbound network policy, optional protocol adapters, credentials via host reference; Federation exports endpoint/exchange configuration | Host/Site Hosting own DNS/TLS routing; Integrations may provide provider-specific adapter without replacing Federation's network authority; prevent SSRF/DNS rebinding |
| **Clock, Theme Manager, host application** | Effective time semantics, accessible presentation tokens and routing/composition; Federation supplies statuses and localised message keys | Clock supplies time validity; GUI is optional and host-selected; no presentation-only dependency for headless operation |

Only public ports are consumed. **Bidirectional network communication does not introduce an implementation dependency cycle.** The host wires independently directional ports, avoids direct reciprocal Nuxt extensions, and preserves one-operation host composition within the governing budget. Absent optional provider ports produce explicitly declared degraded modes; absent mandatory authorisation/persistence denies operation.

### State, resilience and trust rules

- Keep peer associations, scoped subscription and collection-approval state, checkpoints, idempotency receipts and authoritative *local* participation decisions in Federation-owned persistence behind a host-supplied port; no generic shared persistence service or vendor lock-in. Source payload caches are non-authoritative and time-limited.
- Require safe outbound allowlisting, scheme and address checks at each redirect/resolution, bounded parsing and decompression, replay protection, signing/key rotation with verifiable origin binding, rate and resource limits, abuse defences, schema and canonical-origin checks, and tenant/network/Hub partitioning. Prefer open standards after a specific threat/protocol interoperability evaluation; do not preselect ActivityPub/WebSub/AT Protocol as universal wire requirements.
- Treat missing, expired, revoked or contradictory trust, authorisation or disclosure evidence as *deny/quarantine*, with an explicit recoverable workflow when justified. No cross-node inferred consent, privileged personal-record replication or private address leakage. An unreachable origin or unconfirmed withdrawal must appear stale/unknown, not fresh/removed.
- For privacy and UK GDPR/GDPR: minimise personal data in advertisements and logs; identify controller/processor and international-transfer roles per deployment; document purpose, lawful basis, retention, DSAR/erasure/withdrawal paths and legal-hold exceptions with Legal Compliance. No automatic assertion of statutory compliance.
- Publishing node, subscribing node and independent Hub each operate without central registry. Disable/revoke federation without disabling unrelated local apps. Withdrawal dispatch and acknowledgement cannot promise removal from all third-party copies; expose traceable uncertainty and downstream notification.
- Policy authority is local, reviewable, scoped and versioned. Hub fees, preferential placement and participation/defederation decisions must not silently alter source business records or masquerade as search relevance guarantees.

### Conceptual GUI / application-test-template host pattern

**Headless core:** no screens, routing or UI dependency required. **Optional Federation sidebar entry** (only when selected and authorised) routes through the host to a **Federation dashboard**, following the representative application-test-template/Theme Manager host pattern rather than registering global navigation itself.

Dashboard: enabled/disabled and network health, role (publisher/discoverer/Hub), participating peers/Hubs, changes pending, last successful reconciliation, stale/unknown warnings. Separate views: (1) Peer directory and invitations/trust proofs; (2) Published collections and audiences/preview/stop publication; (3) Subscriptions and per-Hub terms/permissions; (4) Sync queue, failures, checkpoints and safe retry/reconciliation; (5) Withdrawals, remote acknowledgements and expiry; (6) Quarantine, policy decisions, review/appeals, evidence and cost disclosures; (7) Configuration/keys/endpoints with host-owned secrets not displayed. A Hub composition optionally adds Search/index and moderation panels outside Federation.

Every management action is enforced by server-side Authorisation; hide or disable controls per permission but never trust UI-only checks. Use scoped paginated/redacted read models, explain pending/partial/unknown outcomes, show explicit origin and last-sync timestamps, no automatic remote fetching on unrestricted user URLs. Responsive, keyboard/screen-reader accessible WCAG 2.2 AA, internationalised labels/messages, Clock locale/time and Theme Manager semantic tokens. A discovering-only or standalone Node sees appropriate limited or disabled states.

### Conceptual acceptance matrix (not executable tests)

| Given input / condition | Expected behaviour / published output | Authoritative owner |
|---|---|---|
| Federation disabled; Node locally publishes a job | Local job remains available; no forced Hub/network | Job/source owner |
| Approved public job revision from A to opted-in Hub B, discovery from C | B validates/provides derived indexed reference with origin/version; C links to A, not a Hub-owned transaction | Job owns job; Federation owns receipt; Search owns index |
| Cross-tenant request or remote actor claiming local IAM status | Deny and record minimised audit reason; no derived resource permission | Authorisation and respective resource owner |
| Unknown or unsupported peer version/key, stale proof or unauthorised collection | Quarantine/deny with reason; no index ingestion | Federation local admission; Verification for specific proofs |
| Same change twice, reordered change and lost push notification | One effective local revision, idempotent receipts, snapshot/checkpoint reconciliation and explicit progress/unknown | Origin source for revision; Federation for sync |
| Remote Hub times out after transmission | Mark outcome unknown, retry/reconcile; do not claim delivered or withdrawn | Federation for local delivery status |
| Source withdraws an item while Hub is unreachable | Persist withdrawal intent and retry, mark cached/index data stale according to policy; no claim of global deletion | Origin for withdrawal; Federation for acknowledgement; Search for index action |
| Operator withdraws from Hub B but not Hub D | Stop B exchange, reconcile B withdrawal; D and origin remain unaffected | Federation participation; source retains record |
| Malicious URL/oversized payload/replay/forged key | Reject safely before uncontrolled fetch or parsing and log sanitised evidence | Federation admission; Content Security additional scan |
| Missing optional Search/GUI or external protocol adapter | Publishing-only headless operation still possible; unsupported Hub indexing/adapter clearly reported | Federation/host selection |
| Explicit request to replicate private assessment scripts to unapproved Hub | Deny, no new audience or implied consent; source evidence transfer requires separate owner approval and Verification | Assessment/Authorisation/source |
| Privileged operator inspects system while another tenant is active | Only authorised tenant's peers/receipts visible; redacted private records | Federation scoped read model + Authorisation |

### Decision register and implementation gaps

Previously agreed Node–Hub direction is **retained**; FED-Q01–FED-Q10 remain *open*, not retroactively approved. Review recommendations for owner disposition:

- **FED-11 (proposed):** Confirm a genuine, separately bounded Platform capability owning local peer/subscription/exchange/acknowledgement state, with no mandatory package/repository or shared registry.
- **FED-12 (proposed):** Confirm origin-controlled, explicitly opted-in *public representations only* for v1. Private cross-node data remains out of scope without a separate purpose/consent/security design.
- **FED-13 (proposed):** Confirm direct independently governed Node–Hub publication/subscription, push notice plus authenticated pull snapshot reconciliation, no compulsory Hub-to-Hub replication.
- **FED-14 (proposed):** Confirm local, non-transitive peer trust and separate Verification, Authentication, Authorisation and source-domain disclosure decisions.
- **FED-15 (proposed):** Confirm contract-level status distinctions among requested, authorised, accepted, acknowledged, completed and unknown; idempotent replay and eventual reconciliation, not exactly-once or instant erasure.
- **FED-16 (proposed):** Confirm public source projections, signed/provenanced versioned envelopes where threat model warrants, safe fetch, bounded expiry and explicit partial/unknown states; defer selection of wire standard/adapters.
- **FED-17 (proposed):** Confirm headless-first design and optional host-owned sidebar/dashboard, separate Hub discovery UI, WCAG/i18n/Theme Manager.
- **FED-18 (proposed):** Confirm reciprocal interface descriptions below and capability-owned durable events, without creating cycles or moving authority.
- **FED-19 (open owner choice):** Who may approve a Hub/peer for a tenant and on what independently verifiable evidence and appeals criteria? Recommend tenant-scoped operator decision, local policy and separately validated proofs; no network-wide trust inheritance.
- **FED-20 (open owner choice):** Set publication/snapshot retention and maximum stale-data handling policy: recommend configurable stricter bounds subject to mandatory privacy/safety floors and truthful last-confirmed timestamps; cannot promise a universal real-time SLA.

**Deferred evidence/implementation alignment:** verify the current governing ADR-0017/0018 statuses and full standards; verify related root `CONTRACT.md` surfaces in their own repos before implementation; choose protocol through security/interoperability evaluation; write implementation root `CONTRACT.md`, threat model and `STORAGE-REGISTER.md` when implementation exists; independently validate host composition, interoperability, identity/key rotation, signed feed acceptance, source withdrawal, GDPR impact and operational observability through CI/user acceptance. No implementation, test or compliance evidence is claimed here. Final merge requires fresh master and conflict/architecture review and explicit owner approval.


## Owner approval and standards/library/GUI follow-up — 18 November 2026

**Owner decision:** FED-11 through FED-18 approved, and recommendations for FED-19 (tenant-scoped operator approval with independent trust proof) and FED-20 (configurable bounded freshness and retention under mandatory safety/privacy floors) approved on 18 November 2026. Their status is now **agreed conceptual**, not verified implemented or governing-ADR accepted. Existing FED-Q01–Q10 still require protocol-specific evidence/choices: approval of this direction does not silently select wire format, crypto scheme, discoverability, private-data federation or universal SLA. No implementation or merge approval given.

### Plain-English contract: what consumers may depend upon

**Incoming requests:** register or verify a Node; invite/accept/suspend/revoke a peer; opt in to a public collection and approve/stop publication; subscribe/unsubscribe; publish a source-authorised change or withdrawal; retrieve an approved record; submit an external record to validation; request snapshots/checkpoints or reconciliation; query statuses and history; manage scoped operator policy. These are conceptual commands and queries, not named HTTP endpoints or fixed TypeScript functions.

**Published outputs:** local peer/subscription and collection status; canonical public collection metadata; signed/provenanced representation when applicable; validated remote envelopes and rejection/quarantine reasons; delivery attempts, confirmed acknowledgements, indeterminate results, revision and cursor; committed change and withdrawal events; sanitised operational statuses; access-scoped evidence and reporting views. Source owns business truth and permission to disclose; Federation owns local coordination; peer approval never grants resource access. Public outputs need stable IDs, scope/audience, policy version, source revision, effective and observed timestamps, provenance, error codes, retryability and freshness/unknown state as relevant. Events represent committed Federation facts from its durable outbox, not transport completion or source transactions.

### Logging, Audit and Reporting: reciprocal contract clarification

| Consumer | Federation publishes | Receiving owner's return or authority | Failure mode |
|---|---|---|---|
| Logging | Correlated technical events: peer negotiation, fetch rejection, timeout/retry, schema or signature failure and service health; no secrets/source payloads | Logger provides an operational sink and query tools, not peer/permission truth | If non-mandatory technical logging is unavailable, retain real local state and surface degraded diagnostics; mandatory security evidence still follows Audit requirements |
| Audit | Actor/peer, tenant, action, changed relationship/collection, policy and revision, reason, proof pointer, commit time and correlation for approvals, publication, disclosure, suspension, withdrawal and security incidents | Audit owns accountable, tamper-evident custody, authorised historical evidence and retention; Federation owns peer/disclosure status | Mandatory evidence capture must fail closed or be durably staged in an accepted capability-owned outbox; never silently lose mandatory accountable actions |
| Reporting | Authorised, bounded participation/delivery/freshness/withdrawal aggregates and versioned read models with attempted/accepted/unknown distinctions | Reporting owns templates, aggregation, output and its audience decisions; Federation remains authoritative source | Reporting absence cannot block valid exchange; mark incomplete/unknown rather than inventing totals |

### Established standards to evaluate, not prescriptive complete protocol

| Standard | Useful contribution | Important limitation |
|---|---|---|
| W3C ActivityPub + ActivityStreams 2.0 | Federated actors, objects, social updates and delivery | Social vocabulary does not independently standardise product prices, booking permissions or cross-tenant business trust |
| W3C WebSub | Publisher/hub/subscriber change-notification and subscription lifecycle | Delivery notification is not authoritative record synchronisation; snapshot and recovery still need design |
| RFC 9421 HTTP Message Signatures and RFC 9530 Content-Digest | Integrity and authenticated message binding | Signing key identity, revocation, replay checks, payload policy and legal trust are separate |
| RFC 7517 (JWK), RFC 7515 (JWS), OAuth 2.0 metadata RFC 8414 and optional mTLS RFC 8705 | Key format, verifiable tokens, published issuer metadata and strong machine authentication profiles | Choose a consistent and minimal trust/authentication profile; do not equate authentication with source disclosure permission |
| RFC 7033 WebFinger and RFC 8615 well-known URIs | Optional interoperable discovery/address conventions | No compulsory universal registry or implicit reliable identity |
| JSON Schema 2020-12 + OpenAPI 3.1 | Versioned public envelopes, input validation and documentation | Schemas do not establish permissions or source truth |
| RFC 9110 HTTP semantics, ETag/If-None-Match and RFC 9457 Problem Details | Cache validation, conditional fetch, statuses and structured errors | Staleness, reprocessing and peer acceptance need explicit business semantics |
| OWASP ASVS 5.0, SSRF Prevention Cheat Sheet, WCAG 2.2 AA and applicable GDPR/UK GDPR | Security validation, remote URL safety, accessible operator UI, minimisation and lawful transfer | A technical implementation does not itself certify legal compliance |

**Decision:** start with direct Node-to-independent-Hub opt-in public publication and authenticated pull/reconciliation, optionally push notification. Evaluate WebSub for simple feeds and ActivityPub/Fedify only where its social object model actually fits. Avoid inventing a universal federation protocol or assuming AT Protocol's architecture mandates compatible implementations.

### Permissively licensed open-source implementation candidates

These are **candidates for technical assessment**, not mandatory dependencies, acceptance-tested versions or proof of transitive dependency suitability. Review exact release license/SPDX, transitive notices, commercial use rights, maintainer activity, supported Node runtime, vulnerability/advisory posture, supply chain and exit strategy before adoption. All should remain replaceable behind Federation-owned ports.

| Candidate | Licence indicated by upstream | Role / adoption judgement |
|---|---|---|
| Fedify (`fedify-dev/fedify`) | MIT | Actively developed TypeScript ActivityPub federation toolkit: discovery, signatures, protocol delivery. **Conditional**: best candidate only for ActivityPub adapter, not mandatory core; avoid protocol/framework coupling |
| `panva/jose` | MIT | Mature JOSE/JWS/JWK implementation for signed payloads and key handling; cryptographic profile chosen separately |
| `nodejs/undici` | MIT | Maintained efficient HTTP client; outbound request policy, DNS rebinding/SSRF and resource-limits still owned by Federation |
| `ajv-validator/ajv` | MIT | Mature JSON Schema validation for public versioned exchange envelopes; prohibit untrusted schema compilation/remote references without controlled policy |
| `sindresorhus/p-limit` | MIT | Small, maintained concurrency limiter for bounded network/work queues; not a replacement for Message Queue or Scheduler |
| `digitalbazaar/jsonld.js` | BSD-3-Clause | Conditional JSON-LD parsing for ActivityStreams or linked-data vocabularies; guard remote context fetching and resource consumption |
| `fastify/fastify` | MIT | Mature HTTP server option only if a standalone server adapter is justified; **not** required within the default Nuxt/Nitro host |

Exclude licenses or commercial terms that impose SaaS revenue gates, source-available restrictions, vendor service dependency or hidden proprietary enterprise features. Specifically, the newer Fedify-associated *Feder* project is AGPL-3.0 and therefore is **not** in this permissive-library shortlist. Even permissive licences do not automatically mean a project is actively maintained or all dependencies are compatible; pin audited release versions and record alternatives.

### Verified reference host navigation and GUI proposal

The `nuxt-layers-test/application-test-template` `master` README documents an independent test area `/admin`, homepage `/`, Theme Manager route `/theme-manager`, a shared themed shell with collapsible desktop sidebar/mobile overlay, and an Appearance control in the top bar. `app/pages/admin.vue` shows dashboard cards including a Theme Manager link; `app/pages/index.vue` leads from the homepage into `/admin`. This test host explicitly warns that Theme Manager's unauthenticated **test mode is local-only and must not be exposed publicly**. Its current `nuxt.config.ts` composes Theme Manager in test mode, without installing Federation. These are observed template facts, not a Federation UI implementation.

**Proposed Federation navigation in a derived test application:** host-controlled sidebar `Federation` → `/federation` overview. The host may also show a Federation card on `/admin`; users with no permission see neither active actions nor private data. Required management views if enabled: `/federation/peers` (invite/verify/suspend/revoke and scope); `/federation/collections` (public source-owned projections, preview and audience); `/federation/subscriptions` (Hub selection, opt-in and withdrawal); `/federation/synchronisation` (revisions/checkpoints, stale/unknown, retry and reconciliation); `/federation/governance` (trust, quarantine, reasons, review/appeals and evidence); `/federation/settings` (roles, budgets, endpoint references and key status, never raw secrets). Contextual drawers may reduce page count, but public contracts and operation boundaries are stable.

**Hub operator composition** adds a separate Search/Discovery management route, index coverage and moderation/reporting screens; those are not owned by Federation. Publishing-only or discovering-only Nodes see role-relevant subsets. Headless deployments expose the same authorised contracts without menu/screens.

**User journeys:** (1) Node admin enables Federation, verifies peer, sees pending/active; (2) Publisher approves a public collection then selects an independent Hub; (3) operator inspects synchronisation and stale/unknown or rejected updates, retries safely; (4) publisher withdraws and sees confirmed versus unknown remote acknowledgement; (5) Hub operator quarantines malicious remote publication through local policy/Moderation, then tracks review without changing origin; (6) tenant switch and unauthorised operators never see other tenants' peers, sources or evidence.

**Presentation controls:** host owns menu/routing and authentication integration; capability optional presentation consumes only public operations/read models. Use server-side authorisation for every action, Theme Manager semantic classes, internationalisation, Clock effective dates, WCAG 2.2 AA keyboard/ARIA and responsive patterns. Show source/last-confirmed version and pending/stale/unknown states, accessible confirmations and safe destructive-action review. Avoid silently fetching arbitrary external URLs and avoid global identity sharing. The test host is representative only; do not inherit test-mode authentication bypasses into production.

### Follow-up status

All findings in this section are agreed conceptual recommendations where expressly approved above, or evidence-backed candidates for subsequent architectural selection. No package installation, implementation repo edit, tests or merge authorised. Existing independent counterpart `CONTRACT.md` availability and exact chosen wire profile remain separate implementation investigations.

## Integrations reciprocal conceptual interface — 18 November 2026

**Status: Proposed in [Integrations draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76); not approved as a new decision or implemented.** Federation owns peer relationships, protocol/publishing subscriptions, cross-node disclosure and reconciliation decisions; Integrations may supply optional authenticated external adapters, connection-status and qualified exchange receipts. Connector health must not be construed as peer trust, verified domain truth or federation membership; the domain/Federation owner determines consent and authority. Avoid circular compile-time dependencies using public host-composed contracts. See [Integrations conceptual contract](../integrations/capability-record.md#cross-capability-relationships--directional-public-contract-cooperation), proposed PR #76; concurrent Federation PR #69 remains provisional.

## Moderation dedicated review — reciprocal conceptual boundary (19 November 2026, draft PR #96)

**Status: Proposed, not an accepted public implementation contract.** See [Moderation's dedicated idealised input/output contract](../moderation/capability-record.md#dedicated-conceptual-review--19-november-2026-pr-96). Federation supplies verified peer/collection provenance, trust/withdrawal status and locally admissible signals to Moderation. Moderation may coordinate a Hub-local case, but Federation owns peer exchange/quarantine and origin Node retains its records. Index suppression and origin deletion differ; no global shared-abuse verdict or implicit cross-tenant access.

## Reciprocal boundary — Moderation dedicated review (19 November 2026, PR #96)

**Proposed; non-normative, no implemented port asserted.** Federation owns peer subscription, trust/exchange and quarantine, supplying provenance-bound signals to Moderation. Moderation can adjudicate a Hub-local case but cannot remove the origin Node record; Search performs independent derived-index restriction, with scoped receipts. See [Moderation conceptual contract](../moderation/capability-record.md#dedicated-conceptual-review--19-november-2026-pr-96). Public host-assembled contracts must remain acyclic, scoped and permission-checked.
