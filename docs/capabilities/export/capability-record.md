# Export — capability conceptual record

**Status:** **Conceptual specification ACCEPTED by project owner** (18 November 2026), including EXP-01–EXP-09, idealised public contract, responsibilities, standards, permissive library policy, reciprocal relationships and GUI allocation. This is **not** published implementation approval, conformant format certification, CI acceptance or merge authorisation. EXP-07 technical investigation and EXP-08 implementation alignment remain outstanding. No install/configured/operational/enabled/authorised status is verified. Governing classification remains **Library**; this record does not amend the accepted catalogue. Review: [draft PR #68](https://github.com/nuxt-layers/architecture-blueprint-review/pull/68). Baselines: governing `0725f314abc9ad13f1a65247f54a7ff80772f0b2`, blueprint `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.

## Capability Name
`export` (actual directory `docs/capabilities/export`).

## Purpose and classification

**Established governing scope:** `architecture-rules/docs/catalogue.md` identifies Export as a **Library**, converting validated `rich-text` safe trees into formats such as PDF and DOCX, with extensible formats. `rich-text` owns the safe tree format and validation; Export renders it. Accepted ADR-0011, ADR-0012 and ADR-0017/0018, the Capability Standard and privacy/security/presentation baselines govern its usage.

**Principal architectural challenge:** Earlier blueprint reciprocal notes attributed asynchronous bulk-data requests, recipient/destination management, generated artefacts, delivery/retention and disclosure to Export. These durable orchestration responsibilities exceed the governing **renderer library** scope. A proposed explicit **two-boundary design** prevents silent reclassification:
1. **Export renderer (this governed library):** deterministic, bounded, provider-neutral conversion of a validated authorised input into specified file bytes or an output stream and technical metadata; no domain records, access grants, recipients, persistent jobs, storage lifecycle or delivery.
2. **Owning export workflow (not yet independently allocated):** the calling domain, Reporting for report-owned exports, or a separately justified later platform service coordinates authorised source reads, bulk-disclosure review, snapshot, file storage, distribution, revocation, retention and recovery. Never presume the renderer alone owns those duties.

**EXP-01 owner-approved direction (18 November 2026):** retain the strict renderer Library boundary. Durable export orchestration belongs to its requesting domain or Reporting, reusing Workflow, Scheduler and other public services where appropriate. A separate shared orchestration capability requires later independent justification and approval; it is not created here. No second package is approved by this proposal. Existing Billing/Authorisation notes are preserved verbatim below as history, not reinterpreted as accepted contracts.

## Evidence, dependencies and availability

The `nuxt-layers/export` repository exists, `master` `c75367e66c2d228a4d98193e7307335e6682a678` on review; its inspected tree contains only `.gitignore`, `LICENSE`, `README.md` (`# export`). **No root `CONTRACT.md`, public API, implementation or acceptance evidence is available**. Independently installing and using Export is not established. Related implementations have not been read beyond their public root contracts; no implementation coupling is inferred.

Core input is a versioned safe `rich-text` tree from a caller that has already made source access/disclosure decisions. A format backend may be an optional injected adapter; absence of a requested format returns explicit `unsupported_format`. A pure headless library must operate without Nuxt, Identity, Publisher, Storage, Reporting, external conversion SaaS or a GUI. A host provides any required font/asset resolution, computation and safe output sink via declared provider-neutral ports. Provider uncertainty and capability limitations must be exposed. No implicit network fetches or credentials from document content.

## Owned state, exclusions and native lifecycle

The renderer owns **no authoritative domain records** and need not own durable persistence or an outbox. It owns its public conversion profiles/format registrations, validation and output semantics, with transient work bounded by resource budgets. A conversion call is accepted for execution → validates input and format/options → resolves only permitted embedded assets → converts → verifies output constraints → returns completed bytes/stream plus metadata **or** a typed failure. A cancelled/aborted or partially written stream is never a completed file. Caller owns disposal of partial bytes.

Not owned: original content, document revisions, financial statements, invoice or credential meaning, authorisation, civil evidence, dataset selection, reporting calculations, bulk-extract jobs, recipient rights, file object identity, signed URLs, distribution, legal holds, audit custody or storage quotas. The renderer does not claim a successful PDF means a valid legal invoice, awarded qualification, current credential or lawful disclosure.

### Minimum native services (proposed)
- Convert safe tree to supported format, with format profile, locale, page/layout and accessibility options validated explicitly.
- Return format capabilities and limitations, implementation/renderer version, reproducibility qualifiers, output content type, length when known and content digest when computable.
- Preserve semantic headings, links, tables, lists, image alternatives and reading order as the selected format permits; expose inaccessible/unsupported-content diagnostics rather than silently promising accessible output.
- Enforce deterministic sanitisation, safe asset retrieval via caller-supplied bounded resolver, resource/time/size limits and cancellation; prohibit embedded script execution, arbitrary local file access, unsafe URLs, server-side request forgery and untrusted active content.
- Return per-item faults and partial conversion status where meaningful; do not auto-upload, email, publish or schedule anything.

## Idealised public contract — input

| Public input surface | Source/authority | Required validation; absence and failure |
|---|---|---|
| `ConvertSafeTree` | Authorised caller provides validated safe tree, schema/profile version, chosen format and output options | Required. Reject malformed/unsupported tree, unrecognised format, invalid layout, excessive size, unsupported profile or requested capability without silent fallback. Tree validity **does not authorise disclosure**. |
| `ResolvePermittedAssets` | Host/source owner supplies permitted image/font/resource bytes or bounded references | Conditional on document assets. Validate MIME, quotas, size, trusted origin, expiry, safe references, attribution and permissions; absent resource gives explicit missing/blocked/error result per approved failure policy. |
| `FormatProvider` | Host provides optional renderer backend or locally bundled implementation | Conditional per format. Distinguish unsupported, unavailable, timed out, uncertain and invalid output. Remote service needs separately approved lawful data transfer and secrecy controls. |
| `CancelConversion` / limits | Caller or execution host supplies cancellation and resource bounds | Required limit enforcement. Cancellation is not successful completion; surface partial-output disposal obligations. |
| `AuthorisedSourceSnapshot` | Source-owning domain or Reporting, **outside this library**, selects and approves a specific version and content disclosure | Conditional surrounding workflow, **not** a library permission interface. Unknown/stale/unauthorised content must fail closed before rendering; caller remains accountable. |

**Contract distinction:** a caller's statement that a tree is allowed is not an independent Authorisation decision by Export. A renderer can reject unsafe bytes even if the source owner permits content; it cannot broaden permission. Shared context is only what the operation needs: format/profile and revision, locale, rendering options, source attribution if requested, cancellation/limits and correlation for safe diagnostics. No universal request object or privileged arbitrary user-supplied tenant claim.

## Idealised public contract — output

| Public output surface | Consumer and meaning | Authority and limits |
|---|---|---|
| `RenderedFile` / bounded stream | Host, Publisher, Reporting or other authorised source owner gets completed bytes/stream, MIME, extension, optional digest/length and renderer profile/version | Technical rendering outcome **only**. The caller owns saved artefact and any disclosure. A stream started or accepted is not a completed valid file. |
| `FormatCatalogue` | Consumers discover supported formats, options, accessibility characteristics and unsupported features | Renderer capability declaration; no promise that a deployment has enabled optional adapters without verification. |
| `ConversionOutcome` | Caller receives accepted/executing/completed/failed/cancelled where relevant, structured errors and warnings | Synchronous/ephemeral operation result, not a durable job-status API. Unknown remote outcome must not be represented as completed. |
| `RenderDiagnostics` | Caller/Logging receive scrubbed warnings, coverage gaps, safe correlation and timing | Never include original personal/business content, secrets or generated bytes by default. |
| `Preview` (optional) | Host offers a non-authoritative rendered preview | Previews do not publish or disclose without caller's separate approval; preview access is governed by its source. |

**Queries:** format/option/compatibility queries and stateless conversion; **commands:** convert/cancel. **Domain events:** none required for a stateless renderer. A surrounding durable export/report job owner emits committed job lifecycle events through its own outbox where warranted, handles replay/idempotency and uses Message Queue for transport. Renderer does not assert exactly-once external delivery.

## Cross-capability relationships and reciprocal contract allocation

| Capability | Export receives / depends on | Export supplies / caller owns | Relationship and unavailability |
|---|---|---|---|
| `rich-text` | Versioned safe tree and semantics | Format conversion diagnostics and bytes | Required content-format contract, no private imports; reject incompatible version. |
| `publisher` / `content_editor` | Publisher-approved document revision/safe content; editor only initiates user workflow | Rendered representation; Publisher retains source revisions, approval, withdrawal and disclosure | Conditional; no duplicate Document authority. Native publication works without Export. |
| `reporting` | Approved report representation, source lineage and version | Rendered report file; Reporting owns report definition, snapshot, export job/artefact/distribution | Conditional; no parallel report store. |
| Other domains incl. `billing`, `invoice`, `credentials`, `accounting` | Approved source-specific view/snapshot through owner public contracts | Technical output bytes; domain remains source and authorises disclosure | Conditional; no renderer-derived legal or award authority. |
| `authorisation`, `authentication`, `identity` | **Workflow owner** obtains trusted caller, assurance and permissions; source owner validates subject/resource | No IAM decisions from renderer | Mandatory for privileged calling workflow, not library service dependency. Bulk, recipient and retained-file reads need independent checks. |
| `privacy`, `legal_compliance` | Workflow owner obtains purpose, minimisation, retention, rights, holds, jurisdiction and transfer constraints | Rendering must minimise processing, avoid retention and respect redaction supplied by owner | Applicable legal constraints cannot be weakened by configuration; unknown mandatory controls hold disclosure. |
| `storage`, `media` | Host provides bounded approved assets; workflow owner stores generated bytes if requested | Byte stream/digest only; Storage owns bytes, not source/business file record | Optional from renderer; a missing storage service must not defeat local in-memory rendering. |
| `audit`, `logging`, `observability` | Workflow owner sends risk-based access/disclosure evidence to Audit and sanitised diagnostics to Logging/Observability | Renderer returns narrow technical outcome/correlation | Audit owns evidential custody, Logging technical logs; library never emits unredacted document content. |
| `configuration`, `clock`, `localisation` | Validated host policies/format profiles, locale, timezone or timestamp presentations as required | Rendered locale-aware formatting; no preference or time authority | Optional/contextual; unsupported locale/font/profile explicit, no silent compliance claims. |
| `scheduler`, `workflow`, `message_queue`, `notifications`, `integrations` | Surrounding owner coordinates batch/scheduled export, provider transfer, retry, notification | Operation result, not dispatch receipt | Not required by renderer. Delivery/sync/retries belong to orchestrator/integrations; delivery acknowledgement is separate. |

**Reciprocal documentation:** proposed clarifications should be appended to Authorisation, Reporting, Publisher, Billing and Storage records; all earlier accepted decisions stay intact. Do not convert conceptual edges into direct code dependencies.

## Privacy, security and standards

Baseline: accepted ADR-0001/0002/0006/0008/0009/0011/0012/0014/0015/0016/0017/0018, OWASP ASVS 5 Level 2 (L3 for high-risk disclosure as applicable), WCAG 2.2 AA for optional GUI, GDPR/UK GDPR rights as applicable, BCP 47/CLDR/ECMA-402. Format-specific PDF/UA and PDF/A profiles, accessible document semantics, PDF active-content restrictions and Office Open XML interoperability require capability declaration and actual validation; **do not claim formal PDF/UA, archival or legal conformity without test evidence**. External font licensing, data residency, international transfer and child/sensitive data require context-specific legal assessment.

**Threat model:** unsafe markup and asset URLs; injection in PDF/office generators; SSRF/path traversal; malicious fonts/images; zip bombs and expansion; memory/CPU exhaustion; metadata leakage; invisible redactions; stale/overscoped source material; bearer download URLs; cross-tenant recipient mistakes; remote conversion provider retention. Protect streams, quotas, sandboxed conversions, outbound networking and temporary files; fail securely on unknown result. Source-owner redaction must be applied *before* rendering, and removal must include metadata, embedded objects and accessible representations. Renderer cannot unilaterally certify a data subject request, hold release or destination safety.

## Presentation and GUI

**Classification:** headless library, **no standalone Export dashboard or sidebar entry is justified**. The host's sidebar routes to the owning capability dashboard (Publisher/Content Editor, Reporting, Billing etc.) using the representative `nuxt-layers-test/application-test-template` and Theme Manager pattern. Contextual **Export / Download** action offers allowed format, scope, locale, column/section visibility, redaction, size and output preview. For high-volume/remote jobs, the *workflow owner*, not renderer, supplies review/confirmation, queued/running/partial/completed/failed states, artefact list, expiry and revoke/delete actions, recipient/delivery status and safe download. Separate administrative screens for permitted formats/provider availability, capacity/quotas, failures and retention belong to host/operator or workflow ownership only if needed.

Access-controlled navigation must never imply permissions. Responsive, keyboard-operable, accessible status/labels, themed controls, clear error recovery and internationalised copy are required. Screen designs consume published public interfaces only. A library must be useable with **no GUI**, no browser and no Nuxt application.

## Conceptual acceptance scenarios (accepted criteria; not executed)

| Input/scenario | Expected output and failure | Authoritative owner |
|---|---|---|
| Valid rich-text tree, supported PDF/DOCX profile | Completed bounded bytes and metadata; missing feature warned | Export rendering only |
| Publisher-approved revision withdrawn before download | Workflow denies/rechecks saved-file disclosure; renderer cannot bypass | Publisher + owning workflow + Authorisation |
| Authorised Billing charge snapshot | Permitted scoped converted representation; source revision/period remains attributable | Billing data; Export bytes |
| Reporting multi-source snapshot with incomplete periods | Explicit incompleteness carried through; no false financial certification | Reporting and source domains |
| Malformed tree, malicious asset URL or oversize image | Reject/abort safely; no arbitrary network/file read | Export |
| Tenant A requests tenant B's data or bulk sensitive fields | Deny before rendering/retained-file access; evidence where mandated | Source owner/Authorisation/workflow |
| Replay after streaming interruption | Caller disposes partial output and retries under idempotent workflow identity; no duplicate disclosure | Workflow owner |
| Remote renderer timeout/unknown result | Unknown/failed without completed-file claim; provider data-transfer safeguards applied | Renderer outcome; workflow recovery |
| Revoked user tries previously generated download | Saved delivery independently checked or revoked; stale bearer link not sufficient authority | Workflow owner/Storage-access composition |
| Rendering disabled/unavailable | Source domain continues core transactions; explicit unsupported/unavailable result | Export; source domain |
| Unavailable historical revision or unsupported archival profile | Explicit unknown/unsupported result, no fabricated reproducibility/accreditation | Source owner / Export profile |

## Decision register and challenge

- **EXP-01 — Owner-approved conceptual direction (18 November 2026):** retain governed *renderer Library*; assign durable bulk-export workflow to each owning domain/Reporting and reuse existing orchestration services. Reconsider a separate shared service only if independently justified and separately approved.
- **EXP-02 — Owner-approved conceptual principle (18 November 2026):** input restricted to versioned safe tree plus caller-supplied permitted assets; no internal source queries, permissions, uploads or delivery.
- **EXP-03 — Owner-approved conceptual principle (18 November 2026):** capability/limitation discovery and typed failure are mandatory, no PDF/UA, PDF/A or DOCX standards claims without conformance evidence.
- **EXP-04 — Owner-approved conceptual principle (18 November 2026):** no standalone GUI; contextual action and owner-controlled jobs/recovery in consuming dashboards.
- **EXP-05 — Owner-approved conceptual principle (18 November 2026):** rendering succeeds without Storage, Notifications, MQ, Scheduler, external SaaS or Nuxt. Any backend/format adapter is explicitly declared.
- **EXP-06 — Owner-approved conceptual principle (18 November 2026):** sensitive bulk/saved export requires source-specific and recipient-specific authorisation, privacy/legal constraints, revocation and risk-selected Audit, owned by requesting workflow.
- **EXP-07 — Owner-approved investigation scope; technical work outstanding (18 November 2026):** format adapter interface, canonical safe-tree/version compatibility, PDF/A-UA and DOCX validation methodology, asset restrictions, deterministic output, font licensing, remote backend transfer and quotas; resolve by standards and public contract evidence rather than inventing APIs.
- **EXP-08 — Owner-approved future alignment objective; implementation unverified (18 November 2026):** actual `nuxt-layers/export` lacks `CONTRACT.md`, package and accepted independent consumer; no accepted runtime or CI. Later implementation must publish exact imports/signatures, error codes and minimal consumer evidence under ADR-0012.
- **EXP-09 — Owner-approved reconciliation (18 November 2026):** previous Export reciprocal wording assigning generated files/jobs/recipients to the Library is superseded conceptually by EXP-01's strict renderer ownership. Preserve historical notes for traceability, annotate current reciprocal understanding and require any remaining conflicting conceptual notes to be reconciled without changing accepted governance.

**Challenge result:** no cyclic service dependencies justified; Export must not become a generic document owner, an Authorisation enforcement shortcut, a duplicate Reporting engine or a Storage service. Durable export jobs are owned by the requesting source domain or Reporting in the approved model; a repeated requirement may justify future review, not an automatic new library API. No new ADR or implementation repo changes are authorised by this PR.

## Owner decision recorded — 18 November 2026

The owner initially approved EXP-02–EXP-08 and left EXP-01/09 open; **later on 18 November 2026**, the owner expressly approved **all recommendations** of the standards/library/architecture assessment, including retention of the strict renderer Library boundary, domain/Reporting-owned workflows and optional formats only with defined contracts. This resolves EXP-01/09 at the conceptual level without approving a new orchestrator, runtime dependency or merge. This approval confirms the conceptual constraints in EXP-02–EXP-06, approves the *scope* of EXP-07's technical investigation and the *future objective* of EXP-08's implementation alignment; it does not claim either is finished. The strict renderer-only allocation in EXP-01 and corresponding ownership reconciliation in EXP-09 are now **approved as conceptual direction**; historical reciprocal notes remain visible but superseded for active ownership. Do not silently promote the provisional owner-of-job language in surrounding descriptions to binding architecture. Preserve the one draft PR; **no merge approval has been supplied**.

## Approved standards and open-source design — 18 November 2026

**Owner approval:** Accept the standards-based, commercially permissive, self-hostable and provider-replaceable design recommendations. This is **selection policy and research guidance, not a claim that any dependency is installed, conformant or approved at a specific version**.

- **Formats:** ISO 32000-2 (PDF), ISO 19005-4/PDF/A-4 (archival where validated), ISO 14289-2/PDF/UA-2 (accessibility where validated), ECMA-376/ISO/IEC 29500 (DOCX), ISO/IEC 26300 (optional ODT), RFC 4180 and W3C CSVW (conditional tabular export), RFC 8259 (JSON for structured exchange), RFC 6266 (HTTP downloads owned by host).
- **Security and presentation:** OWASP ASVS 5.0 incl. V1.2.10 CSV/formula injection where applicable; WCAG 2.2 AA for GUI, BCP 47/Unicode CLDR/ECMA-402; source restriction, bounded asset resolver, SSRF/command/ZIP/metadata hazards, redaction and external provider transfer checks. PDF conformance and accessible output require actual validation; HTML accessibility alone does not confer PDF/UA conformance.
- **Preferred core candidates:** PDFKit (MIT) for direct PDF, `docx` (MIT) for DOCX; compare pdfmake (MIT) and WeasyPrint (BSD-3-Clause) for layout/accessibility; Playwright (Apache-2.0) is an optional browser-backed renderer, not a required runtime. `csv-stringify` (MIT), ExcelJS (MIT) and Archiver (MIT) are conditional on separately agreed structured-data or packaging contracts. Assess dependencies, vulnerabilities, native runtime, fonts and latest released versions before selection.
- **Licence policy:** Prioritise complete source under OSI-approved commercially permissive MIT/Apache-2.0/BSD licenses, not open-core gated features or required SaaS. LibreOffice/Pandoc are genuine open-source but subject to non-permissive/copolyft licence review and heavy operational boundaries; no mandatory dependency.
- **Core stays the validated rich-text-to-document library.** CSV/XLSX are **conditional, not automatically in scope**: require an independently validated tabular data model/interface and approval of any governing-boundary change. Avoid duplicating Reporting, owning source queries or promising an unrestricted dataset export engine.

## Representative host, presentation and screens — verified 18 November 2026

**Observed public reference:** `nuxt-layers-test/application-test-template` `master`, README and `app/app.vue` provide homepage `/` (no admin sidebar), `/admin` test dashboard, responsive collapsible **Capabilities** sidebar, host-owned top bar and Appearance control, and Theme Manager link `/theme-manager`. Its `nuxt.config.ts` extends Theme Manager in local test mode. `nuxt-layers/theme-manager/CONTRACT.md` documents actual screens `/theme-manager` and `/theme-manager/:id`, a semantic token vocabulary and known public-composition limitations. This is a reference design, **not** proof Export has screens or that the template is safe to deploy publicly.

**Approved GUI allocation:** As a stateless library, Export has **no dedicated sidebar item, admin dashboard, database-managed job queue or universal file-history screen**. The host exposes contextual **Export/Download** on Publisher/Content Editor, Reporting and other authorised capability screens. For demonstration, a derived Export-specific test application MAY add an **Export (test)** sidebar entry and `/export` *test harness/dashboard* showing example content, format options, page/locale/accessibility settings, preview, convert/download, technical result and errors; this is a host-owned acceptance surface, **not** production Export-owned UI. Never expose this test screen as an unrestricted business-data export. Production operations (bulk queue, history, recipients, stored artefacts, expiry, delivery and revocation) belong on the owning capability/Reporting dashboard. Settings for renderer availability or provider health, if needed, are host/operator controls and are not new business authority.

**Presentation rules:** Compose through public contracts and host navigation, no private capability routes or imports; Theme Manager semantic tokens and light/dark states, mobile navigation and keyboard focus, WCAG 2.2 AA, i18n/localisation; server-side authorisation and redacted previews; clear processing/failed/cancelled/unknown/completed states, download safeguards and alternative text. A local derived test host can exercise the renderer without Storage/Reporting/IAM/remote providers using deliberately non-sensitive fixtures; security assertions require proper independent acceptance later.

## Approved public interface clarity — 18 November 2026

**Implemented status:** `nuxt-layers/export` currently has no root `CONTRACT.md`, package API or independent tests on inspected baseline, therefore there are **no verified published input/output interfaces**. The following describes the approved *idealised* future contract:
1. **Inputs:** discover format capabilities; submit one versioned safe `rich-text` tree with approved locale, formatting and accessibility profile, output format, optional bounded asset bytes/resolver, cancellation and limits. For a separately approved tabular adapter, validated schema/rows would be an additional independently scoped input, not a hidden source query.
2. **Outputs:** available format/profile declarations; completed file bytes/stream with MIME, version, size/digest when feasible; warnings/coverage, typed error/unsupported/timeout/cancelled/unknown result; transient progress only where supported. No durable job ID, domain disclosure or guaranteed destination receipt.
3. **Who supplies what:** Publisher/source domains supply already approved view models and revision attribution, Reporting supplies approved report representations, Rich Text defines safe content; host supplies safe asset/font and backend ports when used. Renderer returns only output and safe technical results. Authorisation, Privacy, Legal Compliance are applied by the requesting workflow; Storage owns saved bytes; source/Reporting owner manages file references, recipients, retention and disclosure; Logging consumes scrubbed conversion telemetry, Audit consumes attributable high-risk disclosure evidence submitted by workflow, Reporting consumes files/status while retaining all report-data authority.
4. **Failure semantics:** a conversion completion does not imply file delivery; a valid tree does not confer permission; a stale/unknown permission, source revision, format capability or remote backend result must not be silently treated as success; no guarantee of exactly-once external delivery.

## Conceptual acceptance and completeness disposition — 18 November 2026

**Decision: ACCEPTED for the blueprint conceptual review.** The owner reviewed and accepted all standards/library/format-neutrality recommendations and the complete conceptual scope of EXP-01–EXP-09; the full input/output meaning, command/query behaviour, non-domain-event reasoning, failure and recovery semantics, authoritative allocation, cross-capability reciprocal notes and host-owned presentation/test-dashboard pattern are recorded above. In particular, EXP-01 and EXP-09 select the headless rendering Library boundary and supersede older job/recipient/storage ownership assertions in historical notes; their retention below is evidence of original proposals, not current authority. This acceptance is architectural sign-off only; it is not an assertion of operational, implemented, security-tested, legally compliant or standards-conformant software. CSV/XLSX, ODT and ZIP remain conditional format additions with independently agreed contracts and evidence, not automatic public interfaces. Technical work under EXP-07 and independent acceptance under EXP-08 are deliberately deferred to implementation. This PR must still pass latest-master technical/architectural checks and receive **separate explicit approval for the protected squash merge**.

## Deferred and sign-off

Public `CONTRACT.md`, implementation/format and accessibility conformance, licence/security testing, acceptance evidence and provider checks are **not done**. The conceptual direction **EXP-01–EXP-09 is owner-approved as bounded above**; EXP-07 technical investigation and EXP-08 future implementation alignment remain incomplete. **Conceptual acceptance has been granted; final approval of this PR's squash merge has not been given.** Before merge, perform technical Git reconciliation, latest accepted governing/blueprint status, pending parallel PR compatibility and full cross-capability review; merge requires separate explicit approval.

---

## Historical reciprocal notes preserved from original record

## Cross-capability note — Authorisation of bulk export (15 November 2026)

**Status:** Proposed reciprocal interface, not an implemented Export/Authorisation integration. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) supplies current action/resource permissions and bounded visible scopes; each owning domain supplies the source records and applicable legal/privacy restrictions. Export must separately enforce bulk-disclosure permission, tenant boundaries, snapshot freshness, recipient/destination controls and the difference between export job acceptance and completed disclosure. Download links and derived copies must not bypass revocation or become cross-tenant bearer access by default. Export's review remains incomplete.

## Cross-capability note — Billing data export, scope and authority (15 November 2026)

**Proposed reciprocal relationship, not an implemented Export adapter.** [Billing](../billing/capability-record.md#cross-capability-completeness-review--further-interfaces-and-relationships-15-november-2026) supplies scoped, versioned and authorised commercial charge queries/snapshots with lineage, currency/period and completeness indicators. Export owns the generated file/package, recipient/destination, job and delivery/retention lifecycle; it cannot independently broaden source access or become Billing's authoritative charge archive. Rights must be rechecked for the requested dataset, sensitive columns, recipient and saved artefact, including cross-tenant/party and bulk export. Privileged exports produce risk-selected Audit evidence. External provider authority migration requires reconciled identifiers, revisions and corrections, not a raw file assumed complete. An Export outage must not prevent native Billing transactions.

## Reciprocal decision — redundant Document capability retired (17 November 2026)

**Owner-approved resolution, 17 November 2026:** no independent Document capability or source authority is needed. Export continues to produce authorised artefacts from Publisher's or the relevant domain owner's public data, without re-owning their records, permissions, holds or disclosure decisions. Historical conditional review: [Document](../../../reviews/document-directory-removal-2026-11-17.md).
