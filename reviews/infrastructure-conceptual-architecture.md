# Infrastructure — conceptual architecture and public contract (18 November 2026)

**Status:** Proposed working design; owner sign-off pending. **Classification recommendation:** retain `infrastructure` as a Foundation responsibility, **implemented principally as host-owned operational composition and provider integration**, not a new mandatory cross-capability Nuxt Layer, business database, deployment service or storage abstraction. A narrow separately packaged operator/health contract is optional **only after** independent reuse and ownership are demonstrated. Catalogue candidacy is not approval to implement.

**Opening governing master:** `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. **Blueprint master:** `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. The current governing capability standard and accepted ADR-0015, ADR-0017 and ADR-0018 were inspected; accepted ADR-0012/0016 obligations are retained. Existing `nuxt-layers/infrastructure` repository is identified, but **no root `CONTRACT.md` could be retrieved on `master`**: no actual package/API is inferred. Related Clock, Configuration and Storage root contracts were read. Latest governing decisions supersede obsolete provisional comments in blueprint descriptions.

## Classification and ownership gate

- **Distinct outcome:** supply, apply, observe and recover the trusted host's operational runtime (databases, deployment platform, networks, worker/Temporal instances, time synchronisation, secrets and backup infrastructure) so separately owned capabilities can operate.
- **Authority:** the infrastructure **host/operator**, not a tenant application or individual capability, owns actual infrastructure resources and authorised operational change decisions. Provider control planes own their reported resource states. An infrastructure adapter may maintain narrow operation requests, evidence and checkpoints, but no second domain registry is justified.
- **Not owned:** Identity tenant/group/principal ownership; Authentication sessions; Authorisation decisions; Clock's formatting and temporal semantics; Storage's public object operations and consumer access controls; Site Hosting's verified domains and tenant-to-host routing; capability databases/outboxes and migrations' business correctness; Scheduler's schedules; Workflow's business processes; Message Queue's message transport; Temporal gateway SDK integration; Observability metrics and alerts; Logging diagnostics; Audit accepted evidence; commercial entitlements; provider truth.
- **Packaging options:** (A) host-owned operational composition and documented deployment/integration contracts (**recommended**); (B) separate framework-independent operational control capability, only if independently justified state and consumers emerge; (C) generic infrastructure Nuxt Layer (**not recommended**, conflates deployment authority and browser capability). The existing infrastructure repository may contain IaC/scripts/acceptance infrastructure without constituting an independently installable capability.
- **Persistence:** no new business store. Operational history/checkpoints only if host orchestration needs durable, replay-safe records; authoritative provider evidence and dedicated Audit/Observability records remain with their owners.
- **Disposition:** retain catalogue entry as *Foundation responsibility / operational composition candidate*, pending explicit approval of classification and any dedicated package. No normative catalogue change, repository deletion or implementation alteration.

## Host-owned lifecycle

Plan/declare intent → authenticate and authorise privileged change → validate security/policy/provider/compatibility → record approved immutable plan and pre-change evidence → apply guarded operation → independently observe/reconcile actual state → complete, mark degraded/uncertain, compensate or invoke recovery → preserve history and accountable evidence → retire/decommission under retention/hold controls. Requested, accepted, running, applied, verified, failed and **unknown** are distinct. Changes to secrets, network, database, backup and UTC source cannot be treated as completed merely because a provider acknowledged a request.

Native duties: versioned deployment configuration and provider inventory; safe database/queue/worker startup and readiness; secure secret injection and rotation coordination; backup/restore orchestration and tested recovery paths; provider incident/degradation classification; time-sync provider approval, NTP/NTS trust, leap-smear compatibility, step/slew and holdover; health/status projection. Resource creation and implementation-specific provisioning remain host/provider actions. No universal tenant-configurable infrastructure administrator.

## Idealised public inbound contract

| Inbound surface | Producer / authority | Meaning, validation and failure |
|---|---|---|
| `ReadInfrastructureStatus` | authorised host/monitor | installation/environment/resource scope, permitted fields, freshness; insufficient permission denies, unreachable provider yields unknown/degraded, never fabricated healthy |
| `ProposeOperationalChange` | strongly authenticated and authorised platform operator / host | resource intent, reason, target/revision, evidence, approval references, expected state, idempotency; validate allowlist, policy, capability impact, concurrency, permitted window; invalid/conflicting rejected |
| `ApproveOrCancelChange` | independent authorised governance actor | operation ID, approved plan revision, role/assurance/expiry; no self-authorised floor weakening, stale approval invalid, cancellation only if reversible |
| `ApplyOrReconcileChange` | trusted operator automation | approved plan ID, concurrency token and retries; recover after crash, never repeat an unsafe non-idempotent provider action on uncertain outcome |
| `RequestBackupRestoreOrRecovery` | approved operator/incident procedure | scope, data owner, snapshot provenance, recovery point, privacy/retention constraints, safety acknowledgements; hold on ambiguous target or unverifiable integrity; recovery cannot imply business correctness |
| `ConfigureTimeSynchronisation` | privileged host infrastructure authority | approved UTC authority candidate, NTP/NTS verified properties, trust and provider policy revision, allowed fallback and smear regime; **Configuration does not own source selection** (CFG-07). Tenant locale/zone never changes shared UTC |
| `IngestProviderEvidence` | trusted provider agent/control plane | resource revision, state, observation instant, health, sync/backup/restore evidence, signature/authentication and expiry; unauthenticated/stale/conflicting evidence remains unknown |
| `ReadQualifiedConstraints` | Legal Compliance/Privacy and capability owners where relevant | applicable controls, residency, retention/hold, security requirements and dependent readiness; no source-owner migration assumed, inability to prove mandatory guard blocks unsafe actions |

The host supplies trusted credentials and deployment configuration, not browser secrets. All mutating interfaces are **server-only** and require server-side Authorisation and appropriately recent phishing-resistant Authentication for critical operations where applicable. Identity gives trusted operator identity/tenant/installation scope, not an automatic infrastructure grant. Configuration may publish *permitted declarative settings* but not override immutable host/provider policy or secrets. Interfaces describe meaning, **not implemented names or endpoints**.

## Idealised public outbound contract

| Outbound surface | Consumer and permitted conclusion | Provenance/failure |
|---|---|---|
| `InfrastructureReadiness` | host, deployment gate, capability operators: runtime dependencies present/readiness known | per resource/installation, evidence source and age; ready/degraded/unknown/unavailable; never equals capability business health |
| `OperationalChangeResult` | initiating host operator, Workflow where used | requested/approved/applying/provider-acknowledged/verified/failed/uncertain/compensated status, change ID, revision, operator and evidence references | authoritative only for host coordination; provider assertion remains qualified |
| `ResourceCapabilityStatus` | Scheduler/MQ/Temporal gateway and hosting adapters | connection readiness, approved endpoint/credential reference, capacity constraints; secrets delivered over trusted channels, not a general public discovery API |
| `UtcSynchronisationStatus` | Clock host composition, Observability, authorised operator | desired/applied source, authenticated trust evidence, source revision, offset/uncertainty, freshness, failure, holdover, leap/smear compatibility, recovered state; may certify only independently verified policy conditions | fails degraded/unknown when unverified; Clock `now()` remains synchronous host-supplied instant and never does NTP itself |
| `BackupRecoveryEvidence` | data owner, Audit, authorised operator | verified snapshot identity, coverage, recovery-point window, integrity, restoration reconciliation and exceptions; a backup receipt is not tested restoration | restricted disclosure; owner must validate logical data correctness |
| `InfrastructureChangeCommitted` / `InfrastructureIncidentChanged` | Audit, Logging, Observability, approved notifications | host-owned operational transition facts with correlation/replay identifiers; never grants downstream authority | only after committed coordination transition, at-least-once delivery, deduplication, no exactly-once assertion |
| `SanitisedOperationalSummary` | Reporting/operator dashboard | authorised aggregated resources, availability and historical change summaries | redact secrets, provider tokens, private endpoints, personal data; show staleness and partial coverage |

**Shared context:** installation/environment, trusted actor and assurance, authorised operation/resource, optional tenant effect (not tenant authority), correlation and idempotency keys, expected revision, policy and source revision, effective UTC instant and synchronisation confidence, independent approval evidence, provider identity, provenance, result finality. No mandated universal request object. Commands never bypass data owners' migrations or privacy constraints.

## Cross-capability relationship matrix (conceptual, not package imports)

| Cooperating owner | Inputs Infrastructure obtains | Outputs Infrastructure supplies | Availability and boundary |
|---|---|---|---|
| Host/application composition | deployment intent, credentials, approval, provider selection | applied state, readiness, results | **required** host trust anchor; host owns actual IaC/cloud control plane |
| Identity / Authentication / Authorisation | verified operator and scoped access/assurance decisions | privileged action target and evidence | **required for interactive changes**; never infer rights from tenant hierarchy or deployment admin label; break-glass is exceptional and independently audited |
| Configuration | permitted schema-checked operational values and revision | effective applied revision/status | optional for host-managed settings; **not** NTP source authority |
| Clock | temporal representation and host `now()` port contract | qualified UTC host instant and sync quality for host consumers | time source essential; Clock is not an NTP implementation |
| Observability / Logging / Audit | monitoring observations / diagnostics / independent evidence acknowledgements | metrics and health / sanitised logs / privileged event evidence | conceptually cooperating, independently authoritative; failure to send evidence triggers governed fail-safe for critical changes |
| Privacy / Legal Compliance | holds, residency, jurisdiction and deletion constraints | operations affecting protected state and evidence | conditional to affected data; uncertain binding prohibition holds unsafe operations |
| Storage | public object provider constraints, ownership of file-byte access surfaces | host provisioned S3 credentials/endpoints and resource health | Storage owns its consumer contract, no general database/Temporal/backup reclassification as object storage |
| Site Hosting | required ingress/domain/certificate operational intents | reverse-proxy, TLS, deployment readiness | Site Hosting owns domain proof and mapping, host runs proxy/certificates |
| Scheduler / Message Queue / Workflow | worker, transport and orchestration readiness requirements | infrastructure endpoints, health and deployment status | no reassignment of schedule, message, approval or process ownership |
| `temporal-gateway` | provider-neutral host connection/worker requirements | vetted Temporal connection and operational readiness | ADR-0015 library owns SDK integration only, no business state |
| Capabilities owning Postgres schemas/outboxes | approved migration/backup requirements, consistency checkpoints | running Postgres, connectivity, safe change/recovery evidence | each capability owns schema, domain migrations and transactional outbox |
| Notification/Reporting | optional incident notices and authorised summaries | qualified incident/status change | optional; outage does not silently convert an unsafe state to success |

**Direction:** consumers use documented host-supplied ports; Infrastructure never imports business implementation or reads private tables. Hosts compose provider resources and capability interfaces. Avoid a reverse `Infrastructure → Scheduler → Infrastructure` cycle: use host-managed bootstrap/reconciliation mechanics for infrastructure-critical recovery, not application Scheduler/Workflow as an essential prerequisite. Monitoring is allowed to degrade without making critical mandatory Audit evidence optional.

## Security, privacy, reliability and provider neutrality

Apply least-privilege service identities, separate deployment from tenant governance, scoped secrets, encryption, secret rotation, network segmentation, safe migrations, change review/separation of duties, signed/versioned artefacts, supply-chain assurance, recoverable backups and protected recovery credentials. Infrastructure-level authority must never become unrestricted tenant-data visibility. Maintain evidence of provider region, workload/data residency, costs, portability and exit tests. Snapshot coverage, RPO/RTO targets, restoration integrity, retention/deletion rights and partial outage response are deployment-specific **open technical evidence**, not invented guarantees. Do not log secrets or privileged payloads. OS/server clock synchronisation cannot be weakened by per-user locale, tenant display settings or browser input. Fail closed where identity, privilege, mandatory holds or UTC trust cannot be evidenced; ordinary read-only monitoring can display *unknown*.

## GUI and host integration

**No public/tenant sidebar entry.** For a privileged host operator, an optional `Operations → Infrastructure` sidebar entry leads to an Infrastructure dashboard using the application-test-template's host-owned navigation pattern, not automatically registered by a Nuxt dependency. Screens: environment readiness/resource topology; provider/connection health; deployment versions and change queue with approvals/impact/preflight; backup and restore status with high-risk confirmation; secret rotation *status* (never secret values); incidents/maintenance and recovery; **Time synchronisation** showing authoritative NTP/NTS policy and measured quality; change/evidence history and alerts. Restricted drill-downs, explicit stale/unknown states, step-up and dual approval for destructive actions, accessible confirmation and failure notices. Headless monitoring/control is the default; operators may use external secure deployment consoles instead of a newly created UI. WCAG 2.2 AA, responsive layout, BCP 47, accessible theme tokens via Theme Manager. No browser-side provider credentials or private schema access.

## Conceptual acceptance scenarios

| Input situation | Expected result / authority |
|---|---|
| Valid signed host bootstrap and verified provider | readiness with observed revision/quality; host/provider authority |
| Operator submits approved revisioned deployment | pending until independently verified applied; host coordination |
| Replay same operation ID | same outcome or reconciled unknown, never duplicate destructive restore; host |
| Stale change plan or unauthorised tenant admin | rejected without provider action; Authorisation + host |
| Provider acknowledges backup but integrity unverified | accepted/unknown, not verified/restorable; host/provider, source data owner separately |
| Restore from incorrect tenant or held resource | hard rejection/hold; source owner Privacy/Legal Compliance constraints |
| NTP source unreachable or untrusted | quality degraded/holdover/unknown, no false trusted UTC; host/Clock boundary |
| Leap-smear incompatibility or invalid timezone-as-source | refuse policy application; Infrastructure |
| Temporal/queue service unavailable | readiness degraded; do not fabricate business schedule/job/message success |
| Provider timeout after change submission | reconcile using provider revision before safe retry; no false completion |
| Revoked operator or high-risk self-approval | deny action despite deployment or parent-tenant status; IAM |
| Infrastructure offline, UI still accessible | read-only stale/unknown with last observed evidence and incident; Observability |
| Attempt to modify a capability's domain migration through generic control | unsupported; owning capability retains lifecycle |

## Decisions and evidence register

- **Established:** architecture-rules capability standard; ADR-0015 infrastructure integration library distinction; ADR-0017 tenant/operator separation; ADR-0018 mandatory policy floor; ADR-0012/0016 contract/composition/direction; existing Clock and Configuration owner-approved UTC/CFG-07 decisions as recorded in blueprint.
- **INF-01 — Open owner decision:** endorse Foundation *operational responsibility and host composition* rather than mandatory independent Nuxt Layer; allow separately reusable headless control only with demonstrated authority.
- **INF-02 — Open owner decision:** confirm operator-only optional GUI and no tenant-facing infrastructure source controls.
- **INF-03 — Open owner decision:** approve narrow public inbound/outbound contracts and the provider-uncertainty/verified-result distinction; exact type definitions are deferred.
- **INF-04 — Open owner decision:** authorise recovery and backup approval boundaries, including independent sign-off, exceptions and legal holds; set jurisdiction-specific policy separately.
- **INF-05 — Open owner decision:** preserve Infrastructure's exclusive privileged time-source selection and host qualified UTC quality contract as distinct from Clock and Configuration.
- **Technical investigation, not owner policy:** inspect implementation root contract when available; provider SDK/availability and support; deployment model; restore proofs; synchronisation thresholds/fallback/NTS; definitive service exposure and versioning.
- **Implementation alignment:** publish any chosen independent root `CONTRACT.md`, compose under accepted ADRs, demonstrate provider/operational tests and security evidence separately. This review performs none of these tests.
- **Sign-off:** pending INF-01–05; no assertions of operational/compliance readiness.

## Review challenge and consequences

A centralised 'infrastructure capability' that controlled every domain's database, secrets, business migrations and tenant authorisation would violate bounded ownership and generate an unreviewable privileged bypass. Conversely, mere IaC configuration should not be packaged as a fake runtime capability. Prefer host-side operational contracts with limited independently demonstrable status and control surfaces. Align working catalogue/register terminology to the chosen *provisional* classification; preserve governing catalogue until a separate approved governance change. Reciprocal notes are added in the source records, clearly non-normative.
