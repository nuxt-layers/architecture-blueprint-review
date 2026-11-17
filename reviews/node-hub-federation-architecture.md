# Node–Hub Federation — Conceptual Architecture Review

**Status:** Review-approved direction for documentation (17 November 2026), not an accepted ADR, capability contract or implementation plan.  
**Authority:** `nuxt-layers/architecture-rules` current accepted ADRs and normative standards take precedence.  
**Related:** [Federation capability record](../docs/capabilities/federation/capability-record.md), [working catalogue](../docs/capability-catalogue.md), [register](../docs/capability-register.md), [capability classification gate](capability-classification-gate.md).

## Problem and intent

Allow independently operated Nuxt Layers installations to publish selected information for discovery by other participants without transferring authoritative domain data, forcing every Node to join one platform or making any Hub a mandatory intermediary. Examples: forum topics, marketplace listings, jobs and events. A Node can host several local applications under one deployment, and may optionally operate a local network or Hub services.

## Agreed conceptual distinctions

| Term | Meaning | Classification |
|---|---|---|
| Node | An independently governed installation, able to run standalone and optionally participate in a network | Deployment/participant role; not a standalone business capability |
| Federation | Cross-node peer participation, exchange, subscriptions, publication delivery and synchronisation | Candidate Platform capability, subject to ownership gate |
| Hub | A Node operating optional discovery/indexing and participation services for other Nodes | Application composition and operator role, not automatically an independent capability |
| Hub operator | Accountable organisation/person deciding Hub participation policies and administration | Governance role; local Identity/Authorisation remain authoritative |
| Network | Open interoperable protocols used by participating Nodes and Hubs | Architectural agreements, not one central service |

**Agreed direction:** Every Hub operates as a Node; any suitably configured and authorised Node may become a Hub; not every Node needs a Hub. A Node may publish to several Hubs or none. A Node that provides Hub services retains its ordinary local capabilities. An installation may host multiple separately governed Hub services where isolation can be proven.

## Design boundaries

1. **Node autonomy:** independent operation without a Hub or network connection. Hub departure must not remove underlying records or prevent local applications from operating.
2. **Origin authority:** the source Node and its domain capability own records, prices, availability, user data, transactions and business decisions. A Hub keeps only authorised, derived discovery representations and its own operational records.
3. **Hub replaceability:** no exclusive registrar, proprietary mandatory subscription, unavoidable rent-taking intermediary or central root operator.
4. **Participation not permission:** peer trust is distinct from Identity membership, Authentication proof, Authorisation grants, legal constraints and privacy consent.
5. **Heterogeneous deployments:** a Hub may use some Nuxt Layers components but the open protocol must not require counterparties to run Nuxt.
6. **Simple start:** direct Node publication to independently operated Hubs; Hub-to-Hub exchange and distributed index replication are optional future models, not requirements now.

## Reference flow: job listing

1. The originating `job` domain capability authorises and publishes a vacancy and its canonical public representation.
2. A federation boundary advertises the approved collection and issues a durable change notification/reference (source event owned by the domain).
3. An independently operated Hub verifies the publisher, validates permitted data and synchronises from the canonical source.
4. Search indexes the derived entry, preserving origin/provenance, revision and freshness.
5. Another Node or public user queries the Hub and receives a canonical link; applying or booking remains with the originating Node.
6. Origin updates/withdraws the record; Hub handles idempotent updates, tombstones, expiry and snapshot/checkpoint reconciliation when messages are lost.

The Hub does not guarantee live inventory, price, eligibility or authoritative transaction completion.

## Architecture options and trade-offs

| Model | Advantages | Costs and risks | Recommendation |
|---|---|---|---|
| A. Independent Hubs with Node subscriptions | Simple, replaceable, local policy control, no distributed consensus | Duplicate derived indexes; discovery of Hubs is manual initially | **Preferred initial model** |
| B. Hub-to-Hub exchange | Greater reach and discovery | Trust transitivity, loop prevention, provenance, moderation and withdrawal propagation | Defer with protocol extension points |
| C. Distributed/replicated shared index | Broad joint availability | Coordination, consistency, partitioning, governance, cost and failure complexity | Defer unless objectively required |

The term “distributed bucket” should not imply shared ownership of application data or distributed storage: initial Hubs are independently operated **derived discovery indexes**, not a common database.

## Classification and ownership gate

Federation plausibly owns a durable peer, subscription, collection-negotiation and synchronisation lifecycle and should have its own candidate capability record. Hub orchestration itself does not justify a new stateful `hub` capability; it composes Federation, Search, Content Security, IAM, Audit, Logging and optional application-specific presentation. Domain owners supply authorised public records; Search owns indexing/relevance; Message Queue transports events rather than federated internet semantics. No new repo, Layer, generic registry or shared database follows automatically.

## Interface and governance implications

- Logical public surfaces: peer discovery; participation/subscription; collection declarations; publication change; authenticated source retrieval; inbound validation; synchronisation/withdrawal; Search index handoff; evidence/administration; optional GUI.
- Support push notifications plus pull recovery, stable identifiers, source revision, protocol/version negotiation, bounded record envelopes, freshness/TTL, replay and idempotency.
- Restrict outbound fetch and inbound payloads; guard against SSRF, peer impersonation, replay, denial-of-service, index poisoning, metadata leakage, malicious or erroneous defederation and abuse.
- Hub search results are derived, possibly stale, and link back to authoritative source. Separate publication trust from truth of content.
- Governance requires explainable peer/content policies, documented refusal and appeal, lawful removal, minimised audit evidence and tenant isolation.
- Conceptual interfaces: host-owned sidebar entry to optional Federation admin dashboard (peers, collections, subscriptions, sync health, trust, review); Hub composition adds category discovery tools. Headless and accessible modes supported.

## Standards to evaluate, not preselect

WebSub for feed-change notification; ActivityPub for social activity federation; AT Protocol's personal-data-server/relay/app-view separation as an architectural reference; signed HTTP exchanges as appropriate; open HTTP/JSON-based versioned collection representations. Select or adapt established protocols on demonstrated requirements; avoid inventing a universal networking standard prematurely.

## Decisions still open

Network identity and trust root; full vs category-specific exchange schemas; exact feed/protocol adapters; authoritative peer verification; data disclosure beyond public collections; search/query and federated moderation interfaces; timing/consistency commitments; Hub directory discovery; operator obligations and economic transparency; criteria for Hub-to-Hub replication. See FED-Q01–FED-Q10 in the capability record.

## Consequences and next work

- Preserve current `architecture-rules` modular-monolith default, ADR-0012 minimal-host composition and ADR-0016 directed acyclic dependency model. Bidirectional network messages are not circular local package dependencies.
- Do not automatically amend the existing IAM suite, move records, introduce a blockchain or claim operational federation.
- Next review should specify an independent protocol and a minimal proof scenario: Node A publishes → Hub Node B indexes → Node C discovers; test disconnected operation, duplicate/missed updates, withdrawal, multiple Hubs and hostile remote inputs.
- Only after validation propose changes to governing architecture and applicable `CONTRACT.md` files through separate accepted review.
