# Integrations — Capability Conceptual Record

**Status:** INT-01–INT-06 owner-approved conceptually on 18 November 2026; INT-07–INT-09 owner-approved conceptually; non-normative; not implementation-ready. **Classification:** established **Platform** responsibility; proposed framework-independent service with provider-specific connector adapters and optional separable Nuxt administration UI. **Opening authority:** `architecture-rules/master` `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; **opening blueprint:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. **Review:** [draft PR #76](https://github.com/nuxt-layers/architecture-blueprint-review/pull/76). **Implementation evidence:** [nuxt-layers/integrations](https://github.com/nuxt-layers/integrations) exists on `master`, but its README is only `# integrations` and root `CONTRACT.md` is absent at review; **no public runtime contract, implemented connector, test or operational readiness is verified**.

## Purpose and classification gate

Integrations is the provider-neutral **external application connection and exchange coordinator**: register available adapters, govern scoped connections and remote grants, adapt provider operations to declared provider-neutral consumer interfaces, transport authenticated calls and callbacks, track technical synchronisation/checkpoints, and expose evidence, observability and uncertain outcomes. This is independently meaningful platform operational state and lifecycle, not merely a collection of SDKs. **Retain** the Platform capability; represent individual vendor adapters as optional connectors behind its ports, not independent domain owners or mandatory Nuxt Layers. A framework-independent core with optional Nuxt presentation is preferable to mandatory framework coupling; no separate deployment is required by this review. The host selects and supplies infrastructure and keys under accepted ADR-0012's one-call/50-line composition budget, without writing provider-specific relays.

The governing catalogue names Google Docs, Microsoft 365 and social feeds as examples, **not supported implementations**. Domain-specific external integrations (accounting, banking, commerce, LMS, CRM, government registries, assessment, credentials, identity proofing) use the same transport discipline but keep domain policy with the respective owner. Integrations and `iam-integration` are separate: the latter composes IAM members, not arbitrary SaaS connections. Infrastructure integrations such as Temporal Gateway remain distinct infrastructure integration libraries under ADR-0015.

## Authority, minimum owned state, exclusions

| Integrations owns (only when justified) | Excluded authority |
|---|---|
| Adapter registration and declared provider operation catalogue: versions, scopes, schema, provider terms, residency and limitations; adapter health and compatibility | Domain service definitions, statutory legal interpretation and guarantee of third-party availability |
| Tenant- and purpose-scoped connection records, remote account binding, consent/approval references, credential **references**, authorised status, revocation/expiry and reconnection lifecycle | Identity's tenants/groups; Authentication sessions; Authorisation access decisions; Profile personal facts; secret values belong in host secret management/vault |
| Versioned mapping configurations, technical sync cursors, remote identifiers, callback deduplication and reconciliation queues | Canonical invoices, accounts, orders, bookings, stock, contacts, content, courses, assessments, credentials or authoritative remote facts |
| Technical attempts, remote acknowledgements, delivery receipts, provider capability snapshots, uncertainty, failure/recovery transitions and minimum operational history | Workflow approval decisions, Audit independent compliance evidence, Logging general log lifecycle, Message Queue's message delivery responsibility |
| Own state-change events and durable outbox when it changes its authoritative connection/sync state | Domain outcome events; a provider webhook is evidence, **not** a locally committed domain outcome |

**Minimum persistence:** scoped connection/remote-account metadata and grant state, encrypted or secret-store credential references (not secrets), adapter versions, operation/mapping versions, checkpoint and deduplication/reconciliation state, technical attempts/uncertainty and owned outbox. Stateless operations need not write unnecessary records; technical caches are bounded and non-authoritative. Retention/deletion/hold rules apply. Do not centralise domain records or create an undifferentiated copy of provider data.

## Native services and lifecycle

1. **Discover/approve adapters:** publish declared provider, operation, scope, schema/version, allowed territories, rate/cost, verification status, security requirements and feature limits. Default unregistered or incompatible operations to unsupported.
2. **Provision connection:** authorised tenant/purpose requests an approved adapter and remote account; obtain explicit remote consent/authentication where needed; bind opaque secret reference; verify credentials/scopes and record approval evidence. States: `requested → authorisation-pending → verifying → active`, or `rejected/failed`. `active → degraded/reauthorisation-required/suspended → active` on validated recovery; `active → revoking → revoked` on withdrawal. Failed revocation remains `revocation-uncertain`; do not claim remote grant removed.
3. **Execute remote operation:** consumer supplies domain-authorised intent and expected mapping/capability; validate scope, entitlement, local access, provider limits, idempotency and data minimisation; return `not-submitted`, `submitted/accepted-for-processing`, `remote-confirmed`, `remote-rejected`, `unsupported` or `outcome-unknown` with provider-specific evidence. A transport 2xx is not a completed business act.
4. **Receive callbacks and synchronise:** authenticate signature/key, audience, nonce/replay and tenant/account correlation; quarantine ambiguous or invalid sources; record stable provider delivery ID; transform into evidence for domain adjudication through a public port/event. Support incremental/full sync only where provider supports it, respecting source revision and rate limits.
5. **Reconcile/recover:** stale tokens, schema drift, provider outages, partial batches, rate limiting and ambiguous timeouts enter explicit degraded/unknown state and retry or manual review; no automatic authority switching, duplicate side effect or destructive remote write on uncertainty. Pause and reconcile before cutover. Credential compromise triggers revocation/rotation and Audit notification via authorised channels.
6. **Decommission:** stop new requests, drain/cancel bounded work where safe, revoke credentials/remote subscriptions where supported, apply retention and legal holds, close mappings and expose evidenced final state. No provider-supported revocation means explicitly limited conclusion.

No outside provider is essential to the **core service**. Individual adapter usage is conditional; a given domain feature can require a specifically validated connector and must fail closed when absent.

## Idealised public inbound contract

Each item describes a conceptual public port, not a committed API signature.

| Source → input | Authority and validation | Absent/stale/invalid semantics |
|---|---|---|
| Host/operator → approved adapter registration, deployment/secret-store references, allowed processing geography, network policy | Host approves deployment and stores secrets; Integrations validates provider metadata, adapter authenticity/version and accessible secret reference | Missing adapter/secret → unavailable; incompatible revision → unsupported; never expose secrets |
| Configuration → approved tenant/service provider-selection reference, mapping/feature option revision | Configuration owns setting value and precedence; Integrations validates scope/approval against live connection and declared adapter capabilities | Selection without active compatible connection → not-ready, not silently enabled |
| Identity/Authentication/Authorisation → tenant/subject binding, assurance, `decide(caller,action,resource)` | IAM owns identity/session and decision; validate resource, tenant, purpose and fresh approval server-side for every protected operation | Missing/denied/indeterminate → fail closed; remote authentication is not local permission |
| Domain owner → connector intent (operation, source record reference/revision, domain-owned authorisation evidence, scope, required outcome, mapping version, idempotency/correlation) | Domain owns transaction semantics; Integrations validates operation/scope, request shape, freshness and side-effect safety | Stale revision/unsupported scope → reject; timeout after dispatch → outcome unknown, require reconciliation |
| External provider → authenticated responses, webhooks, grant assertions, remote revision, receipts and error metadata | Provider is source of its assertions only; Integrations verifies authenticity, tenant binding, anti-replay and expected protocol | Unverifiable → quarantine; delayed/conflicting → stale/conflict status, never domain overwrite |
| Verification/Legal Compliance/Privacy → required trust/processing restrictions and lawful purpose constraints | Specialist owns assessment of evidence and governing constraint; Integrations enforces supplied effective restriction | Unknown mandatory legal/trust condition → no disclosure or regulated operation |
| Scheduler/Workflow/Message Queue → invocation, approved orchestration state and delivery notices | These owners control timing/approval orchestration/message transport, not provider/domain truth | Retry only within idempotency, retention and back-off policy; no completion inferred from delivery |
| Clock → current time and deadline/timezone interpretation | Clock owns temporal semantics | Unreliable/unknown expiry → block freshness-dependent action |

Every input distinguishes asserted source facts, caller command, effective policy and provider evidence; conditional ports must describe an explicit no-provider mode. Contract consumers never need private tables or vendor SDK types.

## Idealised public outbound contract

| Output → authorised consumers | Meaning and guarantee | Status/provenance/disclosure |
|---|---|---|
| Adapter discovery and support matrix → host, Configuration, domains, admin UI | Supported-by-adapter operations, permission scope, schema/version, geographical limits and checks; **not** provider availability promise | Source, checked-at, expiry, version, unsupported/unknown; tenant-filtered |
| Connection status and grant capability → domain, operator, Audit | Locally validated connection lifecycle, remote grant evidence and effective scoped readiness; **not** domain authorisation | Tenant/account, purpose, grant/secret-reference version, expiry/last-check, degraded/revocation uncertainty; never credentials |
| Remote operation result/receipt → requesting domain, Workflow | Submission and verified remote response, or explicit unknown; only domain can conclude business success and emit its outcome | Correlation, idempotency, attempt/provider ID, request/mapping versions, observed/effective time, remote acknowledgment type |
| Provider assertion/changed-record envelope → source-owning domain, Verification, allowed consumers | Authenticated, minimised, provenance-rich external claim; authenticity is not truth or suitability | Provider, remote account/ref/revision, audience, source/effective/received times, validation and freshness; scope-filtered |
| Sync/checkpoint/reconciliation read model → operator, domain, Observability | Progress, partial failures, drift, cursor/checkpoint and unresolved conflicts; not a complete authoritative domain dataset | Completeness, as-of, mapping/version, outstanding uncertainty and retryability |
| Owned connection/sync lifecycle event → Audit, subscribed consumers via outbox/Message Queue | Event after committed Integrations-owned state change; duplicate and out-of-order delivery possible | Event ID, tenant, version, source, correlation and minimal payload; subscribers re-query authoritative state |
| Sanitised operational diagnostics → Logging/Observability/Reporting | Technical metrics, rate/cost and error status, never domain financial truth or secrets | Redaction, tenant limits, retention and provenance |
| Controlled export of connection/mapping metadata → authorised admin/Export | Non-secret portable configuration and provider references; not usable tokens or domain-owned data | Version, ownership, redaction and explicit import compatibility |

## Commands, queries, events and shared invariants

**Commands:** `registerAdapter`, `requestConnection`, `completeGrant`, `verifyConnection`, `rotateCredentialReference`, `suspend/revokeConnection`, `configureMapping`, `submitProviderOperation`, `reconcileAttempt`, `start/pause/resumeSync`, `decommissionConnection`. Names are illustrative business interfaces. Enforce per-operation permissions, state transitions, expected versions, idempotency and explicit accepted-versus-completed results; asynchronous workflows expose recovery handles. Unsafe or unsupported operations are rejected, never guessed.

**Queries:** `listCompatibleAdapters`, `getConnectionStatus`, `getOperationCapabilities`, `getAttempt/Receipt`, `getSyncStatus`, `listReconciliationItems`, `getMappingVersion`. Authorised tenancy/purpose, bounded freshness, completeness and provenance are part of every query; avoid unrestricted tenant-wide provider data reads.

**Events (only committed owner facts):** `ConnectionActivated`, `ConnectionDegraded`, `GrantRevocationRequested/Confirmed/Uncertain`, `MappingActivated`, `SyncCheckpointAdvanced`, `ProviderAttemptReconciliationRequired`, `ConnectionDecommissioned`. Provider-domain facts are conveyed as qualified evidence and not mislabeled domain lifecycle events. Own transactional outbox under ADR-0012; Message Queue transports it. At-least-once/replay tolerant; no exactly-once distributed-delivery claim.

**Context/invariants:** tenant and authorised resource; subject/assurance/access decision; purpose and permitted disclosure; adapter/provider/remote-account identity; request/source revision, mapping and policy versions; correlation/idempotency; source/observed/effective/checkpoint times with Clock semantics; provider evidence and verified versus self-reported status; attempted, accepted, completed and unknown states. No universal request DTO is mandated. Tenant boundaries are checked at ingress, egress, credentials, callbacks and data stores. Rejected/unknown status cannot silently become success; cached provider claims cannot become new domain records until adopted by the domain owner. Remote provider authority is never silently promoted to local authority; migration requires approved selection, reconciled checkpoint and explicit cutover.

## Cross-capability relationships — directional public-contract cooperation

| Capability | Input to Integrations / output from Integrations | Ownership, absence and dependency |
|---|---|---|
| Configuration | Effective provider selection, declaration revision → connection readiness/capability facts | Configuration owns settings; Integrations owns connection lifecycle; host-composed public ports avoid direct mutual imports |
| Identity, Authentication, Authorisation, Profile | Tenant/caller/assurance/decision and permitted disclosure → scoped status/evidence | IAM/Profile retain authority; required protected-operation checks fail closed |
| Verification, Legal Compliance, Privacy | Evidence trust and lawful constraints → attributed provider evidence, retention/process trace | Specialist adjudicates trust/legal constraints; unresolved mandatory constraints fail closed |
| Accounting, Billing, Invoice, Booking, Order, Inventory, Asset, Product, CRM | Authorised domain intent/records → provider result, mapped evidence, checkpoints | Each domain owns its data, status, external-primary selection and cutover; optional per adapter |
| Course, Assessment, Qualification, Credentials | Approved external LMS, examination, registry and issuer requests → qualified source evidence and callbacks | Domain retains learning, marking, recognition and award meaning; absence means unavailable integration, not false outcome |
| Publisher, Reviews, Notifications, Search, Localisation, Moderation | Scoped publish/import/scan/send/query intent → third-party transport/evidence | Owner retains content, review, dispatch, search, translation or moderation decisions |
| Federation | Approved peer-facing adapter requirements → transport/capability status | Federation owns peer/subscription/disclosure and cross-node reconciliation; Integrations does not substitute for federation protocol or peer trust |
| Workflow, Scheduler, Message Queue, Clock | Approval process, scheduling, transport, temporal service → status/receipts/committed events | Public ports/host wiring and owner-originating outboxes; no cycles or hidden package imports |
| Audit, Logging, Observability, Reporting | Governed evidence capture and diagnostics → minimal events/metrics/receipts | Independent audit evidence, operational logs, monitoring and reporting owned elsewhere |
| Infrastructure/host secret manager | Secret reference, networking, compute and persistence → health/readiness | Host/Infrastructure controls deployment and vault; Integrations owns its business-operational connection state |

A reference in this table is **logical cooperation**, not a mandatory compile-time import. Any eventual dependencies (including Nuxt `extends`) must be declared and jointly acyclic under ADR-0016. Domain-to-Integrations service consumption with callback ports supplied at composition is preferred to bidirectional package dependencies.

## Configuration, legal, security and privacy

Tenant/organisation administrators may request integration configuration only within Authorisation and approved policy; elevated assurance and dual approval may be necessary for financial write access, remote account transfers, secret rotation and destructive bulk sync. Host secret management stores tokens, private keys and client secrets; no token in generic configuration, events, logs or exports. OAuth/OIDC scopes, CSRF/state, webhook signatures, replay protection, egress allowlists/SSRF defence, token audience, rotation, least privilege, secret encryption, sandbox/prod separation, provider package supply chain, quotas/rate-limit circuit breakers and incident revocation must be addressed in detailed design. Treat external payloads as untrusted (input/schema validation, content sanitisation), and verify provider terms, processor/subprocessor status, lawful basis, international transfers, data residence, minimisation, retention, deletion and government-sector access restrictions via Privacy/Legal Compliance. No vendor or statutory compliance approval is inferred by a technically valid connection. Baseline OWASP ASVS 5 L2, L3 where security-critical, and WCAG 2.2 AA for UI.

## Conceptual presentation / GUI

**Headless core mandatory; optional admin/operator presentation justified.** The host owns routes, sidebar/Capabilities navigation and branding; optional Integrations dashboard is shown only if enabled. Use Theme Manager semantic tokens, accessible keyboard focus, WCAG 2.2 AA, responsive layout, i18n and accessible screen-reader status messages.

- **Connection dashboard/list:** tenant-filtered provider cards, connection status, last verification, purpose, capabilities, expiry, cost/rate and known limitations; clearly separate selected, configured, connected, authorised and operational.
- **Add/authorise connection:** provider discovery, lawful-use/terms and scope notice, consent/assurance, secure provider redirect/return, remote-account selection, test connection and explicit activation.
- **Connection details:** permitted operations, scopes, masked credentials, mapping revisions, owner-linked external identifiers, health/limits, recent sync receipts, revoke/renew/pause actions with confirmation and reauthentication for sensitive changes.
- **Mapping and sync workspace:** dry-run previews, source-to-domain mapping proposals for domain-owner approval, checkpoints, reconciliation queue, uncertain attempts, retries with side-effect warning, audit trail and changeover workflow.
- **Operator view:** degraded/expired/unsupported states, provider outage, webhook trust failures, quarantine/replay review and redacted diagnostics; no disclosure of another tenant's provider accounts.

When presentation is disabled, all legitimate functions remain available to authorised server consumers through the documented headless contract. No automatic global menu registry or testing app change is implied.

## Conceptual contract acceptance scenarios (not executable tests)

| Input | Expected behaviour/output | Final authority |
|---|---|---|
| Host registers vetted adapter without a tenant connection | Discovery shows adapter available but connection not ready | Integrations |
| Approved tenant grant, verified scopes and approved selection | Connection activated with versioned scope/expiry/provenance | Integrations for connection; Configuration for selection |
| Accounting submits posting to external provider | Recorded remote request/receipt or unknown; local ledger not mutated by Integrations | Accounting |
| Invalid/foreign-tenant callback, or insufficient caller assurance | Quarantine/deny, no disclosure or domain mutation; diagnostic evidence | IAM decision; Integrations quarantine |
| Duplicate webhook or same idempotency key | Single logical technical attempt/checkpoint; replay-safe notifications, not duplicate side effects | Integrations |
| Request times out after remote submission | Explicit outcome-unknown, reconciliation needed, no automatic fallback | Integrations; domain adjudicates |
| Provider schema changes or token expires | Mark unsupported/degraded, pause unsafe operations, renew/reconcile before resuming | Integrations |
| External provider is disconnected during pending Booking action | Record uncertain/cutover-incomplete; do not rebook natively or claim cancellation | Booking |
| Course remote completion claim arrives | Qualified provider evidence only; Course/Assessment decide local admissibility | Course/Assessment |
| Admin requests revocation; provider unavailable | Local operations disabled; remote revocation remains uncertain, visible for follow-up | Integrations |
| Consent withdrawn or retention deadline reached | Stop prohibited disclosure; retain only lawfully required minimal evidence | Privacy/Legal Compliance constraints; Integrations enforcement |
| No configured provider or presentation | Headless service remains available; provider-dependent operation is explicitly unavailable | Integrations |

## Review findings, decisions and acceptance status

**Established:** Platform classification and provider-adapter responsibility in governing catalogue; ADR-0012, ADR-0016 and Capability Standard obligations. Existing conceptual owner approvals in the historical notes below remain intact (e.g. BIL-05, ORG-01–08, CFG-08, COURSE-10/12, ASMT-13/14, VER-01–12), each limited to its stated scope.

**Proposed for owner approval (new, not pre-approved):**
- **INT-01:** Retain a provider-neutral Platform capability with independently owned connection/grant, technical mapping/checkpoint and uncertainty lifecycle; vendor adapters remain conditional connector packages.
- **INT-02:** Keep provider authentication/transport and technical evidence separate from domain business authority, regulatory adjudication and IAM access decisions.
- **INT-03:** Require explicit tenant/purpose/provider-scope selection, qualified capability discovery and verified connection activation; no automatic fallback or dual authoritative writes.
- **INT-04:** Adopt the inbound/outbound conceptual contract, explicit submission-versus-completion and unknown outcome semantics with replay-safe reconciliation.
- **INT-05:** Require secure callback/consent/credential-reference lifecycle, provenance, retention and narrowly scoped disclosure.
- **INT-06:** Support headless operation and optional separable administration/reconciliation GUI using host navigation and Theme Manager.

**Owner-approved decisions INT-07–09:** INT-07 separates local installation-operator approval of plugin software/publisher from organisation/tenant approval of scoped use; a central Nuxt Layers marketplace is never required. INT-08 requires one effective authoritative writer per domain-defined business scope, native or external, with approved mapped/reconciled cutover and no automatic fallback or dual writers. INT-09 applies proportionate risk-based approval, assurance and compliance gates to integrations and sensitive individual operations; independent/two-person approval and provider certification apply when required by policy or law, not indiscriminately. The detailed [authorisation and display policy](#int-07-09-approved-governance-and-user-specific-entitlement--18-november-2026) governs per-person permitted discovery and use.

**Technical investigations (not owner-choice substitutes):** versioned adapter manifest/schema and signature model, OAuth/token broker versus host vault responsibilities, retry/backoff and replay windows, safe callback identity binding, signed grant evidence, provider API deprecation monitoring, operational SLOs, payload minimisation and cost reporting. Set standards through evidence and accepted policy rather than inventing guarantees.

**Implementation alignment:** root `CONTRACT.md` absent; publish an independently usable consumer contract, explicit port dependencies, error codes, status/versioning and operational limits; test host composition budget through CI/user-owned work, not this review. No currently verified implementation/contract. **No conceptual sign-off, legal certification or runtime acceptance asserted.**


## Owner approval and supplementary interface examination — 18 November 2026

**Owner decision:** INT-01–INT-06 approved conceptually on 18 November 2026 in the Integrations review conversation. INT-07–INT-09 were subsequently owner-approved conceptually, including individually authorised discovery/use (see detailed dated decision below). This still does **not** mean a deployable implementation. Root `nuxt-layers/integrations/CONTRACT.md` remains absent at this check. `nuxt-layers-test/application-test-template` has a README describing a local development/test shell; its root `CONTRACT.md` was not retrievable; Theme Manager's published contract is available but explicitly records implementation-composition gaps. No implementation change follows from this conceptual approval.

### Reciprocal Logging, Audit and Reporting public interfaces

| Cooperating capability | Integrations supplies (through deliberately public interfaces) | Integrations receives, if applicable | Authority and operational guarantee |
|---|---|---|---|
| **Logging** | Redacted diagnostic events: request/adapter and operation IDs, tenant-safe correlation, permitted severity/error category, latency, retry status, rate limits, timeout, callback verification failures and degraded provider health | Supported log submission/diagnostic sink and sink health/availability, with redaction and routing policy | Logging owns technical record/sinks and retention; logging an operation does not establish execution, remote success or Audit evidence custody. Logs must exclude OAuth tokens, webhook secrets and raw sensitive payloads. Optional Logging outage must not forge or erase transaction outcomes |
| **Audit** | Classified origin-authenticated source events via Integrations-owned committed outbox/approved submission: connector creation, delegated scope approval/revocation, secret reference rotation, high-risk export/transmission, sensitive administrator changes, quarantined callbacks and failed/reconciled significant remote actions | Accept/reject/quarantine/evidence receipt and required event classifications/retention/disclosure constraints through Audit contract | Audit owns independent immutable/tamper-evident evidential receipt, verification and review, not Integrations operation truth or domain outcomes. Do not assume message delivery equals Audit acceptance; mandatory Audit capture failure must be observable and follow a risk-specific fail-closed/queued obligation |
| **Reporting** | Authorised, scoped/versioned read models for connector counts and statuses, adapter support, API usage/rates/cost, success/rejection/unknown outcome classification, sync lag/checkpoints, reconciliation backlog, source and effective times, completeness and coverage | Report reference, definition/version, generation/completion status, permitted output/export and failure/refresh status | Reporting owns report definitions, derived measures, saved reports and disclosure; Integrations owns source technical facts. Do not treat external-system reports as canonical domain reports or infer completion from transport acceptance |

**Cross-cutting:** all three cooperation paths need public schema/version, tenant/purpose/authorisation, source/effective/observed time, correlation, sensitivity and permitted recipient. No reads of private stores or circular package imports. Integrations can serve its own minimal health/status screens without Reporting; its security-relevant outbox/evidence obligations must not rely on best-effort Logging. Audit and Reporting can be absent where optional, except when a declared regulated workflow requires Audit evidence, in which case the absence mode must respect policy and fail closed or maintain an explicitly assured durable pending state.

### Design standards and open-source dependencies (researched 18 November 2026)

**Relevant standards:** IETF OAuth 2.0 and security BCP [RFC 9700](https://www.rfc-editor.org/rfc/rfc9700.html) with PKCE/state/issuer checking, OIDC where provider supports it; HTTP semantics/idempotency [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html); HTTP error details [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457.html); [OpenAPI](https://spec.openapis.org/oas/latest.html) for HTTP operation descriptions, [AsyncAPI](https://www.asyncapi.com/docs/reference) and [CloudEvents](https://cloudevents.io/) for event/webhook envelopes where suitable; JSON Schema for versioned provider payload validation; OpenTelemetry semantic conventions and W3C Trace Context for correlation; OWASP ASVS 5 L2 (L3 security-critical), OWASP API Security Top 10 (especially object-level authorisation and SSRF), WCAG 2.2 AA, GDPR/UK GDPR and applicable sector-specific regulatory procedures. **Do not mandate every provider support these standards:** adapter-specific transports/protocols vary; contracts preserve provider-neutral meanings.

**Permissive reusable candidates (not selected dependencies):**

| Library / licence | Appropriate bounded use and lock-in assessment |
|---|---|
| [panva/openid-client](https://github.com/panva/openid-client), **MIT** | Mature OAuth 2.0 / OIDC client for supported providers; enforce accepted security profiles and isolate behind credential/grant ports |
| [panva/oauth4webapi](https://github.com/panva/oauth4webapi), **MIT** | Lower-level standards-based OAuth flows where precise protocol control is needed; select one of it/openid-client when possible |
| [nodejs/undici](https://github.com/nodejs/undici), **MIT** | HTTP client/connection pooling; Node built-in fetch may make direct dependency unnecessary |
| [ajv-validator/ajv](https://github.com/ajv-validator/ajv), **MIT** | JSON Schema validation for external provider data and manifest compatibility |
| [colinhacks/zod](https://github.com/colinhacks/zod), **MIT** | TypeScript-first runtime validation for local command and result boundaries; avoid two competing canonical schema systems |
| [sindresorhus/p-retry](https://github.com/sindresorhus/p-retry), **MIT** | Bounded exponential retry for safely retryable operations; cannot create side-effect idempotency on its own |
| [open-telemetry/opentelemetry-js](https://github.com/open-telemetry/opentelemetry-js), **Apache-2.0** | Trace and metric instrumentation via open standards; optional telemetry adapter, not authoritative audit ledger |
| [pinojs/pino](https://github.com/pinojs/pino), **MIT** | Structured technical logging implementation behind Logging contract; do not invent a second logging owner |
| [fastify/fastify](https://github.com/fastify/fastify), **MIT** | Optional standalone HTTP/webhook boundary where justified; not required for a Nuxt/Nitro host |

These projects expose source code under commercially permissive licences; **that does not make any SaaS provider, OAuth registration, cloud API, data feed, licence key or downstream integration free/open/replaceable**. Check exact version, transitive dependencies, release cadence, licence notices and supply-chain before implementation. Avoid selecting a monolithic hosted integrations platform, proprietary connector marketplace or vendor-specific workflow engine as the canonical service. Reuse existing PostgreSQL/Message Queue/Scheduler/Temporal composition rather than introducing a new broker.

### GUI and test-host presentation review

The representative [application test template README](https://github.com/nuxt-layers-test/application-test-template/blob/master/README.md) establishes a responsive app shell with homepage `/`, development admin/test dashboard `/admin`, collapsible Capabilities sidebar and existing Theme Manager link to `/theme-manager`. It states derived test apps add capability-specific scenario/navigation entries and consume published contracts. Theme Manager's [public contract](https://github.com/nuxt-layers/theme-manager/blob/master/CONTRACT.md) records semantic theme vocabulary and the existing page patterns; it also warns that its own one-call production composition is incomplete. The template is **local only**, not a production security pattern.

**Proposed host-owned navigation:** in an enabled, appropriately authorised deployment, sidebar **Capabilities → Integrations** points to a capability-dashboard route such as `/integrations`; do not mandate that exact path or assume automatic menu registration. The capability supplies public server operations and optional separately enabled presentation routes/components; host chooses routes, role visibility and shell branding. The Integrations entry and dashboard may remain disabled without affecting headless APIs.

| Screen / journey | Required public contract / state |
|---|---|
| **Integrations dashboard** | Available/active/degraded connections, safe counts and outstanding actions from scoped status queries; no connection secrets |
| **Provider catalogue** | Available and unsupported providers, permissions, legal limitations, version/terms, rate/cost disclosures via adapter discovery |
| **Add connection wizard** | Tenant/purpose/provider choice, scope notice, approved OAuth redirect/return, remote-account confirmation, test and activation via public commands |
| **Connection detail** | Masked credential reference, last validation, supported operations, remote-account binding, renewal/suspend/revoke and irreversible-action confirmations |
| **Mapping and synchronisation** | Versioned mapping preview, import/export scope, checkpoint history, discrepancy resolution and manual reconciliation through domain-owner approval |
| **Operations and incidents** | Request history, outcomes (submitted/confirmed/rejected/unknown), retry/circuit-breaker and quarantine views with permissions |
| **Settings and provider governance** | Authorised provider enablement, scope/cost limits, lifecycle and mandatory approvals; host/Configuration owns declarative selection |
| **Linked reporting and audit** | Permission-scoped links into Reporting's summaries and Audit's evidential views, never duplicate their records |

**Accessibility/interaction:** WCAG 2.2 AA, keyboard-first OAuth/error/retry journeys, labelled status beyond colour alone, accessible confirmations, responsive sidebar/overlay, i18n, locale-aware times via Clock and semantic styling via Theme Manager; all screens consume public contracts and recheck permissions on the server. Use explicit empty/degraded/offline/unauthorised/expiry/revocation-uncertain states. The host might put a capability card on `/admin`, while the main route lives within the same shared shell. No local tests were run and no test template files were modified.

**Further conceptual acceptance:** unconfigured host displays no functional provider account; admin sees permitted provider catalogue, creates connection and returns to its dashboard; unauthorised caller cannot see cross-tenant connections even through guessed route; expired grant shows reconnect rather than reporting active; provider timeout shows an unknown/reconcile action rather than 'done'; without UI the headless contract remains functional; Logging absence does not suppress Audit obligations; Reporting absence does not prevent operational status queries; compliance-required Audit outage yields documented non-silent failure behaviour.



## INT-10 — Discoverable live integration plugins (owner-approved direction, 18 November 2026)

**Owner direction approved:** As with the approved [Gaming runtime plugin model](../gaming/capability-record.md#23-runtime-plugin-loading--requested-capability-implementation-approach-proposed), Integrations supports **discoverable, independently deployable runtime connectors**, allowing a host to discover, review, enable, upgrade, suspend and withdraw connectors without rebuilding/redeploying the principal Nuxt application. **Live discovery is not automatic trust or activation.** This extends INT-01's provider-neutral adapter concept, does not reopen INT-01–06 and does not imply an implemented loader.

### Two explicit installation paths

1. **Static, build-time adapters** are reviewed software dependencies included by the host's ordinary build/composition process. The installed code may register its public adapter contribution.
2. **Dynamic, server-side connector plugins** are independently packaged/deployed adapter services, addressed through versioned provider-neutral ports and authenticated network/process boundaries. The runtime registry discovers their descriptor and endpoint at run time. The host Nuxt build remains unchanged; these plugins are **not** injected into `nuxt.config.ts`, Nuxt `extends`, or an arbitrary Node module loader. Deployment and registry discovery are separate decisions.

**Trust boundary:** Games can offer browser-sandboxed external presentation; integrations often handle confidential financial, personal or regulated data and can perform destructive remote actions. Preferred isolation is a **separate restricted server-side process/container or equivalent sandbox** with network egress policy, minimal identity, resource quotas and short-lived scoped credentials. No arbitrary downloaded third-party JavaScript is imported into the privileged host process. An isolated connector's HTTP or RPC response remains untrusted; Integrations validates all responses. The host's own approval and credential protections apply regardless of signed artefacts.

### Plugin manifest, approval and live registry

A **versioned, declarative plugin descriptor** (schema defined through documented public contract) declares: immutable plugin and publisher identity; package/version/build digest and signature or integrity proof **where supported**; deployment/health and authenticated protocol endpoint; protocol/contract versions; supported operations and their read/write/destructive classification; provider API versions and required OAuth scopes; data categories, countries/regions and processing location; outbound hosts and inbound callback requirements; webhook verification approach; mapping schemas/revisions; idempotency/read-back guarantees and limitations; quotas/cost; supported locales; licence and support/retirement policy. Discovery records may be incomplete; **unknown critical claims prevent activation**, not silent default approval. No remote manifest can grant itself privileges.

**Public inbound:** `registerDiscoverySource` (host-authorised allowlisted registry); `discoverPlugins` (scheduled/on-demand fetch); `submitPluginManifest`; `validatePluginCompatibility`; `approvePluginVersion`; `enablePluginForScope`; `disable/suspendPlugin`; `upgrade/rollbackPlugin`; `retirePlugin`; and authorised review of plugin health/cost/processing restrictions. These conceptual commands require tenant/purpose, requested resource scope, actor/assurance, policy revision, expected registry revision, provenance and idempotency. Dynamic discovery is read-only until approval; no remote package is automatically executed.

**Public outbound:** `listDiscoveredPlugins`, `getPluginManifest`, `getPluginCompatibility`, `getPluginStatus`, `listApprovedVersions`, `getPluginRolloutStatus`; scoped provider discovery and plugin lifecycle events through Integrations-owned outbox; explicit unsupported/incompatible/suspended and degraded/unknown states; source and approval evidence. Consumers discover **a supported connector**, not an implied active tenant grant, domain permission, verified provider or business-success guarantee.

**Lifecycle:** `discovered → validated → approved → deployed/available → enabled → operational`; independent failure states `invalid/incompatible/quarantined/degraded/suspended`; controlled `upgrading/rolling-back/retired`. An approved plugin can remain inactive. Plugin **availability** is distinct from a tenant's separately consented **connection** to an external provider. Disablement prevents new operations and revokes connector runtime privileges as feasible; in-flight external side effects become explicit completed/failed/unknown evidence and require reconciliation, not destructive cancellation guesses.

**Safe rollout and removal:** pin each active operation, outstanding callback, sync checkpoint and mapping to a compatible plugin version; require signature/integrity/source verification, version-contract checks, smoke/health checks performed by deployment/CI, staged rollout where justified, controlled drainage, replay/idempotency and non-destructive rollback. Never silently migrate or erase external authority, tokens, mappings, provider IDs, checkpoints or historical audit evidence. Incompatible upgrade blocks dependent operations until reconciled. An undiscoverable registry does not delete already verified plugins; freshness and trust expiry policy determine if they can continue.

**Security, operation and ownership:** public descriptor is not a permission decision; approval and enablement are scoped to an authorised tenant, purpose, data classification, processing jurisdiction and operator. Audit records approval, sensitive enablement, version change and quarantine evidence; Logging receives sanitised discovery/health diagnostics; Reporting receives authorised plugin counts, version/support status and operational metrics. Configuration may select permitted plugin references, never create an active connector by preference alone. Infrastructure/Coolify or host-provided deployment services run plugin containers; Scheduler discovers/checks them; Message Queue carries committed registry state events. Registries/transport remain replaceable and do not mandate a proprietary marketplace, arbitrary public package source, Redis or an external hosted integration platform.

**GUI addition:** within `Capabilities → Integrations`, provide a **Plugin Catalogue** with discovered, unverified, approved, installed/available, enabled, disabled, incompatible and retired entries; detail/permissions/data-residency/licence screens; trusted source management; administrative approval and lifecycle controls; version history, rollout/rollback, incident quarantine, provider status and tenant-level binding. Plugin enablement must not be confused with separate *Connect account* OAuth/consent. Use host sidebar/dashboard shell, public contract APIs, server authorisation and Theme Manager vocabulary.

**New conceptual acceptance:**
- Register an approved remote adapter endpoint during host uptime → compatibility and publisher evidence validated; admin approves/activates; connector appears in catalogue and works without Nuxt host rebuild.
- Malicious, unsigned/untrusted or incompatible plugin appears in discovery → quarantined/unsupported, no execution or credentials issued.
- Plugin is enabled for Tenant A but not Tenant B → Tenant B's discovery is appropriately scoped and operations rejected.
- Plugin upgrade occurs with ongoing provider operation → original version pinned or operation safely reconciled; no duplicate external side effect.
- Provider callback arrives after plugin was disabled → authenticated/recorded and reconciled under allowed policy, never treated as a new approved operation.
- Registry unavailable → show cached/source-freshness/degraded status; do not fabricate new plugin approval.
- Plugin is removed or rolled back → historical receipts, Audit references and lawfully retained checkpoints remain available; pending effects explicitly unknown where necessary.

**Open implementation investigation:** manifest schema/registry protocol, signature trust roots and revocation, process/container RPC and mTLS/service-identity, scoped secret broker, deployment/health hooks, rolling upgrade strategy, callback routing when plugin versions change, supply-chain checks, whether a shared lightweight plugin catalogue standard with Gaming is justified **without merging their domain ownership**, and compatibility with deployed infrastructure. **Decision interaction:** INT-07 (local installation-operator trust then tenant enablement) and INT-09 (risk-based authorisation, with higher assurances/independent approval where justified) have since been owner-approved. Plugin runtime support must enforce individual permissions and data disclosure. No new infrastructure repository or package is approved here.

## INT-07–09 approved governance and user-specific entitlement — 18 November 2026

**Status: owner-approved conceptual decisions, not implemented or new normative governance.** The owner approved the proposed defaults for INT-07, INT-08 and INT-09, and clarified **per-user visibility and use of integrations within an organisation**. This decision supersedes the earlier `open` labels in this record; historical review notes remain retained.

**INT-07 — two-stage plugin trust and organisation activation.** The installation operator (including the owner of a self-hosted installation) reviews/approves plugin publisher, package integrity, compatibility, security and allowed processing. A tenant/organisation then independently approves enabling that plugin for specified business purpose, data scope, remote account and permitted operation classes. Plugin discovery, trust approval, deployment/availability, tenant enablement and individual use are separate states. No central vendor marketplace, central Nuxt Layers permission or automatic discovery-to-execution privilege is required.

**INT-08 — domain-owned single authority per scope.** The respective business domain (Accounting, Booking, Inventory etc.) owns the selection/meaning of native or external authority for its specific resource/function/period; exactly one effective authoritative writer exists for that scope. External grant/connection does not independently switch authority. Changeover requires domain-authorised mapping, reconciliation of outstanding operations and verified checkpoint/cutover; no silent fallback, competing writer or inferred completion during provider outage.

**INT-09 — proportionate risk-based, per-operation control.** Policy classifies the plugin's requested data/operations and any particularly sensitive action as low/medium/high/critical (illustrative policy categories, not universal statutory categories). The effective required assurance, privileges, approvals and constraints arise from the operation's real scope, reversibility, sensitivity, relevant legal rules and approved organisation policy; mandatory two-person checks, specialist certification and elevated reauthentication apply only where required. A high-risk integration may be organisationally enabled while lower-trust users have no right to discover or use it. Sensitive actions must be re-authorised independently of plugin activation.

### Individual users: discovery and permitted use

**Owner's example:** In the same organisation, the owner may be authorised to **see and use both a public-weather provider and a banking connector**, while a lower-trust user may **see and use only the weather connector**. Organisation ownership is not an unconditional bypass of statutory/security restrictions; the owner also requires the appropriate financial permissions and assurance. Conversely, a delegated financial officer could be permitted banking functions without becoming the organisation owner.

**Required public input:** caller identity and active tenant/organisation context from Identity and Authentication; current subject assurance/reauthentication; resource/action-specific Authorisation decision and applicable approved role/grant/delegation policy; tenant-enabled plugin, purpose, data and provider-account scope; risk classification and Legal Compliance/Privacy constraints where necessary; current feature/connection state. Roles or hierarchy alone must not be treated as blanket inherited access. A shared tenant-wide enabled flag **never** grants access to all tenant members.

**Required public outputs:** `listVisiblePlugins(caller, organisationContext)` returns only allowed catalogue descriptors and personally allowed operations, suitably minimised; `getPermittedPluginActions(pluginId, resourceContext)` yields the current authorised operation classes and reauthentication/approval requirements without revealing restricted accounts or existence; `getVisibleConnections` exposes only accounts permitted for that user. All results carry readiness, source and permission/freshness limits. Denied items are **omitted**, not simply shown as clickable/disabled, where even their existence is restricted. An administrator with approved discovery but not use permission may see a 'restricted' listing only if the policy explicitly authorises its disclosure.

**Important semantic split:** `plugin.discover`, `plugin.manage`, `connection.view`, `connection.manage`, `integration.use`, and finer-grained actions such as `banking.balance.read`, `banking.payment.initiate`, `provider.data.export` are separate *illustrative* action permissions evaluated via Authorisation against plugin, connection, remote account and underlying business resource. Discovery permission and GUI menu display are not use permissions. The server rechecks the actual action on each command/query/callback access; stale cached UI entitlements, direct API calls, guessed URLs or changed account privileges must not bypass denial. The relevant domain capability also enforces its own business permissions.

**Screens:** Host sidebar → Integrations dashboard, provider catalogue and connection/action menus are projected from the user's current authorised discovery/read results, not from unfiltered tenant/global provider inventory. The organisation owner can see Weather and Banking; the low-permission member sees Weather only. Privileged users receive additional management/approval views only with explicit `plugin.manage`/connection-specific permission. When a user's grant is revoked, the next protected operation denies immediately; UI/cache refresh removes the restricted entry, including cross-device sessions as appropriate. Missing permission data or security policy fails closed. Support accessible 'not authorised' responses without leaking provider existence.

**Reciprocal contract obligations:** Authorisation owns the decision, grants, risk-aware resource/action evaluation and revocation; Identity owns organisation membership and caller relation; Authentication owns assurance and reauthentication. Configuration owns approved tenant/provider choices; Integrations owns registry/connection and filtered projection of what it can safely disclose. Domain owners retain their own action authority and external/native cutover decisions. Audit receives attributed grant/approval and denied sensitive-operation evidence according to risk catalogue, Logging gets minimised diagnostic events and Reporting may use only appropriately authorised aggregates (avoid counts that reveal restricted providers).

**Conceptual acceptance:** (1) Owner with approved banking and weather rights sees both and can invoke only scoped allowed actions; (2) low-trust colleague sees and uses weather, cannot list or call banking routes, connection details, catalogue entries or endpoints; (3) user who can see banking but cannot initiate payments sees only permitted banking read actions; (4) revoking rights closes API access immediately and invalidates or expires visible catalogues; (5) plugin disabled/connection expired masks even otherwise permitted actions; (6) cross-tenant query or provider callback cannot disclose account existence; (7) escalated operation prompts verified reauthentication/two-person approval only where effective policy requires it; (8) a domain cutover never changes solely because connection becomes active.

**Implementation follow-up, not a conceptual blocker:** settle concrete permission taxonomy and delegated admin semantics against actual Authorisation/Identity published contracts, cache invalidation and expiry, trusted callable discovery query, outbox/denial evidence, UI route guards and test fixtures. The conceptual distinction between global plugin trust, tenant enabling and **per-person discover/use** is approved.

## System-wide mandatory server-side authorisation — owner confirmation (18 November 2026)

**Status: owner-confirmed system-wide requirement; already established by the governing [Architecture](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/architecture.md) invariant "Access is decided on the server. Client-side checks are for the experience only", and by normative contract/security obligations.** This review records the mandate explicitly for Integrations; it does not create a new governing ADR or replace Authorisation.

Every protected read, query, command, write, export, administrative operation, plugin invocation, asynchronous/background action and disclosure must validate the relevant trusted caller/service principal, tenant/organisation context, requested action, target resource, applicable policy and current Authorisation decision **at the trusted server/enforcement boundary** before executing or returning protected information. Missing, denied, expired, ambiguous or unavailable decisions **fail closed**. Actions performed by scheduled jobs or external callbacks use their independently authorised trusted service/event context, not an impersonated browser user or a webhook's bare assertion. Domain capabilities enforce their own invariants as well.

Client-side filtering, hidden navigation, disabled controls and route middleware serve usability and minimise exposure but **never replace server checks**. A valid request URL, enabled plugin, connected external account, tenant membership, role label, payment entitlement or trusted provider response alone confers no access. Both read paths and mutations require checks; secure server-side query scoping and response filtering prevent ID enumeration, cross-tenant access and aggregate leakage. Cached authorisation information cannot override revocation or defined freshness limits. Audit risk-selected denials/privileged changes without leaking secrets; Logging receives sanitised failures.

**Scenario:** organisation owner may see/use Weather and Banking only with actual action-specific rights; lower-permission user sees/use Weather only. Calling Banking's API directly, guessing connection IDs, querying provider statuses, invoking plugin RPC or triggering an async job must still be denied and must not reveal restricted banking information. If the policy service is unreachable, Banking access is refused rather than silently allowed. User interface changes alone are never proof of enforcement.

**Acceptance:** attempt each protected endpoint/command directly without UI, with denied/missing/revoked/foreign-tenant credentials, and through queued/plugin pathways; verify denial before data access or side effect. Verify permitted users succeed only within granted operation/resource scope, and no unauthorised data appears through search, reports, caches or error messages. These are future CI/user-driven tests, not locally executed tests in this conceptual review.

## Historical reciprocal notes (preserved verbatim)

## Review notes — contacts, financial providers and ownership (14 November 2026)

**Provisional conceptual notes only; verify root public contract before detailed Integrations specification.**

- Provider connectors (e.g. Xero/QuickBooks, payroll, procurement, banking, CRM) manage connections, provider-specific identity and field mapping, transport, checkpoints, provider limitations and status; they never silently become the owner of Product, Inventory, Asset, Order or Accounting domain facts.
- Accounting and Invoice independently select an approved authority per tenant/accounting context and supported service. Provider scope and compatibility must be verified; no assumption a connected product implements every accounting or invoicing operation.
- A connected customer/supplier directory may be externally authoritative under a specific approved mapping, but **Identity** and **Profile** remain authoritative for platform identities and personal-data disclosure.
- Provider outage does not silently switch authority. Changeover requires approved mapping, reconciled balances and outstanding work, source/remote IDs, versioned checkpoints and explicit cut-over.
- Imported financial transactions, asset registers, stock costs, supplier records and contacts must be validated and authorised by their owning domain, with provenance and replay/deduplication handling.

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Provider-neutral connection and transport mechanisms; never own commercial, physical-stock or financial domain records.
- **Related capability notes:** [accounting](../accounting/capability-record.md), [invoice](../invoice/capability-record.md), [order](../order/capability-record.md), [product](../product/capability-record.md), [inventory](../inventory/capability-record.md), [logistics](../logistics/capability-record.md).
- **Open architectural questions:** Per-tenant authority/connector selection, provider compatibility, external party-directory mappings and reconciled changeover.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.

### Government, accounting-framework and financial-provider interface notes

- **Accounting frameworks and tax rules** are not ordinary connector payload transforms. [Accounting](../accounting/capability-record.md) owns financial posting meaning and approved framework/rule application; [Legal Compliance](../legal_compliance/capability-record.md) owns obligation/constraint determination. Integrations owns provider connection, credentials, schema adaptation and transport/checkpoint evidence.
- **Government portal adapters** may handle authenticated tax/financial submissions, acknowledgements, status checks, amendments and delivery errors for a tenant/accounting entity. Accounting remains owner of the authoritative reconciled return and its business state; a successful HTTP transport does not prove a filing was accepted.
- **Provider capability discovery** must declare supported operations, geographical/period/API restrictions, scope and permissions, synchronisation semantics, read-back and mapping capabilities. Missing regulated functions or required rules must surface as unsupported/requires-review, not silent local fallback.
- **Change control:** tax-framework updates, remote schema revisions, connector credential changes and provider migration require versioned mapping, evidenced effective dates, safe retries/idempotency and explicit authorisation. Connector code cannot bypass Accounting's immutable posting/period controls.
- **Open:** which provider registration/attestation, sandbox certification, government gateway security, legal acceptance evidence and integration-country constraints require Legal Compliance review before enablement?

## Cross-capability note — External Billing authority and provider interoperability (15 November 2026)

**Agreed conceptual relationship: BIL-05 approved on 15 November 2026; provider functionality remains unverified.** [Billing](../billing/capability-record.md#modes-provider-authority-and-migration) selects a single authoritative commercial-charge mode per approved scope (native or verified provider), validates commercial semantics, controls cutover and reconciles charge status. Integrations owns provider connection, credential-reference management, capability discovery, mapping, transport, webhook provenance, retries and revocation, not the charges. Missing provider acknowledgement means pending/uncertain, not success or failure; no silent native fallback, duplicate periods or competing charge authority. No connector implementation or provider operation is asserted.

## Cross-capability note — External Booking provider authority (15 November 2026)

**Proposed reciprocal relationship, not verified provider support.** [Booking](../booking/capability-record.md) controls selection of one effective authoritative capacity owner per resource/scope/period, reservation business lifecycle, local mappings and reconciliation state. Integrations owns configured connections/credentials, provider operation discovery, authenticated webhook/transport and technical sync checkpoints. Booking supplies authorised hold/confirm/amend/cancel intent and idempotent identity; Integrations returns authenticated, provenance-rich external operation evidence, capability limitations and failure/uncertainty. Provider timeout or webhook receipt does not prove successful booking. Authority transfer needs reconciled checkpoint/cutover, no dual-writer capacity guarantees and explicit unsupported-operation handling.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved, TEN/COM/OWN and policy details proposed; no implementation assertion.

Provide verified external company registry, payment and authority evidence transport and provider status, not adjudication of legal authority, commercial settlement or domain ownership. Preserve mapping/provenance, tenant isolation and provider uncertainty.

References: [tenancy](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy](../../proposals/policy-and-governance-boundaries.md), [recovery](../../reviews/organisational-ownership-and-recovery.md). Conceptual relationship, not mandatory package dependency.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Review-approved documentation direction, not an implemented interface or governing ADR. See [safety review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

Provider-neutral external adapters may support specialist image/NCII detection, URL intelligence, KYB/KYC, age assurance, fraud signals and regulatory submission transport where appropriate; respective specialists/domain owners own semantics and use. Record lawful sharing, processing location, provider/version, costs, timeout, idempotency, unknown outcomes and exit. An external acknowledgement does not establish authoritative legal filing truth.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

External proofing, age-assurance and merchant-verification adapters should be provider-neutral where approved by public contracts: trusted callbacks/nonces/audience, lawful provider processing and data minimisation, claim quality, expiration/revocation, errors, billing, retries and outages. Integrations transports qualified assertions, not independent legal identity, merchant permission or content access decisions.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Proposed Verification capability consumes national ID, age/KYB, document-proofing or credential issuers through provider-neutral Integrations/host adapters where contract-appropriate. Integrations owns transport and connection lifecycle, never the attested truth or local eligibility; country-specific APIs need lawful provider access, data-residency and usage-right checks.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Integrations owns connections, provider authentication, credentials, status and synchronisation; Configuration may expose authorised provider selection references. Selected does not mean connected, deployed or enabled. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-08 (Option B):** versioned setting declarations, staged activation and explicit migration/rollback protect provider selection revisions; Integrations remains responsible for provider availability, connection credentials, transition and reconciliation. A settings migration cannot silently activate an unverified provider.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Integrations may adapt remote LMS course catalogues into provenance-marked Course draft imports and controlled exports; Course owns any locally accepted definition. Provider claims do not establish enrolment, completion, course accreditation or publication. This note does not complete the separate integrations review.

## Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)

**Status: Owner-agreed boundaries, no independently completed integrations review or implemented API.** [Course](../course/capability-record.md) and [Assessment candidate](../assessment/capability-record.md): **COURSE-10 agreed principle:** provider-specific accreditor/awarding-body registers, recognition status, issuer/delegate mandates, qualification codes and credential status/award responses are obtained through authenticated, provenance-rich Integrations connectors. They must expose origin, effective dates, verification time, stale/unknown/revoked status and reconciliation; cannot silently transform remote assertions into Course, Assessment or qualification authority. Course can retain safe verified-as-of recognition references; actual award/credential lifecycle belongs to a separately reviewed authority boundary.

## COURSE-12 — Qualification authority reciprocal note (18 November 2026)

**Status: Owner-approved conceptual responsibility; detailed Qualification review and implementation pending.** [Qualification candidate](../qualification/capability-record.md): **COURSE-12 owner-approved:** Qualification owns qualification-specific authority/recognition and award-decision semantics, while Integrations owns provider-specific accreditation and awarding-body API adapters, authenticated registry evidence, delegated mandate lookups, external award responses and status callbacks. Source authority, scope, effective time, last verification, expiry and unknown/conflict status accompany claims; external connectors never grant local legal powers or overwrite qualification awards silently. No change to previously approved integrations ownership.

## Assessment external examination provider interface — 18 November 2026

**Status: Assessment ASMT-13/14 owner-approved conceptual relationship; provider connector implementation not asserted.** [Assessment](../assessment/capability-record.md): Integrations authenticates and transports external assessment evidence, provider status, callbacks, capability discovery, source identifiers, checkpoints, retries and uncertain results. Verification evaluates issuer/source trust within scoped claim, jurisdiction and effective-time requirements. Assessment decides locally whether the externally reported mark/evidence is admissible, preserving historical source snapshots and qualified freshness; source connectivity or signed messages alone never create grading, qualification or credential authority. Provider timeout remains unknown; correction/revocation requires explicit reconciliation. No cyclic package dependency.


## Qualification independent conceptual review — reciprocal interface (18 November 2026)

**Status: proposed detailed contract under [Qualification review](../qualification/capability-record.md), PR #65; COURSE-12 ownership remains owner-agreed.** Qualification relies on provider-neutral interfaces for trusted recognition/approved-centre/delegation evidence, external award decisions, correlation-aware submissions and verifiable callbacks. Integrations owns connector mechanics and provider authentication, not the meaning or authority of qualification decisions. Preserve source/observed/effective times, uncertainty and idempotent reconciliation; provider outage is not withdrawal of recognition. This note does not complete this adjacent capability's independent review or assert an implemented contract.



## Reciprocal conceptual note — Credentials lifecycle and public contract (18 November 2026)

**Status: proposed Credentials review alignment (18 November 2026; [PR #62](https://github.com/nuxt-layers/architecture-blueprint-review/pull/62)).** Integrations supplies provider-neutral connectivity/transport to issuer mandates, remote issuance/signers, credential registries and status services. Provider requests/callbacks carry correlation/idempotency, source attribution, authenticity and effective/freshness context. Credentials retains issuance, representation and credential-status decisions; external award and registry authorities retain their actual source standing. Transport success is not an issued credential; outage is not revocation; reconcile duplicates and uncertain outcomes.

## Reconciled master reciprocal notes — 18 November 2026

## Events interface reciprocity — 18 November 2026

**Events EVT-08 (owner-approved, 18 November 2026):** [Events](../events/capability-record.md) must expose a provider-neutral public contract to Integrations: authorised event/occurrence snapshots, change/withdrawal requests, local/external stable ID mappings, authority scope and version; receive verified proposed external changes, provider version, delivery status, retry checkpoint and conflict evidence. Integrations owns connector credentials, webhook verification, provider-specific schemas, transport, provider recovery and connection lifecycle, never Events programme or status. A provider acknowledgement cannot commit an Events change. See [contract and reconciliation details](../../../reviews/events-contract-attendance-and-handover.md). This is conceptual, not a verified published API.

## Federation — reciprocal conceptual note (18 November 2026)

**Status:** Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69), not a published implementation contract or completed independent review. See [Federation conceptual contract](../federation/capability-record.md).

Integrations may supply replaceable external protocol/provider adapters through public ports; Federation retains participation, provenance, subscription, delivery and reconciliation authority. Third-party transport acknowledgement is neither local source completion nor trusted remote standing. Unsupported provider yields explicit degraded status. Public directional ports, explicit absence modes and acyclic package dependencies apply.



## Inventory reassessment reciprocal proposal — 18 November 2026 (PR #81)

**Status: proposed, not approved or implemented.** Integrations supplies provider-neutral connections, source mapping, signed/evidenced remote observations and synchronisation status. The **proposed** revised Inventory boundary distinguishes marketplace stock mirrors, 3PL custody observations and an optional explicitly selected external-authoritative stock master. No automatic takeover, provider-presence authority inference or simultaneous dual writers; scoped cut-over, fencing and reconciliation are required if that future mode is selected. Integrations does not own stock balances. See the [Inventory reassessment contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md) and [Inventory record](../inventory/capability-record.md#renewed-conceptual-design-challenge--18-november-2026-draft-pr-81). This note preserves earlier approvals in this capability and does not complete its independent review.


### Inventory manufacturing traceability — owner-approved conceptual reciprocity (18 November 2026; PR #81)

**Approved Inventory-side conceptual requirement:** Provider-neutral barcode scanners, labels, optional MES/ERP/3PL and subcontractor coating connections can supply attributed stock observations, mapping and sync health. Inventory validates scans and maintains its chosen authoritative stock account; a scan, offline cache or plugin installation cannot grant access or promote an external system to stock master. External authority mode requires explicit account-level governance and cut-over. This note approves the **Inventory-side requirement only**, does not change this capability's independent approval status or claim a running integration. See [shop-floor flow and public contract](../../../reviews/inventory-conceptual-reassessment-2026-11-18.md#owner-decisions-and-manufacturing-material-flow-refinement--18-november-2026).

## Cross-capability note — Invoice conceptual public contract (18 November 2026)

**Owner-approved Invoice conceptual review (18 November 2026); reconciled with merged Integrations PR #76; implementation not verified.** [Invoice](../invoice/capability-record.md) owns document authority, issuer selection, idempotent issuance, confirmed versus unknown provider status, reconciliation and cut-over policy; Integrations supplies approved connector capabilities, authentication/mapping/transport/read-back and checkpoint evidence. A transport success never proves issuance; no native failover after ambiguous remote result. Both conceptual boundaries are owner-approved; no implemented integration is asserted.


## Recruitment reciprocal contract proposal — 20 November 2026

**Status: Proposed in [Recruitment draft PR #99](https://github.com/nuxt-layers/architecture-blueprint-review/pull/99), not owner-approved or implemented.** Recruitment sends job-board/ATS intents and receives provenance-qualified provider receipts; Integrations owns transport, not hiring decisions or candidate cases. Cooperation uses published contracts/host ports, without private state or mandatory cyclic imports. [Recruitment record](../recruitment/capability-record.md).


## Legal Compliance reciprocal conceptual contract — 19 November 2026 (draft PR #85)

**Status: proposed, pending owner approval; not an implemented or published interface.** [Legal Compliance dedicated conceptual contract](../legal_compliance/capability-record.md) proposes scoped, time/version/source-qualified legal applicability, mandatory restrictions, holds, deadlines and uncertainty. **integrations** supplies only authoritative, minimally necessary resource/service/activity/tenant context and completion/refusal evidence through documented public contracts; Legal Compliance does not take ownership of integrations's records, business decisions or enforcement. Statutory interpretation is not personal Authorisation, Privacy's specialist consent/rights rules, or proof of regulator acceptance. Missing or conflicting mandatory legal qualification holds only the affected unsafe action; authorised source owners report applied decision version and partial/failed enforcement. Cross-capability cooperation is host-composed, not an implicit direct package dependency. Existing neighbouring decisions and active PR proposals retain their own status.
