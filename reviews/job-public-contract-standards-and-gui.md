# Job — plain-English contract, cooperation, standards and presentation review

**Status:** Companion to owner-approved conceptual JOB-01–JOB-09; non-normative; not an implemented root `CONTRACT.md`, legal opinion or sign-off on technology choices. [Job capability record](../docs/capabilities/job/capability-record.md) · [draft PR #84](https://github.com/nuxt-layers/architecture-blueprint-review/pull/84). Prepared 20 November 2026.

## 1. Issues to consider

Job now **defines employment positions**, not vacancies or employment. Its position identity, owner, permissions, descriptive data, skill/qualification requirements, revisions, approval, effective dates, historic retrieval, retirement and lawful retention need explicit business rules. A position can exist without an approved vacancy or employee. Its grade/pay-band *reference* is not advertised salary or an individual employee's agreed wage. Position validity must be checked when Recruitment opens vacancies or Employment records an assignment, without Job taking either domain's state.

Key remaining design issues: local versus recognised occupation and skills taxonomies, employer-specific classification and titles, valid requirement alternatives, sensitive internal-grade visibility, approvals and segregation of duties, future-dated changes, corrections versus overwrites, translation, duplicate position codes within an owning organisation, safe retirement of positions referenced by active engagements/vacancies, history and deletion/retention. Deployment and independent packaging are separate classification decisions; avoid unnecessary dependencies and provider lock-in.

**Boundary:** Owner-approved JOB-01–09: `job` owns **position definitions only**. **Recruitment** is the separately favoured Domain candidate for vacancy/requisition approval, advertising and applicant selection, subject to its own complete review. **Employment** owns actual engagement/assignment/occupancy. Workflow and Scheduler execute tasks/time triggers, not business decisions. Neither an active position nor its retirement creates or terminates an employee or opening.

## 2. Likely public input and output contract — plain English

**There is no verified published Job `CONTRACT.md` or implementation API.** Names below are *idealised operations* and must eventually be published, versioned and tested independently; they are not invented existing endpoints.

| Job receives (input) | Job returns or publishes (output) |
|---|---|
| Authorised request to create a position with owning organisation, title, duties, classification and effective date | New stable position reference, approved or draft status, version, provenance and accepted/committed/rejected outcome |
| Request to revise duties, grade reference or skill/qualification requirements, with expected revision and effective date | New position revision and history; clear conflict if the revision is stale |
| Authorised approval, activation, suspension or retirement command | Position lifecycle state, effective time, decision evidence reference and event on committed change |
| Scoped read/query with position ID, permitted tenant/owner, optional revision or as-of date | Authoritative current or historical position definition, validity, source revision and access-controlled fields |
| Request for essential/desirable requirements and accepted alternatives at a frozen version | Versioned requirements for Recruitment, Qualification and Employment, **not** a candidate suitability or legal eligibility verdict |
| Trusted caller, permission decision, policy/taxonomy references, idempotency key and correlation context where needed | Clear failure and unknown/status codes, attributable operation outcome and committed `position.created/revised/statusChanged` facts through owned durable outbox |

**Invariants:** All protected operations check server-side Authorisation and separate tenant/owner scope; a received event never grants rights. Commands validate at runtime, reject unsupported vacancy/application/employment commands, use expected revisions and idempotency, and do not promise exactly-once distributed delivery. Reads describe provenance, completeness, effective time and visibility; rejected writes disclose no sensitive records. Events represent committed authoritative Job changes only. Do not expose private database tables or external provider SDK types; use provider-neutral public ports and the accepted host composition budget.

## 3. Capability inputs and outputs

| Cooperating capability | Information Job needs from it | What Job provides in return |
|---|---|---|
| Identity / Authentication / Authorisation (essential for protected operations) | Stable subject/group/tenant and ownership context, authenticated caller/assurance and server-side decision | Position resource identifier, ownership and required action for authorisation; attributed result, no role/membership mutation |
| Configuration (conditional) | Versioned, scoped local position categories, permitted fields and approval policy | Validation of position-domain meaning and operation status; Job does not own configuration storage |
| Clock (effective-time interpretation) | Canonical instants, zones and versioned time semantics when needed | Position effective dates/revisions; Job does not own clock settings |
| Qualification / specialist occupation authority (conditional) | Recognised qualification/occupation/scheme references and their source/version, not applicants' award dossiers | Frozen position requirements and alternatives for authorised evaluation elsewhere |
| Recruitment (consumer; not a required Job dependency) | **Nothing mandatory for Job**; future authorised independent consumer may request a frozen position | Position identity, status, duties and versioned requirements; **not** vacancy/opening, candidate, advert or selection outcomes |
| Employment (consumer; not a required Job dependency) | **Nothing mandatory for Job** | Optional position ID, revision, effective status and descriptive data; Employment alone owns engagements and assignments |
| Integrations (optional if external position catalogue) | Qualified external HR position catalogue changes with provider provenance/authority and reconciliation | Locally authoritative or source-qualified position references and conflict/unknown status; no ATS/job-board requirement |
| Reporting / Audit / Logging | No business information needed for normal native position operation; their own receipts/health may inform operation safeguards | Respectively authorised source views, attributable evidence and minimised diagnostics under distinct contracts |

Conceptual cooperation is **not** a cyclic package dependency. Job should be able to operate as a headless native catalogue without Recruitment, Employment, Publisher, Workflow, Scheduler or third-party HR software.

## 4. Logging, Audit and Reporting: distinct public contract relationships

| Relationship | Job sends via public interface | Other capability returns/owns | Important limit |
|---|---|---|---|
| **Logging** | Sanitised diagnostics: invalid input type, revision conflict, storage/outbox failure, dependency timeout, permission-denial category, latency, safe correlation and tenant scope | Logging owns structured diagnostic records, severity/routing, sink/health/acceptance status | A successful log entry does **not** prove a position approval, committed revision or audited event. No full job descriptions, private salaries, credentials or needless personal data in log payloads. |
| **Audit** | Source-authenticated, risk-selected accountable events: creation/approval/sensitive change, suspension/retirement, policy override, privileged export or denied high-risk action as appropriate, with actor/assurance, target reference, before/after revision references, outcome, effective time, evidence and event ID | Audit owns evidence receipt, custody, integrity/completeness verification, scoped review, retention and disclosure; may report accepted/rejected/pending/uncertain receipt and gaps | Job retains domain facts and its durable outbox. An Audit receipt does not change position state. Missing required audit capture is visible and may hold risk-sensitive operations under an explicitly defined policy. |
| **Reporting** | Authorised position current/as-of reads, version history, grade/classification summaries and committed change signals for invalidation; scope, provenance, effective time and completeness | Reporting owns derived report definitions, snapshots, refresh, generated output, export and delivery status | **No vacancy, recruitment or workforce figures from Job.** Recruitment owns vacancy source; Employment owns actual staffing. Report aggregates obey tenant/group/field restrictions, small-cohort inference protections and rights revalidation on export. |

**Failure boundaries:** Logging unavailability should not silently change Job business outcomes. Audit backlog or rejection is not interchangeable with logging failure and follows independently qualified capture/hold/recovery policy. Reporting outage must not block native Job reads/edits. No private store reads, event loop or bidirectional package imports are required. Publish bounded source facts; subscribers deduplicate and handle delayed/out-of-order delivery.

**Evidence baseline:** Blueprint [Logging](../docs/capabilities/logging/capability-record.md), [Audit](../docs/capabilities/audit/capability-record.md), and [Reporting](../docs/capabilities/reporting/capability-record.md) contain conceptual interfaces. Direct root `CONTRACT.md` lookups in `nuxt-layers/logging`, `nuxt-layers/audit` and `nuxt-layers/reporting` returned 404; no actual public packages/interfaces were verified. This section is a reciprocal conceptual requirement, not an integration claim.

## 5. Established standards to reuse

| Standard/source | Fit and caution |
|---|---|
| **ILO ISCO-08** occupation classification ([ILO](https://ilostat.ilo.org/methods/concepts-and-definitions/classification-occupation/)) | Stable cross-country occupation category codes; distinguish an occupation class from an employer's own position identity |
| **European ESCO** occupations/skills taxonomy ([official site](https://esco.ec.europa.eu/en/use-esco)) | Reusable multilingual skill/occupation relationships and downloadable linked data; external taxonomy terms should be optional, versioned references, not hard dependencies on a remote service |
| **Schema.org Occupation** ([vocabulary](https://schema.org/Occupation)) | Suitable semantics for descriptions of occupations; **Schema.org JobPosting** ([vocabulary](https://schema.org/JobPosting)) applies to actual Recruit­ment-approved public vacancy adverts and should not be emitted for an unpublished Job position |
| **ISO 8601, RFC 3339, IANA timezone database, ECMA-402 / BCP 47 / CLDR** | Consistent effective dates, locale/language, time zones and presentational formatting; reuse the platform's Clock and localisation interfaces instead of duplicating rules |
| **JSON Schema 2020-12 / OpenAPI** where actually used | Portable, framework-neutral schema documentation/validation for a future public transport contract; do not imply a mandatory HTTP API |
| **OWASP ASVS 5.0**, **WCAG 2.2 AA**, **UK GDPR/GDPR** as applicable | Governing security and accessibility baselines plus qualified privacy/retention/access requirements; named standards do not themselves establish legal compliance |

Choice of taxonomies must avoid force-fitting local job titles into global codes, must record scheme/version/issuer and support unclassified or unknown cases. Evaluate taxonomy content rights separately from code-library licences.

## 6. Mature, commercially permissive open-source libraries — candidates only

No library is approved for adoption in this conceptual review; verify release maintenance, licence/NOTICE, transitive dependency rights, security and compatibility again at implementation time. Prefer **one** validator rather than several.

| Package | Licence / purpose | Architectural placement |
|---|---|---|
| [Zod](https://github.com/colinhacks/zod) | **MIT**, runtime TypeScript input/output schema validation | Candidate for public contract boundary validation; alternative to Valibot/Ajv |
| [Valibot](https://github.com/open-circle/valibot) | **MIT**, modular typed validation | Lean alternative to Zod, not an additional mandatory dependency |
| [Ajv](https://github.com/ajv-validator/ajv) | **MIT**, JSON Schema validation | Useful **instead** if machine-readable published schemas become primary |
| [node-postgres (`pg`)](https://github.com/brianc/node-postgres) | **MIT**, PostgreSQL driver | Established data access; ADR-0012 host pool shape where required; Job owns its schema and storage, not shared persistence |
| [fast-check](https://github.com/dubzzz/fast-check) | **MIT**, property-based testing | Future CI verification of revision/idempotency, tenant boundaries and lifecycle invariants; tests not executed here |
| [Pino](https://github.com/pinojs/pino) | **MIT**, structured logging | Potential **Logging implementation**, not a Job-owned second logger; consume Logging's published interface |
| [OpenTelemetry JS](https://github.com/open-telemetry/opentelemetry-js) | **Apache-2.0**, portable traces/metrics | Shared Observability integration, not a second audit log |
| [date-fns](https://github.com/date-fns/date-fns) | **MIT**, date helpers | Optional implementation aid **only if Clock cannot already provide the semantics**; do not create competing timezone/date decisions |

These are genuine permissively licensed upstream codebases, not restricted-source database substitutes or commercial-only features. They do not require SaaS or vendor-hosted services for the described functions. **Avoid premature extra libraries**: native JS/TypeScript `Intl`, existing Clock, platform contracts and PostgreSQL may suffice.

Licence evidence: [Zod MIT](https://github.com/colinhacks/zod/blob/main/LICENSE), [Valibot MIT](https://github.com/open-circle/valibot/blob/main/LICENSE.md), [Ajv MIT](https://github.com/ajv-validator/ajv/blob/master/LICENSE), [pg MIT](https://github.com/brianc/node-postgres/blob/master/LICENSE), [fast-check MIT](https://github.com/dubzzz/fast-check/blob/main/packages/packaged/LICENSE), [Pino MIT](https://github.com/pinojs/pino/blob/main/LICENSE), [OpenTelemetry Apache-2.0](https://github.com/open-telemetry/opentelemetry-js), [date-fns MIT](https://github.com/date-fns/date-fns).

## 7. Likely Job GUI and representative host integration

**Evidence:** `nuxt-layers-test/application-test-template/README.md` (master, read during review) documents an application shell with homepage `/`, administration/test dashboard `/admin`, responsive collapsible sidebar, top bar, Theme Manager's `/theme-manager` and its Appearance control. Derived test apps add capability-specific scenarios/navigation without replacing the shell. The test mode is **local-only and unauthenticated**; it is **never** a production security model. `nuxt-layers/theme-manager/CONTRACT.md` documents current host-composition limitations; do not assume its internal test providers are a published production API.

**Recommended host flow:** the host adds an accessible, permission-filtered **Positions** sidebar item under a relevant administration/workforce section → a Job **Positions dashboard** (illustrative host path `/job`, not a promised exported route). It may show number of active/draft/retired position definitions only, never number of vacancies, hires or staff.

**Job-owned optional screens:**
1. **Positions list/dashboard:** search/filter by accessible owner, position code, name, class and status; create action only for authorised actors; scoped counts.
2. **Position detail/view and revision history:** duties, location/work-mode, classification, grade reference, requirement version, effective status, clear historical/as-of selector.
3. **Create/edit/review:** accessible form with validation and meaningful errors; draft, submit, approve, suspend/retire operations presented only when permitted; optimistic concurrency warning and confirmation for sensitive transitions.
4. **Qualification/skills requirements editor:** essential/desirable criteria, recognised scheme/code reference, alternatives, explanatory notes and source/version; not candidate verification or hiring verdict.
5. **Restricted administrator history/export:** attributable change timeline and limited exports; actual Audit review is through Audit capability, not a Job evidence database.

**Outside Job GUI:** vacancy requests/approval, staff establishment/seat funding, job posting, candidate pipeline, interview decisions, offers and hiring handover belong in proposed Recruitment screens. Contracts, actual staff, assignment and termination views belong in Employment. Host may provide cross-links with appropriate permission checks and source references, never shared private tables.

**Presentation constraints:** consume only published Job queries and commands through host server composition; application owns menu/route organisation; capability owns domain validation and, if packaged, its optional screens under accepted ADR-0009. Host links `/admin` → Positions dashboard like Theme Manager; Theme Manager provides tokens and appearance. Use semantic markup, WCAG 2.2 AA keyboard/focus/reflow, BCP 47 localisation and Intl/CLDR formatting; show empty/unavailable/denied/conflict/pending states honestly. The representative template does not itself prove a Job route or screenshot exists.

**Acceptance seed:** unauthorised user cannot access a route, record, counts or export; cross-tenant search denied; valid editor can create/revise with history; conflicting save clearly resolved; retired position remains historically attributable; optional Qualification unavailable without inventing claim; clicking a Recruitment shortcut does not grant vacancy rights; headless Job works with no presentation/Recruitment/Employment; manually verify accessible desktop/mobile/light/dark/keyboard views.

## 8. Follow-up and sign-off

Update future root `CONTRACT.md` only after the implementation/repository is approved. Publish explicit public ports, dependencies, errors, example host composition and consumer acceptance; comply with ADR-0012's 50-line Nuxt host budget and no private imports. The conceptual Job boundary is owner-approved; library selection, detailed interface schemas, GUI routes, regulatory fit and production integration are **not**. Keep [Recruitment's proforma](../docs/capabilities/recruitment/capability-record.md) separate for vacancy and selection design. PR #84 remains draft, and no tests, implementation edits or merge were authorised.
