# Conceptual capability review — classification and ownership gate

**Status:** Blueprint **working review method**, proposed for use in subsequent alphabetical capability reviews; **non-normative**. The governing source remains `nuxt-layers/architecture-rules`, not this file.

**Evidence baseline (15 November 2026):** `nuxt-layers/architecture-rules` `master` `2eea557fa3acbf9412fea065d2a3cdda42a764fc`: `docs/capability-standard.md` (Classification and Implementation types), `docs/catalogue.md` (organisational archetypes, candidate consolidation and presentation entries), `docs/architecture.md`, and accepted ADR-0001/0002/0009/0011/0012/0015/0016. See the prior blueprint [rationalisation review](catalogue-rationalisation-dependencies.md) and [organisation consolidation review](organisation-candidate-consolidation.md). Verify the **live governing `master` and accepted status afresh** when conducting a future review.

## Purpose

**A catalogue entry is a name for a proposed responsibility or architectural building block, not proof of an independently stateful service, database, Nuxt Layer or repository.** Before describing a capability's idealised inputs/outputs, dependencies, persistence or graphical screens, make an evidence-based classification and ownership recommendation. This prevents duplicate records and inappropriate domain authority in presentation-only aggregators, organisational archetypes, application compositions and libraries.

This gate **does not** replace the governing standard's responsibility classifications: **Foundation, Platform, Domain and Presentation**. Separately record an **implementation kind** (Nuxt capability layer, framework-independent capability, stateless library, infrastructure integration library, external connector, application composition or a validated organisational archetype). A presentation contribution can be independently reusable without becoming a business-data owner; a framework-independent service may have optional Nuxt presentation; a composition may aggregate many domains without owning them. Do not flatten these distinct axes into one mutually exclusive enum.

## Mandatory first substantive step — classification and ownership

After checking governing `architecture-rules` and blueprint `master`, the current catalogue/register and any available root public `CONTRACT.md`, complete the following **before proposing new business records, tables, APIs or screens**.

| Gate question | Required written finding |
|---|---|
| **1. Distinct responsibility** — What outcome does this entry deliver, and what other owner already performs it? | Bounded purpose, existing source owners and what would be duplicated or lost if consolidated |
| **2. Authority** — Does it decide or authoritatively store new business/platform facts, enforce independently meaningful invariants or operate a distinct lifecycle? | Explicit record/decision owner, or **none**. An entry can own rules/services without a database; an admin UI alone is not an independent domain |
| **3. Presentation versus domain** — Is its main job to assemble dashboards, forms, workflows or views of other owners through their public contracts? | Presentation/aggregator role, source contracts, data authority, user journeys and server-side security boundary; no invented user or transaction store |
| **4. Composition versus capability** — Does it choose capabilities, configure an application, supply navigation/routes/branding or provide archetype specialisation? | Application/composition or organisational archetype recommendation where no independent domain lifecycle is proven |
| **5. Implementation form** — Would it be better represented by a small stateless library, infrastructure library or provider-specific connector? | Implementation-kind rationale; separate provider transport from the business semantics of its owning capability |
| **6. Persistence necessity** — What is the *minimum* owned state, if any, and why is it owned here? | Distinguish **business source records**, independent operational coordination state, optional derived/cached projections, presentation preferences and host-supplied configuration. State may be **none**. Never add a schema/store simply to justify a catalogue name |
| **7. Public boundary** — Which authoritative contracts are consumed; what new output or orchestration is supplied; what happens when a dependency is absent? | Directional required/optional edges, read/write/command/event authority, permissions and failures. No direct access to private stores; no joint dependency cycles |
| **8. Security and GUI** — How can users access it and who can see/act on aggregated content? | Server-authorised source reads and commands, aggregate disclosure/tenant isolation, likely screens only if applicable, host-owned navigation, optional/headless mode and accessibility |
| **9. Evidence and uncertainty** — Is a root implementation `CONTRACT.md` actually published? What governing provisions have been accepted? | Verified paths, SHA and direct evidence; label proposal, agreed conceptual decision, implementation evidence and acceptance separately. Do not claim implementation based on the catalogue or test template |
| **10. Minimal coherent platform** — Is a separate capability *and* repository justified by independent authority/reuse/testing/security? | Explicit disposition, trade-off and consequence for catalogue/register, other records and later review; do not automatically create a repo |

### Architectural form and example guidance

| Recommended form | Ownership and public interface pattern | Data-store default and examples already grounded in governing catalogue |
|---|---|---|
| **Independent Foundation / Platform / Domain capability** | Cohesive rules/decisions and/or owned records, their lifecycle and independent public contract. Optional screens may accompany a headless core | Own persistence only **where required by actual state**; e.g. Billing's charge lifecycle, Identity memberships. Distinct domain ownership must be evidenced |
| **Presentation-only capability or aggregator** | Own UI interaction, accessibility, component state and cross-capability presentation; consume other owners' published queries/commands and return UI results, not business facts | **No new business tables**; may use only justified bounded UI preferences or presentation cache where permitted. `ui`, `content-editor`, `gallery`, `company-console`, `user` are catalogue examples |
| **Application composition / organisational archetype** | Select, wire and specialise existing capability contracts and host routes/branding/navigation; role-oriented dashboards/flows, possibly presenting many domains | No second entity/membership/transaction authority. `application-compositions`, `shop`, `business`, `organisation` by default. Some labels require later independent-domain evidence |
| **Stateless library / infrastructure integration library / connector** | Reusable functions, transport or provider adapter; business meaning remains with an owning capability | No artificial domain persistence or mandatory Nuxt shell. `rich-text`, `template-engine` candidate, provider SDK/transport integration |
| **Coordination/orchestration component** | Routes/coordinates public operations and may own *execution* status, retries, durable checkpoints or configuration under a justified separate responsibility | Operational state is **not** the source business transaction. Could be a capability, composition or integration depending on evidence; decide per review |

**Cautions:** Reporting can own report definitions, generated artefacts and execution lifecycle without owning originating charges or ledger entries; it is not automatically a *stateless* presentation capability. Conversely, a presentation-only console can still be reusable, complex and security-critical without holding original business data. Independent state is evidence of possible ownership, not a universal necessary condition; a framework-independent rule/service may be stateless and still have a coherent public contract. If a role-oriented UI demands new independent approval records, decide which existing source capability owns them before inventing a new domain.

## Required disposition and consequences

Choose **one** review outcome for the catalogue entry, with source evidence, confidence and a record of alternatives:

1. **Retain as independently owned capability** — show distinct authority and public contract, classify Foundation/Platform/Domain/Presentation as applicable; evaluate separately whether a Nuxt layer/repository is justified.
2. **Retain as presentation-only contribution** — no ownership of source business records; document owner contracts, optional screens, navigation, security and read-only/command-forwarding semantics.
3. **Reclassify as composition, archetype or library** — document what it assembles and who owns underlying facts; preserve useful catalogue vocabulary as needed.
4. **Consolidate into a named existing owner** — identify which public contract/screen would expand and why this avoids duplicate records.
5. **Defer pending evidence** — identify exact unknown contract, independent lifecycle or record owner, the next review and safe interim interpretation.

A disposition is **not a normative catalogue change** until separately approved through the proper governing repository. Maintain the entry in the working catalogue/register with a clear provisional status, rather than deleting it or marking it implemented. A conceptual approval does not authorise a new package, schema or deployment.

### Required review-record subsection (copy into each alphabetical capability record)

```markdown
## Architectural classification and ownership gate

- Governing authority, accepted ADRs and checked commit SHA:
- Current catalogue class and implementation-evidence status:
- Distinct responsibility / existing owners:
- Authoritative source data, decision rules and lifecycle (or explicitly none):
- Presentation-only, composition, archetype and library alternatives:
- Recommended responsibility classification:
- Recommended implementation kind / reason for independent repository:
- Owned persistence: business | operational | derived | preferences | none; justification:
- Required/optional public inbound and outbound contracts, absence and failure:
- Likely navigation/screens or explicitly not applicable; server access and disclosure:
- Disposition: retain | presentation-only | reclassify | consolidate | defer:
- Proposal versus owner-approved versus implemented/accepted status:
- Reciprocal notes / catalogue-register or ADR follow-up and acceptance evidence:
```

Do **not** pre-populate a candidate's approval or actual `CONTRACT.md` from this template. Review the currently published contract if one exists, or state **unverified / no confirmed implementation contract**.

## How the gate changes the rest of a comprehensive review

| Later review part | Stateful authoritative capability | Presentation-only or GUI-led aggregator | Composition / library |
|---|---|---|---|
| **Inputs and outputs** | Commands/queries/events on owned authoritative records; state/finality, revisions and provenance | Source capabilities' authorised reads and commands; derived UI summaries, navigation, action feedback, display freshness; no authority over their records | Explicit public wiring/delegation or library functions; no fabricated domain events |
| **Dependencies and degradation** | Minimal required contracts; conditional owners; fail closed for mandatory controls | Optional sources show unavailable/partial/stale without asserting business success; never query another capability's private schema | Host/configuration inputs or narrow provider/function dependencies; avoid cycles |
| **Persistence** | Only owned domain and durable coordination/outbox state where justified | None by default; any settings/cache must have an owner, purpose, retention, tenant and security model | No domain database; operational state only if function justifies it |
| **GUI** | Optional separable screens over own headless contract; side-menu/dashboard integration in test template | Screens and user journeys are **primary deliverable**; data authority stays with source owners; host controls nav/branding and server security still applies | Composition owns host navigation/branding; stateless library may have no GUI |
| **Acceptance** | Independent business invariant/state/recovery/contract evidence and, where applicable, GUI tests | Cross-owner scopes, permissions, aggregate inference, filtering, stale/empty states, accessibility and optional-sources absent | Minimal consumer/composition tests, no unnecessary state or host-code inflation |

**Presentation review remains mandatory as an assessment, not mandatory screen creation.** For GUI-led aggregators, describe navigation, dashboard/list/detail/edit/review/reporting journeys using `nuxt-layers-test/application-test-template` as an *illustrative tested host pattern* (host-owned Capabilities sidebar → capability dashboard) while avoiding a claim that the template implements automatic navigation registration or production security. Apply Theme Manager's semantic tokens, WCAG 2.2 AA, i18n and server-side Authorisation. For headless services/libraries record **no standard GUI** and why.

**No universal storage assumption:** The governing standard says *stateful* capabilities own their schemas and stores. It does **not** require a database from every catalogue entry. Do not turn a derived cache, operating log, user preference or workspace configuration into a duplicated canonical domain record.

## Review quality and approval checklist

A classification-first review is ready to put forward for approval only if it:

- distinguishes class, implementation kind, data/state ownership, repository and deployment as **separate** decisions;
- checks for existing canonical owners and redundant state or screens;
- records credible presentation/composition/library alternatives and an explicit disposition;
- provides idealised public inbound/outbound contracts and reciprocal notes **appropriate to that disposition**, without importing private implementations;
- covers permissions, privacy, aggregate disclosure, optional dependencies, presentation/headless mode and accepted architecture;
- records implementation evidence versus architectural proposal and future acceptance criteria;
- identifies any *actual* governing catalogue/standard/ADR amendment as a **separate follow-up**, never silently declaring this blueprint document normative.

**Suggested sequencing:** apply to **all remaining alphabetical reviews**, starting at the next unreviewed entry. Revisit already-completed records only if the classification test exposes a material contradiction or an obvious duplicated owner; do not re-open accepted domain decisions solely because the working method has gained a clearer checklist.
