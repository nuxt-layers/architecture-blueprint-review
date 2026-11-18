# Infrastructure review — approved decisions, Clock boundary, standards, libraries and GUI (18 November 2026)

**Status:** Owner approved INF-01 through INF-04 and the recommendations of PR #75. INF-05 is **approved with an explicit Clock boundary clarification**: Infrastructure uses Clock's *published date/time interpretation and formatting* where applicable, but Infrastructure/host remains authoritative for operating-system NTP/NTS synchronisation, source selection and verification, measured quality, fallback and recovery. Clock's synchronous `now()` must use the host's time source and must never fetch NTP/network on its own. This clarifies—not replaces—the already approved CLK-03/04 and CFG-07 boundaries. No new direct package dependency or circular import is mandated. UTC sync health is sourced from Infrastructure/Observability; Clock formats the status timestamps. **Approval is conceptual only**, not an implemented root CONTRACT or production acceptance.

## Plain-English outstanding considerations

The host has to configure and operate the environment without taking over capability data, credentials or decisions. Successful provider requests are not necessarily completed operations; the host must independently reconcile outcomes. Define who may deploy, approve, restore, rotate secrets, inspect infrastructure and enter controlled break-glass. Each environment needs security boundaries and tenant isolation, durable provider-neutral operational evidence, reproducible configuration, compatible migrations, independent backup and recovery, and a tested way to recover if the platform Scheduler/Workflow/Message Queue is itself unavailable. Time synchronisation must indicate proven source trust, offset, age and holdover, not just the wall-clock reading. Consent, privacy, legal holds and retention apply to backed-up data without letting infrastructure operators claim business ownership. Keep development-only Docker/Temporal/Postgres setup separate from actual production assurance; the current Infrastructure README explicitly disclaims production readiness and calls this repository **not a Nuxt layer**.

## Approved conceptual public contract (not currently published implementation API)

Inputs into host infrastructure coordination: `ReadInfrastructureStatus` from authorised monitor; `ProposeOperationalChange` from privileged host operator; `ApproveOrCancelChange` from independent authorised reviewer; `ApplyOrReconcileChange` from trusted automation; `RequestBackupRestoreOrRecovery` under restrictions; `ConfigureTimeSynchronisation` exclusively from the privileged Infrastructure authority; `IngestProviderEvidence` from trusted providers; and `ReadQualifiedConstraints` from legal/privacy and other authoritative owners. Validate strong caller assurance, scope, approval, expected revision, idempotency, source and freshness. Rejected and unknown are distinct; never assume authorisation from merely receiving an event.

Outputs: `InfrastructureReadiness` for host and capability consumers; `OperationalChangeResult` for operator/approved Workflow; `ResourceCapabilityStatus` for deployment consumers; `UtcSynchronisationStatus` for host, Observability and authorised operator; `BackupRecoveryEvidence` for data owners and Audit; committed `InfrastructureChangeCommitted` and `InfrastructureIncidentChanged` facts for approved subscribers; and `SanitisedOperationalSummary` for Reporting. Each output records actual versus requested status, revision, observed time, origin, evidence quality and disclosure limits. Events may be replayed/duplicated and must not claim exactly-once distributed delivery.

## Cooperating capabilities: authoritative input and output

| Other owner | Infrastructure receives | Infrastructure supplies; boundary |
|---|---|---|
| Identity, Authentication, Authorisation | verified operator principal, assurance and decision | action/resource context and attributable results; never automatic cross-tenant access |
| Configuration | validated, permitted host settings and versions | applied/rejected revisions; cannot delegate NTP policy authority to tenant settings |
| Clock | validated temporal interpretation, format, interchange and (when required) date/time operations | trusted host instant and independently measured synchronisation quality via host/Observability; Clock never operates NTP |
| Privacy / Legal Compliance | constraints, holds, required retention and jurisdiction evidence | affected-operation evidence and safe refusal; never domain-policy reownership |
| Site Hosting | domain/proxy/certificate requirements | deployment/proxy/TLS operational state; domain ownership remains Site Hosting |
| Storage | object-store requirements via published interface | approved provider connection and status; business-file authorisation remains Storage's consumer |
| Scheduler, Message Queue, Workflow, Temporal gateway | infrastructure/runtime/connection prerequisites | worker/queue/database/service readiness; no business schedules, transports, workflow records or Temporal SDK API ownership |
| Domain-owned database/outbox capabilities | migration/backup consistency and owner acceptance requirements | supported Postgres/backup/recovery environment and evidence; never mutate private schema as a generic business operation |
| Observability | status observations, measured incidents and alert evidence | measured infrastructure, dependency and UTC quality facts with freshness |
| Logging | structured technical diagnostics and correlation contract | sanitised operation traces and fault details, with credentials removed |
| Audit | acknowledgement/integrity requirements for security evidence | high-risk change, break-glass, restore and policy/privilege transitions with actor, approval, revision and evidence links |
| Reporting | authorised reporting and scope contract | resource/availability/incident/restore aggregates, never raw credentials or unreviewed customer data |
| Notifications | approved operator/incident routing | safe incident alert facts; optional |

**Logging versus Audit versus Reporting:** Logging answers *what happened technically and what diagnostic correlation identifies it*. Audit answers *who was accountable for a privileged change, whether the evidence was accepted and what control/approval applied*. Reporting answers *what authorised operational patterns or compliance-relevant summaries can be derived*. Infrastructure supplies factual event and evidence references to all three, but none becomes an Infrastructure-private database or substitutes for another. Logging failures should not obscure operational results; failures to capture mandatory high-risk Audit evidence require a defined fail-safe, reconciliation and accountable escalation. Reporting can be unavailable without preventing core infrastructure control.

## Standards and open conventions to reuse

- **RFC 5905 (NTPv4)** and **RFC 8915 (NTS)** for network time transport/authentication; use Clock and IANA tzdb for civil timezone handling, not custom NTP parsing in Node.
- **NIST SP 800-53 Rev.5** (AC, AU, CM, CP, IA, IR, SC, SI, SR control families) and **NIST SP 800-34 Rev.1** for controls, contingency plans, backup/restore and recovery testing.
- **CIS Controls v8.1** for inventories, hardened configuration, access and network protections.
- **OWASP ASVS 5.0** as already required by governance (L2 minimum; L3 on critical high-risk operations).
- **OpenTelemetry semantic conventions and OTLP** for vendor-neutral metrics/traces/log correlations; Observability owns application telemetry.
- **Open Container Initiative (OCI)** artefact/image specifications for reproducible container images; **SPDX 2.3/3.0** and **CycloneDX** SBOM conventions for component provenance; **SLSA** supply-chain provenance as useful.
- **RFC 3339**, IANA tzdb, WCAG 2.2 AA and BCP 47 for interchange/UI; use Clock's actual published API for timestamp interpretation.
- **PostgreSQL native backup/WAL and point-in-time recovery concepts** for database recovery; explicitly test compatible extension versions, Temporal persistence and logical consistency.

These are architecture aids, **not claims of certification** or automatically applicable legal requirements. Versioned technical references and externally selected controls require deployment-specific acceptance.

## Source-verified, commercially permissive and portable open-source options

Prefer **standalone local/core functionality with no paid SaaS/control-plane prerequisite**, pin versions, review transitive licences and avoid proprietary provider modules.

| Candidate | Verified project licence | Proper role / limitations |
|---|---|---|
| [Docker Compose](https://github.com/docker/compose) | Apache-2.0 | Existing local multi-container development/acceptance orchestration; does not itself provide full production disaster recovery |
| [Caddy](https://github.com/caddyserver/caddy) | Apache-2.0 | Optional HTTP reverse proxy and automatic TLS; not a replacement for Site Hosting domain verification |
| [pgBackRest](https://github.com/pgbackrest/pgbackrest) | MIT | PostgreSQL backup, WAL and restore; verify actual recovery on application and Temporal-specific DBs |
| [restic](https://github.com/restic/restic) | BSD-2-Clause | Encrypted portable file/volume backups; not sufficient by itself for live PostgreSQL PITR |
| [Kopia](https://github.com/kopia/kopia) | Apache-2.0 | Alternative encrypted backup/snapshot solution; select **one** alongside specialised DB backup, not every tool |
| [OpenTelemetry JS](https://github.com/open-telemetry/opentelemetry-js) | Apache-2.0 | Stable instrumenting APIs/SDK where appropriate; send telemetry through Observability |
| [Prometheus and node_exporter](https://prometheus.io/) | Apache-2.0 | Self-hosted metrics collection and host observations; no managed SaaS dependency required |
| [Zod](https://github.com/colinhacks/zod) | MIT | Validate server-side operational requests and configuration for any future TypeScript control adapter |
| [node-postgres (`pg`)](https://github.com/brianc/node-postgres) | MIT | Only where a direct SQL client is actually required; do not replace host database ports or read other capabilities' tables |
| [Open Policy Agent](https://github.com/open-policy-agent/opa) | Apache-2.0 | **Optional** policy-as-code evaluator for complex host deployment checks; never displace Authorisation's ownership |
| [PostgreSQL](https://www.postgresql.org/about/licence/) | PostgreSQL Licence (permissive) | Existing database foundation, but each capability owns its own domain schema/records |

**Licensing exclusions/qualifications:** OpenTofu's MPL-2.0 is genuinely open source but weak copyleft rather than strictly permissive; only consider if MPL is accepted by explicit policy and external providers/modules pass separate review. Pulumi's Apache-2.0 CLI/core is open source, but a commercial control-plane ecosystem exists: do not introduce it without an independently hosted backend/exit assessment. `chrony` supports NTS and is an established OS synchroniser, but it is **GPLv2**, hence outside the strict permissive *library* shortlist; running an unmodified GPL system utility can still be commercially lawful, subject to legal/licence review. Avoid proprietary Terraform post-1.5 licensing, non-portable hosted-only modules and unwarranted changes to an already working Coolify deployment. None of these selections is yet an approved new dependency.

Source citations are maintained as primary project licence/repository URLs in the table, plus RFC and NIST references above. Verify current versions, vulnerability posture, maintenance and exact licence terms at adoption.

## GUI assessment using the representative application-test-template

**Verified template pattern:** `nuxt-layers-test/application-test-template` provides a homepage `/` without sidebar, a separate `/admin` with responsive collapsible sidebar, a host-owned top bar, local Theme Manager test mode, a `/theme-manager` demonstration route and configurable branding. The template explicitly says derivative hosts add capability-specific scenarios/navigation. Theme Manager's current root contract cautions that its full server composition is **not** yet ADR-0012 compliant, and unauthenticated test mode must **never** be deployed publicly. Do not claim route auto-registration or use Theme Manager's test mode as operational authorisation.

**Proposed host-owned navigation:** `Home → Administration → Operations → Infrastructure`; conceptual dashboard route `/admin/infrastructure`, with child pages or tabs `Overview`, `Environments & resources`, `Deployments & approvals`, `Backups & restore`, `Time synchronisation`, `Incidents`, and `Evidence & history`. Routes are **proposals**, not declared by the implementation or test template.

- Overview: readiness/health, critical dependencies, last verified observation, unknown versus degraded, affected environment.
- Environments: installations and infrastructure dependencies, provider version/status, connectivity and safe metadata, no credentials.
- Changes: plan differences, approval queue, revision and effects, reason/rollback, independent authorisation and cautious retry.
- Backup/recovery: recovery point/time, last verified restore, exceptions, protected restore confirmation and audit reference.
- Time synchronisation: selected/applied NTP/NTS source, trust/offset/freshness/holdover and history from Observability; render instants via Clock.
- Incidents: degraded service history, impact and recovery state; separate operator notices.
- Evidence/history: approved changes and audit pointers, sanitised logs and Reporting summaries without pretending those sources are owned by Infrastructure.

**Security and presentation:** menu and each server operation are separately authorised; hide unauthorised actions but never use hiding as enforcement; step-up and dual review for sensitive restore/secret/time changes. Render accessible keyboard navigation, responsive mobile overlay, WCAG 2.2 AA labels/errors, BCP 47/i18n and Theme Manager semantic tokens. Headless operation and existing secure host/Coolify consoles remain fully legitimate; avoid building duplicate configuration screens if the deployment platform already owns them. A test application must not be treated as production access control.

## Decision and evidence register

- **INF-01 APPROVED (18 November 2026):** host-owned Foundation operations, not mandatory Nuxt capability.
- **INF-02 APPROVED:** optional platform-operator-only presentation; no tenant infrastructure controls.
- **INF-03 APPROVED:** idealised input/output semantics; implementation names and endpoints still absent.
- **INF-04 APPROVED:** safe backup/restore, independent approval and legal/privacy constraints.
- **INF-05 APPROVED WITH CLARIFICATION:** Infrastructure selects, authenticates and maintains trusted UTC synchronisation; **uses Clock for interpreting/formatting and safe temporal operations via published public contract**; Clock does **not** become the OS/NTP service, and the host provides the trusted instant. Do not mandate an Infrastructure ↔ Clock cyclic package relationship.
- **Remaining technical work:** production infrastructure/provider choice and policy, latest implementation contract evidence, UTC sync thresholds, secrets, real restore tests, historical quality, CI acceptance and mandatory latest-master reconciliation.
