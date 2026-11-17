# Nuxt Layers — Parallel Capability Conceptual Review Protocol

**Status:** Blueprint working procedure; non-normative.  
**Scope:** `nuxt-layers/architecture-blueprint-review` capability conceptual reviews, including concurrent reviews in separate ChatGPT conversations.  
**Governing repository:** `nuxt-layers/architecture-rules` (`master` accepted authority).  
**Representative presentation test host:** `nuxt-layers-test/application-test-template`.  
**Companion:** [Capability review starter prompt](capability-review-starter.md).

## Objective and expected deliverables

Review one assigned capability thoroughly in each conversation, while allowing multiple conversations to work on different capabilities concurrently. Preserve the alphabetical programme without making its reviews strictly sequential.

Every genuine capability review must establish its purpose/classification, authoritative ownership and exclusions, native services and lifecycle, **idealised public input and output contracts**, cooperating capabilities, security/privacy/legal constraints, provider boundaries, conceptual presentation/GUI, acceptance scenarios, outstanding decisions, and a traceable GitHub PR. An item may instead be a composition, library, archetype, presentation-only capability or other architectural artefact; do not force it into a conventional data-owning capability.

**Operating rule:** one target capability, one conversation, one dedicated branch, **one draft PR opened at the beginning**. GitHub assigns PR numbers; do not preallocate them or rely on sequence. A conversation may modify relevant reciprocal and shared documents, using reconciliation rules below.

The blueprint is **non-normative**. The authority hierarchy is **accepted ADRs → normative governing standards → approved public capability contracts → implementation evidence**. Do not claim conceptual approval means implementation readiness, legal compliance or accepted governance.

## Phase 0 — Create the review branch and draft PR immediately

This is the **first operational phase** of each new capability-review conversation. A short read-only check precedes repository writes to avoid duplicate PRs.

1. Identify the *actual current* directory name under `docs/capabilities/`; **do not normalise underscores to hyphens or infer paths from display names**. Confirm the target, branch convention and active PRs; if an active target review already exists, resume it rather than create a duplicate.
2. Inspect current `master` identity/commit SHA of both `nuxt-layers/architecture-rules` and `nuxt-layers/architecture-blueprint-review`, with relevant PRs. This preliminary retrieval records the opening baseline; the full authority analysis follows in Phase 1.
3. Create a descriptive, unique branch from the latest blueprint `master`, e.g. `review/[directory]-conceptual`.
4. Make a minimal *meaningful* initial commit, such as `reviews/[directory]-review-baseline.md`, recording target, branch baseline SHAs, review scope, relevant current evidence, intended contract/ownership/GUI deliverables and open PRs. Do not overwrite a substantive capability record merely to create a PR.
5. **Open a draft pull request against `master` now**, before substantive conceptual design. PR body identifies the target, exact initial governing/blueprint SHAs, related work, anticipated changes and current non-normative status.
6. Report branch and URL. Continue updating **that same PR** throughout the review.

If repository access or PR creation fails, state the blocker, do not invent links and do not claim Phase 0 completed. A PR may require at least one changed file; it cannot be opened on an empty branch.

## Phase 1 — Establish authoritative architectural baseline

**Mandatory before substantive capability design or edits.**

### 1.1 Governing rules

Retrieve current `architecture-rules` `master`; record its exact commit SHA. Discover current paths and inspect applicable:

- Platform Charter and architectural principles.
- **Accepted** ADRs (verify acceptance, supersession and effective status; do not treat proposals as binding).
- Normative Capability Standard and classification.
- Capability Catalogue and composition/dependency rules.
- Consumer-facing contracts, one-operation host composition and acceptance obligations.
- Security, OWASP/WCAG baselines, privacy, Identity/Authentication/Authorisation, Legal Compliance, provider neutrality, infrastructure and persistence rules.
- Internationalisation, accessibility, event/outbox and interface/permission responsibilities where applicable.

Follow accepted hierarchy; report contradictions rather than silently replacing governing direction.

### 1.2 Working blueprint

Retrieve latest `architecture-blueprint-review` `master`, record SHA. Review README, catalogue/register, target record, existing proposals and reviews, findings/decisions, related capability conceptual records, **open and recently merged PRs** that affect target. An unmerged PR is provisional; do not mislabel it as approved. If `master` advanced after Phase 0, report both baseline and new current SHA.

### 1.3 Baseline report

Report governing SHA, blueprint SHA, exact target directory and alphabetical position, review branch/draft PR, accepted requirements, existing findings/approvals, related public contracts, neighbouring active PRs, contradictions and open decisions.

## Phase 2 — Investigate existing implementation and published contracts

Determine whether an implementation repository actually exists in the `nuxt-layers` organisation. If so, record identity, default branch and SHA, root `CONTRACT.md`, published purpose and input/output surfaces, commands/queries/events, required/optional dependencies, configuration, security, known limitations and evidence.

**Do not infer an API or completed behaviour from a repository name.** Inspect related capability repositories through their published **root `CONTRACT.md` only**, unless wider inspection is expressly authorised. The target implementation can be reviewed for needed evidence subject to existing project access rules; no local builds/tests or implementation edits.

If a target root contract exists, reconcile *actual* inbound/outbound interfaces, authority, lifecycle and obligations with the idealised conceptual contract. Distinguish **Established/verified**, **documented but unverified**, **agreed conceptual**, **proposed**, **open**, **implementation gap** and **acceptance evidence**.

## Phase 3 — Purpose, classification, authoritative ownership and native behaviour

Establish purpose, intended consumers, independently meaningful capability boundary and classification; distinguish data owner, service, presentation-only, composition, archetype or library. A capability may legitimately own no persistent domain state; a catalogue entry alone does not justify a new package.

Document:

- Authoritative records and source of truth; decisions/policies; state and lifecycle; derived versus source information; evidence ownership; exclusions.
- Minimum native services, validation, invariants, permissions, independent operating mode, failure/recovery, state transitions and supported/unsupported behaviour.
- Essential, optional and conditional external providers; connected/native authority; provider selection, discovery, costs, migration, import/export, synchronisation, reconciliation, withdrawal/revocation and uncertainty.
- What information the target must obtain from other capabilities and what it supplies back; never duplicate another domain's record or business decision.

## Phase 4 — Idealised public input/output contract (mandatory)

Specify interfaces at the **business meaning and authority** level, not fixed endpoint, framework, database or protocol detail. A receiving event does not confer authorisation.

### 4.1 Classify findings, decisions and IDs

- **Established:** governing requirement or verified published contract.
- **Agreed:** explicitly owner-approved conceptual principle.
- **Open decision:** substantive alternative requiring owner approval.
- **Technical investigation:** resolvable by evidence, standards and professional judgement.
- **Implementation alignment:** future published contract/runtime change.
- **Acceptance:** demonstrable evidence needed to satisfy architecture.

Discover issues before numbering; do not manufacture a fixed quantity. Preserve existing IDs, consolidate overlap, track approval explicitly and do not repeatedly reopen settled choices. Resolve technical investigations independently where reliable; present genuinely consequential alternatives with rationale.

### 4.2 Inbound interfaces

For each meaningful input document **source**, **facts/commands/evidence/settings supplied**, **purpose**, **authoritative owner**, **validation**, **required/optional/conditional nature**, **staleness/unknown/invalid/contradictory failure semantics**. Distinguish source facts, commands, provider evidence and effective policy context.

### 4.3 Outbound interfaces

For each meaningful output document **authorised consumers**, **semantics and permitted conclusions**, **authoritative guarantee versus someone else's fact**, **lifecycle status**, **provenance/version/effective time**, **privacy/tenant/disclosure rules**. Cover authoritative information, accepted versus completed results, queries/read models, events, export/reporting and provider status as appropriate. Do not expose private persistence types as the conceptual contract.

### 4.4 Interaction models

Explain legitimate **commands** (validation, permissions, state transition, idempotency, result/recovery), **queries** (authorised scope, freshness, completeness, provenance) and **events** (committed authoritative changes, duplicate/replay, subscriber semantics). Deliberately omit models that have no genuine purpose; explain why. Do not promise impossible exactly-once distributed delivery.

### 4.5 Shared context and invariants

Determine necessary tenant/organisation, caller/assurance/authorisation, owner resource reference and revision, correlation/idempotency, policy/version, effective date/time/Clock semantics, provider source/evidence and completion status. **Do not mandate a universal request object.**

State consumer guarantees about authority, validation, isolation, disclosure, state consistency, reversibility, historical traceability, versioning, unknown failure, idempotency, provider uncertainty and explicit unsupported operations.

### 4.6 Conceptual contract acceptance

Provide representative **input → expected behaviour → output → authoritative owner** scenarios for native operation, cooperating capability, tenant isolation/authorisation, invalid inputs, replay, external provider failure, recovery, historical/lifecycle change, downstream consumption and unsupported acts. These are conceptual acceptance criteria, not executable tests.

## Phase 5 — Full cross-capability interfaces and reciprocal notes

For every material relationship explain: inputs needed, outputs supplied, which party owns facts and decisions, essential/optional/conditional dependence, unavailability, required public interface, and direction/acyclicity. **Conceptual cooperation is not automatically a package import.**

**Reciprocal edits are expected and authorised.** Where an adjacent capability is affected, append a concise dated, status-marked note to its record, linking to the target's conceptual contract; preserve previously accepted decisions and avoid prematurely completing the adjacent review.

**Concurrent safeguards:** Check active PRs before editing the shared file; review provisional competing findings; use bounded additive notes rather than replacing another review's work. If proposed interfaces conflict, mark both clearly and raise reconciliation, never silently override. Multiple reviews may update shared documents; conflicts are handled during integration, not by suppressing useful findings.

## Phase 6 — Configuration, security, assurance, privacy and compliance

Evaluate applicable relationships with Configuration/Profile, Identity, Authentication, Authorisation, Verification, Legal Compliance, Privacy, Content Security, Moderation, Integrations, Audit, Logging, Observability, Reporting, Workflow, Scheduler, Message Queue, Clock, Federation, Search, and other domain owners. **Only include those actually relevant**.

Separate statutory/security floors, organisational policy, configurable options, personal preference and external-provider terms. Record purpose/tenant isolation, source approval, minimisation, retention, GDPR/UK GDPR where applicable, security threat model, recovery and disclosure. Qualified legal interpretation is needed for service/jurisdiction/effective-date matters; technical standards compliance does not establish legal compliance.

## Phase 6A — Presentation, GUI and host integration

For each capability determine whether it requires user-facing, administrator/operator, optional presentation or is headless. Identify dashboard, menus, forms, queues, contextual actions, viewer/review, access/assurance and tenant control. Follow the host application's sidebar-to-capability-dashboard pattern, using `nuxt-layers-test/application-test-template` and Theme Manager as representative usage where appropriate.

Presentation consumes **public conceptual contracts**, never private tables; host owns navigation/integration; owner retains domain data. Document accessibility (WCAG 2.2 AA), i18n/localisation, responsive interaction and Theme Manager integration. If no GUI is justified, explicitly record that.

## Phase 7 — Independent architectural challenge

Challenge missing responsibilities, ownership conflicts, duplicated state, native operation gaps, inbound/outbound omissions, event/command/query semantics, failure/recovery, dependency cycles, isolation, external assumptions, authorisation, Audit/Logging/Reporting, jurisdiction, GUI gaps and unnecessary new capability boundaries. Confirm consumers could integrate without private implementation access. Raise true architectural alternatives for approval; investigate technical unknowns without asking for permission to do ordinary research.

## Phase 8 — Documentation update and decision discipline

Update `docs/capabilities/[ACTUAL_DIRECTORY]/capability-record.md`, retaining the existing pro-forma and prior accepted content. Include:

1. Capability identity, classification, status and cited evidence.
2. Purpose and independent justification.
3. Authoritative owned records, policy, decisions and exclusions.
4. Native service, information model, lifecycle and failure semantics.
5. **Idealised public inbound contracts** and validation/absence semantics.
6. **Idealised public outbound contracts** and consumers/authority.
7. Commands/queries/events or justified omissions.
8. Shared context, provenance, invariants and versioning.
9. Required/optional provider and infrastructure relationships.
10. Configuration, IAM, privacy/security/compliance.
11. Cross-capability inputs/outputs and reciprocal links.
12. Conceptual GUI/admin and headless mode.
13. Contract acceptance scenarios.
14. Established, approved, proposed and open decisions.
15. Deferred implementation/acceptance work and conceptual sign-off status.

Do not confuse the conceptual record with the implementation repository's actual root `CONTRACT.md`. Update relevant reciprocal records, catalogue, register, proposals, decisions and findings where the review warrants it. Keep commits on the original draft PR throughout.

## Phase 9 — Architectural consequences and parallel consistency

Assess effect on classifications, neighbouring contracts, catalogues, previous conceptual decisions, open reviews, governing ADRs and standards. Do not change `architecture-rules` without separate explicit authorisation. Identify newly overlapping PRs and whether they require reconciliation; preserve traceability and do not treat unmerged proposals as accepted. Update PR body with exact baselines, scope, public surfaces, decision status, changes, gaps and verification performed. Make PR ready-for-review when appropriate, preserving user approval and repository policy.

## Phase 10 — Mandatory pre-merge technical AND architectural validation

**Required after conceptual review and again when baseline materially changes before merge.** Compare against **current `master`**, not merely the initial SHA.

- **Git:** current head/base revisions, update requirement, merge conflicts, PR mergeability, protected-branch checks and CI status. Resolve conflicts preserving both approved lines of work.
- **Governing rules:** new accepted ADRs, normative changes, classification and contract obligations.
- **Cross-capability architecture:** newly merged/updated PRs, reciprocal findings, owner and source-of-truth collisions, incompatible public interfaces, cycles and misunderstood evidence.
- **Documents:** exact capability names and paths, relative links, catalogue/register, stable decision IDs, approval statuses, unintentional deletions and changed-file scope.
- **Acceptance:** confirm no unverified implementation/compliance claims, review notes and required checks. CI/user executes tests/builds; assistant does not run them.

Summarise outstanding concerns, checks, changes and readiness. **Obtain explicit owner approval before merge**. Immediately before merge recheck head/base revisions, mergeability, checks and branch policy; if base advanced, revalidate affected work. Use approved squash-only protected-master workflow. Confirm merged and closed status from GitHub; never assert success from a proposed merge.

A Git-clean PR can still violate the conceptual architecture: **both conflict types must be checked**.

## Phase 11 — Completion and handover

Report agreed purpose/classification, ownership, services, **inputs from cooperating capabilities and outputs supplied**, commands/queries/events, integrations, legal/security, GUI, approved and open decisions, updated files, PR/merge status and next alphabetical capability. Review is conceptually complete only if independently understandable, contract-coherent, consistent with accepted authority, with unresolved decisions explicit. Conceptual sign-off is not operational readiness.

## Parallel Capability Review rules (PCR-01–PCR-10)

| ID | Mandatory rule |
|---|---|
| **PCR-01** | Establish a dedicated branch and **draft PR immediately** after basic identity/baseline checks; use it throughout |
| **PCR-02** | Review current governing and blueprint authority before substantive design |
| **PCR-03** | Independently define capability ownership, native behaviour and mandatory public input/output contract |
| **PCR-04** | Document necessary reciprocal interfaces in adjacent records, including those under concurrent review |
| **PCR-05** | Clearly distinguish established evidence, owner-approved concepts, proposals, open questions and implementation |
| **PCR-06** | Preserve unique domain authority; prevent duplicated records and hidden private coupling |
| **PCR-07** | Allow justified shared catalogue/register/decision documentation changes |
| **PCR-08** | Detect and reconcile conflicting concurrent proposals instead of overwriting them |
| **PCR-09** | Check actual Git conflicts, current governing rules, architectural coherence, docs and CI before merge |
| **PCR-10** | Require explicit approval; check again immediately before the protected squash merge and verify it closed |

## Working constraints

Use live repository evidence, British English and established platform architecture. Read only related implementations' root `CONTRACT.md` unless authorised otherwise. The user/CI runs builds/tests. Do not introduce unnecessary technologies or duplicate capabilities. Do not create implementation repositories or change normative governance without approval. **Start each new review with Phase 0; keep the PR open until completion and explicit merge approval.**
