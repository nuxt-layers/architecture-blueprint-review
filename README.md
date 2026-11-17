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
3. **Apply the [classification and ownership gate](reviews/capability-classification-gate.md)** before assuming an entry owns records or needs persistence, screens, a repository or a Nuxt Layer. Record alternatives and the recommended disposition.
4. Record verified evidence in a review; distinguish findings, alternatives, proposals, approval for further review and formally adopted decisions.
5. Develop working architectural changes under `docs/` and record consequences, dependencies, security/privacy effects, affected consumers and any proposed ADR/standard amendments.
6. Treat a blueprint PR as **review approval only**. A proposed change becomes normative only through the appropriate independently reviewed and accepted PR in `architecture-rules`.
7. After governing adoption, reconcile both the working documents and review records against the latest accepted source without silently discarding upstream changes.

**Existing governing requirements remain in force throughout review**, including ADR-0012's single-call composition/50-line host budget and ADR-0016's directional, jointly acyclic contract and Nuxt extension dependencies, unless properly amended.

## Classification-first capability review (non-normative working method)

**Mandatory first substantive review gate:** Before prescribing a database, business record, independently deployed service, Nuxt Layer or UI screen for a catalogue entry, determine its **actual responsibility and implementation kind**. Follow the reusable [Capability Classification and Ownership Gate](reviews/capability-classification-gate.md); the earlier [Catalogue Rationalisation Review](reviews/catalogue-rationalisation-dependencies.md) remains relevant evidence.

This is a **review method, not a new governing architecture rule**. Existing `architecture-rules` standards already distinguish Foundation/Platform/Domain/**Presentation** responsibility classes from implementation kinds (independent capability, presentation, composition, stateless library, infrastructure integration or connector) and allow stateful capabilities to own their stores **where necessary**. Catalogue presence alone does not prove business-state ownership or the need for a database, repository or Nuxt Layer.

For each alphabetical entry, record: distinct owned decisions/records/lifecycle **or none**; canonical neighbouring owners; presentation, archetype, composition or library alternatives; minimal justified business/operational/derived/preferences persistence **or none**; proposed classification and implementation form; idealised public inbound/outbound interfaces and absence behaviour; suitable GUI/navigation requirements **or explicitly not applicable**; and an explicit **retain, presentation-only, reclassify, consolidate or defer** recommendation. Mark owner approvals and verified root `CONTRACT.md` evidence separately. Do not reclassify accepted governing records or create new packages through a blueprint PR alone.

Presentation-led dashboards may aggregate source capabilities through public contracts and maintain transient view state without acquiring those capabilities' business records. Reporting may own its report definitions/results without becoming the owner of originating transactions; orchestrators may own execution/checkpoint state without owning domain outcomes. The later dedicated presentation review still applies according to the classification result.

## Conceptual presentation review (non-normative working method)

Every capability's alphabetical **conceptual review** should describe its likely user interfaces **where applicable**, without prescribing implementation technologies, page source files or a separate UI package. Record: intended audiences and permissions; core headless versus optional separable presentation; likely dashboard, list/detail, create/edit, approval, review, reporting and settings screens; navigation entry and host ownership; conceptual user journeys; disclosure, failure, empty and degraded states; relevant Theme Manager/`ui` vocabulary, accessibility and internationalisation; presentation-off mode; and conceptual acceptance scenarios. Record **not applicable** where a stateless library, infrastructure integration library or genuinely headless service has no standard screens.

The current representative consumer pattern is **`nuxt-layers-test/application-test-template`**: the host-owned responsive sidebar's Capabilities section links to an enabled capability dashboard inside the shared application shell, as the Theme Manager link illustrates. The host may also provide a card on its administration/test dashboard. This is an explicit local testing/navigation pattern, **not** an accepted universal automatic menu-registration API, production authentication boundary or obligation to make every capability a Nuxt Layer. Consult the template beyond its root contract only when the applicable review explicitly authorises broader inspection.

Accepted ADR-0009 continues to govern: core services are independent of presentation; optional capability screens are audience-specific, separable and themed through Theme Manager's semantic vocabulary; navigation, routing, branding and trusted caller/context are host-owned. Access control remains server-side. Keep implementation layout, detailed screen composition and actual UI tests for subsequent design and delivery. A conceptual screen inventory does **not** authorise edits to the application-test-template repository.

## Documentation maintenance

Prefer small, purposeful changes. Preserve source provenance and historical review evidence, repair relative links on moves, and avoid introducing a new repository, capability, manifest or runtime service just to organise documentation.


## Current cross-capability proposals — tenancy, policies and platform commerce (16 November 2026)

Review the [organisational tenancy and governance proposal](proposals/organisational-tenancy-and-governance.md), [commercial onboarding and entitlements](proposals/commercial-onboarding-and-entitlements.md), [policy and governance boundaries](proposals/policy-and-governance-boundaries.md) and [ownership/recovery review](reviews/organisational-ownership-and-recovery.md). These are blueprint evidence and proposed public contracts, not accepted governing changes or implemented capabilities. ORG-01–ORG-08 have owner conceptual approval; others need explicit governing reconciliation. The `business` archetype remains in the catalogue/register but its redundant capability directory is removed after transferring its sole Billing note.

## Node–Hub federation conceptual review (17 November 2026)

The [Node–Hub architecture review](reviews/node-hub-federation-architecture.md) records the owner-approved conceptual direction: an autonomous **Node** is an installation/network participant; optional **Federation** is a candidate Platform capability for cross-node publication and synchronisation; a **Hub** is an application composition/operating role that uses Federation, Search and relevant governance services. Any suitably configured Node may operate Hub services; every Hub operates as a Node, but ordinary Nodes need not use Hubs. [Federation's capability record](docs/capabilities/federation/capability-record.md) documents conceptual ownership, public inputs/outputs, peer contracts, dependencies, presentation, risks and open decisions. The [working catalogue](docs/capability-catalogue.md) and [register](docs/capability-register.md) carry the provisional classifications. No normative adoption, implementation repository or runtime is implied.

## Online Safety and Content Governance (17 November 2026)

The [cross-capability conceptual review](reviews/online-safety-content-governance.md) records the owner-approved proposed model for UK Online Safety Act-aware content and conduct safeguards across publishing, media, comments, commerce and Hub federation. The new [Moderation candidate record](docs/capabilities/moderation/capability-record.md) and requested [capability-report.md pro-forma](docs/capabilities/moderation/capability-report.md) preserve the full future-review notes and proposed logical input/output contracts. Reciprocal notes appear in affected capability records. The working [catalogue](docs/capability-catalogue.md), [register](docs/capability-register.md), [decisions](records/decisions.md) and [findings](records/findings.md) index this review. No runtime work, independent compliance certification, vendor commitment or normative ADR amendment is implied.

## Identity, Age and Eligibility Assurance (17 November 2026)

The owner-approved [cross-capability conceptual review](reviews/identity-age-eligibility-assurance.md) distinguishes identity proofing, privacy-preserving age assurance, authentication, verified organisational representation and domain-specific eligibility. It documents proposed public interfaces, local/federated trust, evidence ownership, provider integrations and operational safeguards. Reciprocal notes are recorded in Identity, Authentication, Authorisation, Marketplace, Legal Compliance, Integrations, Federation, Moderation, Publisher and Audit. **No new verification capability, provider or normative ADR is approved.**
