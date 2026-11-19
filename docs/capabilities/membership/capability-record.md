# Capability Record — Membership

**Capability:** `membership` (paid/scheme participation, **not** Identity group membership).  
**Classification:** Proposed **Domain capability**, pending owner approval; standalone repository/implementation not established.  
**Conceptual review:** 19 November 2026, draft PR #93; **no owner approval of MEM decisions yet**.  
**Opening governing authority:** `nuxt-layers/architecture-rules@b920ce0d8b361de000a6739a16123dbdc56df7a7`.  
**Opening blueprint baseline:** `nuxt-layers/architecture-blueprint-review@6dac83a03da8704f7945ee1bc894f2248300445a`.  
**Implementation:** Organisation repository search did not identify a dedicated `nuxt-layers/membership` repository. No published `membership/CONTRACT.md`, actual runtime endpoints, provider adapters, tests or working GUI are asserted.

## Status, purpose and classification

**Established governing distinction:** [Identity and Access](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/identity.md) gives Identity exclusive authority over identities, tenants, groups and direct group-membership lifecycle. [Capability Standard](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/capability-standard.md) requires cohesive independently justified responsibilities, owned state/outbox and public acyclic contracts. The governing [Catalogue](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/catalogue.md) lists paid/scheme `membership` as a *candidate*, not an implemented capability. Applicable accepted ADRs and normative security/privacy/presentation standards prevail over this working record.

**Proposed responsibility:** Membership operates voluntary or governed **participation in a named scheme**—for example a professional association, sports club programme, charitable supporter scheme or loyalty/benefits membership. It evaluates scheme-specific admission, terms acceptance, classifications, tenure, renewals, suspensions, termination and **benefit eligibility** with attributable effective times. This has an independent business lifecycle even when no purchase, app account, recurring payment or Identity group join occurs. It is therefore a defensible **Domain** boundary, but not automatically an independent package or Nuxt Layer.

**Primary consumers:** scheme administrators, scheme participants (including non-Identity external counterparties), authorised verifying services, Booking/Events/Pricing/Order/Subscription/Billing and Reporting. Scheme participation is **not** application authorisation or tenancy ownership.

**Evidence labels:** *Established* = accepted governing constraint or verified published interface; *agreed* = prior owner-approved principle in another record, not approval of MEM designs; *proposed* = current review recommendation; *open* = substantive owner choice; *unverified* = implementation/assurance evidence absent.

## Authoritative records and strict exclusions

| Membership owns — proposed | Remains authoritative elsewhere |
|---|---|
| Versioned scheme definition, scheme category/level, eligibility criteria and administrative effective dates | Identity's groups, hierarchy, principal status and **group-membership associations** |
| Participation application, evidence references, admission/decline and controlled appeal/review state | Verification's source attestations; Profile's personal attributes; Legal Compliance's statutory determination |
| Scheme-specific participant reference and approved binding to a business party or consented Identity link | Business-party/customer identity and contact details, Identity account, Authentication sessions |
| Accepted scheme terms/version, consent *reference* where relevant and participation period | Privacy's consent record/legal-basis rules, Publisher's terms text, legally binding contract determinations |
| Membership participation lifecycle, scheme renewal offers and participation state | Subscription's commercial plan subscription lifecycle and platform/seat feature entitlements |
| Benefit eligibility **under scheme rules**, use limits and benefit consumption ledger where indispensable | Pricing's tariffs/discount calculation; Booking's inventory/capacity; Order's sale; Billing's charges; Payment Gateway's money movement |
| Pro-rata membership *eligibility/period* consequences, not calculated charges | Billing's monetary proration, charge cycles and disputes; Invoice's legal documents; Accounting's ledger |
| Membership authoritative decisions, revisions and domain outbox | Audit's evidence custody, Logging's diagnostics, Message Queue's delivery, Reporting's aggregates |

**Key invariant:** Participation, an Identity group relationship, a Subscription entitlement, a payment receipt and a permission decision are **different facts**. No implicit conversion between them. A scheme may intentionally require an active Identity-group relationship, but Identity must independently execute its authorised lifecycle; Membership only requests or receives a result through a public contract. A failed or absent group change does not masquerade as success.

## Native service and lifecycle

**Scheme setup:** authorised administrators define scope (owning tenant/group/organiser), effective term rules, levels and eligibility, admission/review criteria, benefits, quotas, grace periods, renewal windows, cessation, data retention and published terms version. Changes are versioned; existing participants preserve agreed effective-policy history.

**Application and admission:** create a participant application from an authorised party reference or privacy-safe guest identifier; supply declared evidence/terms acknowledgement; check required attestations and capacity/eligibility constraints, require human decision when policy demands; accept, waitlist, decline or withdraw with reason and review rights. Do not silently make an external customer an Identity account.

**Participation states:** `applied → pending_review → approved_pending_effective → active → grace | suspended → active | ended | expired`; `applied/pending_review → rejected | withdrawn`; approved pending effective may return to review, be cancelled, or expire. **These are conceptual states**; any automatic transition needs an explicit configured policy, effective time, reason and evidence. Historical facts remain stable, corrections append superseding decisions.

**Renewal:** create an offer/renewal intent and retain consent or approval; distinguish requested renewal, legally accepted commitment, charge requested, invoice issued, payment settled and **new membership term effective**. Policy determines whether verified payment is a precondition; uncertain settlement means `pending` rather than automatic access. Grace, cancellation, cooling-off, backdating and refund consequences are explicit, never inferred.

**Benefit decisions:** answer scheme-based eligibility for a concrete benefit/action and effective time, with scope, level, available quota, qualifying membership version, policy provenance, reservation/consumption result and validity window. A positive membership-benefit result is **not** permission to access a resource, a final price, a booked seat, or evidence of physical fulfilment. Quota consumption must be idempotent and compensated/reconciled when Booking/Order fails.

**Recovery:** reject stale policy/version and mismatched beneficiary/tenant; retain recoverable pending external evidence and an operator review queue; on replays return the prior result; use source-owned transactional outbox for committed events, delayed/reordered delivery tolerance, reconciliation and explicit remediation. No exactly-once cross-system guarantee.

## Idealised public inbound contract

| Input source | Accepted facts, command or evidence | Validation, authority and absence handling |
|---|---|---|
| Authorised scheme administrator/application | Create/amend/suspend scheme; admission/renewal/termination decisions; effective policy, actor and reason | Trusted caller and server Authorisation, scheme owner and revision, MFA/approval for sensitive changes; deny or hold on uncertainty |
| Prospective participant/business-party authority | Apply, withdraw, acknowledge terms, request renewal, update eligible declared information | Verified or guest subject binding, consent/legitimate basis, anti-enumeration; unverified claims are not official identity/qualification proof |
| Identity / Profile | Optional principal/group reference, standing, scoped and consented attributes | Identity authoritative only for group membership/tenant; Profile for data disclosure; missing account permitted where scheme allows guests |
| Verification / evidence issuer | Signed/qualified eligibility attestations, expiry, revocation and provenance | Check trust, beneficiary binding, permitted purpose and freshness; unknown/revoked = pending/deny, never approved by self-assertion |
| Authorisation / Authentication | Trusted actor/session/assurance and resource-scoped allow/deny/unknown | Mandatory for protected operations; unauthorised requests never mutate the scheme |
| Configuration / Legal Compliance / Privacy / Clock | Tenant-configured scheme rules; qualified legal duties/holds; lawful processing/consent constraints; timezone and effective dates | Lawful floor overrides preferences; contradictory or stale mandatory policy blocks affected action; preserve exact rule version |
| Subscription / Billing / Payment Gateway / Invoice / Order | Subscription term references; assessed dues/charge/invoice/payment confirmations; purchase commitments | Consume each provider's *own* verified completed facts, not request acceptance as settlement; absent integration must have declared free/manual mode |
| Booking / Events / Pricing | Event/benefit scope, service eligibility, authoritative capacity outcomes and tariff revisions | Membership does not overrule availability or prices; unknown means no confirmed booking/discount |
| Integrations / external scheme registry | Permitted external issuer decisions and synchronised records with version, source and effective time | Explicit native/external authority mode, credentials via host/Integrations; stale/conflicting provider data held for reconciliation |

Inputs are public business contracts, **not invented TypeScript types or implementation endpoints**. Each carries only applicable tenant/scheme and subject references, caller/resource authority, correlation/idempotency, source/evidence version, effective time and decision status; no mandatory universal request object.

## Idealised public outbound contract

| Surface and consumers | Authority / permissible conclusion |
|---|---|
| Scheme catalogue and terms revision — application, Publisher, enrolment UI | Approved offered scheme/benefit definitions and effective policy; does not certify lawful terms in every jurisdiction |
| Participation application/renewal command result — applicant, administrator, Workflow | Accepted/rejected/pending with stable reference, policy revision and reason category; acceptance is not completion or billing settlement |
| Membership participation status query — scoped participant, scheme admin, permitted domain | Authoritative scheme state, effective term, approval provenance, freshness and certainty; no unrestricted Profile disclosure |
| Benefit eligibility decision and conditional consumption/reservation result — Pricing, Booking, Events, Order | Authoritative *scheme* benefit eligibility only, constraints, quota and version; downstream still checks its own authority and completion |
| Outstanding dues/renewal intentions — Billing/Subscription/Order | Attributable scheme obligations or commercial requests; **not** an invoice, final charge, recognised revenue or payment confirmation |
| Scheme participation lifecycle events — allowed subscribers through outbox/Message Queue | Committed `application-reviewed`, `participation-activated`, `renewal-pending/completed`, `level-changed`, `suspended`, `terminated`, `benefit-reserved/consumed/released` with version and replay identity; no right conferred by event delivery |
| Scoped export, history, policy and reconciliation — Audit, Reporting, Privacy, operator | Source history, correction lineage, authorised data-subject export and provider discrepancies; Audit retains separate custody |

**Queries** must define completeness, staleness, attribution and lawful audience. **Commands** declare validation, authorisation, idempotency and actual vs pending transitions. **Events** follow committed owner changes; consumers deduplicate and independently re-authorise, never treat transport as permission. Compatibility/versioning changes follow the public contract standard.

## Cross-capability relationships and dependency direction

| Neighbour / mode | Inbound to Membership | Membership returns / no authority transfer |
|---|---|---|
| **Identity**, conditional for linked account | Scope, principal/group/standing reference; separately reported group membership | Scheme status/requests only; never mutate Identity membership directly; guest scheme participation supported |
| **Authentication / Authorisation**, required for protected actions | Session assurance and scoped resource decision | Scheme-owned resource descriptor and required action; only Authorisation grants access |
| **Profile / business-parties**, conditional | Minimised personal or counterparty reference, lawful contact and verification | Scheme participation association; no duplicate personal/business record |
| **Subscription**, conditional | Its independent subscription term/entitlement state | Scheme enrolment/benefit intent; Subscription does not become the scheme's participation owner |
| **Pricing**, optional by commercial scheme | Price/discount policy and rate revisions | Validated member-benefit qualification; Pricing computes price |
| **Billing / Invoice / Payment Gateway**, conditional for paid scheme | Final charge, invoice and settlement/refund facts from respective owners | Authorised dues and term/request context; Membership does not charge or collect |
| **Order**, conditional | Customer acceptance/change/cancellation references | Scheme-level offer/benefit qualifications; no fictional order |
| **Booking / Events**, conditional | Capacity, reservation, attendance and lifecycle evidence | Member benefit qualification and quota decision; no booking or attendance record |
| **Verification**, conditional | Qualification/age or standing attestation | Eligibility decision only; no self-issued authoritative verification |
| **Configuration / Workflow / Clock / Scheduler**, conditional | Rule configuration, human decision result, temporal semantics and timer triggers | Scheme-policy facts, review tasks, renewal/expiry task intents; Scheduler does not own membership renewal |
| **Legal Compliance / Privacy**, required as applicable | Duties, constraints, consent/basis and holds | Domain source records and permitted processing status; no legal/compliance verdict |
| **Audit / Logging / Message Queue / Reporting / Integrations**, shared ports/optional consumers | Evidence custody, diagnostics, delivery and external registry coordination | Attributable membership decisions, own outbox, scoped reporting and provider discrepancy information |

**Cyclic coupling avoided:** one capability may consume another's published facts through host composition, but reciprocal updates are contracts/events, not paired mandatory package imports. No mandatory dependency on Billing, Subscription, Booking or a specific external provider: free/manual schemes remain viable. Mandatory policy, IAM and ownership checks fail closed where applicable.

## Configuration, security, privacy and provider modes

Scheme settings are validated, versioned and scoped to authorised tenant/group owners: eligibility/level definitions, dues model, admission, benefits and consumption, terms, renewal/grace, geographic applicability, notification templates, export/retention and provider authority. Differentiate law, organisational rule and participant preferences. Rights/fees are never derived from an untrusted client flag.

Enforce server-side ASVS 5.0 Level 2 baseline, stronger assurance for privileged admission overrides, financial-impact changes, unusual benefit issuance, identity linkage and mass exports. Deny cross-tenant and cross-scheme leakage, prevent ID enumeration, duplicate enrolment, benefit replay, forged payment webhooks, stale attestation and administrator self-dealing. Support separation of duties, review trails, anonymisation where law permits, protected correction, held records, erasure requests, least-purpose disclosure and data minimisation. WCAG 2.2 AA and locale-safe formatting apply to UI.

**Provider neutrality:** `native`, `external-authoritative` and carefully scoped `hybrid` are potential per-scheme modes; each must declare exactly who decides admission, renewal and status, trusted source revision, synchronisation latency, suspended/unknown states, conflict handling, import/export, migration, withdrawal and cost approval. Integrations owns transport/credentials, not programme decisions. Unavailable external authority blocks positive external-only membership/benefit assertions; imported replicas are marked derived and stale.

No jurisdiction-specific claim about UK consumer cancellation, charity/association obligations, regulated profession membership, VAT or cooling-off is made without qualified legal validation and effective-date evidence.

## GUI and host integration

**Optional separable GUI with headless core.** Host sidebar route to **Membership dashboard** (host owns navigation; no new magic auto-registration). Administrator views: scheme list/setup, level/benefit rules, applications/review queue, participant directory (privacy minimised), renewals/arrears, payment/provider discrepancy queue, benefit consumption and policy/history audit links. Participant views: available schemes, application/terms, participation card and expiry, renewal or cancellation requests, available benefits and privacy/export actions. External participants may use secured guest-link flows without forced Identity account creation. Sensitive actions require server authorisation and explicit confirmation; no direct private-database reads.

Display *requested*, *pending*, *active*, *grace*, *suspended*, *expired*, *cancelled*, *payment unknown* and *external stale* accurately, rather than a misleading single paid badge. Accessible keyboard/dialog/error focus, responsive forms, BCP 47/CLDR translations, date/zone precision and Theme Manager tokens; host composition uses published contracts and representative `nuxt-layers-test/application-test-template` only for future acceptance, not claimed running.

## Conceptual contract acceptance scenarios (not executed)

| Input → expected behaviour | Output / authority |
|---|---|
| Authorised free scheme, approved guest application → activate with terms and effective time | Participation active; Membership, no Identity group created |
| Identity group membership ended → separately re-evaluate any scheme policy that *requires* it | Membership remains separate; conditional benefit suspended as policy directs; Identity owns group fact |
| Paid renewal requested, Billing accepted charge request but settlement unknown → hold effective renewal | Pending renewal and uncertainty; Membership; Billing/Payment own respective facts |
| Confirmed settlement with scoped source and revision → apply approved term policy once | Versioned renewal activation; Membership |
| Same benefit redemption key replayed → no second quota decrement | Existing consumption outcome; Membership |
| Booking rejects capacity after benefit hold → release or reconcile quota, no imaginary reservation | Membership quota release, Booking denial |
| Wrong-tenant administrator, stale terms, forged provider message → reject/hold without partial acceptance | Stable deny/invalid/unknown reason; owner of each fact retained |
| Provider unavailable and authoritative externally → fail closed for new positive claims, show known historical state labelled stale | Pending reconciliation; Membership does not invent provider approval |
| Cancelled/backdated membership and legal retention hold → correct effective record, preserve lawful history, restrict access | Immutable supersession/hold lineage; Membership and Legal Compliance |
| Export subject participation → disclose authorised scheme facts only, no unrelated records | Redacted export with provenance; Membership/Privacy |
| App tries to convert scheme active into admin access or Identity group membership → refuse unsupported act | Explicit unsupported/denied; Authorisation/Identity retain authority |

## Architectural challenge, decisions and follow-up

- **MEM-01 — Classification (proposed):** retain an independent *scheme participation* Domain boundary, rather than collapse it into Identity or Subscription. Its own admission, terms, benefits and renewal state justify it; package and deployment decisions deferred.
- **MEM-02 — Scheme authority (proposed):** Membership owns programme participation and benefit qualification; Identity always owns group membership, Subscription commercial subscription rights and Authorisation access decisions.
- **MEM-03 — Participants (proposed):** allow non-Identity guests through verified, privacy-minimised party references; optional consensual Identity linkage never rewrites Identity/Profile.
- **MEM-04 — Commercial coupling (proposed):** free/manual scheme native mode; paid membership coordinates commercial owners' confirmed facts, with no fictitious charge, payment, invoice or order.
- **MEM-05 — Benefit consumption (proposed):** scheme-qualified benefits plus idempotent quotas, while Pricing/Booking/Events independently own their own outcomes and compensation.
- **MEM-06 — Renewal/cessation (proposed):** explicitly separate enrolment, billing, settlement, effective term, grace, pause, cancellation, expiry and legally governed refunds.
- **MEM-07 — External schemes (proposed):** provider-neutral native/external/hybrid authority with versioned reconciliation and fail-closed uncertainty.
- **MEM-08 — Contract and GUI (proposed):** public authorised commands/queries/outbox events and optional WCAG-compliant GUI, no private dependencies.
- **MEM-09 — Material open decision:** can one scheme have several independently liable participants/beneficiaries (family/corporate/team membership), and who may authorise transfer or delegation? Recommend **explicit scheme-specific participant and beneficiary relationship records with separate payer, legal party and qualifying individual**, no implicit Identity inheritance; owner approval requested.
- **MEM-10 — Material open decision:** is fee-conditioned activation required for *all* paid membership products, or configurable per jurisdiction/scheme? Recommend **per-scheme and legally constrained effective-state policy**, retaining separate entitlement, obligations and actual settlement evidence; owner approval requested.

**Technical investigation:** source verification contracts, minimum participant binding, external authority health/reconciliation SLAs, duplicate applicant detection respecting privacy, benefit counter consistency, historical rule effective-time semantics, statutory cancellation/cooling-off and tax scope, and provider selection. Resolve by source/contract evidence and legal specialists, not invented platform claims.

**Implementation alignment and acceptance (deferred):** publish independent root `CONTRACT.md` if a package is authorised; architecture-specific API/version model; host composition, stores/outbox, idempotency, provider adapter, threat model, storage register, consumer/UI acceptance and CI tests. This conceptual review does **not** establish implementation readiness or compliance certification. **All MEM-01–10 await owner disposition**; adjacent reviews remain independent.

## Prior preserved classification gate (17 November 2026)

### Classification gate — Paid/scheme Membership remains a candidate (17 November 2026)

**Status:** Retained for a future independent conceptual review, not confirmed implementation or standalone repository. Identity already owns **membership of an Identity group** and its lifecycle; this candidate concerns **scheme/commercial participation** such as enrolment, annual dues, paid benefits, eligibility, terms, renewals and entitlements (e.g. a club member's discounted tickets). Before sign-off, prove independently owned decisions and state not already supplied by Subscription, Billing, Order, Booking and Identity. A paid membership does not automatically grant Identity group membership or unrestricted access. Define its idealised public inputs/outputs, group/tenant scoping, external customer treatment, cancellations, pro-rating, legal policies and event behaviour in its scheduled review. Retain directory and candidate classification in this preservation PR.

