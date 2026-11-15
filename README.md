# Nuxt Layers — Architecture Blueprint Review

**Status:** Non-normative architectural design and review workspace.

The repository develops proposed capability descriptions, registers findings and decisions, and preserves evidence for changes that may later be proposed to the governing architecture. It is not an implementation repository or a source of normative architectural authority.

**Governing authority:** [`nuxt-layers/architecture-rules`](https://github.com/nuxt-layers/architecture-rules), its accepted ADRs and normative standards. Verify its current `master` before making or promoting a proposal.

## Repository structure

| Directory | Responsibility | Documents |
|---|---|---|
| [`docs/`](docs/) | Working architectural documents being developed for review | [Capability Catalogue](docs/capability-catalogue.md) and [Capability Register](docs/capability-register.md) |
| [`proposals/`](proposals/) | Unaccepted design specifications and proposed architecture changes | [Register design](proposals/capability-register-design.md), membership governance and performance/rendering |
| [`reviews/`](reviews/) | Investigations, sources, comparisons, alternatives and acceptance scenarios | Capability discovery, IAM, integrations, execution, commerce and rationalisation reviews |
| [`records/`](records/) | Consolidated review history and traceable decisions | [Decisions](records/decisions.md) and [Findings](records/findings.md) |

The **working catalogue** describes what capabilities and other architectural building blocks could or should exist. It began as a copy of the governing catalogue and is expressly **not** a replacement for it.

The **working register** is an index of those catalogue entries, their classifications and evidence status. It does not infer implementation readiness from an architectural entry or create a runtime registry. Its proposed design and application discovery principles belong in [`proposals/capability-register-design.md`](proposals/capability-register-design.md).

The historical [decisions](records/decisions.md) and [findings](records/findings.md) records are deliberately retained as accumulated review evidence, not accepted ADRs. Detailed reasoning belongs with its [review](reviews/) or [proposal](proposals/).

## Review and adoption process

1. Confirm the current governing revision and the accepted ADRs and normative standards.
2. Consult other repositories **only through their public root `CONTRACT.md`**, unless wider inspection is expressly authorised.
3. Record verified evidence in a review; distinguish findings, alternatives, proposals, approval for further review and formally adopted decisions.
4. Develop working architectural changes under `docs/` and record consequences, dependencies, security/privacy effects, affected consumers and any proposed ADR/standard amendments.
5. Treat a blueprint PR as **review approval only**. A proposed change becomes normative only through the appropriate independently reviewed and accepted PR in `architecture-rules`.
6. After governing adoption, reconcile both the working documents and review records against the latest accepted source without silently discarding upstream changes.

**Existing governing requirements remain in force throughout review**, including ADR-0012's single-call composition/50-line host budget and ADR-0016's directional, jointly acyclic contract and Nuxt extension dependencies, unless properly amended.

## Conceptual presentation review (non-normative working method)

Every capability's alphabetical **conceptual review** should describe its likely user interfaces **where applicable**, without prescribing implementation technologies, page source files or a separate UI package. Record: intended audiences and permissions; core headless versus optional separable presentation; likely dashboard, list/detail, create/edit, approval, review, reporting and settings screens; navigation entry and host ownership; conceptual user journeys; disclosure, failure, empty and degraded states; relevant Theme Manager/`ui` vocabulary, accessibility and internationalisation; presentation-off mode; and conceptual acceptance scenarios. Record **not applicable** where a stateless library, infrastructure integration library or genuinely headless service has no standard screens.

The current representative consumer pattern is **`nuxt-layers-test/application-test-template`**: the host-owned responsive sidebar's Capabilities section links to an enabled capability dashboard inside the shared application shell, as the Theme Manager link illustrates. The host may also provide a card on its administration/test dashboard. This is an explicit local testing/navigation pattern, **not** an accepted universal automatic menu-registration API, production authentication boundary or obligation to make every capability a Nuxt Layer. Consult the template beyond its root contract only when the applicable review explicitly authorises broader inspection.

Accepted ADR-0009 continues to govern: core services are independent of presentation; optional capability screens are audience-specific, separable and themed through Theme Manager's semantic vocabulary; navigation, routing, branding and trusted caller/context are host-owned. Access control remains server-side. Keep implementation layout, detailed screen composition and actual UI tests for subsequent design and delivery. A conceptual screen inventory does **not** authorise edits to the application-test-template repository.

## Documentation maintenance

Prefer small, purposeful changes. Preserve source provenance and historical review evidence, repair relative links on moves, and avoid introducing a new repository, capability, manifest or runtime service just to organise documentation.
