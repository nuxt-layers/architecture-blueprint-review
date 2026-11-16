# Organisational tenancy, digital control and accountable governance

**Status:** Blueprint conceptual proposal; not an accepted ADR, implementation contract or authorisation for engineering. **Owner-approved:** ORG-01–ORG-08 (16 November 2026). Other TEN/OWN principles are supported in discussion but require explicit decision-by-decision adoption and governing reconciliation.

**Evidence baselines:** governing `architecture-rules/master` `2eea557fa3acbf9412fea065d2a3cdda42a764fc`; blueprint `master` `442b3018c580562cac7cb513dbee9e7ad5d9a707`. See [policy boundaries](policy-and-governance-boundaries.md), [commercial onboarding](commercial-onboarding-and-entitlements.md) and [ownership/recovery threat review](../reviews/organisational-ownership-and-recovery.md).

## Terms and ownership

- **Installation/host:** composed application, operator infrastructure, provisioning authority and routes. Not itself an Identity tenant.
- **Tenant:** Identity-owned security/data-isolation scope. It is not an Identity group, legal person, commercial account or application deployment. Isolation is enforced even on shared infrastructure.
- **Group/organisation:** Identity-owned group context and memberships; legal entity or operational activity represented by the group is owned by the appropriate domain. An organisation need not equal a tenant.
- **Archetype:** validated description of group purpose (company, business, club, council, committee), permitted metadata, selectable capability composition, proposed role profiles and non-authoritative relationships. Distinct `organisation-model` ownership requires separate lifecycle proof; do not fabricate one.
- **Creator:** provenance of original act, not irrevocable authority or ownership of resulting records.
- **Digital owner:** verified human exercising governed tenant/group digital control; not synonymous with shareholder, director, creator, administrator or payer.
- **Controlling real-world party:** person or legal organisation with legitimate authority over digital representation and assets, established from independently verified governing instruments, applicable law and contracts. Legal authority must not be inferred from a director/shareholder title alone.
- **Administrator:** explicitly delegated, scoped and revocable operation permissions; can be a contractor.
- **Subscriber/bill-to party:** independently authorised payer under commercial agreement. Tenant parentage and digital ownership do not make that party automatically responsible for payment.

**Accepted baseline:** `architecture-rules/docs/identity.md` and ADR-0003 make Identity authoritative for tenants, opaque identities, groups, single-parent **group** hierarchy and memberships; Authorisation evaluates actor/action/resource/context; no access or membership follows from group parentage. This proposal does **not** treat a group hierarchy as an accepted tenant hierarchy.

## ORG decisions — owner approved

| ID | Agreed conceptual direction | Boundary / remaining work |
|---|---|---|
| ORG-01 | Free personal registration and policy-governed self-service organisation requests | Identity privileged tenant/root-group provisioning is presently operator-only; build a controlled host-facing process rather than exposing migration credentials |
| ORG-02 | Tenant and organisation are distinct; creation into new or appropriately authorised existing tenant | No automatic tenant-per-group requirement; exact allocation and billing policies remain to design |
| ORG-03 | Identity owns digital group/tenant governance; legal ownership and statutory offices are distinct | Independently evidence real-world controller; no title-based automatic takeover |
| ORG-04 | Validated organisational archetypes and configurable feature compositions | Do not add a new `organisation-model` store/repository without independent lifecycle evidence |
| ORG-05 | Explicit typed cross-organisation relations; no second Identity group parent | No implied access via relationships |
| ORG-06 | Employees, customers, contractors, paid members and external invitees are different relationships | Customer is not automatically an Identity member or billable workforce seat |
| ORG-07 | One authenticated person may switch among many authorised organisational contexts | Server resolves tenant/group/subject and repeats access checks; selector alone cannot grant access |
| ORG-08 | Office appointments, chairperson status and term-specific governance may require independently governed facts | Identity membership is not statutory office, authorised approver status or a recorded vote |

## Tenant hierarchy proposal (NOT currently accepted or implemented)

- **TEN-01/02:** tenant is isolation boundary, distinct from group; person may have memberships in multiple authorised tenants.
- **TEN-03:** propose zero-or-one direct parent tenant per tenant, acyclic, with independently persisted identity/governance relationship. Do not conflate with the accepted group forest.
- **TEN-04:** parent may receive expressly scoped, reviewable administrative delegation; **never** automatic read access to child customers, finances, personal data or owner-only resources. Platform operator as provisioning parent gets no blanket client-data permissions.
- **TEN-05:** active tenant requires at least one verified accountable human digital owner; shared owners and controlled succession/transfer; if last owner becomes unreachable, enter restricted recovery state, not fabricated ownership. AI may assist but cannot satisfy human ownership baseline.
- **TEN-06:** real-world controller, director, shareholder, digital owner, creator, administrator and subscription payer remain separate, attributable references.
- **TEN-07/08:** operator has its own organisational tenant for selling services; installation/bootstrap sets up a verified founding human platform administrator and host business without ordinary permanently unrestricted 'god-user' privileges. Infrastructure, platform, tenant and business access remain separate.

Tenant hierarchy, last-owner rule, bootstrap and recovery need a **separately accepted governing amendment**; current Identity root `CONTRACT.md` only documents operator-only provisioning and group-owner safeguards. Avoid silently assigning cross-tenant powers.

## Digital ownership and anti-lock-in (OWN-01–OWN-05, proposed)

1. Record separately creator provenance, digital owner, delegated administrator, real-world controlling authority and commercial payer.
2. Share, transfer, revoke and recover digital ownership with attributable decisions, human standing, applicable policy versions and independent protections.
3. Never give service providers or contractors irrevocable digital control because they created or configured accounts; avoid creator-as-owner permanence.
4. A company's legitimate authority can seek independent, evidence-based recovery after hostile administrator lockout, without allowing a fraudulent claimant to seize it. Include dispute/hold and independently reviewed restoration.
5. Support authorised portable export of source-owned business data, documents, configuration and relevant history; subject to privacy, ownership, legal hold and retention. No contractor veto.

**Risk controls:** verify real-world control without automatically interpreting corporate law; step-up, independent approvers, cooling-off/notices, dual control and appeals where appropriate. No single administrator can edit policy and immediately use weakened policy to transfer ownership. Require effective dates, prior version and audit evidence. Legal ambiguity suspends contested privileged changes, not normal read access where authorised.

## Illustrative conceptual public interfaces

| Source / command or fact | Target | Result / authority / failure |
|---|---|---|
| Verified person, standing, assurance and scoped creation request | Host onboarding → Identity | Pending/provisioned tenant and founding group references; no request-browser access to privileged provisioning, fail closed on unverified actor |
| Governing authority evidence and approved succession decision | Appropriate legal/governance owner → Identity | Protected owner-change command and Identity-owned owner state; contested evidence -> held/review |
| Explicit parent-child proposal, parent approval and scope | Identity + Authorisation | Versioned relationship, scoped administration grants; reject cycles and implicit data permissions |
| Group membership/role facts and selected tenant | Identity → Authorisation/host | Server-authorised context and permitted navigation; absent membership is not automatic denial of a genuinely independent grant, and context switch is never a grant |
| Approved organisation archetype/feature choices | Configuration or validated archetype owner → host | Enabled services and menus only after subscription entitlement and server access; version/provenance retained |
| Domain resource owner, historical business data | Booking/Asset/Accounting/etc. → authorised UI/export | Source remains authoritative; group creator departure does not relocate ownership |
| Domain ownership/lifecycle changes and governance actions | Identity/domain owners → Audit/Reporting/Notifications | Attributable proof, risk-based capture and permitted disclosure; no duplicate source-of-truth |

Events are authoritative facts only from owning capability, with durable delivery and retry/deduplication as applicable. No conceptual relationship authorises cyclic package imports. Public surface names and implementation APIs remain deferred.

## GUI journeys

Host account/context switcher lists authorised owned/managed/member contexts with role-specific links and freshness. Tenant administrators have governance/owners, delegation, subscription, quota, invitations, pending approvals, evidence and export screens. Other roles only see permitted views. Show pending, unavailable, disputed, orphaned, partially provisioned and revoked states clearly. Host owns sidebar/routes and branding; specialist capability presentation is separable. All protected writes and disclosures are server-authorised; support WCAG 2.2 AA and i18n.

## Acceptance cases

1. One person creates three businesses with separately scoped tenant/service records and joins a club/council/committee without merging identities.
2. Parent tenant administers an explicitly delegated child without viewing child private resources by default.
3. Former director or external contractor loses delegated access and cannot block independently verified owner recovery or export.
4. Solo owner's unexpected loss triggers restricted reviewed recovery, never arbitrary new ownership or deletion.
5. Council chair appointment and committee membership do not implicitly convey authority to spend or access confidential information.
6. Changing payment party leaves group/tenant data and legitimate governance ownership intact.
7. Replayed provisioning/ownership events never create duplicates or declare uncertain outcomes confirmed.

## Governing amendment candidates / open decisions

- ADR-0003 and `docs/identity.md`: proposed tenant parentage vs existing *group-only* single-parent hierarchy; human tenant-owner floor and orphan/recovery semantics.
- ADR-0005 IAM suite and `docs/capability-standard.md`: scope/ports and owner verification, independent delegation/assurance, bootstrap obligations.
- ADR-0012 shared caller/access shapes and 50-line host composition: new provisioning port must not bypass security or burden host with business logic.
- ADR-0016: preserve directional acyclic contract/Nuxt dependency graph despite reciprocal conceptual flows.
- Security/Privacy/Legal Compliance: evidence processing, purpose, retention, access and appeal constraints.
- Still open: where legal-entity verification and contractual party master live; whether `organisation-model` owns any independently versioned lifecycle; pricing/tenancy allocation and recovery operating policy.

No governing changes or implementation are approved by this blueprint PR.
