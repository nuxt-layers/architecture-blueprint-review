# Capability Record — Gaming

## Capability Name:

`gaming` — game rules and competitive participation outcomes.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

**Proposed conceptual Domain candidate (18 November 2026); not owner-approved.** A directory and catalogue entry exist, but `nuxt-layers/gaming` was not accessible (GitHub 404) at review time. No root `CONTRACT.md`, implementation, published API, package, deployment, compliance or test evidence is asserted. An inaccessible repository is **not** proof that no implementation exists.

**Evidence:** Governing `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master` `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`; [opening review](../../../reviews/gaming-conceptual-review-baseline.md). ADR-0017 and ADR-0018 are **Accepted** at that governing revision. This document proposes an *idealised business contract*, not the implementation's root contract.

## Purpose

Support independently governed games, game instances, participants, verified turns/moves/attempts, authoritative outcomes, standings and rule-based competitive progression across individual, group, educational and organised play. A simple game embedded in an application need not create a separate capability: the reusable game-state/outcome lifecycle must justify this boundary.

## Classification

**Recommendation: retain as Domain candidate, subject to owner approval and independent lifecycle evidence.** A genuine game-specific rule engine and authoritative match/result lifecycle are distinguishable from Events (calendar/programme), Assessment (learning evaluation), Identity (people/groups) and Reporting (derived analytics). The default implementation form is a framework-independent headless domain core with an optional Nuxt adapter/presentation; packaging and separate repository remain undecided. A game-specific application composition or stateless rule library is preferable if no cross-application owned session/result lifecycle is needed. No autonomous gambling/wagering capability is inferred.

## Authoritative ownership, exclusions and native behaviour

**Proposed owned records/decisions:** immutable/versioned game definition and ruleset references (only for the game domain; third-party licensed content remains with its owner); tournament/competition rules if they govern gaming-specific rounds; game instance and lifecycle; participant entries and game-specific eligibility determination based on verified external facts; turn/attempt ledger and accepted game actions; official scoring/adjudication and result revisions; standings/ranking methodology, season/leaderboard scope, recalculation version and official corrections; dispute/forfeit resolution over *game results* with attributed evidence. Rankings from Gaming are authoritative **within a declared competition and ruleset**; they do not prove educational competence, general identity standing or commercial rewards.

**Other authorities remain distinct:** Identity owns principals/groups/memberships; Authentication owns session assurance; Authorisation decides protected access; Profile owns personal attributes; Events owns scheduled real-world sessions/programme; Booking owns seat/time reservations; Assessment owns educational assessments and marks; Course/Training/Credentials own their own learning/award outcomes; Product/Pricing/Order/Payment Gateway/Accounting own commerce and money; Publisher/Media own publication and media; Moderation owns cross-domain safety cases; Audit owns separate evidential custody; Reporting owns derived cross-source reports. No game operator can manufacture these facts.

**Conceptual game lifecycle:** draft rules → validated/approved → published version → retired; configured instance → registration open → ready/locked → active → provisionally complete → under review (when required) → confirmed result → archived; cancellation, no-contest, correction and disqualification have explicit reasons, permission and compensating history, not silent replacement. Participant status: invited/registered → eligible/checked-in → active → finished/withdrawn/disqualified, with eligibility revalidation at critical transitions. Immutable original moves and adjudications preserve provenance; corrections create new revisions. Real-time transport is replaceable and must not define score authority.

**Native mode:** local rules/instances, participant admission, deterministic validation, sequencing, dispute controls and result computation operate without third-party gaming providers, provided required caller/access, persistence (where stateful) and applicable safety/legal ports are available. Do not call an optimistic client event a committed move. Conflicting/offline turns are rejected or explicitly adjudicated; irreversible actions cannot be retried under a new idempotency key without duplicate protection. Recovery replays committed moves, checks result versions and rebuilds derived standings; unrecoverable integrity gaps suspend confirmation. No unverified exactly-once messaging claim.

## Dependencies

**Essential *contractual needs* when applicable:** verified Identity principal/group/tenant references, Authentication caller/assurance, server-side Authorisation, scoped game-owned durable persistence and Clock semantics; legally required Privacy/Legal Compliance restrictions and safety controls fail closed. Ports may be supplied by the host rather than direct package imports. Anonymous/pseudonymous offline play is a separate application policy that must not imply a verified Identity principal.

**Conditional cooperation:** Events/Booking for scheduled venues or attendance; Assessment/Training/Course for educational use (Gaming never declares the educational grade); Moderation/Content Security for safety restrictions and referrals; Media/Publisher for game assets and publication; Notifications for authorised notices; Scheduler for deadlines; Workflow for formal appeals; Message Queue for outbox delivery; Reporting for aggregate analyses; Audit, Logging, Observability and Search for their distinct duties. Optional absent services disable their corresponding feature rather than corrupt game-state authority. Avoid directed dependency or Nuxt extension cycles.

## Optional integrations

External game engines, tournament platforms, anti-cheat services, consoles, multiplayer hosts, identity/age evidence providers and external rankings via `integrations` adapters. Accept externally attested results only with verified provider identity, contract/scope, game/ruleset version, event provenance, sequence, source timestamps and signed or equivalent verifiable evidence proportionate to risk. Distinguish provider-submitted, validated, accepted, disputed, final and unknown. If the provider is lost, retain locally accepted history, mark unconfirmed results as unknown and offer documented reconciliation/export/withdrawal; no automatic promotion of provider claims. Provider fees and licensing are host/commercial concerns, not native game rules.

## Version

Not released. Conceptual identifiers: game definition/ruleset version, instance revision, participant-entry revision, turn sequence, scoring algorithm version, result/standing revision, season and evidence source; effective and observed timestamps use Clock. Any eventual published contract must version its commands, queries, events and errors independently of persistence schemas.

## Availability

Installed, configured, operational, enabled, entitled and user-authorised are separate states. A game may be playable with private results while leaderboards/public profiles are disabled; disable unsafe competitive or social features separately. Unverified permission/age/consent/safeguarding/eligibility blocks the affected action. Tenant parentage, group membership, paid entitlements or invitation do **not** imply access to another tenant's game.

## Capabilities offered — idealised public input contract

| Input surface and source | Supplied facts / commands and validation | Required / absence or uncertainty |
|---|---|---|
| Game administrator/host | Define/version rules, create/cancel instances and competitions, set authorised format, scoring, admission caps, tie-breaks, appeals and visibility; validate schema, authorised scope, compatibility and non-retroactivity | Required for managed games; invalid version/ref or conflicting active rules rejects |
| Authenticated participant / trusted game client | Apply to join, check in, play turn/action, concede, leave or challenge outcome; bound actor, instance, ruleset, expected revision, nonce/idempotency, proof and ordered sequence | Conditional on participation; stale revision/replay/out-of-turn action rejected with stable reason; no client-authoritative score |
| Identity / Authentication / Authorisation | Actor and tenant/group references, current authenticated assurance, per-resource decision and expiry | Required for protected actions; unavailable/stale/denied fails closed |
| Configuration / Privacy / Legal Compliance | Versioned approved local settings, retention, consent, age eligibility, safeguarding, territorial and game-type restrictions, legal holds | Mandatory restrictions cannot be weakened; unknown jurisdiction/age where material blocks restricted mode |
| Events / Booking | Event/session reference, timeframe, venue and confirmed booking or attendance eligibility where governing the competition | Conditional; an Events invitation is not a Booking confirmation; unavailable means pending admission |
| Assessment / Course / Training | Authorised linkage for educational play, course assessment requirements and consumer-specific interpretation instructions | Optional/conditional; no inferred grades or training completion |
| Moderation / Content Security / approved integrity provider | Qualified restrictions, source verdicts, reviewed evidence and provider reliability; Gaming validates scope and due-process status | Conditional; signals initiate owned review, not automatically a final cheating finding |
| Scheduler / Workflow / external gaming provider | Deadline triggers, approved review outcomes or provider observations and receipts, with provenance and idempotency | Optional/conditional; delayed job/remote timeout does not prove result finalised |

**Shared input semantics:** Include only relevant tenant, game owner/resource, actor/caller and assurance, permission, policy/ruleset revision, expected state/sequence, correlation and idempotency, evidence/source, effective/observation time. No universal wrapper mandated. Unknown, expired, contradictory and unavailable are distinct from verified false.

## Capabilities offered — idealised public output contract

| Output surface and recipient | Meaning and authoritative guarantee | Disclosure/freshness |
|---|---|---|
| Definition and instance queries → host/player UI | Authorised ruleset, supported actions, instance stage, registration limits, expected revision, deadline and known completeness | Scoped to permitted game/tenant; distinguish draft/active/retired and current versus historic |
| Admission/participation outcome → player, host, Events/Booking where appropriate | Gaming-confirmed entry/check-in and game-specific eligibility outcome; *not* a confirmed seat, Identity membership or payment | Minimum identity references, visibility policy, source eligibility timestamp |
| Action acknowledgement → actor/client | Rejected, accepted-and-committed, or pending external adjudication with idempotency receipt, sequence and revision | Receipt alone never means winner/standing final |
| Official results and score evidence → participant, organiser, Assessment/Training if authorised | Provisional/final/corrected/cancelled outcome, ruleset/scoring version, revision, adjudication evidence and dispute status | Educational consumer independently decides marks, competency or award |
| Rankings/leaderboard → participants, Reporting, authorised discovery | Season/competition-scoped ordered results, tie policy, computation cutoff, ranking revision and exclusions | Explicit privacy, pseudonymisation, delay, small-cohort and anti-harassment rules |
| Authoritative committed events → Message Queue subscribers | GameCreated, ParticipationChanged, ActionCommitted (only where justified), GameFinalised, ResultCorrected, CompetitionCancelled, RankingRecomputed, RestrictionApplied; source ID/version/time | Capability-owned transactional outbox; at-least-once transport, idempotent consumer, no access-grant semantics |
| Reporting/Audit/Logging/Observability/Notifications → specialists | Authorised report source, attributable high-risk action evidence, redacted diagnostics, operational health and notification intentions | Each specialist owns its own resulting records; no secret moves or sensitive proof in logs/public events |
| Export/interoperability → authorised organiser/participant | Ruleset and permitted participation/result history with provenance, redactions, revision and export status | Exclude others' private data, protected anti-cheat signals and licensed content without rights |

**Command/query/event principle:** Commands validate actor and policy on the server, expected revision, action legality, order and idempotency before committing owner state. Queries enforce current disclosure and identify stale/incomplete projections. Durable events arise only from committed changes and may be duplicated or delayed; consumers recheck authorisation before protected effects. Ranking recomputation is a derived computation over Gaming-owned confirmed results, not independently generated truth. Never promise exact-once delivery.

## Configuration

Allowed: game type/rules templates, season duration, tie-breaks, maximum entrants, spectator/publication policy, visibility/pseudonyms, challenge windows, notifications, age-appropriate feature flags, provider selection and data retention only within approved floors. Game rules and scoring retain Gaming validation and versioning; Configuration owns approved settings/precedence, not the interpretation of moves. Strong safety/security controls, applicable law and legal holds are not tenant-disableable (ADR-0018). Policy changes after a match has begun do not silently rewrite its rules or historical official results. Paid game access/entitlements require independently verified commerce contracts and do not grant game administration rights.

## Security, privacy, compliance and integrity

Threat model must address cheating/collusion, forged or reordered turns, compromised clients and servers, replay, racing writes, tampered rankings, sockpuppets, bot abuse, harassment, content abuse, vulnerable adults/children, cross-tenant information leakage, discriminatory eligibility and denial of service. Server-validate rules and turns with concurrency control and verifiable provenance; separate competitor, referee, adjudicator and administrator roles with conflict-of-interest protection and step-up assurance for sensitive changes. Provide dispute/appeal channels and tamper-evident Audit handoff. Do not publish secret anti-cheat details that enable evasion.

Use OWASP ASVS 5 Level 2 baseline and appropriate Level 3 protection, WCAG 2.2 AA, BCP 47/CLDR/Intl, UK GDPR/GDPR constraints as applicable; qualified Legal Compliance determines jurisdiction/effective duties. Online safety, age assurance, children and game-of-chance/gambling classifications vary by activity/jurisdiction: **wagering, cash prizes, staking and payment processing are out of scope pending separate legal and product approval**. Do not infer compliance from a conceptual record. Privacy restrictions apply to player names, behavioural histories, rankings, chat, anti-cheat evidence, exports and right-to-erasure requests; statutory retention/legal holds may constrain deletion. Public standings must not accidentally expose a child's protected identity.

## Cross-capability information flows and reciprocal contract needs

| Cooperating owner | Gaming receives | Gaming supplies / authority limit |
|---|---|---|
| Identity, Authentication, Authorisation | Principal/group/tenant and membership facts, assurance, resource decision | Game-specific player registration and intended action scope; no IAM mutation |
| Profile, Privacy, Legal Compliance, Configuration | Permitted display profile and disclosure, retention/consent/legal applicability, approved settings | Minimal scoped play/result evidence and deletion/restriction requests; no ownership of personal profile |
| Events and Booking | Programme/session/venue and booking confirmations | Competition participation/result and reference; does not book a venue |
| Assessment, Course, Training, Credentials | Curriculum/context, education assessment rules and authorised learner reference | Game evidence/results, not academic scores, qualifications or credential issuance |
| Moderation and Content Security | Safety case/restriction, detection/evidence verdict | Report/context, own enforcement receipt and appeal status; not independent moderation case |
| Reporting, Search | Authorised source queries and visibility requests | Versioned rankings/results with query constraints and withdrawal/correction signals |
| Audit, Logging, Observability | Evidence receipt, correlation and telemetry conventions | Selected attributable security/business events, redacted diagnostics and health |
| Scheduler, Workflow, Message Queue, Notifications | Trigger execution, approval outcomes, transport/delivery receipts | Deadline intents, review requests, committed outbox changes and authorised notices |
| Integrations, Media, Publisher | Trusted external game observations and permitted game content/asset references | Game metadata/result references; publication and file ownership remain external |
| Payment Gateway, Order, Billing, Accounting (only if commercial) | Independently confirmed purchase/entitlement/payment status | Game-specific admission evidence; never payment settlement or ledger entries |

Cross-domain exchange can use host-supplied ports, published services or events without cyclic package imports. No authority flows from mere receipt of an event. Missing optional services preserve the standalone core; missing mandatory protections fail safely.

## Conceptual GUI and headless mode

Host navigation adds **Gaming** to the authenticated sidebar, opening a capability-owned dashboard in the shared shell exemplified by `nuxt-layers-test/application-test-template` and Theme Manager. The dashboard shows My games, available games (authorised), invitations, current turn, upcoming competitions, recent results and accessible ranking summaries. Dedicated views: game catalogue/rules and join; game lobby/participants; accessible board/play interaction and move history; match/result with revision/dispute; tournament bracket and leaderboard; player-specific privacy/disclosure controls; organiser setup, registration, scheduling and referee queue; moderation referrals, appeals and correction review; administrator settings, provider health and audit/reporting links. Sidebar presence is not an authorisation decision; screens hide forbidden actions but server commands recheck. Responsive keyboard/assistive technology interaction, non-colour status, alternate text representations of boards, motion reduction, localised dates and accessible live-score updates are essential. Spectator views show only authorised data. Headless use remains fully supported when the host disables pages/presentation.

## Conceptual contract acceptance examples (not executable tests)

| Input/scenario | Expected behaviour / output | Owner |
|---|---|---|
| Organiser defines game with permitted rules | Approved version and new instance; valid expected action vocabulary | Gaming |
| Player joins with verified scope | Gaming entry accepted; no implied Events seat or payment | Gaming; external source retains its fact |
| Valid turn with revision/idempotency key | One committed sequence update; same key replays receipt without double-scoring | Gaming |
| Out-of-turn or conflicting stale move | Stable refusal and current authorised revision; no state mutation | Gaming |
| Parent tenant queries child tenant leaderboard | Denied unless explicit current resource scope; no inferred inherited access | Authorisation + Gaming |
| Game finalises, Assessment consumes evidence | Versioned final result; Assessment separately decides mark/credit | Gaming / Assessment |
| Provider timeout during external match | Unknown/pending result; cannot publish final ranking until reconciled | Gaming with provider evidence |
| Referee corrects score after appeal | Prior official revision retained, new effective result and ranking invalidation event | Gaming, Audit separately |
| Two identical outbox deliveries | Reporting/other consumer handles duplicates, Gaming source remains unchanged | Gaming / consumer |
| Game cancellation after deadline | Authorised cancellation, participant notices requested; delivery not misreported as complete | Gaming / Notifications |
| Offline game with no optional services | Core local move/scoring works with required security/state ports; optional features disabled | Gaming |
| Unsupported wager or unverified paid prize | Refusal/unsupported operation; never silently routed into payments | Gaming |

## Decision register and independent challenge

- **GAM-01 — Open owner decision:** Retain independent Domain candidate for reusable game-specific rules, authoritative matches/results and rankings, **not** merely screens or an application composition. Recommended yes only if this lifecycle is required across hosts.
- **GAM-02 — Open owner decision:** Game definition/rules and match lifecycle jointly owned by Gaming, but generic content and academic assessment remain external; alternatively split rules into a stateless library where warranted. Recommend cohesive domain-owned ruleset semantics.
- **GAM-03 — Open owner decision:** Competitive rankings authoritative within a declared game/season; external ranking providers require verified reconciliation and explicit source authority. Recommend local accepted-result basis as default.
- **GAM-04 — Open owner decision:** Game-specific competition/rounds are Gaming; scheduled real-world event sessions belong to Events, reservations to Booking. Recommend distinct IDs and no duplicate event calendar.
- **GAM-05 — Open owner decision:** Real-money wagering, financial prizes and game-of-chance gambling services excluded pending separate domain/legal approval. Recommend exclusion by default.
- **GAM-06 — Open owner decision:** Age/safeguarding, privacy and moderation eligibility are mandatory where applicable; public leaderboards and social play are feature-gated. Recommend protective default and fail-closed protected paths.
- **GAM-07 — Open owner decision:** Validated, sequenced and idempotent moves; results are provisional until official; corrections are append-only revisions; provider uncertain means not final. Recommend this invariant.
- **GAM-08 — Open owner decision:** Optional headless core plus host-composed dashboard/organiser/referee screens, with no host-owned gaming logic. Recommend published GUI contracts and disabled-presentation mode.
- **GAM-09 — Technical investigation:** Prove actual implementation existence/contract, supported game classes, deterministic rules engine and whether new platform concepts are needed. No implementation status asserted.
- **GAM-10 — Implementation alignment:** When implemented, publish root `CONTRACT.md`, security model, source-owned outbox, schema/storage register, independent consumer and ADR-0012 Nuxt host evidence; no fixed REST signature is approved here.
- **GAM-11 — Acceptance pending:** Owner to approve boundary and safety exclusions; latest-master technical/architectural reconciliation, PR checks and explicit merge approval remain required.

**Independent challenge:** A universal game engine for every genre may be incoherently broad. Limit initial scope to explicitly supported, deterministic game families and versioned rules. The record does not assume that a chess match, sports tournament, simulation and online shooter share identical validation mechanics or latency guarantees. Games involving user-generated chat, gambling, children or high-stakes prizes may warrant independent safeguards or separate domain reviews. Avoid cyclic dependency between Gaming and Events/Assessment: their calls and event references are routed through public contracts or host composition.

## Deferred work and sign-off

**Conceptual specification proposed, not accepted.** No root gaming contract or implementation tests are available. Resolve GAM-01–08 with the owner, then verify remaining technical evidence and the latest governing/master integration. Actual Git mergeability/CI, policy compliance, and security/functional acceptance are not established merely by this document. **Do not merge without explicit approval.**
