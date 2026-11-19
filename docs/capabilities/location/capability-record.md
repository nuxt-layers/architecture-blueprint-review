# Capability Record — Location

**Capability:** `location` (actual directory `docs/capabilities/location/`).  
**Classification recommendation:** reusable **Platform candidate**, independent place/spatial-reference responsibility with optional headless-first presentation; not automatically a Nuxt Layer, separate service or independently deployed package.  
**Status (19 November 2026):** **proposed conceptual design; owner approval outstanding**. Available/installed/configured/operational/enabled/authorised implementation statuses **unverified**.  
**Review:** [opening baseline](../../../reviews/location-review-baseline.md) · [draft PR #87](https://github.com/nuxt-layers/architecture-blueprint-review/pull/87) · [review protocol](../../review-protocol.md).  
**Baseline:** `architecture-rules/master@b920ce0d8b361de000a6739a16123dbdc56df7a7`; `architecture-blueprint-review/master@6dac83a03da8704f7945ee1bc894f2248300445a`.  
**Evidence:** existing Location pro-forma and Events EVT-09 note (18 November); Asset and Events conceptual records; governing capability standard, architecture, privacy, presentation and accepted ADR-0001/0002/0009/0012/0016/0017/0018. Organisation repository search returned no `nuxt-layers/location` repository; **no published Location root `CONTRACT.md` or implemented API verified**. Related blueprint notes are evidence of proposed reciprocal needs, not installed contracts.

## Purpose, classification and independent justification

Location supplies **reusable, stable, versioned place identity and spatial reference facts** to capabilities that need to describe *where* a physical site, place, addressable destination or bounded area is. It resolves and validates normalised address/place descriptions, coordinates, hierarchies and relevant geographic relationships where supported, with provenance and uncertainty. Without this boundary, Events, Asset, Warehouse, Logistics and other domains risk inconsistent place identifiers, duplicated address corrections and unsafe assumptions about spatial truth.

**Classification gate:** this is not merely a map widget, geocoder adapter or an organisational-location setting. Its independent value is a lifecycle of tenant-governed named places, geospatial evidence and revisions; useful core can work without mapping vendors. Recommend **retain as a Platform candidate** with minimum necessary persistent place records and optional derived indexes. Host composition and domain-specific place assignments remain elsewhere. A small stateless geographic utility may supplement Location, but cannot replace its authoritative place catalogue and changes. Repository and package creation require separate approval.

**Distinguish:** (1) a **place** is a canonical location description and spatial reference; (2) an **address** is a postal/delivery descriptor, not automatically a unique building or reliable coordinate; (3) a **geographic area** is a bounded geometry or qualified region; (4) a **domain placement** says an asset, stock, event or person is currently associated with a place, and remains owned by that domain; (5) **live position/tracking** is sensitive time-varying subject data and is **not** a generic Location source-of-truth. Do not conflate mailing address, legal domicile, land parcel, building, internal room, GPS fix and jurisdiction.

## Authoritative records, decisions and exclusions

| Location owns (proposed) | Boundary / other owner |
|---|---|
| Tenant-scoped stable place ID, place type, names/aliases, address forms, descriptions, spatial geometry/coordinate reference, recorded source, confidence, precision, effective dates, revision and status | Identity owns tenant/group membership; Profile owns a person's private residence/contact address; Configuration owns organisation-provided settings; business domains own where their own resources are assigned |
| Place hierarchy/containment and relationship references (campus/building/floor/room; address/area; parent changes); authoritative only for Location's *registered descriptive* relationships | Asset owns actual asset assignment/custody, Warehouse owns bin/stock occupancy, Events owns event occurrence place assignment; legal ownership, property rights and safety certification are not inferred |
| Validation, canonicalisation, deduplication proposals, correction/merge/supersession redirects with history; ambiguity and disputed evidence | External address/geocoding sources supply evidence, not automatically authoritative place lifecycle; public-address correctness is not guaranteed merely by provider output |
| Sharing/disclosure classification, authorised place-directory reads, provider-evidence provenance and versioned event outbox | Authorisation decides permissions; Privacy/Legal Compliance supply constraints; Audit owns independent evidence, Logging operational logs, Reporting derived analysis |
| Optional derived spatial query/index/cache for registered places | Geospatial accuracy and routing/ETA services are optional; no mandatory GIS/geocoder or location surveillance |

**Does not own:** personal whereabouts; users' movement trails or background GPS; live fleet telemetry; emergency-service dispatch or safety/evacuation approvals; land/title/cadastre; lease/ownership; venue occupancy and fire/accessibility certification; stock balances, warehouse put-away decisions, deliveries, transport routes or event schedules; international border/legal jurisdiction determinations; postal delivery guarantee; map tile licensing; geocoder provider data rights; external administrative boundaries asserted as legal facts without qualifying source.

A tenant place may reference a public/common location, but a globally shared canonical place database and cross-tenant disclosure are **not presumed**. Avoid global unique identifiers that leak a private place's existence.

## Minimum native service and information model

- **Native operation:** authorised create/edit/retire named places, manually enter and validate addresses and coordinates, maintain optional parent/child containment, query permitted places and versions, and correct inaccurate entries without an external map or geocoder.
- **Identity and revisions:** stable opaque place IDs; immutable material history of names, address/geometries, hierarchy, validity and evidence; optimistic version checks; separate effective date and recorded date using Clock semantics. A changing site address must not silently rewrite historic Event or Asset meaning.
- **Geometry and precision:** distinguish point, polygon/area, address-only, unknown/unlocated and approximate location. Explicit coordinate reference system (default interchange WGS 84 where applicable), axis order, resolution and accuracy/uncertainty; require a supported transform before comparing non-equivalent systems. Postal address, coordinates and geocoder result are **not interchangeable guarantees**.
- **Hierarchy and identity:** prevent self-parenting, cycles and unintended cross-tenant place links; typed relationships distinguish contained-in, adjacent-to, entrance-of and alias-of. Multiple names and localised labels need distinct language/provenance.
- **Lifecycle:** draft/unverified → verified/usable according to evidence and policy → revised → superseded/merged/retired; disputed or stale evidence may move status to review/limited-use. No permanent deletion bypasses lawful retention/holds. Retired IDs stay resolvable historically only for authorised consumers.
- **Consequence gate:** for safety-critical or financially consequential use, consumers must request current fit-for-purpose confidence, restrictions and separate domain safety evidence; Location alone cannot approve an event, occupancy or transport route.
- **Provider failure:** native manual operations remain available; external matching/route/geocoding status becomes unavailable/unknown, not fabricated. Provider updates are proposals until accepted under authorised source precedence.
- **Persistence:** only registered places, relationships, revisions, evidence references and a durable producer-owned outbox where events are emitted. Derived indexes/caches are replaceable. Any implementation must publish `STORAGE-REGISTER.md` and independent root `CONTRACT.md`.

## Idealised public inbound contract

| Input/source | Information or command; purpose | Validation, absence and authority |
|---|---|---|
| Authorised host/operator | `registerPlace`, `revisePlace`, `retirePlace`, `mergePlaces`, `resolveDispute`; tenant, type, name/address, optional parent, geometry, source/evidence, expected revision, idempotency key | Verify trusted caller/resource/tenant scope server-side, schema, geometry, parent cycles, provenance, policy and reference safety; conflict/rejected/unknown explicit. Host cannot assign a foreign tenant. Location owns result |
| Authorised domain owner | `proposePlaceReference` or request place resolution for Asset, Events, Warehouse, Logistics etc.; caller's domain reference and asserted location evidence | Proposal is not assignment or ownership; do not auto-publish provider facts. Domain retains placement decision; unresolved yields candidates/unknown, not arbitrary match |
| Configuration/host | Effective permitted precision, provider selection, place-type schema and allowed disclosure settings | Configuration owns validated settings; host resolves context; no override of security/legal floors; unknown policy means restricted behaviour |
| Identity/Authentication/Authorisation | Verified tenant/organisation context, identity/session/assurance and per-resource access decision | A caller-asserted tenant, event or provider webhook is not authorisation; deny or restrict unknown/expired decision |
| Privacy/Legal Compliance | Consent/retention/hold, lawful-purpose, jurisdiction-specific disclosure and processing constraints | Treat policy uncertainty as blocked/restricted for consequential disclosure; these owners retain legal/privacy authority |
| Integrations/external providers (optional) | Geocoding candidates, postal-address validation, map/geofence evidence, provider IDs, quality, licence, version and timestamp | Validate permitted source, licensing, precision, expiry and contradictions; no provider result automatically changes canonical record |
| Clock | Canonical instants, civil-time context, effectivity and time-zone interpretation when relevant | Never infer exact time zone or legal jurisdiction from approximate coordinates alone |
| Workflow/operator review (optional) | Approved correction/merge decision referencing pending change | Workflow coordinates approval; Location alone commits place revision upon valid current authority |
| Domain change/retirement notifications | Places referenced by third-party records, contextual validity concerns, changed site assignments | Domain owns its own relationships. Notification may trigger revalidation, but cannot rewrite external domain facts |

## Idealised public outbound contract

| Surface / consumer | Meaning and authoritative guarantee |
|---|---|
| `getPlace(placeId, asOf?, revision?)` — authorised domains/GUI | Tenant-scoped stable identity, descriptive place data, geometry/address precision, record status, source confidence, applicable revisions and disclosure redaction. Location guarantees **its record**, not physical occupancy, legal jurisdiction or current asset presence |
| `searchPlaces`, `resolveAddressOrCoordinates` — permitted user/domains | Ranked candidates and ambiguity flags; match type, provider/source, accuracy, stale/unverified status and freshness. No match is explicit; nearest result is not proof of exact address or lawful location |
| `getPlaceHierarchy`, `getAreaRelationships` | Versioned containment and geometric relationships within declared resolution; no promise that a point-in-polygon result determines statutory jurisdiction |
| `validatePlaceReference`, `assessPlaceFitness` | Whether an ID exists and is currently allowed for an explicitly stated purpose/required precision. `unknown`, `needs-review` and `unsupported` distinct from `valid`; not a safety certificate |
| `proposeGeocode`, `acceptProviderCandidate` (optional) | Candidate/evidence or authorised committed correction; provider unavailable or results uncertain without replacing native truth |
| `getLocationHistory`, authorised export/correction/retention response | Dated prior descriptions, aliases, supersession links and provenance, subject to tenant and privacy/hold rules |
| `PlaceRegistered`, `PlaceRevised`, `PlaceRetired`, `PlaceMerged`, `PlaceEvidenceDisputed` | Versioned committed Location change notices via producer durable outbox; at-least-once/replay possible. They trigger consumer re-evaluation, **not** external domain state transitions |
| Provider health/coverage/usage status (optional) | Provenance, last verification and operational state, never a guarantee of provider uptime, service eligibility or legal coverage |

**Shared context and invariants:** per-operation scoped tenant, trusted caller and resource permission, place ID/type/revision, expected version when mutating, idempotency/correlation for retries, effective/recorded time, geometry system and precision, evidence/provider licence provenance, redaction tier, result completion state and policy revision *where needed*. No universal mandatory envelope. Explicit `accepted/pending/committed/rejected/conflict/unknown`; historical queries require authorised as-of views. Avoid returning precise coordinates where approximate area suffices.

**Command/query/event semantics:** Commands are authenticated, authorised, checked for stale versions and idempotent on retries; acceptance is not completion. Queries have explicit visibility, precision, freshness and completeness, with no cross-tenant inference via error codes or search scores. Events are committed change notifications, versioned and replay-safe, transported by Message Queue from Location's outbox; no exactly-once distributed assertion or implicit permission grant from event receipt. Provider callbacks must be validated and reconciled, never blindly authoritative.

## Cross-capability public relationships

| Counterpart | Input needed by Location | Output supplied by Location / authority boundary | Dependence |
|---|---|---|---|
| Identity, Authentication, Authorisation | Trusted tenant, actor/assurance, scoped access decisions | Filtered place references, disclosure/command results; never creates tenancy or access | Essential security via host-supplied ports |
| Configuration, Clock | Effective supported place schema/precision/provider settings; canonical time | Location version/effectivity and configured operation outcomes | Essential semantics where used; can use safe defaults for optional settings |
| Privacy, Legal Compliance | Purpose, retention, holds, processing and disclosure constraints | Minimised place exports/deletions/holds evidence; no legal determination | Conditional on records/data and jurisdiction; enforce floors |
| Events | Event time, occurrence, venue reference and relevant purpose | Stable venue/place identity, resolved address, current revision and qualified place restrictions; **not physical occupancy/fire/accessibility authorisation** | Optional to Events; Events EVT-09 is preserved |
| Asset | Asset site reference and proposed place changes | Site/address/geometry and historical place ID; Asset owns placement, title and custody | Optional/conditional |
| Warehouse, Inventory | Warehouse/stock-location reference, mapped physical-place definition where needed | Site/building/area geometry; Warehouse owns internal bins, storage capacity/occupancy; Inventory owns stock status/quantities | Conditional; no generic stock-location takeover |
| Logistics, Order, Delivery | Address/place candidates and planned destination evidence | Normalised address, geocode precision, access/location description; Logistics owns route/shipment outcome, Order owns commitment | Optional/conditional |
| Profile, Customer/Supplier records | Permitted subject-controlled place reference only | Scoped location resolution without publicising private home/delivery address; Profile/domain owner retains personal address and purpose | Optional; no universal address mirror |
| Publisher, SEO, Search, Federation | Authorised publication scope and content/location reference | Approved public place description and coarse/precise disclosure, source/revision; Publisher owns publication, Search indexing, Federation remote propagation | Optional |
| Integrations | Provider connection status, credentials/terms, source evidence | Versioned candidate acceptance and reconciliation outcomes; Location retains its own records | Optional |
| Audit, Logging, Observability, Reporting | Audit/operational/reporting service ports as composed | Material change decision evidence, safe operational diagnostics and authorised data/report feeds; different sinks and owners | Conditional; no takeover of their evidence |
| Workflow, Scheduler, Message Queue, Notifications | Approved decisions, scheduled refresh requests, transport and delivery status | Pending review items, refresh tasks and committed place-change events; no workflow/queue/delivery ownership | Optional infrastructure |
| Localisation, Theme Manager, UI | Language labels/locale and semantic presentation vocabulary | Localisable names, address components/precision for display; presentation owns rendering | Optional UI |

**Acyclicity:** public interfaces pass through host ports/composition. Consumers import Location's stable contract; Location does not import domain implementations merely because domain-referencing operations exist. Reciprocal docs express responsibilities, not package dependencies.

## Configuration, IAM, provider and compliance

- Server-enforced permission levels: view coarse location, view exact restricted location, create/edit, verify/dispute, merge/retire, manage provider settings and export. The absence of a UI control is never enforcement; disabled/unpermitted resources must not leak via search, autocomplete, map pins or errors.
- Limit precise residence, child, employee, sensitive service-site and live-location disclosure by purpose and approved scope. Opt-in collection of device GPS is **not** a default Location feature; platform must not silently establish tracking.
- UK GDPR/GDPR applicability is fact- and purpose-specific. Record lawful basis, data minimisation, retention/erasure/correction, subject rights, third-country transfer and consent if required. Provider licensing may restrict storage, map caches and export. Legal Compliance determines legal duties; compliance is not inferred from implementation.
- Native service remains usable when external geocoders/maps fail, but must not claim verified routing, reachability, property boundary, time zone, legal jurisdiction or exact delivery.
- Use established geographic data conventions **where fit**: WGS 84/EPSG:4326, GeoJSON RFC 7946 for supported geometry, ISO 19111 coordinate referencing, ISO 19115 provenance/metadata, ISO 3166 country identifiers, postal addressing conventions and internationalised address formatting. Prefer mature permissive tools after independent licensing/security assessment, not a mandatory vendor or new format.
- Location data and place history are not a substitute for Audit: emit attributable changes with traceability and obtain an Audit receipt where policy requires. Logging/Observability receive appropriately minimised diagnostics, Reporting derives authorised aggregates.

## Conceptual GUI and host integration

**Optional separable GUI; core is headless.** Host owns navigation, authentication context, routing and responsive capability-dashboard integration. When enabled and authorised, a **Locations** sidebar entry opens a dashboard with search/list, place detail, history and status, place create/edit, parent relationships, uncertainty/evidence review and merge/retire workflow. Map preview is **optional** and must be accompanied by a keyboard-accessible non-map list and textual address/coordinates. Avoid assuming a third-party tile service.

- **Operator:** fast place lookup, permitted label/address and clear unverified/stale warnings; mobile-friendly low-training controls. Do not expose prohibited precise locations.
- **Manager:** create/correct places, resolve duplicates, compare sources, see domain references and impact of renaming/retiring (without editing domain placements).
- **Administrator:** place-type policy, precision and disclosure tiers, provider configuration, access role mapping, import/export and reconciliation status.
- **Denied/empty/offline:** no location or pin leakage; actionable no-result/unknown/multiple-match; degraded no-map experience; explicit provider failure. Do not suggest a failed lookup proves a place does not exist.
- **Design:** WCAG 2.2 AA, semantic HTML, complete keyboard and screen reader support, non-colour status, zoom/reflow, touch usability, BCP 47 localisation, international addresses and right-to-left text, Theme Manager tokens, locale-neutral domain codes and labelled text alternatives. Host test-template sidebar is an example pattern, **not** an automatic registration contract.

## Contract acceptance scenarios (conceptual; not executable tests)

1. Authorised tenant registers an address-only named site with no geocoder → stable tenant-scoped ID, `unverified` precision, revision, committed change; Location owns place.
2. Operator supplies ambiguous postcode/address → multiple ranked candidates with source/quality and **no automatic arbitrary match**; Location owns match assessment.
3. Correct an address with a matching expected revision → new current revision; prior Event/Asset references can resolve historical meaning; Location owns place history, domains own their associations.
4. Concurrent conflicting edit or replayed create key → conflict or same prior committed result; no duplicate place ID; Location owns.
5. User from another tenant searches private coordinates → denied or privacy-preserving non-disclosure; Authorisation owns decision, Location enforces.
6. Event cites a venue whose capacity/fire status is unknown → Location supplies only place facts/restriction provenance; Events must not infer safe authorised occupancy.
7. Asset moves buildings → Asset changes assignment after its own validation; Location does not move the asset when place geometry changes.
8. External geocoder unavailable/licence revoked → manual place records and authorised queries continue; provider match is unknown/unavailable, no fabricated route or confidence.
9. Merge duplicate places referenced by domains → preserve original IDs, redirect/version, publish change; consumers decide their reassociation with confirmation.
10. Tracking/mobile app submits live user coordinates → generic permanent tracking is unsupported; obtain an appropriately scoped separate domain/privacy design.
11. Provider candidate contradicts manually verified evidence → review state with both sources and staleness; do not silently overwrite.
12. Retention/hold or erasure request → apply Privacy/Legal Compliance rules; preserve mandatory protected history and erase eligible data, with explicit result.

## Classification of decisions and outstanding work

**Established:** accepted governing server-side access, capability/public-contract boundaries, separable presentation, privacy/WCAG/i18n, producer-owned outbox and acyclic composition obligations; previously documented Events EVT-09 expectation.

**Proposed (not approved):**
- **LOC-01:** retain Location as Platform candidate for reusable place/spatial-reference identity and revision lifecycle, not global location tracking.
- **LOC-02:** registered places and their provenance are Location-owned; resource placement, private profile addresses, occupancy and legal property facts remain with owners.
- **LOC-03:** native manual place/address-only support; provider-neutral optional geocoding/maps; uncertainty, geometry precision and versioned historic views.
- **LOC-04:** explicit permission and purpose-based precision/disclosure; no implicit cross-tenant sharing, live tracking or inferred jurisdiction.
- **LOC-05:** qualified public commands/queries/events, source precedence, idempotency, replay and durable outbox; no distributed exactly-once promise.
- **LOC-06:** optional headless-compatible GUI with list-first fallback, separate operator/manager/admin experiences and server-enforced access.

**Open owner decisions:** **LOC-07** whether public shared geographic gazetteer data merits a separate trusted common-data owner/port or stays evidence from provider; recommend optional port, no global private master. **LOC-08** whether Location should own complex indoor floor plans/graph navigation or only building/floor/room identifiers and simple containment; recommend latter, specialist navigation separately if justified. **LOC-09** whether any generic geofence trigger lifecycle belongs here or in a distinct operational owner; recommend Location owns geometry only, trigger/observations elsewhere. **LOC-10** restrictions on place names/labels and cross-tenant publication; recommend restricted-by-default, explicit publication through Publisher/domain owner.

**Technical investigations:** precise CRS/GeoJSON profile, address-quality datasets for supported jurisdictions, licensing, suitable open-source spatial libraries, migration and geospatial indexing, threat/privacy assessment. **Implementation alignment:** future root CONTRACT, storage register, provider port and host acceptance; none claimed available. **Acceptance:** composed host and CI must verify authorisation, contracts, keyboard access, DST/as-of semantics, privacy and negative cases. This review is **not signed off**, nor does it approve implementation, legal compliance or merge.

## Events interface reciprocity — 18 November 2026

**Events EVT-09 (18 November 2026; technical interface requirement):** [Events](../events/capability-record.md) needs a place/venue reference, location and suitable versioned location restrictions from Location, with physical occupancy/fire/accessibility suitability obtained from the actual authoritative venue/Asset owner where Location does not own those facts. Events supplies planned occurrence time, status, change/cancellation and affected location references. Missing essential current safety restrictions cannot be presented as authorised occupancy. No direct domain-store access or Events takeover of location/venue facts. [Decision and contracts](../../../reviews/events-contract-attendance-and-handover.md).
