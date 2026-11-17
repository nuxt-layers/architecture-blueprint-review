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
