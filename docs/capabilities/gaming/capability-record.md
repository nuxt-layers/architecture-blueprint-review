# Capability Record — Gaming

## Capability Name:

`gaming` — composable game portal, catalogue, game launch and leaderboards.

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

**Owner clarification agreed in principle, 18 November 2026:** Gaming is intended as a **container/portal for separately developed game layers**, such as an arcade space shooter, puzzles or racing. Each game is an independent layer in its own right. The previous broad game-engine interpretation was incorrect and is superseded in this working record. This is a **proposed conceptual specification, not final approval of the detailed boundaries**. No accessible `nuxt-layers/gaming` root `CONTRACT.md` or runtime was verified; there is no claim of an implemented API.

**Latest known evidence:** Governing `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master` moved since PR opening from `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` to `258bb58e9b64987d1c6bd3e44716c6d3412726c0` at this review. Apply current-master reconciliation before merge. [Opening and review evidence](../../../reviews/gaming-conceptual-review-baseline.md).

## Purpose

Supply a reusable, themed, accessible **Games** capability dashboard and catalogue. The host explicitly composes selected independent game layers. Gaming discovers/receives their documented public contributions, controls available catalogue entries and portal routes, obtains appropriately verified score results and maintains scope-controlled leaderboards. It is NOT a universal game engine and does not own gameplay, game physics, timers internal to gameplay, moves, levels, collisions, original score calculations, individual game routes' private implementation or asset libraries.

## Classification

**Recommended: Platform capability with optional Presentation contribution**, rather than the previous Domain classification, subject to owner approval and governing catalogue alignment. Its reusable game registration, score acceptance/leaderboard lifecycle and cross-game discovery are platform-like services; it owns independently meaningful leaderboard records, but no game rules. If the host only wires static navigation and games have no shared score lifecycle, a lightweight presentation/application composition could suffice; the intended reusable leaderboard and score-validation boundary supports this proposed Platform classification. Do not create an extra repository solely because a candidate has a catalogue entry.

**Implementation form:** a headless gaming core plus optional Nuxt Layer presentation; individual games are separately composable Nuxt Layers with their own headless logic as applicable. The host installs and explicitly selects each; `gaming` must not dynamically execute arbitrary remote package code or infer that a registration grants installation/authorisation. No direct extension from Gaming into individual game layers; use documented public contribution contracts and host composition to preserve ADR-0016's acyclic graph and ADR-0012's one-operation/50-line host budget.

## Ownership and exclusions

| Gaming owns | Individual game layer owns | Other capability owns |
|---|---|---|
| Registered **game descriptors** and availability policy within its catalogue | Its title-specific rules, supported modes, game loop and gameplay state | Host owns package selection, application composition and routes outside Gaming's documented contribution |
| Portal-level launch coordination and permitted game discovery | Its game entry/launch contribution, game screen, controls, assets and loading | Theme Manager owns theme; UI owns generic presentation components |
| Authorised score submission **receipts**, acceptance decision and accepted score history with reference to game evidence | Primary computed score/result and its validation/attestation method; game-specific correction source | Identity/Profile/Authentication/Authorisation own actor, personal data, session and access |
| Leaderboard competition/scope, ordering according to each game's published score policy, revisions and withdrawal/recalculation | Interpretation of score units, tie criteria and playable difficulty/mode | Reporting owns cross-source report definitions/aggregates; Audit owns evidential custody |
| Leaderboard administration, visibility, retirement/retention and replay-safe published changes | Game state, pause/restart, game failures, rules and scoring changes | Privacy/Legal Compliance own applicable consent, retention/legal constraints |

A Gaming leaderboard is the **authoritative portal publication of accepted rankings**, not proof of raw game execution validity. A game owns the original result and must supply appropriate evidence. Gaming rejects or holds scores it cannot validate to the required trust policy; client-only scores are not automatically competitive achievements. Third-party game scores require provenance and approved connector rules.

**Lifecycle:** descriptor proposed → validated/selected → enabled → unavailable/disabled → retired; score submitted → rejected/pending → accepted → corrected/withdrawn; leaderboard generated → published → recomputed/archived. Uninstalling a game removes the playable launch but need not erase permitted historical scores. Rule/scoring-version changes must not silently mix incomparable results. No dependency on Events, Booking or educational Assessment for ordinary arcade use. Wagering, cash staking and real-money prizes are excluded unless separately designed and legally reviewed.

## Dependencies

**Essential functionality:** host-supplied registered game contribution(s); secure server-side authorisation for protected score/administrative operations; persistence under Gaming's own owned schema/port where leaderboards are enabled; clock/time semantics; validated configuration and applicable privacy/security floors. A host may offer a Games dashboard with **no games installed**, displaying an accessible empty state. Public catalogue browsing may be anonymous where authorised; registered score ownership requires a trustworthy actor or explicitly approved accountless pseudonymous design.

**Optional/conditional:** Identity/Profile/Authentication/Authorisation for named player scores; Privacy/Legal Compliance for retention, publication and child protection; Audit and Logging for evidence/diagnostics; Reporting for cross-game analytics; Notifications for player communications; Content Security/Moderation for abusive names, conduct or cheating disputes; Message Queue for durable changes; Search for game discovery; Media/Publisher for published descriptions/graphics; Integrations for external hosted games; Observability for system telemetry. Contract needs are directional and may be host-supplied rather than package imports. Missing mandatory protection fails closed; optional unavailability does not break ordinary game launching.

## Optional integrations

Individual games may choose Phaser, PixiJS, KAPLAY or plain browser APIs; Gaming itself must not impose one rendering/physics engine. Hosted game/provider adapters need independent approval, versioning, isolation, data-flow transparency and withdrawal. Unavailable game manifests/exports give an explicit unavailable/invalid state; no silent fallback to executing untrusted code. Third-party score providers cannot silently overwrite locally accepted rankings.

## Version

**No published contract version.** Proposed versioned game descriptor schema, game package/contribution version, score format/scoring policy version, game mode/difficulty, leaderboard policy revision, accepted score/result revision, event schema revision and provenance. Advertise supported versions and migration/compatibility rules before implementation.

## Availability

Distinguish (a) installed game package (host), (b) valid game public contribution, (c) Gaming registration, (d) enabled/operational launch, (e) score-recording support and (f) permitted leaderboard publication. No games installed is a valid empty state; temporarily broken or retired game is not marked playable. Host navigation visibility does not establish game or score permissions.

## Capabilities offered — idealised public **inbound** contract

| Inbound source and surface | Facts, commands and validation | Absence/failure semantics |
|---|---|---|
| Host-selected individual game layer — **game contribution/registration** | Stable namespace/ID, version, display name, description/icon reference, public launch contribution, modes, input/accessibility capabilities, score format/order/tie rules, score proof requirements, privacy and supported contribution schema | Invalid/duplicate ID, unsupported version or incompatible contribution rejected; no private game imports |
| Host or authorised administrator — **catalogue controls** | Select/enable/disable/retire game descriptor, set visibility/allowed leaderboard periods, set approved policy and status; audited scopes | Unsupported/uninstalled game unavailable; invalid policy or missing permission refused |
| Player/host — **discovery and launch request** | Game ID, permitted actor context and desired mode; host-selected route contribution and permission recheck | Unknown/disabled/incompatible game returns stable unavailable result; no unsafe launch |
| Individual game — **submit result** | Game and version, mode/difficulty, claimed player/approved pseudonym, game-generated result ID, score and units, evidence/attestation/validation result, score version, occurred time, idempotency and correlation | Unverified browser claims rejected/held for competitive board; duplicates replay receipt; conflicts do not overwrite |
| Individual game/authorised adjudicator — **score correction/withdrawal** | Authoritative source revision, reason, evidence, prior accepted result ID, authorised scope | Retain history and recompute rankings; not a blind administrator edit |
| IAM/Privacy/Legal Compliance/Configuration | Authorised principal or limited pseudonym, current disclosure decision, applicable safety/retention/consent settings and effective versions | No implied permissions from having an account, tenant parentage or group membership; unknown required protection blocks action |
| Reporting/Audit/Logging subscribers | Scope-constrained queries, accepted evidence handoff and correlation metadata | No bulk data leakage, no private-store access; diagnostic failure never makes a score valid |

**Game contribution:** a small published descriptor plus public launch and result submission integration points is preferred, not a mandatory global game engine, shared client package or arbitrary game runtime. Inputs are runtime-validated; host passes only the necessary caller/resource/policy context, not a new universal wrapper.

## Capabilities offered — idealised public **outbound** contract

| Output and consumer | Guaranteed meaning | Limits |
|---|---|---|
| Game catalogue/discovery → host/dashboard | Registered available/disabled/retired games, public descriptor and permitted launch destination | Descriptor does not prove game health unless independently checked |
| Launch decision → host/player | Selected authorised game/mode and public launch contribution; possible unavailable/denied outcome | Game remains responsible for its screen and gameplay |
| Score receipt → originating game/player | Accepted, rejected or pending; stable receipt/result ID, reason, revision and idempotency outcome | **Accepted score** means Gaming accepted trusted game evidence, not that Gaming independently simulated play |
| Leaderboard query → player/host/game/Reporting | Game-specific ranked results with mode/difficulty, ordering/tie policy, season, cutoff, provenance, revision and completeness | No meaningful cross-game ranking without explicitly defined comparability; privacy and age rules applied |
| Player's own results → permitted player/game | Scoped accepted history, personal best and status (including corrections/withdrawals) | Profile controls display information; no unrelated player's private scores |
| Committed outbox events → Message Queue/Reporting/other consumers | GameRegistered, GameAvailabilityChanged, ScoreAccepted, ScoreCorrected, ScoreWithdrawn, LeaderboardRecomputed with source ID, version/time | Idempotent consumers, eventual delivery; event is not an access token |
| Audit evidence / Logging diagnostic → specialist capabilities | Attributable accepted high-risk actions and redacted operational errors/timing | Audit owns evidential records, Logging owns technical logs; Gaming owns score facts |
| Reporting source → Reporting | Authorised game, mode, score/result, ranking snapshot, withdrawal and revision data | Reporting must not become ranking source of truth |

**Interactions:** registration, publication, correction and submission are commands, with permissions, expected revision and stable error semantics; catalogue, player history and leaderboards are authorised queries; durable events follow committed Gaming-owned changes. Scores received twice must not count twice. Late score corrections invalidate projections. Failed launch must not mutate scores, and successful game play must not imply leaderboard acceptance.

## Cross-capability interfaces and reciprocal ownership

| Other capability | Information Gaming receives | Information Gaming supplies |
|---|---|---|
| Identity, Authentication, Authorisation | Verified actor/group/tenant/assurance and allowed actions | Game/score resource references for scope checks; no new user accounts |
| Profile, Privacy, Legal Compliance, Configuration | Permitted display name/pseudonym, retention/consent/age restrictions and approved policies | Minimal player score references and publication/withdrawal receipts; no profile ownership |
| Logging | Trace/correlation and technical sink semantics | Errors for registration, launch, score submission, latency and unavailable games, redacted |
| Audit | Evidence acceptance/receipt policy | Attributable leaderboard reset, correction, privileged enablement, suspicious score review and export evidence |
| Reporting | Authorised report definitions, report IDs and refresh/read requirements | Game catalogue and versioned accepted scores, ranking facts and corrections for derived reporting |
| Message Queue/Observability | Transport/telemetry receipts and diagnostic conventions | Committed versioned leaderboard changes and operational counters |
| Content Security/Moderation | Applicable safety verdict/case disposition | Report of abusive game metadata/name or suspicious result, enforcement receipt |
| Search/Media/Publisher | Authorised game discovery, image and publication services where used | Permitted game descriptors, status and launch references |
| Events/Booking/Assessment/Training | Only if a game is embedded in an event, booking or educational activity | Scoped accepted game result evidence, **not** attendance, reservation, grade or credit |
| Each individual game layer | Public descriptor, launch contribution and primary validated result/evidence | Portal listing, authorised launch context, score submission receipt, leaderboard queries |

**Logging vs Audit vs Reporting:** Logging is sanitised engineering diagnostics; Audit is accountable, tamper-evident history of sensitive decisions; Reporting is derived analytics and reports. A high score is a Gaming-owned business fact. Logging cannot prove game validity, Audit receipt does not compute leaderboard position, and Reporting cannot correct a score.

## Configuration

Allow per-tenant/host selected games, ordering, category, launch availability, leaderboard visibility, score retention within mandatory floors, anonymity/pseudonyms, permitted seasons, tie display, game modes, and whether historical rankings remain visible after retirement. Configuration owns scoped approved setting values; Gaming validates its own score and ranking policies. Gameplay tuning, controls and game-rule configuration belong to each individual game. Distinguish per-user preferences (e.g. muted sound) from enterprise safety floors; never retroactively mix game score definitions.

## Security, privacy, compliance and integrity

Adhere to accepted ADRs (including ADR-0012/0016/0017/0018), OWASP ASVS 5 Level 2 baseline (Level 3 where appropriate), WCAG 2.2 AA, BCP 47/CLDR/ECMA-402, UK GDPR when applicable, runtime input validation, least-privilege server-side checks, safe content and tenant isolation. Child users, public rankings, anti-cheat evidence and anonymous/pseudonymous submissions need qualified privacy/safety policy; anonymous casual play must not automatically confer competitive or account ownership. Protect against fake score submissions, score replay, client tampering, path injection, XSS in game names, counterfeit game contributions, cross-tenant rankings, oversized game bundles, malicious dependency assets and silent game disablement. Games are *trusted installed code* only after host review; a registered descriptor is not executable remote code. External IP/trade dress/assets require independent clearance: arcade inspiration does not license original artwork, name, audio or copied source.

## Standards and verified candidate libraries (reviewed 18 November 2026)

**Relevant standards:** OWASP ASVS 5.0 for protected APIs; WCAG 2.2 AA and accessible alternatives for graphics-intensive games; W3C Pointer Events and Gamepad API for input (the latter remains a Working Draft as of November 2026); JSON Schema 2020-12 or an equivalent public versioned schema to define contributions; Web Application Manifest for optionally installable host experience (not mandatory per game); BCP 47/CLDR/ECMA-402 for locale, time and score display; existing governing Nuxt ADR-0012/0016 for public composition and no cycles. Web standards are not, by themselves, a ready-made game contribution protocol; we define a minimal local contract.

| Library | Licence verified from relevant source | Appropriate use | Recommendation |
|---|---|---|---|
| [Phaser](https://github.com/phaserjs/phaser) | MIT | Individual complete 2D arcade games (physics, input, scenes) | Strong optional choice for an arcade shooter; **not** a Gaming dependency |
| [PixiJS](https://github.com/pixijs/pixijs) | MIT | Individual game's accelerated 2D rendering | Alternative if the game owns its own rules/physics |
| [KAPLAY](https://github.com/kaplayjs/kaplay) | MIT | Compact 2D browser games | Optional for simple games |
| [howler.js](https://github.com/goldfire/howler.js) | MIT | Sound/music control within games | Optional, obey audio licensing/preferences |
| [Colyseus](https://github.com/colyseus/colyseus) | MIT | Only separately justified authoritative multiplayer games | **Not needed** for basic single-player leaderboards |
| [Zod](https://github.com/colinhacks/zod) | MIT | Runtime validation of game descriptors and score contracts | Strong candidate for Gaming's boundary |
| [Vitest](https://github.com/vitest-dev/vitest) | MIT | Package/contract test tooling when implemented | Optional development tooling |
| [Matter.js](https://github.com/matter-js/matter.js) | Current repository Apache-2.0; historic npm 0.20.0 labelled MIT | Physics in individual games | Licence **varies by revision**; verify exact release/transitives; not essential |

All candidate licences are commercially permissive, but exact package version, bundled assets, patents/attribution requirements and transitive dependencies must be inspected before adoption. No proprietary hosted leaderboard, cloud engine, Redis/ElasticSearch or other provider-locked service is required. PostgreSQL through capability-owned ports is a natural durable leaderboard implementation choice, not part of the public data types. A rendered score list does not justify buying a hosted service.

## Conceptual GUI and host integration

**Representative host:** `nuxt-layers-test/application-test-template` exposes a shared shell with top bar, accessible responsive collapsible sidebar, homepage `/`, admin `/admin`, Theme Manager dashboard `/theme-manager`, host-owned branding and navigation configuration. Gaming should follow this precedent with a **Games** sidebar entry and dashboard (illustrative routes, host-configurable): `/gaming` overview/catalogue; `/gaming/:gameId` game detail and public launch contribution; `/gaming/:gameId/leaderboard` rankings; `/gaming/me` authorised personal scores; `/gaming/admin` game registration/availability, score integrity review and leaderboard policy. Individual game layers own their actual gameplay screens or declared launch components; Gaming hosts/links them through approved public contributions, without a bespoke universal game board, controls or renderer.

**Dashboard:** game cards with icon, title, availability, description, input requirements and Play action; recently played/featured games where permitted; per-game high score preview. **Game detail:** how to play/controls, requirements, Play and leaderboard; disable Play with a clear reason when unavailable. **While playing:** individual game's canvas/DOM view with appropriate Back to Games, pause/help/sound/keyboard guidance and accessible alternatives owned by game. **Leaderboard:** per-game filter for mode/difficulty/season, position/score/date and verified status; pseudonym/privacy controls; historical/corrected data indication. **Admin:** selected installed games, enable/disable, schema compatibility/error, score review and correction request, privacy/retention, moderation and audit/report links. Host owns top navigation and brand, Gaming owns its UI public contributions, each game owns its gameplay screen.

Accessibility: all portal screens keyboard/assistive-technology accessible; each game must advertise input and accessibility support, with keyboard/gamepad/alternative controls where feasible, focus preservation on canvas entry/exit, reduced motion, mute, non-colour indicators, responsive layout and accessible leaderboard. No claim that a specific game is WCAG-conformant without acceptance evidence. `presentation: false` or equivalent means no Gaming pages and unchanged headless APIs. Asset splitting, lazy game loading and route-level caching minimise impact on the rest of the application.

## Conceptual acceptance scenarios (not executed)

| Input | Expected behaviour / output | Authority |
|---|---|---|
| Host selects two independent game layers | Gaming lists both through supported published descriptors without importing private code | Host chooses packages; Gaming owns catalogue |
| Host has no games | Dashboard shows meaningful empty state; core score services do not claim any playable games | Gaming |
| Arcade game launches | Gaming supplies authorised launch context, game renders own canvas and controls | Game owns gameplay |
| Game submits validated score with stable ID | Gaming accepts once, records provenance, updates per-game leaderboard | Game owns result; Gaming owns acceptance/ranking |
| Browser posts arbitrary unverified top score | Rejected or held; cannot appear on verified leaderboard | Gaming |
| Two games use inverse scoring (high wins vs low wins) | Separate board ordering and tie policies; no accidental cross-game aggregate | Game score contract; Gaming board |
| Same result replayed after timeout | Original receipt returned, never counted twice | Gaming |
| Scoring rules change | Old entries remain version-scoped or migrated only by approved verified policy | Game defines rules; Gaming owns ranking revision |
| Game disabled/uninstalled | Launch unavailable; historical leaderboard retained or withdrawn according to lawful policy | Host/package; Gaming publication |
| User requests another tenant's private results | Denied/redacted; parent tenant does not inherit access | Authorisation/Gaming |
| Child's score published | Only permitted pseudonym/scope; safety floor and consent/disclosure enforced | Privacy/Legal Compliance/Gaming |
| Reporting reads results after correction | Revisions and correction event permit idempotent refresh | Gaming source; Reporting derivative |
| Logging or Audit unavailable | Mandatory evidence failure blocks sensitive changes as policy requires; ordinary sanitized logging outage does not fabricate score acceptance | Gaming/Audit/Logging |

## Decisions, status and challenge

- **GAM-01 — User clarification supersedes old scope:** Gaming is the **container/portal**; independent game layers own gameplay/rules/primary results. Treat the previous universal game engine interpretation as incorrect.
- **GAM-02 — Proposed for approval:** Reclassify Gaming as reusable Platform capability with optional Presentation; game titles are distinct domain/game layers, with host-managed composition.
- **GAM-03 — Proposed for approval:** Gaming owns portal-specific game catalogue/enablement, accepted score history and scoped leaderboards; individual games own their scoring/validation evidence.
- **GAM-04 — Proposed for approval:** Individual games publish versioned descriptor/launch/result contribution contracts; no dynamic untrusted code execution and no direct Nuxt extension cycle.
- **GAM-05 — Proposed for approval:** Exclude gambling, real-money prizes, payment flows and cross-game score comparisons without explicit independent approval and score compatibility.
- **GAM-06 — Proposed for approval:** Safeguard privacy, children, accountless play and unverified browser scores; competitive publication requires verified evidence.
- **GAM-07 — Proposed for approval:** Idempotent score submission, corrections and outbox events, separate result evidence and leaderboard authority; retain historical revision provenance.
- **GAM-08 — Proposed for approval:** Shared host sidebar → Gaming dashboard → independent game screen; per-game leaderboards and admin, optional presentation, lazy-loaded game assets.
- **GAM-09 — Investigation:** Confirm implementation existence, exact game contribution contract, game-result trust mechanisms and selected library version/licence evidence at implementation time.
- **GAM-10 — Implementation alignment:** Publish independent `CONTRACT.md`, canonical public exports, failure codes, persistence/storage register, authorised score transport, owned outbox, headless/host acceptance; no implementation repo changes in this PR.
- **GAM-11 — Acceptance pending:** Owner approval, reciprocal reconciliation, latest-master Git and architecture check, CI/protected-branch evidence and explicit squash merge consent.

**Challenge:** A host-provided list of games can be pure composition; Gaming should own only the durable *portal leaderboard and publication* decisions genuinely shared across games. Do not introduce arbitrary game orchestration, generic tournament management, matchmaking, virtual currency, social chat, user accounts or custom game-asset stores without independent requirements. One game's rules and anti-cheat logic cannot be universalised at this layer. Semantic contract changes require coordinated versioning. Concurrent conceptual reviews may amend related records; no unmerged PR is authority.

## Deferred work and sign-off

**Detailed conceptual design awaiting owner sign-off.** This working document does not certify code, legal compliance or tested interfaces. A later actual Gaming `CONTRACT.md` must be independently usable under ADR-0012 and align with accepted game interfaces. Recheck live governance and blueprint master, overlapping PRs, PR mergeability and checks before any explicitly authorised squash merge.
