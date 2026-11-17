# Capability Record — Clock

## Capability Name
`clock`

## Status
**Established** Foundation responsibility in the governing catalogue. **Verified contract evidence:** existing `nuxt-layers/clock` root `CONTRACT.md` on `master`; development acceptance claimed there, not independently re-run in this conceptual review. Installed/configured/operational/enabled/authorised are host-specific and not inferred. **Conceptual design:** P-CLK-01 through P-CLK-05 approved by the project owner on 17 November 2026. CLK-01 provenance direction approved; CLK-02 ownership refined as set out below. This does not grant implementation authorisation.

## Purpose
Clock is the platform's independent, deterministic temporal semantics service. It gives consumers one explicit vocabulary for instants, calendar dates, local times, zoned times, DST and time-zone rules, conversion, arithmetic, comparison, formatting and validated protocol interchange. It prevents each capability from implementing conflicting date and time interpretations. It does **not** determine when a booking is valid, when a legal deadline applies, when a scheduled job executes, or whether an operation is authorised.

## Evidence and governing authority
- Governing `nuxt-layers/architecture-rules` `master`: `eaca8cfd33e292a43e9552ad8e2946295e168472`; `docs/architecture.md`, `docs/platform-charter.md`, `docs/catalogue.md`, `docs/capability-standard.md`, security, privacy, identity and presentation baselines; accepted ADR-0001, 0002, 0004, 0008, 0009, 0010, 0011, 0012, 0015 and 0016 where applicable. In particular, ADR-0012 gives the shared `now()` clock-port shape and 50-line Nuxt-host budget; ADR-0009 establishes headless-first optional separable presentation; ADR-0016 establishes jointly acyclic declared contract/extension dependencies.
- Blueprint `nuxt-layers/architecture-blueprint-review` `master`: `ff02a072911439c13151e9e827edaa88b710ba2a`; README, working catalogue/register, classification gate, prior findings and booking/configuration reciprocal notes. Blueprint material is not normative.
- Implementation `nuxt-layers/clock` `master`: `96e71c08634334527e281bf62ceca18a7b256a36`, published root [CONTRACT.md](https://github.com/nuxt-layers/clock/blob/master/CONTRACT.md). The implementation claims independent consumption, Quality acceptance and 50-line composition verification; not a formal release. No private implementation inspection performed.
- Existing related root contracts reviewed where available: Configuration and Profile; Booking/Scheduler conceptual records are **not** implementation contracts. The `booking` and `scheduler` implementation root `CONTRACT.md` could not be retrieved and their interfaces are not asserted as implemented.
- Governing authority prevails over working proposals and implementation evidence. This review changes no governing rule.

## Architectural classification and ownership gate
- **Current classification:** Foundation capability; **recommended disposition:** retain as independent, largely stateless semantic capability with an existing documented Nuxt adapter and framework-independent consumer surface.
- **Distinct owner:** temporal type meaning, strict validation, clock-service behaviour, deterministic conversion/formatting and error semantics; it owns **no durable business records, preference records, tenant records, audit trail or business lifecycle**.
- **Alternatives:** a generic stateless library would suffice for some operations, but the established catalogue ownership, shared trusted clock port, unified consumer contract and existing cross-runtime integration justify retaining the named capability. Classification is already governing; no new repository or service is requested.
- **Persistence:** none; no domain schema, migrations or outbox. Time-zone rule data may be supplied/bundled as non-business reference data; cache/telemetry belongs to its respective operator.
- **Dependency:** consumer capabilities use Clock's public contract or structurally equivalent Clock port; Clock must not import those consumers. Mere conceptual relationships do not create package dependencies.
- **Presentation:** headless by default; no standard Clock dashboard or CRUD. Host-controlled settings and optional developer diagnostics are not authoritative Clock-owned screens.

## Dependencies
Runtime temporal/locale/time-zone facilities needed to deliver the published semantics; host-supplied trusted `now()` provider when required for deterministic tests or server authority. Clock has no mandatory dependency on Identity, Configuration, Profile, Scheduler, databases, message queues or third-party network time services. A caller that needs a legally authoritative time source must separately establish and validate the trust properties of its server/host environment.

## Optional integrations
- Configuration/Profile via the **host's** approved effective-preference resolution and scoped disclosure; never a Clock-owned preference lookup.
- Integration adapters may request validated protocol-time conversions, but external providers do not acquire temporal-rule ownership.
- Host monitoring may observe clock/runtime/tzdb health or drift through approved operational facilities; no background synchroniser, NTP client or clock-governance service is proposed inside Clock.

## Version and availability
Implementation `master` SHA stated above. Existing contract describes Nuxt and framework-independent consumers, supported runtime requirements and a private development package, not a released artefact. Run-time acceptance is a separate verification obligation. Capabilities may use deterministic Clock functions independently of a browser, database, IAM or external provider.

## Capabilities offered — native functionality
**Established in published implementation contract:** `now`, `today`, strict canonical `parse`, `isValid`, `serialise`, `format`, `parsePattern`, `formatPattern`, `parseInterchange`, `formatInterchange`, `toZone`, `resolveLocal`, `toInstant`, `add`, `compare`, `difference`, `midpoint`, `isValidTimeZone`, `timeZones`; `createClock`, Nuxt `useClock`, server `useServerClock`; typed `ClockError`. The existing contract sets documented precision, valid ranges, pattern grammar, supported interchange formats and failure codes. It provides no database, HTTP endpoint, events, permissions or GUI.
**Conceptual invariant:** distinguish an instant (absolute point), a date/time without a zone (not an instant), a zoned date/time (zone + offset), elapsed time and calendar time. Never infer a time zone, assume 24 hours in every civil day, accept ambiguous DST resolution without a stated policy, or use localised display strings as storage formats.
**Proposed investigation:** assess explicit rule-data/version provenance for future-sensitive scheduling, legal deadlines and historical re-evaluation. Do not promise reproducibility of a past calculation after time-zone database updates without capturing the applicable rules/version and original interpretation context.

## Conceptual information and lifecycle
- **Input temporal values:** typed canonical instants, calendar dates, times, local datetimes and zoned datetimes; well-defined arithmetic quantities, patterns and interchange format declarations.
- **Interpreting context:** explicit IANA time zone, disambiguation policy, locale, hour cycle and calendar/elapsed rule. Local-time resolution may yield zero, one or more candidate instants; the caller must decide policy.
- **Clock source:** trusted server-supplied time for decisions, or injected deterministic time for test; presentation device time is never a trusted security authority.
- **Lifecycle:** requests are evaluated without Clock-owned durable state. A value is validated/converted/formatted or rejected. There is no Clock-owned business transition, retention or migration of customer records. Changed tzdb/runtime rules can affect future interpretations and require monitoring/recalculation by the owning business capability.

## Idealised public input interfaces (conceptual contract)
| Source / class | Information or command | Purpose and owner | Validation, requirement and failure |
|---|---|---|---|
| Authorised application or consumer / **command** | Typed canonical temporal values; parse, format, validate, convert, compare, arithmetic requests | Clock owns interpretation; business consumer owns source meaning | **Essential to operation**. Reject malformed, out-of-range or incompatible values; no silent coercion |
| Business capability / **source facts** | Jurisdiction or event's effective date, named time zone, schedule/expiry/deadline basis and desired DST policy | Caller owns rule and time-zone *selection*; Clock checks semantics | **Conditional**. Missing zone or disambiguation for required resolution: reject or return explicit ambiguity, never guess |
| Host / **configuration context** | Valid locale/time zone/hour cycle and optional explicit patterns, request-scoped overrides | Configuration/Profile/host own effective values and disclosure | **Optional** for generic service, **conditional** for personalised display. Invalid overrides fail explicitly; safe documented defaults for standalone operation |
| Trusted host / **time provider** | Current instant via structurally documented `now()` port | Host owns time-source trust; Clock interprets and exposes it | **Conditional** for authoritative security/business actions. Invalid/missing injected value fails; client clock never silently substitutes |
| External integrations / **external evidence** | Protocol-defined timestamp text/number and declared interchange format | External provider owns emitted evidence, consumer owns acceptance; Clock validates representation only | **Optional**. Reject unknown/ambiguous/unparseable formats; validation does not establish authenticity |
| Host/runtime / **reference data** | Time-zone and locale rules supported by the running environment | Runtime/provider is rules-data source; Clock guarantees exposed interpretation for its documented version | **Essential to zone operations**. Unsupported/unavailable/inconsistent rules fail; do not fabricate zone offsets |
| Authorisation/Privacy/Legal Compliance / **policy context** | Caller-specific authority and disclosure constraints applied by consuming server | Those capabilities and domain owner retain policy authority | **Conditional**, enforced **outside** Clock. No Clock acceptance is permission to reveal or act upon protected business data |

## Idealised public output interfaces (conceptual contract)
| Output / recipients | Meaning and authority | Status, provenance and disclosure |
|---|---|---|
| Validated typed value / all consumers | Clock confirms syntax, type/range and temporal semantics, **not business truth** | Valid or rejected; preserve value kind, precision and context; no tenant data implicitly attached |
| Current instant or date / trusted server consumer | Current reading from specified clock source; business/security authority depends on that source | Successful reading or failure; provenance is caller-provided source/trust context, not a Clock security certification |
| Zoned conversion / Booking, Scheduler, Billing, Audit and other consumers | Resolved instant/offset for explicitly identified zone and disambiguation | Resolved or ambiguous/nonexistent/rejected; zone/policy supplied by caller; no reservation or job confirmation |
| Calendar/elapsed arithmetic and comparison / consumers | Deterministic temporal result under specified semantics | Result or typed error; original operands and rule selection retained by domain owner if auditability needed |
| Human-readable output / host presentation | Display string under explicit locale/zone/pattern; may lose precision | Formatted result, not canonical storage; host handles permission, accessible labels, scope and SSR consistency |
| Interchange conversion / Integrations, IAM, Notifications and protocol consumers | Conformance to a documented named timestamp representation within supported precision/range | Parsed/formatted result or typed rejection; original source authenticity remains external |
| Time-zone availability / consumers and authorised settings UI | Valid zone identifiers and supported primary-zone options | Valid/invalid/list; environment/tzdb provenance is an **investigation** for audit-sensitive use |
| Typed error / every caller | Stable public failure reason, no internal exception leakage | Invalid config/input/zone/pattern, ambiguity, nonexistence, incompatible types or unsupported operation |
| **Events / none** | Clock owns no durable business-state transitions to announce | **Deliberately omitted**: domain owner emits deadline/reservation/schedule/audit events; no fabricated Clock outbox |
| **Reporting/audit records / none** | Clock supplies semantics, not business history or telemetry ownership | Callers and platform observability/audit owners record relevant context, with privacy minimisation |

The published root contract is the actual implementation surface; this table is its **conceptual interpretation**, not a declaration of additional APIs.

## Interaction models
**Commands:** pure service invocations (parse/convert/resolve/format/arithmetic) returning a result or structured error; no business command acceptance, transaction, idempotency key or lifecycle transition inside Clock. Repeated calls with identical inputs and identical temporal rules/source should be deterministic. `now()` and `today()` depend on the selected clock reading.
**Queries:** current time, zone validation/availability and immutable result calculation; queries never expose business records. Locale output must never be mistaken for a persisted canonical value.
**Events:** deliberately none in the documented implementation; business owners publish their own material changes and operational systems log/observe health separately. A future reference-data-change signal, if useful, must undergo separate ownership/contract review.

## Shared context, provenance and invariants
The consumer supplies tenant/subject/resource/correlation **only where its domain operation requires them**; Clock itself need not create or persist these. Preserve, at the authoritative caller: original source representation where evidentially necessary; canonical instant/date; intended zone; governing jurisdiction/policy; chosen ambiguity policy; relevant rule/configuration version; correlation/operation identity and trusted timestamp source. This is not a universal request-object requirement.

1. **Ownership:** time interpretation does not confer business authority. No Clock tenancy database, no preference duplication, no schedule/booking ownership.
2. **Safety:** server-side access and expiry enforcement; never trust user-controlled browser time for security. Reject unclear type, offset or DST cases by default.
3. **Precision:** conversion and serialisation must honour declared precision and documented lossy formatting; no hidden day/24-hour equivalence.
4. **Consistency:** preserve absolute instants through zone conversion; avoid reinterpreting a canonical instant as local time.
5. **Failure:** stable typed validation errors, no fabricated fallback when authoritative time source or required zone rules unavailable; explicit unsupported operations.
6. **Availability:** pure core requires no database, identity, network or provider lifecycle; optional integration absence does not disable generic temporal services.
7. **Security/privacy:** Clock input/output must not bypass domain Authorisation or expose protected information; logging of values requires classification and minimisation.
8. **Versioning:** changing rules, pattern conventions or precision can alter results; changes require compatibility and regression evidence.
9. **No distributed-delivery claim:** Clock itself has no durable events or delivery semantics.

## Configuration, security and compliance
- **Configuration:** declarative approved scoped settings, provenance and overrides; Clock validates semantics. Existing Configuration contract advertises host-declared six `clock.*` presentation keys, **not built-in keys**. The host resolves effective values.
- **Profile:** canonical personal `locale` and `zoneinfo` are distinct from organisation defaults; avoid competing preference stores. Effective precedence/locked preferences remain a broader proposed integration, not Clock's decision.
- **Identity / Authentication / Authorisation:** tenant identity, sessions, privileges and access decisions remain outside Clock. Server business owner must enforce them even for a timestamp supplied by Clock.
- **Legal Compliance / Privacy:** jurisdictions, legal calendars, retention periods, evidential requirements and holds are determined by their authoritative policies and domain owners, not by Clock. Clock can calculate a caller-defined calendar deadline but cannot certify it is lawful; specialist legal assessment where required.
- **Integrations:** adapters validate external date formats and preserve provenance; they never unilaterally redefine local business deadline policy.
- **Audit / Logging / Observability / Reporting:** domain owner retains material audit events; Logging records sanitised errors and operational faults; Observability records latency/error rates/time-source health; Reporting consumes authorised derived facts. Clock should not emit sensitive temporal inputs as default telemetry, nor become a second audit store.
- **Message Queue / Workflow / Scheduler:** each owns transport, workflow or execution respectively. Clock supplies typed time calculations through published functions/ports without queue/workflow dependency.

## Cross-capability relationships and absence behaviour
| Cooperating owner | Clock receives | Clock supplies | Requirement / unavailable behaviour |
|---|---|---|---|
| Configuration / Profile / host | Approved effective viewer values and zone selection | Validation and formatted results | Optional personalised display; default standalone formatting, never reuse another viewer's values |
| Booking / Events / Asset | Event occurrence, venue/resource zone and caller-owned booking rule | Ambiguity-safe time resolution and elapsed/calendar calculations | Conditional; reject unclear conversion; owner remains responsible for reservation validity |
| Scheduler / Workflow / Task | Requested schedule time or due-date rule | Canonical instants, calendar arithmetic and DST interpretation | Conditional; consumer must not execute based on untrusted client clocks |
| Billing / Accounting / Payroll | Domain-defined accounting or settlement periods and jurisdiction | Date boundaries and elapsed/calendar calculations | Conditional; no financial posting or statutory policy authority transferred |
| Authentication / Authorisation / Identity | Session/credential/grant expiry instant and trusted time source as controlled by their caller | Canonical comparison/interchange | Conditional; absence of authoritative clock must fail closed for security-sensitive action |
| Integrations / Notification / Publisher | Named protocol time format, date/time source | Strict interchange conversion and human-readable display | Optional; invalid external timestamps rejected and reported to originating adapter |
| Audit / Logging / Observability / Reporting | No direct sensitive event stream required | Error classes, diagnostics/temporal semantics for owner-supplied evidence | Optional; these owners decide evidence capture, retention and disclosure |
| Legal Compliance / Privacy | Caller-identified authoritative jurisdiction/rule | Calendar/zone calculation only | Conditional; Clock cannot decide whether rule applies or disclose protected facts |

All edges are conceptual public-contract interactions; host composition or structural ports avoid a bidirectional dependency on Clock's consumers.

## GUI and host presentation (Phase 6A)
**Headless is the correct default.** The published Clock implementation supplies **no screens, pages, date picker, dashboard or HTTP routes**. Its host integration does not need a Clock sidebar entry. Ordinary users see Clock only as time/date formatting, time-zone-aware forms and accessible contextual information in business screens. Preference editing belongs in the host's Profile/Configuration presentation, where authorised. A developer/operator diagnostics screen (clock-source status, supported zone/rule version, SSR consistency, sample DST resolution) may be added **as an optional host-owned or operational view**, not an independently justified Clock business dashboard; access is server-authorised, information sanitised.
The representative `nuxt-layers-test/application-test-template` host-owned sidebar/dashboard pattern is relevant for demonstrating consumer screens; it does not imply auto-registration or require modifying that repository. Any optional screen must remain separable, WCAG 2.2 AA, accessible with explicit zone labels, internationalised, themed through Theme Manager vocabulary, SSR/hydration stable, and must never invoke protected domain decisions on the browser alone.

## Conceptual contract acceptance scenarios
| Scenario / input | Expected behaviour / output | Authority |
|---|---|---|
| Native standalone: canonical instant + explicit zone | Valid zoned conversion, reversible instant, no network/database/IAM | Clock semantics; caller owns meaning |
| Booking recurrence at DST gap/overlap | Reject ambiguity by default; explicit policy resolves when provided; no implied confirmed booking | Clock conversion; Booking confirmation |
| Cross-capability deadline: seven calendar days in named jurisdiction | Caller supplies calendar rule and zone; Clock calculates DST-aware boundary, not 168 elapsed hours by assumption | Domain/legal owner chooses policy |
| Tenant/user preferences | Host supplies authorised resolved locale/zone; presentation consistent for SSR/hydration, no cross-tenant preference leakage | Configuration/Profile/host |
| Invalid zone, impossible date, ambiguous local time | Stable typed error, no guess or silent coercion | Clock |
| Repeated deterministic request with fixed provider | Identical validated result; no second write, event or idempotency ledger | Clock |
| Spoofed client time for session expiry | Server does not treat it as authoritative; protected operation denied if reliable time unavailable | Authentication/Authorisation + host |
| External malformed timestamp | Named protocol parser rejects and adapter retains provenance/error | Clock syntax; Integrations evidence |
| Historical event after zone-rule changes | Stored instant remains unchanged; reconstruction requiring historical policy/version reports missing evidence rather than guaranteeing same civil outcome | Business owner; version-provenance investigation |
| Unsupported operation or missing runtime feature | Explicit unsupported/initialisation failure; no fabricated result | Clock/runtime |
| Presentation unavailable | Core still operates; no mandatory sidebar or screen | Clock core/host |
| Audit and reporting consumer | Domain owner emits authorised auditable event containing its time evidence; Clock does not claim to deliver it | Audit/Reporting/domain owner |

## Findings and decision discipline
**Established E-CLK-01:** Clock is a Foundation capability in the governing catalogue. **Established E-CLK-02:** headless implementation contract currently supplies the documented pure/date-time operations and no database, events, UI or HTTP. **Established E-CLK-03:** Profile/Configuration/host own user/scoped preferences; Clock interprets validated overrides. **Established E-CLK-04:** ADR-0012/0016 composition and acyclic dependency requirements apply.

**Owner-approved P-CLK-01 (retain ownership):** keep Clock as independent stateless semantic Foundation capability, not a scheduler, preference store or time synchronisation platform. **Owner-approved P-CLK-02 (contract):** treat the published operations as the native baseline and the inbound/outbound tables above as the idealised consumer responsibilities. **Owner-approved P-CLK-03 (GUI):** no Clock-owned business screens; host-owned preference/diagnostic presentation only when justified. **Owner-approved P-CLK-04 (observability):** capture time-source/rule-version health via operational capabilities and caller-owned evidence, never default raw per-user input logging. **Owner-approved P-CLK-05 (security):** fail closed if a trusted time source is required but unavailable.

**Agreed conceptual decision CLK-01 — temporal rule provenance (17 November 2026):** record enough explicit time-zone rules-data version and resolution provenance for high-assurance historical explanation or reproduction where needed, without making Clock the owner of business evidence. Exact API shape, version capture granularity and reproducibility limits remain technical investigations; current implementation contract does not assert this metadata.

**Agreed CLK-02 direction (17 November 2026), with operational assurance details proposed:** preserve Clock's synchronous, injected `now()` provider. Configuration may govern an approved, restricted deployment-level choice of upstream NTP/NTS sources, subject to Infrastructure/operator-enforced allowlists, deployment controls and audit; Profile has no role in such choices. Infrastructure owns host OS time synchronisation and provider connectivity; Observability owns source availability, measured offset/drift, freshness and alert histories; Logging owns technical diagnostics; Audit owns accountable policy/selection changes. Clock consumes trusted host time and exposes temporal semantics rather than initiating per-request NTP calls, owning a daemon or claiming source verification. Where source assurance is required and unavailable, the owning security-sensitive server operation fails closed. NTP server selection is a privileged infrastructure policy, not an arbitrary tenant/user preference. Candidate sources include NTP Pool, Cloudflare (NTS), Google Public NTP (leap smear; do not mix with non-smearing sources), Amazon Time Sync, and NIST; approval requires verifying operator terms, service reachability, client authentication and leap handling. Exact host configuration mechanism, telemetry interfaces, allowable fallback, acceptable skew and alerts remain technical investigations.

**Technical investigations:** tzdb release differences and reproducible historic civil-time resolution; standards-specific leap second handling; runtime clock drift/monotonic elapsed time requirements; literal/locale pattern compatibility; parity across browser/SSR/runtime; long-lived calendar recurrence materialisation and boundary instants. Resolve with evidence rather than manufacturing approval decisions.

**Implementation alignment:** publish any approved extension first as an explicit versioned root `CONTRACT.md` change in a later implementation PR; do not represent CLK-01/02 as implemented. Reconcile only if an actual gap is demonstrated against accepted ADRs. No Clock implementation files changed.

**Acceptance and verification:** independent consumer from root contract; 50-line Nuxt composition; canonical types, precision, DST, cross-zone invariance and deterministic clock injection; server-time security; no private imports, unexpected persistence, events or UI; browser/SSR parity; representative integration scenarios; source-rule version and historical interpretation evidence if CLK-01 is later accepted. This is conceptual analysis only; no CI, builds, end-to-end checks, legal certification or operational audit performed.

## Architectural consequences and sign-off
Retain established Foundation catalogue/register classification. No reclassification, schema, new capability, new provider, universal request object, new ADR or governing edit is proposed. Add reciprocal Clock-contract links to Configuration and Scheduler records without completing their reviews. Booking already documents the Clock boundary. **Conceptual sign-off status: P-CLK-01 to P-CLK-05, CLK-01 provenance direction, clarified CLK-02 ownership/source selection, CLK-03 assurance boundary and CLK-04 wall-clock/monotonic boundary are approved as conceptual decisions. The eight completeness topics are documented; detailed assurance thresholds, versioned provenance implementation, host elapsed-timing interface assessment and acceptance remain deferred.** PR review is not implementation authorisation or normative adoption.

## Owner approval and NTP governance clarification (17 November 2026)

**Owner approved P-CLK-01–P-CLK-05 and CLK-01; CLK-02 refined.** Keep the `ClockPort.now()` interface in Clock. An optional deployment-controlled NTP/NTS provider selection may be declared and governed through Configuration, but its effective application to the host operating-system time synchroniser is Infrastructure's responsibility. Never permit an arbitrary tenant account or Profile preference to reconfigure a shared server clock. Authorised configuration change requires policy validation and accountability, not only a UI selection. The operator screen belongs to Infrastructure's optional administrative presentation (or host operational console) and consumes Observability health; Configuration presents approved setting change controls but does not own live diagnostics. 

**Proposed conceptual inbound/outbound NTP relationship:** an authorised infrastructure operator proposes a provider identifier, permitted endpoint(s), protocol/security mode, leap-smear compatibility policy, fallback rules and effective revision into Configuration's governed setting surface. Infrastructure consumes the approved revision and returns applied/rejected/degraded sync status to operational monitoring; Observability serves current/historical clock offset, source identity, sync freshness, uncertainty and alert status to authorised operators; Logging captures sanitised faults; Audit receives privileged change evidence. Clock receives a trusted `now()` supplied by the host and, where approved by CLK-01, explicit rules-data provenance. A request to Clock must never implicitly make an outbound NTP network query. External hostname presence alone is not verification; prefer NTS where available, define bounded trust criteria, and do not mix differing leap-smear policies (IETF RFC 8633).

**Operational failure and recovery:** missing/invalid configuration cannot silently activate an arbitrary server; an unreachable or unauthenticated source is degraded, not verified; loss of sync is surfaced explicitly and alertable; previously configured policy and applied source revisions must be distinguishable. Infrastructure may continue on a bounded, pre-approved holdover policy, but downstream expiry/financial/security decisions must independently enforce their required assurance thresholds and fail closed when unmet. Clock's pure deterministic conversions remain available even during NTP failure. No new implementation/API is claimed.

**Sources:** [Cloudflare NTS](https://developers.cloudflare.com/time-services/nts/), [Google Public NTP FAQ](https://developers.google.com/time/faq), [NIST ITS](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/internet-time-service-its), [IETF RFC 8633](https://www.rfc-editor.org/rfc/rfc8633).

## Approved UTC source classification and geographic selection (17 November 2026)

**Owner approval:** the project owner explicitly approved the Clock ownership model, the optional infrastructure-operated diagnostics screen, the NTP/NTS provider governance division, and the national-authority versus authenticated-service versus regional-pool distinction. These are agreed conceptual requirements, **not** a production provider approval, new Clock implementation contract or authorisation to operate an NTP daemon inside Clock.

### Canonical time and display time zones
NTP distributes a UTC-based time reference independently of the geographic position of the server. `Europe/London` (GMT in winter, BST in summer), `America/New_York`, `Asia/Tokyo` and other IANA zones describe civil-time interpretation, not different NTP time scales. A United Kingdom-based clock source can support the entire platform and all tenants' time zones. Source selection should reflect host location, latency, diversity, trust and assurance, **not** tenant display time zone. In the default shared-host deployment, ordinary tenants cannot select or modify the underlying host's NTP sources.

### Candidate source classes (evidence, not approved production endpoints)
| Class | Candidate / example | Interpretation and conditions |
|---|---|---|
| National reference authority | UK National Physical Laboratory, UTC(NPL), Teddington (Greater London); NPL Internet Time Service documentation lists `ntp1.npl.co.uk` and `ntp2.npl.co.uk` | UK reference service, not an alternative GMT/UTC time zone; confirm current endpoint availability, permitted access, support, authentication, service assurance and operating conditions before adoption |
| National reference authority | US NIST Internet Time Service (`time.nist.gov`) | National reference-source candidate; authoritative provenance is not by itself cryptographic transport authentication |
| Authenticated public time | Cloudflare `time.cloudflare.com`, with Network Time Security (NTS) support | Prefer authenticated server identity and NTP packet protection where supported; assess independent source/recovery policy and actual network reachability |
| Public service | Google `time.google.com` / `time1.google.com` through `time4.google.com` | Applies leap smearing and does **not** support NTS; do not mix with non-smearing sources in a synchroniser |
| Public service | Amazon `time.aws.com` / provider-specific Time Sync facilities | Candidate subject to deployment support, protocol authentication, leap behaviour and independent verification; no assumption of AWS hosting |
| Community regional pool | UK `uk.pool.ntp.org`, Europe `europe.pool.ntp.org`, other geographic regions via the NTP Pool Project | DNS pools select participating regional volunteer servers; geographic affiliation is not proof of national time-authority provenance or authenticated NTP |
| Community global pool | `pool.ntp.org` | Location-based community routing suitable for evaluation where risk policy permits; do not equate with a single verified laboratory |

The regional classifications offered by the NTP Pool Project are **geographical**, not GMT/EST/CET/AEST offset classifications. For UK deployments an approved UK/NPL or nearby European source may be reasonable, but no rule requires an Australian source merely because an Australian tenant displays local time.

### Proposed public relationships, safeguards and operational UI
- **Clock:** continues to receive trusted `now()` from the host and to supply deterministic semantic calculations; provides approved time-zone-rule provenance under CLK-01 when implemented. No on-demand NTP network requests, runtime preference storage, daemon, clock-synchronisation responsibility or general operational GUI.
- **Configuration:** governs deployment/host-scope, privileged, allowlisted source selection and change provenance where a dynamically governed setting is warranted. Host/infrastructure must remain ultimate authority over whether an approved setting can be applied to the operating-system clock; do not assume Configuration directly mutates OS services.
- **Infrastructure:** validates endpoint/identity, security mode (including NTS where available), leap-smear compatibility, peer diversity, connectivity, synchronisation policy, fallback/holdover, applied-versus-requested revision and recovery. Selection, configuration, actual sync and restoration belong here, not in Clock.
- **Observability:** receives safe live and historical offset, drift, uncertainty/error bound, last successful synchronisation, currently applied source, NTS/authentication state where available, alarms and trend metrics. A source's hostname does not prove its measured authenticity or accuracy.
- **Logging and Audit:** Logging owns sanitised operational faults and correlation; Audit owns accountable privileged configuration changes, source changes and consequential time-integrity/security events subject to its catalogue. Their records are not interchangeable.
- **Profile:** owns personal locale/zone preferences only; cannot choose a host NTP server.
- **Presentation:** Infrastructure or the host optionally offers an authorised **Administration → Infrastructure → Time synchronisation** page. It consumes approved settings via Configuration and current/history/alerts via Observability, clearly distinguishing requested and actually applied source, synchronisation status, current offset/uncertainty and last success. Clock has no mandatory sidebar dashboard. Screen follows host-owned navigation, Theme Manager semantic styling, WCAG 2.2 AA, i18n and server-side Authorisation.

**Failure and acceptance semantics:** invalid/unapproved sources are rejected; unavailable or unauthenticated sources are not reported as verified; failure of the synchronisation service is visible even when a last-known reading exists. Infrastructure may exercise only a defined, bounded holdover/recovery policy. Consumers that require a trusted clock for security or financial decisions must independently fail closed when the applicable assurance threshold is not met. Pure Clock conversion/parsing continues independently. The implementation review must investigate authenticated source trust, network failure, provider terms, multi-source resilience and incompatibility of leap-smear policies.

**External documentation for later technical verification:** [NPL Internet Time Service user guide](https://www.npl.co.uk/getattachment/products-and-services/Timing-services/Internet-Time-from-NPL/its_user_guide.pdf?lang=en-GB), [NTP Pool UK](https://www.ntppool.org/uk/zone/uk), [NTP Pool Europe](https://www.ntppool.org/en/zone/europe), [Cloudflare NTS](https://developers.cloudflare.com/time-services/nts/), [Google Public NTP](https://developers.google.com/time/), [NIST ITS](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/internet-time-service-its). The NPL guide is documentary evidence of offered endpoints, not proof of live availability at deployment time.

**Conceptual approval status:** P-CLK-01–05, CLK-01 and the clarified CLK-02 and source-classification/GUI boundaries are approved. Concrete host integration, exact assurance thresholds, technology choices and operational acceptance remain future design work.

## Approved invariant — UTC authority and local civil time (17 November 2026)

**Owner-approved and mandatory conceptual boundary:** All authoritative platform time readings originate from a **verified, explicitly approved internet UTC time source**, synchronised and assured by Infrastructure according to a governed policy. Clock receives the host-supplied trusted UTC instant and applies the explicitly selected **IANA regional/local time-zone rules**, including daylight-saving transitions, to interpret or present local civil time. The selected time zone does not select, replace or authenticate the upstream UTC source. Conversely, the geographic location or name of the UTC source does not determine the user's local time zone.

**Input:** trusted UTC reading from the host/provider and explicit IANA time-zone context from the authorised caller/host. **Output:** validated canonical instant and/or zone-specific local date/time, offset and ambiguity/disambiguation result. Configuration governs permissible source policy; Infrastructure verifies and operates upstream synchronisation; Clock validates and interprets local time; Profile/Configuration/host supply authorised display-zone preferences. A civil-time display must not be treated as a separate source of authoritative time. No consumer may rely on arbitrary browser/device clock readings for authoritative access, expiry, legal or financial decisions.

**Failure:** where authoritative operations require verification, an unverified, unauthorised, unreachable or insufficiently assured UTC source must not silently become accepted; the responsible server operation fails closed when its policy requires trusted time. Independently valid Clock parsing, conversion and calendar calculations do not require a live NTP connection. Source trust assessment, verification method and acceptable holdover/fallback remain technical design and acceptance questions. The invariant does not impose per-request NTP access inside Clock or promise that any cited public service has already passed verification.

## Final completeness review — eight concerns resolved (17 November 2026)

**Status and approval:** the project owner requested substantive treatment of all eight completeness findings, and approved the recommended CLK-03 and CLK-04 boundaries. This section is an agreed **conceptual responsibility and failure contract**, not a declaration that new implementation interfaces or operational assurance already exist. The documented implementation `CONTRACT.md` continues to define currently callable APIs.

### CLK-03 — trusted clock assurance, degraded operation and recovery (approved)

**Boundary:** Clock supplies typed UTC instant readings from the existing synchronous injected `now()` port and deterministic temporal transformations. It does **not** certify NTP source integrity, read Observability directly, maintain a synchronisation daemon, or decide security policy. Infrastructure must maintain approved/verified upstream UTC synchronisation and report an independently verifiable **applied source + assurance state**; Observability owns time-source health measurements and alert histories. The host composes an authorised, server-side assurance/health read port for domain consumers that require it. This is a **proposed conceptual port**, not a current `ClockPort` member or implemented API.

**Required conceptual assurance information:** host/source identity and approved policy revision; requested versus applied source; authentication/verification outcome (or explicit `unverified`); last trusted synchronisation; measured offset, uncertainty bound or equivalent quality indicator; age of measurement; synchronised/degraded/holdover/unavailable state; validity/expiry of any quality evidence. Every datum carries provenance, freshness and unknown/unavailable semantics. A successful `now()` alone is **not proof** of trusted UTC.

**Enforcement:** the protected business capability (e.g. Authentication/Authorisation, Billing or Booking) owns its risk-specific minimum trust/freshness and validates the assurance evidence server-side before decisions requiring authoritative current time. Unavailable, stale, unverified, contradictory or below-threshold evidence must not be treated as healthy. Such operations fail closed or follow a **pre-authorised, bounded holdover policy** where their owner demonstrably permits it; no unbounded silent downgrade. Clock's pure parsing, comparison, conversion and historical display remain usable during an NTP outage. Infrastructure owns source failover, recovery and monotonicity safeguards as far as its host clock permits; Observability exposes degraded and recovered states; Audit records accountable overrides, source-policy changes and relevant security failures; Logging records sanitised technical faults.

**Recovery:** policy-approved source re-establishment must be measured as healthy before protected traffic resumes; downstream owners re-evaluate expiry and queued/due work rather than assume timestamps or elapsed deadlines were unaffected. Host/source state revisions and uncertainty must be explicit. Avoid claiming end-to-end certification or exactly-once timing on the strength of a source status alone.

### CLK-04 — adjusted wall-clock time versus monotonic elapsed time (approved)

**Wall-clock UTC** identifies calendar instants, stored event timestamps, business due dates and jurisdictional civil-time conversions. It can jump forward or backward after synchronisation corrections, host suspend/resume, VM migration or manual/system changes; it is not an inherently monotonic interval counter. An instant has a defined interpretation but can be observed later than a newer wall-clock reading following a correction.

**Monotonic elapsed time** measures durations, retry/backoff budgets, operation timeouts and performance intervals against a host/runtime monotonic source. It is not convertible into an absolute UTC timestamp without a separately defined correlation; do not persist it as a cross-host or reboot-stable deadline. A monotonic source may have documented suspend/resume behaviours and must be evaluated in host-specific technical acceptance.

**Public contract direction:** maintain current `ClockPort.now(): Instant` and `difference` semantics (difference between supplied instants). Do **not** reinterpret `difference` as a monotonic measurement, nor silently add a monotonic method to the existing published interface. Consumers requiring elapsed timing may use their host/runtime's documented monotonic facility through composition; assess an optional common structural elapsed-time port only if multiple concrete consumers demonstrate a repeatable integration gap. Infrastructure and Observability assess step/slew corrections and drift; Scheduler owns trigger reconciliation and duplicate-safe execution, Authentication owns expiry acceptance and session rules, and domain owners remain responsible for their deadlines and idempotency.

**Adjustment failure scenarios:** backward jumps never automatically revalidate an expired credential or undo committed business outcomes; forward jumps never automatically justify an irreversible business action without independent rule/state checks. Scheduler and business owners examine missed/late due actions and reconcile; they do not assume each logical action ran once. Reject browser time as server security authority.

### Other completeness requirements — agreed scope and deferred mechanics

| Item | Conceptual requirement / ownership | Implementation or acceptance evidence still needed |
|---|---|---|
| **Time-zone database changes (CLK-01)** | Clock validates zones and supplies rule-data/version provenance when approved contract extension is implemented. Business owners retain original zone, local intent, resolution policy, rule/policy revision and canonical instant for reproducibility; future local-time bookings must be re-evaluated under explicit domain policy when rules change, without silently modifying confirmed commitments. | Runtime/tzdb version source, browser/server equality, zone links, migrations, notifications/recalculation rules and historically reproducible resolution with versioned data |
| **Leap seconds and leap smearing** | Infrastructure approves compatible upstream UTC source policies. Do not combine smeared and unsmeared sources in one synchroniser; Clock's published canonical parsing rejects leap-second notation. Domain timestamps retain documented interpretation and precision. | Confirm per-provider smear/step policy, synchroniser configuration, source diversity and leap-boundary acceptance cases; changing Clock's rejection rule requires a separate contract decision |
| **Calendar conventions** | Clock owns the documented proleptic Gregorian date arithmetic, explicit zone and elapsed-versus-calendar distinction. Legal Compliance, Configuration where authorised, and domain owners decide jurisdictions, business/working days, public holidays, local operating hours, cut-off rules and which deadlines are legally effective. Clock must not silently infer national holidays or promise statutory compliance. | Publish dedicated policy/calendar ownership through respective reviews if recurring cross-capability demand establishes it; test end-of-month, local-day and DST boundaries |
| **Deterministic testing and simulated time** | Existing injected `now()` permits fixed time at scoped consumer/test instances without mutable cross-request globals. Simulated progression, freeze/advance, DST gap/overlap, time jumps, source loss and recovery are **acceptance scenarios**; do not claim simulated progression is a built-in Clock API. No production global time override. | Verify fixed-time injection, stepping with test-owned provider, SSR/server isolation, monotonic tests via separate runtime source, and degraded authoritative operations |
| **Server/browser presentation consistency** | Host resolves authorised locale, IANA zone, hour cycle and explicit patterns before SSR; initial hydration uses the same values. A browser's guessed zone is opt-in and may only take effect through an intentional display update. Host avoids leaking another tenant/user's preferences. Display strings must never become canonical storage. | Cross-runtime deterministic snapshots for zone/rule version, locale patterns and DST, accessible zone labels, changed-preference re-rendering, fallbacks and failure surfaces |

### Explicit conceptual acceptance scenarios

| Input/event | Expected response | Owner |
|---|---|---|
| Verified NTP source and fresh assurance evidence, security-sensitive current-time check | Host passes trusted reading and assurance evidence; consumer enforces declared threshold, then makes its own authorised decision | Infrastructure assures, Clock interprets, security/domain owner decides |
| Upstream source becomes unreachable or quality stale | Observability reports degraded; protected operations fail closed absent approved holdover, while canonical conversions continue | Infrastructure/Observability and consumer |
| Approved source restored after a holdover | Measure new health and distinguish requested/applied versions; consumers re-evaluate expiry and pending work | Infrastructure + business owner |
| Host wall clock steps backwards after an expiry | Credential does not become newly valid solely because time stepped; no reversal of already committed event | Authentication/Authorisation |
| Host wall clock jumps forwards across scheduled runs | Scheduler reconciles missed/late work; handlers remain idempotent and business rules are rechecked | Scheduler + originating owner |
| Runtime monotonic source measures a timeout while UTC wall time is corrected | Timeout measurement remains elapsed-time based under stated host behaviour; no fabricated absolute timestamp | Host/consumer |
| Future recurring booking faces a tzdb change | Booking preserves local intent and confirmed state, determines re-evaluation/notification; Clock exposes documented conversion and provenance | Booking and Clock |
| Approved smear-capable source accidentally mixed with non-smear peers | Infrastructure configuration is rejected or flagged degraded; quality cannot be asserted healthy without testing | Infrastructure |
| Local holiday or working-day cutoff presented as a deadline | Domain/legal policy supplies holiday calendar and zone; Clock calculates only specified temporal operations | Domain/Legal Compliance |
| Fixed `now()` provider, simulated jump and browser/server first render | Predictable tests and equivalent initial display, with intentional post-hydration preference changes | Clock test host + presentation host |

**Closure:** no further capability, independent persistence owner, UI or universal time object is justified. CLK-03 and CLK-04 are approved conceptual boundaries. Technical questions (trust thresholds, assurance/port shape, leap sources, correction behaviour and rule-data replay) are delegated to detailed implementation/host acceptance without reopening these decisions. The Clock conceptual scope is ready for owner PR review; passing CI and real production time assurance are separate acceptance matters.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Clock owns `now()`, temporal interpretation, zones and formatting; Configuration supplies approved versioned presentation defaults when registered. Privileged NTP source settings versus Infrastructure static config remain open; tenant display zones cannot control UTC synchronisation. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-07 (Option A) for Configuration's boundary:** Infrastructure is authoritative for NTP/NTS source choices and their application/verification. Clock retains injected trusted time, temporal validation and display semantics. Prior optional Configuration-managed NTP selection remains a historical proposal, *not* the selected architecture; the already approved invariant separating UTC authority and time-zone preferences remains in force.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.
