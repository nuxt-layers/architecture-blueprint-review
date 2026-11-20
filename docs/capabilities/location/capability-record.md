# Capability Record — Location

**Status:** Proposed Platform capability; conceptual review submitted for owner approval, not an implemented or approved contract.
**Review:** 20 November 2026.
**Governing opening baseline:** `nuxt-layers/architecture-rules/master` `b920ce0d8b361de000a6739a16123dbdc56df7a7`.
**Blueprint opening baseline:** `nuxt-layers/architecture-blueprint-review/master` `6dac83a03da8704f7945ee1bc894f2248300445a`.
**Evidence:** [Review protocol](../../review-protocol.md), [governing catalogue](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/catalogue.md), [normative Capability Standard](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/capability-standard.md), accepted [ADR-0012](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/decisions/ADR-0012-trivial-composition.md) and [ADR-0016](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/decisions/ADR-0016-controlled-layer-specialisation-and-composition.md); existing [Events](../events/capability-record.md) reciprocity dated 18 November. No `nuxt-layers/location` repository was found in the organisation repository-name lookup. Consequently no root `CONTRACT.md`, runtime API, committed persistence or presentation is verified. Other pending conceptual reviews are provisional.

## Capability Name
`location` — reusable place and geospatial reference service, not a universal address, facility, tenancy or safety authority.

## Purpose and classification
**Proposed:** Platform capability. Maintain a usable, permission-scoped registry of identifiable physical places and geospatial references and provide predictable geospatial operations to consumers. This has independent value for assets, venues, deliveries, public listings and proximity searches. A pure coordinate mathematics helper could instead be a stateless library; the distinct capability is justified only where place identity, reference stewardship, revision, sharing and lifecycle are needed. No separate repository/deployment is automatically approved. A headless core and optional separable administrator/picker presentation are appropriate.

**Authoritative ownership:** Locally created place identifiers, typed place geometries, names/aliases and supported descriptive attributes, coordinates and coordinate-reference metadata, relationships between place references, quality/provenance, source attestations, status, revision and lifecycle of the *Location-maintained reference*. A place may be a point, bounded area, line/route geometry or venue reference; authoritative physical premises/facility attributes remain with the facility/Asset owner. The source of measured coordinates can be an imported provider or verified survey; Location records the attributed, approved representation and its confidence, not a claim that all physical facts are correct.

**Does not own:** Postal/delivery address records of people, organisations, suppliers or customers; geolocation of persons/devices and location tracking; legal property title; sites/tenant hierarchy or Site Hosting domains; physical asset custody, building safety, accessibility compliance, maximum occupancy, route execution, logistics dispatch, transport directions, venue/session reservations, maps licences, weather, business opening hours or third-party place directories. A location link must not imply any of these facts.

## Status, Version, Availability and Capabilities offered
**Status:** Proposed conceptual design; not Available, Installed, Configured, Operational, Enabled or Authorised. Contract version and runtime availability are **not assigned**.
**Native capability proposal:** register/update/retire a scoped place; attach validated point/boundary/entrance references; spatial containment, distance and proximity within declared precision; resolve a place ID; manage duplicate candidates and redirects; return permitted geometry and descriptive reference with source/freshness; share a place reference only through authorised scope; keep correction lineage, provider provenance and a durable change outbox. Optional geocoding/reverse-geocoding, autocomplete, routing, imagery, address enrichment and GIS overlays require declared providers and must not be assumed native.

## Owned information, invariants and lifecycle
- Stable opaque place ID, owning tenant/scope, optional resource-owner reference, place type and descriptive label; geometry in a declared coordinate reference system (WGS 84/EPSG:4326 for interchange where appropriate), declared precision/accuracy and effective/as-recorded dates.
- Coordinates/geometry are distinct from postal addresses. Where a consumer owns an address, Location holds a permission-scoped **reference or attributed geocode evidence**, not an alternative authoritative mailing address.
- Place status: proposed/unverified → verified/active (based on evidence and permitted approval) → superseded, restricted or retired. Corrections are versioned; a withdrawn provider does not erase previous audit-relevant provenance subject to retention policy.
- Multiple candidate coordinates, conflicting sources and ambiguous names must remain distinguishable. Never silently promote a guessed rooftop/centroid to an exact entrance or safety-approved access point.
- A hierarchy or association (building–floor–room, site–venue, route–stop) is a location **reference relation**, not an Identity group hierarchy, tenancy inheritance or facility-ownership decision.
- Native operation must support explicitly supplied coordinates/geometries and manually verified places without any commercial API, mapping tiles, external internet connection or automatic address resolution. Non-deterministic provider enrichment is optional.
- State changes require authorised caller, revision/concurrency precondition where meaningful, input validation, idempotency for retries, persisted authoritative result and outbox emission. Never claim exactly-once delivery across services.

## Idealised public inbound contract

| Source and input | Requirement and interpretation | Validation, missing/uncertain behaviour |
|---|---|---|
| Authorised place steward or domain owner: create, correct, verify, restrict, retire, link a place | **Core** place commands; domain owner is authoritative for associated resource, Location for its place reference | Server-side resource/tenant access; required coordinates when creating a geospatial point, finite latitude [-90,90], longitude [-180,180], valid ring/topology for polygon, CRS/units and permitted accuracy; reject invalid or unauthorised; version conflict on stale correction |
| Identity, Authentication, Authorisation: caller, tenant and decision context | **Required** for protected records; AuthN supplies assurance, Authorisation permits the exact operation | Missing/ambiguous access fails closed; supplied tenant/subject IDs never confer rights |
| Resource-owning capabilities (Asset, Events, Booking, Logistics, Publisher etc.): resource reference and allowed scope | **Conditional** resource association and visibility; resource owner controls business eligibility, placement decision and resource lifecycle | Missing or stale resource authority blocks any conclusion about that domain; bare foreign ID not proof of association or disclosure rights |
| External gazetteer/geocoder/survey evidence through Integrations | **Optional** coordinates, name, place ID, precision, confidence, licence, provenance and timestamp | No assumed provider accuracy or licence; unavailable → native entries still function; uncertain/contradictory candidates flagged for review, not silently selected |
| Configuration, Privacy, Legal Compliance: permitted providers, disclosure, retention, precision and jurisdiction | **Conditional** effective policy and handling rules | Hard legal/security floors cannot be disabled; unknown required disclosure/retention constraint fails closed |
| Clock: canonical instants/timezone formatting | **Optional composition service / required semantics where effective times are used** | Invalid instants rejected; distinguish event time from record time; no inferred timezone from coordinate alone |
| Operator: merge/split and alias evidence | **Conditional** deduplication without losing old place references | Explicit steward approval, referential impact and redirect/version lineage; never rewrite another domain's authoritative historical record |

## Idealised public outbound contract

| Output and consumer | Meaning and authority boundary |
|---|---|
| `PlaceReference` and `PlaceRevision` queries to authorised domain services and UI | Scoped ID, type, status, label, optional permitted geometry, CRS, accuracy/precision, source, revision, effective/recorded time and provenance. **Authoritative only for Location's maintained reference**, not real-world safety or legal property claims |
| `resolvePlace`, `searchPlaces`, `nearby`, `contains`, `distance` and geometry validation | Explicit search scope, geometry calculation rules, units, completeness, ordering, result limits, freshness and confidence. Spatial proximity is not routability, travel time, capacity or eligibility |
| Place lifecycle events to MQ relay and subscribers | Committed create/correct/verify/restrict/merge/supersede/retire and association change with ID, revision, affected scope, timestamps and minimal permitted data; downstream rechecks domain decisions. Delivery may replay or reorder |
| Export and Reporting | Authorised spatial datasets/aggregates with version and data-source attribution; privacy, licence, retention and coordinates precision enforced. Reporting owns report definitions, not Location place facts |
| Audit and Logging | Security-relevant domain action evidence to Audit (actor/action/reference/before–after revision/outcome), redacted technical diagnostics to Logging; no bulk precise personal location or unneeded geometry in logs |
| External provider state via Integrations | Geocoding response provenance, use restrictions, attribution, quota/error status and source mapping. Location never claims an unverified third-party answer is authoritative |

**Contract shapes are conceptual**, not fixed TypeScript signatures or HTTP endpoints. Every query returns explicit not-found/hidden, ambiguous, invalid, stale, restricted and unavailable semantics without leaking the existence of inaccessible places. External provider candidates remain distinguishable from verified place records.

## Public interaction and operational semantics
**Commands:** `registerPlace`, `reviseGeometry`, `changePlaceStatus`, `associateReference`, `reconcileCandidates`, `retirePlace`. Each accepts the applicable caller/tenant, target and expected revision, source evidence and idempotency key as needed, and returns accepted/completed/denied/conflict/error truthfully. Reconciliation is permissioned; duplicate command replay returns the prior result where safe.

**Queries:** resolve ID and revision, permitted place search, geometry/proximity operations, lifecycle history and export. Explicit coordinate type/units and algorithm limitations; zero results is distinct from unsearched/unavailable. Results do not grant access to linked resources. Derived indexes and tiles may be stale and rebuildable.

**Events:** Only Location-owned committed reference changes from the capability-owned durable outbox, transported via Message Queue without MQ owning business facts. No events for provider guesses before they become committed Location facts. Events are notification of change, not permission to consume restricted geometry.

**Shared context:** caller/tenant and recipient visibility, resource owner and revision, source/version, effective/recorded time, geometry CRS/accuracy, policy version, correlation/idempotency and completion status only where relevant; no universal request object. Cross-tenant sharing requires explicit granting and disclosure policies rather than implicit global place visibility.

## Cross-capability relationships and reciprocal direction

| Capability | Location receives | Location supplies; authority separation | Need |
|---|---|---|---|
| Identity / Authentication / Authorisation | Trusted caller, tenant, assurance, resource-aware decision | Scope/reference for authorisation; never IAM membership or access grants | Required on protected operations |
| Configuration / Privacy / Legal Compliance | Provider selection, rules for accuracy/disclosure, retention, legal restrictions | Geospatial data handling/provenance signals and permitted exports | Conditional policy context |
| Asset / facilities or venue owner | Asset/site identity, stewardship, physical placement and valid safety/access controls | Place/geometry references, revision and proximity; **not occupancy, fire compliance or accessible-route safety** | Conditional |
| Events / Booking | Event venue and session/booking resource references, occurrence and lifecycle | Venue place reference/geometry and verified restrictions **only if Location owns them**; authoritative suitability from resource owner; event or booking decisions remain theirs | Conditional |
| Logistics / Warehouse | Shipment/stoppage/delivery needs, authoritative address or facility refs | Geospatial stop/entrance geometry, approximate distance/area; not dispatch or routing promises | Optional |
| Publisher / Marketplace / Search / Federation / SEO | Published resource references and permission-to-disclose scope | Public-or-restricted place metadata, bounding boxes and revisions; no publication/search/index rights by implication | Optional |
| Clock | Canonical instants and timezone semantics | Place's attributed timezone, if verified, as reference only; Clock decides temporal interpretation | Optional |
| Integrations | Optional geocoder/map/OSM/place data and provider terms through approved adapters | Provider-neutral enrichment request and source/evidence status; provider owns its remote directory | Optional |
| Audit / Logging / Reporting | Applicable event/evidence contracts, diagnostic correlation, reporting demands | Evidential action facts, redacted technical logs, authorised geospatial read/export with provenance | Conditional cross-cutting |
| Message Queue / Scheduler / Workflow / Notifications | Transport, due task execution, approvals and subscriber delivery | Source-owned outbox events, registered maintenance tasks, approval intents and notification triggers; none inherits place authority | Optional/conditional |

No dependency on these consuming domains is needed for Location's standalone native service. Avoid direct cyclical imports; domain owners may reference Location through a public contract while Location uses generic externally supplied resource references. Reverse facts arrive through a host-composed generic port or events, not private domain queries. Recipients must re-authorise on use.

## Configuration, providers, security and privacy
- Minimum native settings: allowed CRS/geometry types, maximum geometry size, precision/accuracy quality gates, per-tenant visibility default (private), optional sharing, source/provider allowlist, retention and export policy, spatial query limits, provider attribution and error policy.
- Person/device movement, precise home/health/child locations, regular geolocation histories and live tracking are **out of scope**. Any proposed sensitive tracking requires separate ownership, lawful-basis and threat-model approval, access controls and location-specific retention safeguards.
- Apply governing OWASP ASVS 5 Level 2, relevant Level 3 for privileged/sensitive handling, server-side authorisation, tenant isolation, abuse and bulk extraction limits, privacy by design, UK GDPR/GDPR where applicable, WCAG 2.2 AA, secure provider keys, redacted logs and audit evidence.
- Geolocation disclosure risk: inference of sensitive premises or protected persons through coordinates, proximity, shape boundaries, error messages, search ordering or aggregate leakage. Enforce authorised query predicates **before** spatial ranking, not after.
- External provider/map tiles may transmit coordinates and user network identifiers. Require provider-specific data protection, terms/licence, caching/redistribution limits, consent or lawful basis where applicable, and host-managed secrets. Accuracy is not a safety certification.
- Native coordinates/geometries need no external service. Optional PostGIS/spatial index or mature geometry tooling is an **implementation investigation**, not a mandatory new infrastructure package or shared persistence owner. Provider-backed derived caches must be disposable; source state stays with Location.
- Standards to evaluate: OGC Simple Features / GeoJSON RFC 7946 for geometry interchange, ISO 19111 for coordinate reference systems, ISO 19115 for metadata/provenance, WGS 84/EPSG identifiers and ISO 3166 where country references are needed; postal address standards (e.g. UPU S42) belong to the address-owning domain. Observe GeoJSON coordinate order (longitude, latitude) versus many UI latitude/longitude presentations. These are design references, not a claim of certification.

## Conceptual GUI / headless integration
**Proposed optional presentation:** host sidebar entry **Locations** → capability dashboard. Dashboard lists scope-filtered place references, quality/review status and provider exceptions. Detail view displays a map/geometry when permitted, coordinates, declared accuracy, revisions, provenance and linked resource references. Forms support create/import, permitted point placement and polygon edit, preview/validate, review/approve, merge/supersede/retire, safe redaction and export. Resource-owning domains may embed a place picker; they must retain resource decisions.

**Permissions:** viewers cannot use editing controls; editors cannot self-approve where separation-of-duty policy requires review. Search must not reveal private pins. Map tiles optional with a text/table/coordinate fallback. WCAG 2.2 AA keyboard access, non-map alternatives, responsive design, localisation and Theme Manager semantic tokens required. Host owns routes, menu registration, branding and orchestration; no assumed existing screen API. `presentation: false` keeps fully operational headless queries/commands and their security checks; a Nuxt adapter, if built, must meet ADR-0012 one-call/50-line budget.

## Conceptual acceptance scenarios (not executed tests)

| Input | Expected behaviour/output | Authority |
|---|---|---|
| Authorised manual point with valid coordinate pair | Stable scoped place ID, revision, provenance and outbox change; no external API dependency | Location |
| Longitude/latitude swapped or out of range; invalid polygon | Validation error, no persisted change | Location |
| Tenant A queries Tenant B's private place ID or nearby geometry | Denied/non-disclosing result before spatial ranking | Authorisation + Location |
| Accepted geometry correction with expected revision | New revision and historical lineage; subscribers see replay-safe event | Location |
| Repeat same idempotent update | Stable prior result; no duplicate authoritative mutation | Location |
| External geocoder times out or reports conflicting matches | Candidate marked uncertain or provider unavailable; no invented verified geometry; native query works | Integrations evidence + Location |
| Venue event requests capacity/suitability from a place point | Place geometry is available where authorised; occupancy/safety is **unknown** until venue/Asset owner supplies it | Events + Asset/venue owner |
| Asset moves from site A to B | Asset owns placement change; Location updates an authorised reference/association if requested, never transfers asset custody itself | Asset + Location |
| Retired/merged place referenced by historic booking | Versioned redirect or historical reference, no silent rewriting or retrospective change | Location + Booking |
| Publisher requests public pins for confidential premises | No public coordinates without explicit disclosure rights | Publisher + Location |
| Map provider absent, presentation disabled | Headless native coordinate entry, reads and geometry calculations remain accessible via permitted contracts | Location |
| Export request or provider licence prevents redistribution | Filter, coarsen or deny with explicit reason; no unlicensed provider data leak | Location + Privacy/Legal Compliance |

## Decision and evidence register
- **Established (governing):** Contract-only boundaries, capability-owned state/outbox, explicit acyclic dependencies, tenant-authorised operations, native secure operation, ADR-0012 composition limits, optional separable presentation and governance/security/privacy baselines.
- **Established (blueprint):** Catalogue proposes Location for geospatial/place references but excludes universal postal address/site tenancy; Events has an 18 November reciprocal note.
- **LOC-01 — Proposed:** Retain a Platform capability only for independently managed place registry and geospatial reference service; do not promote mere geometry helpers into a stateful domain.
- **LOC-02 — Proposed:** A Location place ID/geometry is authoritative only as a location reference; facility, delivery address, eligibility, legal status and tenancy remain with their domain owners.
- **LOC-03 — Proposed:** Provider-neutral offline/manual coordinates are native; geocoding, maps, tiles and routing are optional integrations.
- **LOC-04 — Proposed:** Versioned accuracy, source, disclosure and effective-time semantics on all public geometries; no implicit public pin or exact-entrance claim.
- **LOC-05 — Proposed:** Optional admin GUI and domain place picker; core remains usable headlessly.
- **LOC-06 — Open decision:** Is a tenant-controlled shared/global place directory or cross-tenant reuse needed? Default is isolated records with explicit controlled sharing; global canonical place identity is **not** assumed.
- **LOC-07 — Open decision:** Should non-spatial postal address normalisation be a separate reusable address capability, or remain domain-owned? No transfer of address authority agreed.
- **LOC-08 — Open decision:** Does a reusable routing/navigation service warrant a later separate capability? Distance/containment does not imply directions.
- **LOC-09 — Technical investigation:** Precise geometry model, topology validation, PostGIS needs, source licensing, precision limits, geometry performance and index strategies.
- **LOC-10 — Implementation alignment:** A future root `CONTRACT.md`, public exports, store/outbox, permission catalogue, GUI, host-composition and contract/negative acceptance evidence require a separately authorised implementation plan.
- **Conceptual sign-off:** Pending explicit owner approval; no tests or runtime validation claimed.

## Existing Events reciprocity — retained and reconciled (18 November 2026)
**Events EVT-09 (18 November 2026; technical interface requirement):** [Events](../events/capability-record.md) needs a place/venue reference, location and suitable versioned location restrictions from Location, with physical occupancy/fire/accessibility suitability obtained from the actual authoritative venue/Asset owner where Location does not own those facts. Events supplies planned occurrence time, status, change/cancellation and affected location references. Missing essential current safety restrictions cannot be presented as authorised occupancy. No direct domain-store access or Events takeover of location/venue facts. [Decision and contracts](../../../reviews/events-contract-attendance-and-handover.md).

**20 November interpretation:** Location exposes its own reference/geometry restrictions and their provenance, not building safety or regulated capacity assertions. Events must receive required safety evidence from the actual venue/Asset owner. This keeps EVT-09 intact without transferring authority.

## Future alignment and pre-merge review
Review reciprocal notes and active neighbours against current master before merging; particularly Asset, Events, Booking, Logistics, Publisher, Search, Audit, Logging and Reporting. Check protected master, PR diff and mergeability, accepted governing changes, approval status, document links and source-of-truth collisions. A clean Git diff does not prove contract coherence. No local tests/builds; no implementation repo modifications. Do not merge without explicit approval.
