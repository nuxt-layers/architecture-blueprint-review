# Capability Record — Booking

**Capability:** `booking` — **proposed Domain capability**, candidate for independent business responsibility; no implementation repository or released service verified.
**Review:** 15 November 2026; conceptual recommendations **proposed for project-owner approval**, not signed off.
**Governing baseline:** `nuxt-layers/architecture-rules` `master` at `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.
**Blueprint baseline:** `nuxt-layers/architecture-blueprint-review` `master` at `3cf22433209c1cb1d9376099a9607741911a258a`.
**Representative template:** `nuxt-layers-test/application-test-template` `master` at `8b7b142b84b5ec2379d4e2e727914fe344187d64`; no runtime acceptance performed.
**Implementation evidence:** Direct lookup of `nuxt-layers/booking` returned 404, and organisation repository search returned no matching repository. No default branch, root `CONTRACT.md`, implemented interfaces or screens can be verified. This does not prove that no other package includes related functionality.

## Architectural authority and evidence

**Established:** [Platform Charter](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/platform-charter.md), [Capability Standard](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/capability-standard.md), [Catalogue](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/catalogue.md), [Security](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/security.md), [Privacy](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/privacy.md) and accepted ADR-0001/0002/0006/0008/0009/0012/0014/0015/0016 govern responsibility, source-owned persistence and outboxes, server-authorised access, provider neutrality, independent public contracts, optional presentation and one-call/50-line Nuxt composition. All sixteen current ADR files are accepted; their current amendments, not unmerged blueprint ideas, govern. The governing catalogue defines Booking as a **Domain candidate**: “Reservation lifecycle, availability and capacity for resources; neither a clock nor execution scheduler.”

**Existing blueprint evidence:** [Asset](../asset/capability-record.md) already distinguishes asset eligibility, custody and condition from Booking time-slot reservation. [Billing](../billing/capability-record.md) expects booking and service-delivery evidence for commercial charging, but does not inherit Booking lifecycle ownership. [Authorisation](../authorisation/capability-record.md) owns resource-aware access decisions; [Audit](../audit/capability-record.md) holds evidential custody; [Logging](../logging/capability-record.md) diagnoses operations. The [classification gate](../../../reviews/capability-classification-gate.md) forbids inferring separate repositories or persistence from catalogue names. Related records remain non-normative and may themselves be incomplete.

**Status meanings:** **Established** = accepted governing requirement or verified public contract; **Proposed** = recommendation here; **Open** = material architectural choice requiring approval; **Unverified** = runtime/provider behaviour with no independent evidence.

## Architectural classification and ownership gate

| Gate | Finding |
|---|---|
| Distinct responsibility | **Proposed:** coordinate a bounded, time-specific claim against explicitly offered resource capacity and manage that claim's authoritative reservation lifecycle. |
| Authority | Booking owns its reservation intent, holds, confirmations, allocation ledger and release decisions within its declared booking scope; it does **not** own whether a physical asset is safe, commercially priced or lawfully usable. |
| Alternatives | A calendar UI is Presentation only; a scheduler executes future work; an Asset assignment is custody; an Inventory reservation is stock commitment; an Order records commercial acceptance. None independently expresses the general reservation lifecycle across appointments, rooms, equipment, services, seats and capacity pools. |
| Classification | **Retain as proposed Domain capability**; a separate repository, Nuxt Layer and deployment are not yet authorised. |
| Persistence | **Proposed business state:** durable reservation and hold records, capacity commitments, rule/version references, cancellation/amendment lineage, deduplication, reconciliation and source-owned outbox. Derived availability search results need not be authoritative or persisted. |
| Public boundary | Narrow server-authorised commands, availability/booking queries, owned domain events and optional capacity-eligibility/commitment ports. No access to neighbours' private stores. |
| GUI | Optional separable capability-facing management screens over a headless core; host owns navigation, routing and branding. No assumed universal menu-registration API. |
| Disposition | **Proposed: retain**, pending owner approval of the material decisions BK-01–BK-05 below. No implementation or operational availability is implied. |

## Purpose, consumers and exclusions

**Proposed conceptual definition:** Booking accepts authorised requests to reserve finite availability for a specified interval, unit or session; evaluates its own reservability rules against current authoritative availability/constraints; prevents incompatible claims in a single defined capacity authority scope; manages temporary holds, confirmation, amendments, expiry, cancellation, no-shows and completion; and publishes attributable outcomes to consumers. Reservation is not guaranteed fulfilment.

Typical consumers are service operators, customers, staff, appointment systems, venue/facility managers, event organisers, rental applications, asset custodians, Billing, Order, Reporting and approved external booking providers. The same public vocabulary should accommodate a single resource, a fungible capacity pool, a named service slot or a configured multi-resource requirement without presuming all examples have identical policies.

| Booking owns (proposed) | Explicitly remains elsewhere |
|---|---|
| Reservable offering's **booking rules**, reservation windows, hold policy, lead/cut-off time, booking quotas and booking-side capacity commitments | Asset owns physical asset master data, use eligibility, condition, custody and maintenance; Location owns location facts where applicable |
| Reservation identity, requester/beneficiary references, party/quantity requirements, time interval, hold token and its expiry, booking/hold/amendment/cancellation lifecycle | Identity/Profile own person identifiers and personal information; Authentication establishes principal; Authorisation decides permissions |
| Booking-side capacity ledger and conflict-free reservation arbitration **only when Booking is the selected capacity authority** | Inventory owns stock quantities and stock reservations; Events owns event programme/sessions if separate; resource owners own fundamental capability, safety and eligibility constraints |
| Booking-originated availability projection from accepted capacity supply, blackouts and confirmed commitments, with freshness/completeness | Clock owns time-zone/date-time semantics, Scheduler due triggers, Workflow approvals; no duplicate clock/calendar or general-purpose executor |
| Booking rules applied to reservation changes, waiting lists where enabled, attendance/no-show/service status evidence when Booking is designated source | Order owns sales contracts and commercial acceptance, Pricing tariffs, Billing charge assessment, Invoice legal invoices, Payment Gateway funds, Accounting postings |
| Reservation provenance, locally authoritative state, idempotency, provider mapping/reconciliation for Booking's authority scope, outbox/domain events | Integrations owns connector transport/connection credentials; MQ delivery; Audit evidence custody; Logging technical diagnostics; Notifications message delivery |

**Important stock distinction:** a customer's request for ten saleable units is **not** a Booking capacity commitment when Inventory already owns those units' reservations. Likewise, Booking cannot mark a room safe while Asset reports a restriction or treat a payment authorisation as a booking confirmation without satisfying the booking and payment policies.

## Native functionality and information lifecycle

**Proposed self-sufficient services:** register/book a reservable offering against an authoritative resource reference and approved policy; publish availability windows/remaining booking capacity with clear freshness; validate requester eligibility, blackout and lead/cut-off constraints; hold an amount of capacity for bounded time; confirm, amend, reschedule, cancel or expire without overselling the same committed pool; optionally manage waiting-list offers; record attendance/no-show/check-in and completion *only to the degree this is a Booking-owned service outcome*; report operational exceptions and reconcile uncertain operations; provide authorised history/export and a replay-safe event/outbox mechanism. Native operation must work without a marketplace, provider, Scheduler or commercial/payment integration.

**Conceptual record groups:** `ReservableOffering` (offering ID, authoritative resource/owner references, capacity unit and rules/version); `CapacitySupply` (effective availability, eligible limit and source-version provenance); `Reservation` (stable ID, tenant, authorised requester/beneficiary references, interval/session and zone, quantity, status, revisions and lineage); `Hold` (bounded unconfirmed commitment, expiry, fencing/attempt identity); `Allocation` (Booking-owned capacity commitment against pool and interval); `ProviderAuthorityMapping` (explicit authority scope, external identity, revision/sync checkpoint); `BookingOutcomeEvidence` (source-attested check-in/no-show/service status, with authority and privacy); `BookingPolicyReference` (effective policy and change version).

**State model (proposed):** request evaluated → rejected, waitlisted or **held** → confirmation attempted → **confirmed** or pending external confirmation / expired / rejected. Confirmed → amended or rescheduled (with explicitly linked old/new commitments), cancelled, no-show or completed. Failed provision, disputed provider results and inconsistent capacity move into **exception/reconciliation required**, never silently into confirmed. An amendment retains lineage and does not transiently oversell; a hold expiring does not automatically cancel an already verified confirmation. Status can be projected from canonical state but not rewritten retroactively. Final booking state is not necessarily service-delivery, commercial or financial finality.

**Capacity concurrency:** all competing claims sharing a capacity-authority scope must be arbitrated against one authoritative commitment boundary. A read-only availability search is never a lock. Hold/confirm/release are concurrency-safe, repeatable and version/authority-checked, including overlap/partial-capacity cases; capacity cannot become negative or be overcommitted by races. For externally authoritative scopes, confirmation depends on verified provider acknowledgement rather than a locally invented capacity guarantee. Absence of required eligibility or occupancy facts yields unavailable/held/rejected, not speculative confirmation.

**Time:** Booking carries precise instants, local advertised wall-clock times, zone and interval boundary convention; Clock provides interpretation, DST gap/overlap validation and formatting. Capacity interval overlap and duration limits are Booking rules; Scheduler executes optional timed handlers. A reminder delivery is not a state transition.

## Idealised conceptual public input interfaces

The following are **proposed logical interfaces**, not actual module names, endpoint routes or implementation contracts.

| Source / input class | Information / command and purpose | Ownership, validation, requirement and failure |
|---|---|---|
| Authenticated actor / application — **command** | Create offering (if authorised), search and request reservation, hold, confirm, amend, cancel, check in, mark no-show, complete, resolve exception; request idempotency, quantity and time range | Authentication/Identity/Authorisation own actor facts and access decision; Booking validates booking policy and current source revision. **Essential**; deny invalid, unauthorised or cross-tenant commands without mutation |
| Configuration / tenant operator — **policy context** | Effective booking windows, slot length, capacity presentation, cancellation/hold/waitlist rules, visibility, auto-confirmation, provider selection, retention | Configuration owns setting lifecycle/provenance; Booking owns validation and applying domain invariants. **Essential policy**, safe documented defaults only where permitted; contradictory/missing mandatory values fail closed |
| Resource/capacity authority — **source facts** | Resource or capacity-pool ID, offered capacity, eligibility, availability/blackouts, constraints, revision, effective periods, invalidation/withdrawal | Asset/Events/Location/service owner or another explicitly delegated source owns resource facts. **Essential for relevant resource types**; stale, missing or revoked information prevents new firm confirmation |
| Asset / Inventory / service fulfilment — **conditional commands/evidence** | Checked external commitment/release or assigned resource reference, safety/licence limits, stock reservation result, delivery/attendance attestations | Originating domain remains authority; Booking must not manufacture external stock/custody or service completion. **Conditional**; compensation/reconciliation on partial or uncertain outcome, with no duplicate allocation |
| Clock — **time context** | Valid time-zone/instant conversion, temporal ambiguity validation and display semantics | Clock owns temporal interpretation; Booking owns slot policies. **Essential reliable semantics**; invalid local times or ambiguous unqualified requests are rejected/clarified |
| Pricing, Order, Subscription, Membership — **commercial/eligibility facts** | Offer/contract reference, entitlement and permitted party size or access, cancellation terms, commercial approval | Source domain owns price, contract, entitlements. **Conditional**; missing necessary commercial/eligibility permission blocks confirmation, while free native bookings need none |
| Payment Gateway / Billing — **conditional result** | Deposit/payment authorised or settled, charge assessment, reversal/refund status, payment expiry | Payment Gateway owns payment execution; Billing charges. **Conditional** when rule requires deposit/prepayment; pending payment cannot be presented as confirmed under pay-first policy |
| Scheduler / Workflow — **operational trigger or approval** | Expiry attempt, reminder/check-in timing, manual approval outcome, versioned decision | Booking revalidates current state, actor and due condition; receiving a trigger/event is not authority. **Optional/conditional**; time-based validity must also be enforced natively on reads/writes |
| Integrations / external provider — **external evidence** | Provider authority/identity, authoritative hold, confirm, modify, cancel, availability snapshot, webhooks, version/checkpoints and verified source | Provider owns external state in connected-authority mode; Integrations owns connection/webhook trust. **Optional**; unavailable/contradictory responses remain pending/uncertain for reconciliation |
| Legal Compliance / Privacy / Authorisation — **constraints** | Applicable legal restrictions, consent/disclosure/retention, tenant scope and current action decision | Specialist policy authority remains elsewhere. **Mandatory where applicable**; fail closed for prohibited disclosure/action; retain lawful-minimum evidence |
| Imported historical records — **external evidence** | Prior reservation IDs/status/revisions/party references and cutover checkpoint | Provenance and non-duplication mandatory; import is not implicit provider authority transfer. **Optional**; quarantine collision, bad chronology or unsupported source state |

## Idealised conceptual public output interfaces

| Output / consumer | Business meaning, authority, status and provenance / disclosure |
|---|---|
| **Availability enquiry** — authorised applications, search/UI, resource owners | Offerings, available intervals, remaining Booking-authoritative capacity and limitations; include scope, effective policy/source revision, as-of time, zone and projection freshness. An enquiry is **not** a reservation or guarantee |
| **Reservation operation result** — requester, host, Order/commerce, capacity owner | Accepted/held/pending-confirmation/confirmed/rejected/cancelled/amended/expired/uncertain state; authoritative Booking ID, version, source refs, expiry, reasons, retry guidance and correlation. Distinguish received command from committed confirmation |
| **Reservation and hold detail/history** — permitted staff, customers and consuming capabilities | Scoped current and as-of lifecycle, linked amendments/releases and authorised party reference; mask personal details unless purpose and permission allow; history shows source/time/actor/policy-version provenance |
| **Capacity commitment and release** — resource/capacity owner | Requested/confirmed/withdrawn Booking commitment, interval, quantity, resource reference, stable operation key and version; no assertion of physical Asset custody or Inventory stock reservation |
| **Service participation evidence** — Billing, Reviews, fulfilment, Reporting | Attendance, check-in, completion, no-show, cancellation or amendment facts **only where Booking is authoritative for that fact**, with effective time, source and correction chain. A booking alone proves neither service delivery nor an authorised review |
| **Commercial event/evidence** — Billing, Order, Payment Gateway, Accounting via proper owner | Booking confirmation/amendment/cancellation and applicable fee-trigger evidence; Booking does not calculate charge, invoice, execute/refund payment or post ledger entries |
| **Operations, exceptions and reconciliation** — admins, Integrations, observability | Provider scope, pending/uncertain mappings, stale supply, conflicts, under/over-allocation alarms, checkpoint, backlog and recovery actions; never claim provider confirmation on transport acknowledgement |
| **Booking-owned domain events** — MQ, Audit intake, authorised subscribers | Versioned accepted business changes from Booking's durable outbox; tenant, booking/resource references, source revision/time/actor correlation and minimal payload. Duplicate/redelivered/out-of-order events need idempotent consumer handling |
| **Authorised exports/report source data** — Reporting, Export, administrators | Booking-owned volumes, utilisation, cancellations, lead times and lifecycle with access-controlled dimensions, provenance and completeness; financial metrics remain Billing/Accounting's authority |
| **Optional presentation interfaces** — host/user | Accessible dashboard, calendar/availability, management and customer journeys calling the same protected headless contract. UI state and labels are not authoritative outcomes |

### Proposed logical public surfaces

1. **BK-S01 Offering and capacity supply** — validate/register resource references, booking rules, supply/blackout changes and capacity authority without reowning the source resource.
2. **BK-S02 Availability and reservation enquiry** — scoped, provenance-aware availability and current/historical booking queries, explicit freshness and reservation-versus-quotation distinction.
3. **BK-S03 Reservation lifecycle commands** — hold, confirm, amend, reschedule, cancel, expire, resolve and release with conflict, idempotency, policy and authorisation handling.
4. **BK-S04 Participation and external commitments** — conditional check-in, no-show/service evidence, coordinated Asset/Inventory commitments, external authority and reconciliation.
5. **BK-S05 Integration and event exchange** — owned lifecycle events/outbox, durable Audit evidence cooperation, Billing/Order/Notifications/MQ outputs and provider status.
6. **BK-S06 Administration, reporting and presentation** — policy views, operational exceptions, permission-scoped exports, dashboard and optional separable screens.

These surfaces are **conceptual groupings**, not six repositories, classes or endpoint requirements.

## Commands, queries and events

**Commands:** `registerOffering`, `setBookingRules`, `requestHold`, `confirmReservation`, `amendReservation`, `rescheduleReservation`, `cancelReservation`, `expireHold`, `recordAttendance`, `markNoShow`, `completeBooking`, `resolveBookingException`, `reconcileProvider` are **illustrative domain actions**. Each has server-checked scope and state, source versions, operation identity, conflict/validation outcomes and no assertion of success before the required authoritative commit. Offering management, attendance and payment gating are permission-/configuration-/domain-conditional.

**Queries:** availability by offered capacity/time and party size; booking by ID; authorised booking list and timeline; utilisation/capacity ledger; pending and provider exceptions; policy/effective revision; scoped export. All expose freshness and completeness. Do not return unfiltered guest identities through public search. Queries must not quietly create holds.

**Events:** `BookingHeld`, `BookingConfirmed`, `BookingAmended`, `BookingCancelled`, `BookingExpired`, `BookingCheckedIn`, `BookingCompleted`, `BookingNoShowRecorded`, `BookingReconciliationRequired`, `BookingAuthorityChanged` are illustrative owned event meanings. Emit only after the corresponding Booking-owned committed change and through a durable owner outbox; map source event IDs and versions. A provider webhook is untrusted evidence until verified and applied; Audit receipt and MQ transport status are separate facts.

**Common interaction context:** tenant/organisation, trusted actor and assurance, protected resource, authority mode and capacity scope, booking ID, effective policy and supply versions, operation/correlation/idempotency IDs, interval and IANA zone, originator, provenance and effective/observed timestamps. No mandatory universal request object is proposed.

## Contract invariants, failures and recovery

- **Single capacity authority per defined resource scope and time:** Booking confirms against its own authoritative pool, or an explicitly chosen external provider/domain confirms its own pool; Booking cannot invent a second independent capacity guarantee.
- **No overselling within Booking's authority:** holds and confirmations consume finite capacity and overlapping requests arbitrate atomically in the logical business model. A stale availability query offers no guarantee.
- **Eligibility is external where owned externally:** current Asset safety, service eligibility, Inventory reservation, required entitlements, commercial terms and legal constraints are enforced; an available slot is not permission or lawful eligibility.
- **Access, isolation and minimisation:** server Authorisation/tenant scope on every mutation/read, especially guest/contact information and aggregate inference; no permissions from a public identifier, provider callback or event alone.
- **Idempotency:** same trusted operation and key returns the same attributable outcome or explicit conflict; retries cannot double-book, double-cancel or cause duplicate billable evidence. Cross-capability delivery is at-least-once/replay-tolerant, not fictitiously exactly once.
- **Finality:** accepted ≠ held ≠ confirmed ≠ fulfilled ≠ billed ≠ paid. Provider timeout is **uncertain**, not proof of failure or success. Confirmation is only issued on verified capacity authority acknowledgement under applicable rules.
- **History:** amendments, cancellations, source invalidations, manual overrides, retention and authority cutover are versioned and attributable, not destructive rewrites. Exceptional overbooking/manual override requires authorised policy, explicit disclosure and audit.
- **Failure:** absent mandatory permissions/policy/capacity facts → deny/hold/unavailable; duplicate key → replay; contradictory external evidence → exception; expired hold → release when valid; outbox/MQ outage → retain event for retry; Audit critical-evidence failure follows approved risk-tier policy rather than fabricated receipt. Provider recovery requires read-back/reconciliation before replaying potentially committed operations.
- **Compatibility:** explicit business event/contract versions, unsupported-state and unsupported-provider-operation errors, no leaking provider SDK models or private persistence schemas.
- **Native independence:** no remote provider, scheduler or payment service is universally required; individual configured booking flows may validly require a payment/approval/provider dependency and must report its absence.

## Cross-capability relationship matrix

| Capability | Booking receives | Booking supplies | Requirement / failure and ownership |
|---|---|---|---|
| [Asset](../asset/capability-record.md) | Equipment/room eligibility, condition, available assignments and restrictions; checked physical allocation where needed | Reservation windows, proposed/confirmed/released capacity claim and collision information | Conditional. Asset owns eligibility/custody; stale restriction blocks firm confirmation; no reciprocal implementation import |
| [Inventory](../inventory/capability-record.md) | Stock availability and authoritative stock-reservation result | Demand/request and release reference | Conditional; Inventory stock commitment remains authoritative, Booking does not reserve stock twice |
| [Events](../events/capability-record.md), [Location](../location/capability-record.md), service owner | Event sessions, location/resource configuration, capacities, changed blackouts | Booked seats/sessions and cancellation/attendance reference | Conditional; owner keeps event/location source facts |
| [Identity](../identity/capability-record.md), [Profile](../profile/capability-record.md) | Stable actor/customer/group IDs and permitted contact detail | Booking participant references only; no duplicate identity directory | Conditional for authenticated party; guest model requires BK-04 decision. Missing trusted identity context must not generate privilege |
| [Authentication](../authentication/capability-record.md), [Authorisation](../authorisation/capability-record.md) | Trusted principal/assertions and resource-action decision | Protected resource descriptors, intended action and denial/review signals | Mandatory for protected operations; fail closed; customer self-service does not bypass scoped server checks |
| [Configuration](../configuration/capability-record.md), [Clock](../clock/capability-record.md) | Approved effective booking settings; time semantics/zone | Booking-specific validated settings and effective time usage | Essential semantics; do not duplicate configuration preference store or clock |
| [Pricing](../pricing/capability-record.md), [Order](../order/capability-record.md), [Subscription](../subscription/capability-record.md), [Membership](../membership/capability-record.md) | Price offer, commerce acceptance, entitlement eligibility/terms | Booking hold/confirmation/cancellation evidence | Conditional; commercial owner decisions remain distinct |
| [Billing](../billing/capability-record.md), [Payment Gateway](../payment_gateway/capability-record.md), [Invoice](../invoice/capability-record.md), [Accounting](../accounting/capability-record.md) | Deposit/payment and charge-status evidence only when relevant | Booking occurrence/cancellation/attendance charge triggers, reference and adjustment reason | Conditional; no duplicate invoice, ledger or fund movement. If prepayment is required and unresolved, confirmation remains pending |
| [Integrations](../integrations/capability-record.md) | Verified connection/provider capabilities, external authority results, sync/checkpoints | Requested operation and mapping/reconciliation status | Optional; owner picks a single effective capacity authority per scope |
| [Scheduler](../scheduler/capability-record.md), [Workflow](../workflow/capability-record.md) | Trusted expiry/reminder triggers and approved decision outcomes | Due-time hints, idempotent handlers and approval requests/status | Optional/conditional; Booking checks deadline itself; no scheduling/orchestration ownership |
| [Message Queue](../message_queue/capability-record.md) | Transport attempts/acknowledgement | Booking-owned durable outbox domain events | Optional transport; event delivery not source state/confirmation |
| [Audit](../audit/capability-record.md) | Evidential acceptance/integrity or coverage status | Significant authorised/denied/exception booking outcomes with producer provenance | Risk-tier conditional; Audit owns custody, Booking outcomes; critical evidence failures explicitly handled |
| [Logging](../logging/capability-record.md), [Observability](../observability/capability-record.md) | Diagnostic or aggregate health interfaces | Sanitised provider timeouts, contention, retries, reconciliation/latency, occupancy health and correlation | Optional; diagnostics are neither audit receipts nor Booking business records |
| [Notifications](../notifications/capability-record.md), [Mailer](../mailer/capability-record.md) | Delivery status (not proof of recipient attendance) | Permissioned booking notices, reminders, confirmations, cancellations | Optional; delivery failure not silent cancellation or unconfirmed success |
| [Reporting](../reporting/capability-record.md), [Search](../search/capability-record.md), [Export](../export/capability-record.md), [Reviews](../reviews/capability-record.md) | Authorised report/search/extraction orchestration or verified service-review criteria | Minimised, scoped booking metrics, indexes, export facts and verified experience evidence | Optional; read-model display not Booking authority; booking alone not proof of service experience |
| [Legal Compliance](../legal_compliance/capability-record.md), [Privacy](../privacy/capability-record.md) | Jurisdiction/retention, disclosure, consumer protection, required consent and data-rights policy | Booking facts necessary for governed access, minimised retention/disposal and compliance review | Mandatory when applicable; specialist jurisdiction-specific validation required |

Dependency direction must be contract-mediated, explicit and acyclic at package level. Reciprocal **information flow** is not a mandate for reciprocal imports. Public contracts are required for any implemented cross-capability operation; the matrix does not certify that the neighbouring contracts already expose these interfaces.

## Configuration, security, legal obligations and external authority

**Configuration:** effective scope may be tenant, organisational unit, offering, resource or channel; define precedence/validity and audit sensitive policy changes. Booking validates rule coherence and states which changes apply to existing confirmed reservations. No arbitrary operator configuration may override resource safety, tenant boundaries, statutory protections or confirmed contractual commitments.

**Security:** Authorisation decides access to specific booking actions and resources on the server; Booking evaluates business-specific eligibility and conflict. Separate staff/operator/customer/guest/service-provider views, delegated booking-on-behalf-of, refund-adjacent actions, bulk export and exceptional override permissions. Authenticate webhook provenance, replay-window, tenant/provider mapping and delegated authority. Apply OWASP ASVS 5 Level 2 and relevant higher controls; WCAG 2.2 AA, localisation and no insecure client-only policy enforcement.

**Privacy:** dates, availability and capacity may imply sensitive presence, whereabouts, service use or attendance. Publish minimal availability rather than guest lists; control purpose, erasure/retention, sensitive bookings, pseudonymisation and historical identity references. Named participants/contacts belong in appropriate identity/profile/privacy-controlled systems where possible; booking keeps only necessary booking-specific associations. No assumption of a universal retention duration or unrestricted cross-tenant resource visibility.

**Legal:** variable consumer cancellation/refund rules, accessibility provision, age/guardian suitability, permits, sector-specific sensitive appointments, room/facility constraints, tax and payment obligations, cross-border data handling may apply. Legal Compliance determines applicable duties with qualified specialist validation; Booking records the applicable approved policy, not a universal legal verdict.

**Connected authority modes (proposed):** (1) Booking-native authoritative pool; (2) externally authoritative scoped pool with local pending/canonical references and verified provider confirmations; (3) transitional migration/reconciliation, explicitly controlled and time-bounded. Never permit two live writers to certify the same capacity without an explicit common arbiter. Provider discovery must identify supported hold/confirm/cancel/update operations, guarantees, freshness, rate limits and uncertainty. Cutover needs freeze/checkpoint/export/import, deduplication, verification, rollback policy and full provenance. A sync cursor or webhook acknowledgement is not evidence of successful reservation.

## Optional graphical interfaces and navigation

**Proposed presentation:** headless Booking contract with optional separable screens using Theme Manager semantic tokens and reusable `ui` components. As illustrated by [application-test-template](https://github.com/nuxt-layers-test/application-test-template), the **host** may place Booking in the Capabilities sidebar and route to a Booking dashboard in the shared shell. The template is illustrative; it does **not** prove an automatic menu API or production booking screens.

| Screen / journey | Typical actions and important constraints |
|---|---|
| Booking dashboard | Upcoming reservations, current capacity/occupancy, pending holds, conflicts, exceptions and reconciliation; audience-scoped data |
| Availability/calendar | Day/week/list and accessible alternative, filters by venue/resource/service/zone/quantity; show freshness, blackouts and hold disclaimer |
| Booking creation and checkout handoff | Choose slot/party, eligibility, temporary hold, commercial/payment/approval dependencies and distinct final confirmation |
| Reservation detail and lifecycle | View booking version, participants (restricted), linked order/payment refs; reschedule/cancel/check-in under explicit permissions and policy |
| Resource and booking rules | View authoritative resource link, supply/capacity and policy, availability exceptions, effective changes and source provenance |
| Waitlist and exception workbench | Offer/waitlist administration if enabled, provider uncertainty, duplicate/conflict reconciliation and manual governed override |
| Reporting and export | Utilisation, attendance, no-shows, cancellation, lead times, provider coverage, scoped export requests |
| Administration and provider status | Configuration provenance, effective authority, connection coverage, reconciliation checkpoints, notification state and audit references |

Customer self-service and operator administration are separate permission/audience surfaces; a public calendar must never expose full participant details. Empty/partial/stale/offline/denied states are explicit. Keyboard-first access, localisation, time-zone ambiguity, high-contrast themes, no colour-only status and clear reservation versus payment status are conceptual requirements. Host may disable all Booking presentation; source operations remain protected and independently usable.

## Conceptual public-contract acceptance scenarios

| Scenario and input | Expected behaviour and output | Authority |
|---|---|---|
| Native room booking; two simultaneous requests for last unit | Exactly one eligible claim confirms; other receives conflict/alternate, no overbooking; history/event trace | Booking capacity claim; Asset eligibility |
| Read available 10:00, another user holds it, then request confirmation | Fresh recheck rejects/conflicts or selects an alternative; search did not guarantee reservation | Booking |
| Tenant A reads/edits tenant B's reservation; public user searches names | Denial or appropriately minimised availability; no information leakage | Authorisation + Booking disclosure |
| Invalid DST local time, negative quantity, outdated resource capacity version | No mutation; attributable validation/stale/conflict result | Clock time semantics, source owner and Booking |
| Retry confirmation and duplicate provider callback | One authoritative change, stable idempotent result and one logically owned event; subscribers deduplicate delivery | Booking / selected provider |
| Payment-required booking where payment provider is unavailable | Hold or explicit pending state subject to expiry/policy, never falsely settled/confirmed | Booking lifecycle; Payment Gateway funds |
| Remote provider times out after accepting confirm | Mark uncertain, query/reconcile authoritative provider before retry; no second reservation invented | External provider; Booking reconciliation |
| Equipment becomes unsafe after confirmation | Existing commitment flagged/reviewed and safe remediation/cancellation; no booking overrides Asset restriction | Asset eligibility; Booking reservation |
| Amend to overlapping duration with contested capacity | Version-checked move/alternative or rejection; no gap/oversell disguised as confirmed | Booking |
| Hold expiry after Scheduler outage | Deadline is enforced by Booking itself when next observed, release/reconcile and emit event | Booking |
| Booking cancelled and Billing already charged | Booking emits corrected cancellation/fee evidence; Billing decides charge adjustment; Payment Gateway refunds only on authorised instruction | Booking, Billing, Payment Gateway |
| Historical attendance supplied to Reviews/Reporting | Verified provenance and permission-limited evidence; attendance not inferred from mere confirmation | Booking if assigned attendance authority; consumers own derived decisions |
| Unsupported provider has no hold operation | Explicit unsupported/pending or configured alternative; never invent provider hold semantics | Integrations discovery and selected provider |
| Audit/MQ/Logging unavailable | Domain outbox retains events; reporting separates evidence custody, message transport and technical diagnostics; critical-capture policy enforced | Booking source event, Audit custody, MQ delivery, Logging |

## Architectural decisions, investigations and acceptance

**Proposed decisions for owner approval (not previously approved):**

- **BK-01 — Independent bounded domain:** retain Booking for time/session capacity reservations, distinguish from Asset custody, Inventory stock commitments, Order commercial acceptance and Scheduler execution. **Recommendation: approve.**
- **BK-02 — Capacity authority model:** select one effective authoritative reservation arbiter per resource/pool/channel scope and valid period, with controlled native/provider migration and reconciliation, no independently guaranteed duplicate pool. **Recommendation: approve.**
- **BK-03 — Lifecycle scope:** support native finite holds, confirmed/amended/cancelled bookings, expiry and exceptions; waiting list, attendance/no-show and completion are conditional features with explicit source authority. **Recommendation: approve.**
- **BK-04 — Party/customer representation:** support opaque authorised participant/guest/counterparty references without making Booking a second identity/profile directory; define when guest contact custody is temporarily Booking-owned and its retention. **Recommendation: approve principle; leave detail conditional on Privacy/Profile public contract.**
- **BK-05 — Presentation and commerce independence:** optional separable Booking screens, native free/manual booking, conditional checkout/payment and external providers, no assumed Order/Payment requirement for every reservation. **Recommendation: approve.**

**Technical investigations (not approval questions):** interval representation and overlap algorithm; multi-resource atomicity and alternative supply; recurrence and DST handling; hold fencing/idempotency expiry under race; policy version changes affecting existing commitments; provider supported operations and external ID mapping; capacity source freshness; default waitlist fairness; retention matrix and vulnerable-person bookings; arrival/check-in service authority; source invalidation and cancellation compensation; exact contract compatibility and reusable open-source foundations.

**Implementation alignment:** no Booking implementation contract exists to reconcile. Actual public contracts for Asset, Inventory, Events, Integrations, Scheduler, Audit, Logging, Reporting, Notifications, Payment Gateway and other candidates remain unverified unless individually published. Do not assert those interfaces are currently available.

**Acceptance/verification:** independent root `CONTRACT.md` sufficient to compose without internal code; contractual scope/authorisation/security; native/no-external-provider acceptance; concurrency and replay/partial failure; tested provider reconciliation; composed 50-line Nuxt host where applicable; appropriate screens and WCAG 2.2 AA; risk-proportionate Audit evidence, privacy and legal review. No tests, builds, UI audits or regulatory validations have been run for this proposal.

## Architectural consequences and conceptual sign-off

**Proposed:** retain the governing catalogue's Domain-candidate classification, subject to BK-01 approval. This review **does not amend normative catalogue, ADRs or standards**, create a repository, or approve deployment. Reciprocal conceptual notes in neighbouring records reference this record without completing their own alphabetical reviews. The register should remain candidate until accepted and independently evidenced. Existing template pro forma and the Asset cross-capability note have been incorporated into this fuller record.

**Conceptual sign-off:** **awaiting project-owner decisions BK-01–BK-05**. The idealised input/output boundaries and scenarios are specified for review, but no operational capability, production readiness, provider conformance or legal certification is established.
