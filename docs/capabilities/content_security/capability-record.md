# Capability Record — Content Security

**Capability:** `content-security`; actual blueprint directory `content_security`.  
**Classification:** Platform (established catalogue responsibility).  
**Review status:** Owner-approved conceptual decisions CS-01–CS-16; documented idealised architecture remains non-normative and not an implemented operational contract.  
**Evidence (17 November 2026):** Governing `architecture-rules/master@2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint opening `master@41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`; draft [PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55). The repository `nuxt-layers/content-security` exists at `master@f27469c66aee3cc13e81a0e0fd0554125ab884cb` (initial commit), but root `CONTRACT.md` is not found; runtime/API/CI/acceptance claims are **unverified**.  
**Governing rules:** accepted ADR-0012, normative Capability Standard, Security and Privacy; accepted ADR-0001/0002/0009/0011/0016 where applicable. ADR-0018 was marked **proposed** within its file when inspected: do not treat as accepted solely because present on master.

## Purpose and justification

Reusable, trustworthy assessment of submitted or changed content and associated links, attachments and threat indicators, supplementing—not substituting for—each source capability's own validation. Scanning is independently reusable across Publisher, Comments Engine, Media, Marketplace listings, uploaded files and selected federation intake. It separates detection engineering, datasets, provider-specific signals and assessment provenance from adjudication and content ownership.

**Owns:** assessment requests/jobs and scoped status; classification taxonomy interpretation for technical detection (with qualifications); scanner profiles and rule execution within enforceable floors; assessment results, confidence/limitations and relevant evidence references; risk-signal correlations; provider capability/status evidence; assessment invalidation/expiry; rescanning coordination and minimal capability-owned outbox/receipt history as justified. Assessment history is not a raw-content archive by default. If persistence is needed, it owns its own schema, migrations, outbox, retention and storage register.

**Does not own:** original content or bytes; upload records/objects, publication or comments lifecycle; authorisation; final legal findings; cross-domain reports, moderation investigations, adjudication or appeals; domain enforcement; policy applicability law; audit's independent evidential record; user profiles; search indexes; federation peer restrictions; site configuration authority; provider credentials; all malware defence for the platform. A positive or negative result is **evidence**, not content owner's permission or a conclusive determination of illegality.

## Native service and lifecycle

1. Validate trusted resource owner, tenant/scope, content class, revision or immutable digest, declared purpose and disclosure constraints. Allow bounded direct ephemeral payload or owner-controlled short-lived read reference where justified; never assume a signed URL permits external onward transfer.
2. Resolve approved assessment profile, required checks by modality (text, URL, image/file metadata or other declared capabilities), policy version, jurisdiction and intended audience. Do not claim support for a modality absent a verified scanner.
3. Perform local technical validation and safe canonicalisation (size/type, encoding, URL resolution limits, safe decompression, anti-SSRF/network isolation, malicious archive protections), then run configured first-party and/or qualified external checks. Sanitisation and safe rich-text parsing remain the appropriate owner's responsibility.
4. Produce separate per-check outcomes `clear` (only for specified checks), `indicator`, `inconclusive`, `not_applicable`, `not_run` and `error`; overall scope completeness is explicit. Never equate no hit, low confidence or provider outage with globally safe content.
5. Bind verdict to exact tenant, owner/resource, revision/digest, modality, check set and policy/provider/dataset versions. When source edits, resource permissions, URLs, policies or threat intelligence change materially, invalidate or schedule reassessment; consumers must refuse stale results when current evidence is mandatory.
6. Support bounded cancellation, retry/backoff, timeouts, idempotency, duplicate deliveries, partial results, provider cost limits, secure quarantine references and reconciliation of accepted versus completed work. Required assessments missing/unknown trigger **source owner's** risk-defined protective policy, typically pending/hold for potentially public exposure; Content Security does not directly publish or suppress.
7. Supply minimised evidence/reference material to authorised moderation and Audit consumers; isolate restricted hash matches and sensitive content. Consumer access is purpose-bound; protect vulnerable subjects, whistleblowers and reporter identity.
8. Retain only necessary scan-job state and results for a defined purpose and period; respond to provenance-safe export, erasure/hold and provider deletion requests within policy. Historical results must remain historically qualified, not rewritten after classifier updates.

**Operation without external providers:** Native profile/checks must be explicit, not falsely represented as universal protection. A provider-free installation can accept and perform only genuinely supported local checks, or return `unsupported`/`unknown`. A profile requiring absent checks is not eligible for clearance. Loss of a required persistence/credential/assurance port fails safely. No one universal third-party scanning service is mandatory.

## Comprehensive screening classification — 17 November 2026

**Status:** Proposed detailed screening catalogue; classification and check applicability are *not* a declaration of implemented scanners or blanket owner approval of every detector. Owner-approved CS-09/10/11/12 Option C remain binding conceptual choices. See [comprehensive screening and control catalogue](../../../reviews/content-security-screening-catalogue.md).

- **S1 — Untrusted text, structured input and application security:** all text fields, forms, imported text, rich text, Markdown, HTML, URLs, spreadsheets and prompt/tool inputs receive applicable source-owner schema, injection prevention, safe processing and output-encoding controls. **These controls must not require a Content Security service request for every keystroke/field.** Content Security offers reusable URL, sensitive-information, spam and attack-indicator assessments where needed.
- **S2 — File/media safety:** images, documents, attachments, archives and any supported audio/video need applicable type/content validation, limits, malware/active-content detection, isolated decoding, metadata privacy, safe variants and controlled delivery. Office documents, templates, PDFs, spreadsheets and exports must address macros, scripts, dangerous embeddings, external fetches and formula injection.
- **S3 — Harmful-content classification:** qualified checks for CSEA/grooming, NCII, harassment, threats, illegal sexual material, violence, hate/incitement, suicide/self-harm encouragement, fraud, phishing, prohibited trade, doxxing, manipulative/impersonation signals and other scoped categories. **Profanity/offence are separate configurable community-policy categories, not automatic legal findings.** Legal Compliance qualifies duties, Moderation adjudicates cross-domain cases, owners enforce.
- **S4 — Third-party and federation trust:** validate external feeds/imports, signed claims when available, source/digest/revision provenance, remote check limitations, replay/poisoning and independently authorised Hub exposure. Remote `clear` must not automatically be adopted.
- **S5 — Ongoing safety:** rescan or invalidate where policy requires after content/variant/URL changes, new intelligence, provider failures, audience changes, source restoration and expiry. Search, CDN and federation withdrawal receipts are distinct from scanning status.

**Requirement tiers:** **B** baseline mandatory control for every relevant untrusted input; **F** format/feature mandatory protection; **R** risk/policy-mandatory check, requiring service/audience/jurisdiction qualification; **O** optional defence in depth; **N/A** inapplicable/unsupported (never cleared). A requirement applies to its relevant operation and trust boundary, **not** every technical check to all fields.

**Contract handoff:** published check IDs and coverage must express executor ownership, eligible modalities, required/optional applicability, revision/digest and policy versions, assessment evidence/provenance, supported status, pending/unknown/stale semantics, sensitive retention, provider and threat-feed constraints, disclosure and proper source-owner action. A scan that passes malware detection does not establish that an image is lawful, and a text toxicity classifier does not replace secure rendering or prove guilt.

**Pending detailed policy/implementation alignment:** first-release enabled formats, required check sets per public/closed/private context, provider qualification and legal scope, retention schedules, false-positive thresholds, cost/latency and fallback. No local tests/builds or implementation changes have been performed.

## Idealised inbound public contract

These are conceptual contract surfaces, not proposed endpoint signatures.

| Source | Facts, command or evidence | Authority; validation and missing/invalid behaviour | Requirement |
|---|---|---|---|
| Source owner (Publisher, Media, Comments Engine, Marketplace, other registered domain) | `requestAssessment` with resource class, tenant, opaque ID, exact revision/digest, media/type, limited permitted material or reference, intended visibility, reason, correlation/idempotency | Source remains owner of bytes and revision; reject cross-tenant, stale, forged or inaccessible references; cannot disclose content merely due to a scan request | Required per registered source |
| Host IAM / Authorisation | Server-authenticated caller, assurance and purpose-scoped permission for scanning, viewing results, overrides and sensitive evidence | IAM owns identity/session/access; fail closed on absent or ambiguous decision; service principals are least-privileged and attributable | Required |
| Configuration and owning source policy | Versioned scope, enabled checks, threshold/profile, severity routing, provider budget, rescan trigger and failure/unknown treatment within hard floors | Configuration owns approved scoped settings; Content Security validates its scanner settings; source owner decides publication/hold. Missing mandatory settings block clearance | Required applicable settings |
| Legal Compliance and Privacy | Qualified jurisdiction/service duties, prohibited disclosure, retention, lawful-purpose and hold constraints | These owners supply scoped conditions, not automatic criminal findings. Uncertain mandatory duty must be surfaced, not guessed | Conditional mandatory by service |
| Provider/Integrations | Versioned classifier/hash/URL reputation evidence; timestamps, dataset/licence scope, processing location, errors, latency/cost | Evidence may be forged, stale or incomplete; verify trust, schema, privacy permission and source provenance before use; provider cannot authorise exposure | Optional individually; conditionally required by selected policy |
| Scheduler/Message Queue | Due re-assessments, timeout/retry triggers and outbox delivery acknowledgements | Delivery timing never validates a verdict; replay is idempotent | Conditional coordination |
| Moderation / authoritative reviewer | Request authorised result disclosure, contextual evidence, reassessment, or challenge/correction reference | Moderation owns case/appeal; scan cannot be edited to fit verdict; reassess creates new version | Optional |
| Security operations | Emergency check-rule revision, recognised threat intelligence feed and detector disable/replace proposal | High-risk changes approved with separation of duties and rollback; do not let tenant policy defeat mandatory platform controls | Conditional |

**Input validation:** explicit MIME/format and size bounds, content canonicalisation limitations, Unicode/locale, URL/redirect/SSRF defence, archive expansion, input poisoning, model prompt injection, forbidden material handling, expected revision, tenancy, provenance and cost. A check incapable of examining a type reports `unsupported`, not `clear`.

## Idealised outbound public contract

| Consumer | Surface and meaning | Authoritative guarantee / limitation |
|---|---|---|
| Source owner | `assessmentAccepted` with job ID and pending scope; `getAssessment` with check states, category/indicator, confidence/limitations, resource revision, policy/check-set versions, expiry, request and completion times | Owns **technical scan evidence only**; clearance only applies to completed named checks on bound bytes/revision; no publication permission |
| Moderation | Scoped detection referral, risk indicators, minimised evidence references and review-needed reason | Moderation may open case and decide; detector does not adjudicate or expose reporter details |
| Authorised admin/security GUI | Sanitised scan statuses, capability/support matrix, provider health/cost, policy applicability and bounded appeals/recheck controls | Never imply provider unavailable = zero threats; sensitive evidence gated |
| Audit | Attributable assessment, scanner/policy changes, override/reassessment and disclosure receipts with IDs, actor, versions and outcomes | Audit maintains independent trusted record; raw harmful content is not copied by default |
| Logging/Observability | Redacted correlation IDs, errors, latency, supported capability status and aggregate counters | Operational evidence only, not independent audit/case truth |
| Reporting | Permissioned, minimised scan volumes, category distributions and uncertainty/false-positive quality measures | Derived statistics; prohibit profiling individuals or engagement/reputation ranking by detector score |
| Queue/Scheduler | Committed assessment-completed/invalidated/expired events and due work from capability-owned outbox | At-least-once possible; subscriber deduplicates, orders per resource where required and rechecks source authority |
| Provider operations / integrations | Purpose-authorised disclosure payload and provider acknowledgement/deletion status | Provider uncertainty and processing locality disclosed; not proof of legal compliance |

**Results must carry:** tenant/scope, owning resource/revision or digest, assessment/job/check ID, accepted/started/completed/effective timestamps and Clock semantics, policy/profile revision, engine/model/dataset/provider versions, confidence and limitations, category/severity where supported, supported modality, partial/missing checks, expiry/reassessment requirement, completion versus delivery distinction, correlation, source/provenance and authorised visibility. No universal request type or private DB representation is imposed.

**Commands:** submit/reassess/cancel, inspect limited status, manage approved profiles/providers and revoke/expire result; source owner alone performs hold/release/publication. Accepted ≠ completed. Idempotency keys are tenant-and-owner-scoped, replay returns original accepted/committed result; changed payload with same key conflicts. **Queries:** scope-checked, revision-bound with freshness/completeness/unknown indicators, paginated and minimised. **Events:** only committed changes from Content Security's own outbox, with duplicate-safe consumers; delivery is not exactly once and never creates content-owner authority.

## Cross-capability responsibilities and directions

| Partner | Inputs Content Security needs | Outputs supplied to partner; failure rule |
|---|---|---|
| Publisher / Content Editor | Publisher registered document revision, intended publication and controlled snapshot; Editor only invokes Publisher's public action | Revision-bound scan result to Publisher; publisher enforces prepublication hold. Editor shows result only via authorised Publisher/public scan view, no private source/DB coupling |
| Media / Storage | Media owns image/file metadata, variants and access; Storage owns bytes and signed transport | Malware/inappropriate-media and metadata check results for specific original/variant; Media prevents unapproved derivative/CDN exposure and rechecks when bytes change |
| Comments Engine | Candidate text, links, target/revision, permitted scope | Explicit scoped verdict/inconclusive/unknown; Comments Engine enforces its local visibility and holds; not approval to post |
| Marketplace / Product / Reviews | Submitted listing/review/payload and authoritative seller/target context through source owner | Threat indicators only; Marketplace/review owner determines local disposition and verified commerce facts |
| Moderation | Case-scoped queries and lawful context as available | Detection evidence/referral; no case, appeal or sanction ownership. Moderation may request a revised assessment, not rewrite original |
| Configuration | Approved effective scanner settings, values, versions | Validated supported profiles, policy applicability issues and health; no delegation of legal or enforcement ownership |
| IAM / Verification | Trusted caller and risk-qualified assurance via published host ports; verification claims only when legally justified | Gated evidence access and audit-safe command decisions; no new identity or civil/age verification inference |
| Legal Compliance / Privacy | Applicable safeguarding limits, processing grounds, retention/holds, cross-border transfer | Scoped assessment disclosure/processing evidence; domain owner and law/purpose owner make separate decisions |
| Audit / Logging / Observability / Reporting | Authorised sinks/ports and purpose limits | Independent audit events; sanitised diagnostics/health; minimised aggregate statistics, never raw sensitive evidence by default |
| Scheduler / Workflow / Notifications / Message Queue | Registered due tasks, workflows/notification rules and outbox transport | Rescan/expiry work, assessment events and appropriate review-needed signals; no independent approval or messages to users without owner decision |
| Federation / Search / Hub | Origin content provenance, trusted local inspection scope if actually authorised | Technical findings for local Hub policy; each origin/Hub owns its exposure and removal. Do not send private bytes or trust remote `clear` unconditionally |
| Rich Text / Integrations | Safe text syntax/normalisation where available; vetted provider-specific adapters | Classifier feedback and provider capability statuses, not tree parsing/rendering or connector credentials |

**Dependency direction:** source capabilities invoke the published Content Security service through host wiring/ports; Content Security must not import their internal libraries or reverse-call their private state. Domain owners retain enforcement. Conditional coordination through published event/services is not automatically a static package dependency. Check the combined Nuxt extension and contract graph before implementation.

## Security, privacy, legal, provider boundaries

Apply OWASP ASVS 5 L2 and appropriate L3 high-risk controls, server-side authorisation, cross-tenant isolation, safe file handling, egress/SSRF constraints, scanning-worker sandbox limits, secrets isolation, integrity-protected intelligence feeds, model evasion/poisoning resistance, limited retention, provider access logging and reviewer separation of duties. Check resilience to Unicode obfuscation, multilingual risks, false positives/negatives, link-shortener redirects, deleted or newly malicious URLs, hash collision/context misuse, duplicate uploads and races between scan and publish.

**Risk taxonomy:** potential CSEA/grooming, threats, harassment, coercion, NCII (including synthetic), hate/incitement, suicide/self-harm, violent/extremist content, fraud/phishing/scams, dangerous links/malware and illegal sales, each only where a supported detector exists. Separate risk indicators, suspected statutory offence, legal constraints and formal determination; jurisdiction and service classification must be qualified. A detector cannot universally identify illegality, and neither a “clear” result nor high confidence is a legal guarantee.

**Privacy/especially sensitive content:** use least-privilege ephemeral inspection, restrict evidence references, prohibit unapproved outward transmission, distinguish private versus public/group content, honour approved purpose and lawful basis, protect E2EE by not assuming access/backdoors/client-side compulsory inspection, document transfers and retention. Consent is not universally the legal basis for safety processing. No mandatory provider sharing by default. A proposed architecture does **not** certify UK Online Safety Act or GDPR compliance; recheck applicable Ofcom requirements/service classification and legal duties at deployment. Mandatory safeguards are not silently deactivated due to cost, provider downtime or disabled configuration.

**Provider lifecycle:** inspect technical capabilities, coverage by modality/language, dataset accuracy/update frequency, contracting/licensing, jurisdiction/processors, usage/cost, latency/rate limits, API version and exit/removal. Support native/minimal checks and explicit no-provider mode where appropriate; selected mandatory check absent = incomplete/held. Provider replacement produces new provenance/version, not retroactive changes to earlier assessments.

## GUI and headless composition

Headless service is primary; **optional security/operator presentation** and contextual source-app indicators may be offered through public contracts. Host supplies sidebar link to a Content Security dashboard only when role and capability selection allow it; host owns navigation and routing. The dashboard needs coverage/health, job queue and recent failures, incomplete or expired checks, modality/provider coverage matrix, scanner profile/settings with approval and rollback, safe recheck, provider billing/usage and audit-linked history. Moderation's queue is a **separate** case UI; avoid duplicating decisions or displaying sensitive submitted material to all security operators.

Publisher, Comments Engine, Media and Marketplace screens display a compact contextual status (pending, completed with qualified checks, flagged, unknown, stale), safe next action and authorised appeal/recheck entry point. Content Editor consumes source-public interfaces rather than creating an enforcement screen. Implement WCAG 2.2 AA, keyboard/screen-reader semantics, accessible non-colour status descriptions, responsive layouts, localised messages, locale/timezone via Clock, Theme Manager semantic tokens and no unsafe previews. Support `presentation: false` and a concise independently usable root contract; a Nuxt adapter must keep the ADR-0012 one-call/50-line composition budget.

## Representative conceptual acceptance (not executable tests)

| Given input | Expected outcome | Authority |
|---|---|---|
| Unchanged allowed text with all declared checks completed | `completed` and named check results, version/limits; publication still source decision | Content Security result; Publisher disposition |
| URL assessment hits phishing dataset | Indicator with dataset/source/expiry; hold/review chosen separately | Content Security → domain owner |
| Image scanner lacks image support | `unsupported`/`incomplete`, never `clear` | Content Security |
| Required provider times out | Explicit unknown/error, secure pending/hold by owning domain policy; retry without false clearance | Scanner status; source state |
| Two concurrent scans same idempotency key | Same result for identical request; different request conflicts; no duplicate authoritative completion | Content Security |
| File updated between scan and publication | Old verdict marked stale; source refuses reuse for new revision | Media/Publisher |
| Different tenant asks for evidence | Deny without cross-tenant data, even with guessed job ID | IAM + Content Security |
| False positive challenged | New assessment/qualified case reference; historical result immutable with correction trail | Content Security; Moderation case |
| External provider leaks/fails to delete | Visible provider compliance/uncertainty, stop unauthorised further transfer, escalate; no false deletion receipt | Content Security + Privacy/Legal |
| Content owner removes item, CDN/Hub stale | Scanner does not certify remote removal; owner/Hub reconcile independent receipts | Source/Media/Federation |
| Private E2EE item not available for scan | No assumed plaintext or mandatory bypass; report `not_accessible` under service-specific policy | Host/source, not scanner |
| Detector config attempts to lower mandatory floor | Validation refuses weakening and preserves accountable version | Content Security + governing constraints |
| Unsupported direct `publish` or `banUser` request | Reject; never mutate source or Identity state | Source/Identity owner |

## Decisions, evidence gaps and follow-up

**Established:** governing Platform classification and detection-only ownership; public-contract and security/privacy/composition rules. **Approved conceptual direction (prior review):** separate detection (Content Security), adjudication/cases (proposed Moderation), owner enforcement, legal applicability and independent Audit; provider results must remain provenance-qualified and unknown must not be represented as clear. These are not implemented contracts.

**Owner-approved CS-01 (17 November 2026):** Define classification/check results as scoped, versioned technical evidence and require explicit unknown/unsupported states.  
**Owner-approved CS-02 (17 November 2026):** Source owner decides risk-based exposure/hold; required unavailable checks cannot silently clear.  
**Owner-approved CS-03 (17 November 2026):** Local/minimal supported checks permitted, but do not promise universal provider-free safety coverage.  
**Owner-approved CS-04 (17 November 2026):** Scoped ephemeral material references over blanket content copying and third-party transfer.  
**Owner-approved CS-05 (17 November 2026):** Preserve historical results with revisions; invalidate on edits and material policy/detector changes.  
**Owner-approved CS-06 (17 November 2026):** Provide headless service plus optional technical operator GUI; Moderation owns cases/reviewer decisions.  
**Owner-approved CS-07 (17 November 2026):** Treat per-modality/provider capabilities and no-provider modes explicitly; qualify cost, lawful transfer, accuracy and deletion.  
**Owner-approved CS-08 (17 November 2026):** Separate scanner assessment lifecycle from source-domain hold, case adjudication, appeals and Audit.

### Owner-approved conceptual decisions — 17 November 2026

**Approval scope:** The owner explicitly approved **Option C** for CS-09, CS-10, CS-11 and CS-12 in draft PR #55. This approves the conceptual principles below, **not** specific thresholds, provider choice, implementation, legal compliance, acceptance evidence or merging. CS-01–CS-08 were additionally and explicitly owner-approved on 17 November 2026; all CS-01–CS-16 are now conceptually approved.

- **CS-09 — Option C: Risk-based coverage and timing.** Apply baseline security validation to all untrusted submissions and risk-, modality-, exposure-, audience- and jurisdiction-specific assessment profiles. Run mandatory checks before the relevant exposure where required. When a required check is missing, unsupported, stale or unavailable, communicate an incomplete/unknown assessment and have the authoritative content owner apply a protective pending/hold/reject policy; never fabricate clearance. Not every private byte is to be automatically shared with an external classifier.
- **CS-10 — Option C: Proportionate disclosure.** Give contributors understandable outcomes and safe challenge/review routes without exposing attack-enabling detection methods, confidential threat feeds or other people's data. Release additional technical evidence only to appropriately authorised reviewers/administrators within purpose, privacy and tenant limits. A remote Hub receives only permitted, provenance-qualified information.
- **CS-11 — Option C: Data-minimised evidence.** Normally retain only the scoped result, version/provenance, relevant revision reference and necessary receipts; do not duplicate the source material as a general archive. Store especially sensitive evidence only with justified purpose, constrained access, defined retention/disposal, applicable legal holds and independent accountability. Exact schedules and legal obligations remain to be qualified by service, jurisdiction and evidence category.
- **CS-12 — Option C: Safe emergency detector isolation.** Authorised operators may isolate a compromised/unreliable detector promptly, using approved fallback checks where available. Mandatory safeguards must remain effective; otherwise the originating owner restricts relevant exposure pending safe assessment. Require attributable emergency action, least privilege, notifications/escalation where appropriate and post-incident review; emergency action does not grant permission to weaken compulsory protection.

**Implementation design still open:** exact initial modality/check matrices, detector thresholds and schedules, user notices, provider/data residency choices, evidence-specific retention periods, operational break-glass roles, retry budgets and consent/legal interpretations. These are refinements within the approved Option C boundaries, not reopening the choice of principle.

## Security scanning execution, admission and accountability — clarified 17 November 2026

**Where execution happens:** An originating application's/Node's **trusted server-side ingress boundary**, through a host-composed Content Security public port. Content Security coordinates and owns scanner selection, provider/dataset/check versions, assessment status and qualified evidence. Actual detectors may run in an independently isolated local worker/process/container or through a vetted external specialist service if legal, privacy, egress, provider availability and data transfer policies allow. **The conceptual contract does not require a separate microservice, a particular container orchestrator or universal third-party forwarding.** Browser-side hints are optional convenience checks and are never authoritative clearance.

**Who is responsible (distinct obligations):**

| Actor | Owns and must enforce |
|---|---|
| Application/Node ingress and originating domain (Publisher, Media, Comments Engine, Document where determined, imported/federated content owner) | Authenticate/authorise requests, input validation and parser limits; ensure required scan coverage under effective policy; keep untrusted material away from normal storage, previews, publication, indexes and distribution; admit only the exact revision/digest for which mandatory pre-admission evidence is satisfactory; own hold/reject/publish/remove and restoration |
| Content Security | Interpret the registered check profile and run/coordinate required supported detection, source/provenance-qualified per-check assessment, scanner capability/health and isolation, no false-clear status, reassessment/invalidation and minimal technical evidence; notify owners of failure, unknown, stale, revoked or superseded checks |
| Isolated scanner execution / Integration adapter / Infrastructure | Enforce lowest privileges, resource and network isolation, safe temporary handling and allowed third-party egress; Infrastructure supports execution but **does not** become authority for classification or source content state |
| Moderation | Cross-domain reports/cases, contextual investigations, decisions and appeals; may refer qualified decisions to owners but cannot bypass source gates or make detector evidence a legal finding |
| Receiving Node/Hub and Federation | Independently evaluate remote claims, enforce local admission/exposure checks, prohibit blind `clear` reuse and propagate/reconcile withdrawal without claiming remote deletion |
| Privacy / Legal Compliance / Authorisation / Audit | Respectively qualify processing and retention, duties, caller permissions and independent receipts; no blanket content copies in technical logs |

**Admission boundary:** Receipt of an upload into a bounded private inspection buffer/ingress compartment is not acceptance into authoritative application state. The default outcome for dangerous, unsupported, indeterminate or failed mandatory **pre-admission** checks is rejection and disposal of temporary material. Narrow legally mandated evidence preservation, if any, must be segregated under its own qualified authority and strict access/retention. Passing pre-admission checks is **not** permission for public exposure: the source owner may require additional pre-publication checks, authorisation and safety policy. Later intelligence or complaints may cause a *previously admitted* item to be held or removed; that distinct post-admission case should not weaken admission safeguards.

**Lifecycle and trace:** `received_for_inspection -> validated -> assessment_pending -> checked | rejected_or_unavailable -> (owner admits exact digest/revision, if eligible) -> potential publish/hold/revoke`. These are conceptual phases across distinct owners, **not** one Content Security-owned business state machine. Persist accepted-versus-completed assessment receipts separately, with check coverage, actor/source/tenant, policy/check version, expiry, minimal evidence and event/outbox/duplicate semantics as relevant. No server, Hub or application is justified in asserting a universal guarantee that all risks were detected.

## Additional owner-approved conceptual decisions — 17 November 2026

**Approval scope:** The owner approved CS-13, CS-15 and CS-16 and expressly approved the refined CS-14 *verify-before-admission* boundary in PR #55. These are conceptual choices only; no implementation or merge authorisation.

- **CS-13 — Mandatory baseline protection (agreed).** All content-owning capabilities implement applicable secure validation, parsing, output encoding, rendering, access control and safe ingestion for untrusted fields, files and imports, independently of Content Security's availability. Content Security provides additional required or optional risk-based assessments, never a replacement for secure processing. The check classification distinguishes baseline, format/feature-mandatory, risk/policy-mandatory and optional controls.
- **CS-14 — Verify before admission (agreed).** Unverified submissions MUST NOT enter normal authoritative content storage, ordinary previews, publication, search indexes or Federation distribution. **Receiving bytes for inspection is not admission.** Use memory-bound validation where feasible; larger payloads may occupy a strictly isolated, non-public temporary ingress area with limits, least privilege, no application/content readers, no general processing/serving, bounded expiry and controlled destruction. The originating capability admits the exact revision/digest only after all applicable **pre-admission** requirements succeed. **Admission is not publication approval:** separate pre-exposure checks, authorisation, policy and revision checks still apply. Unsafe, unsupported, stale or inconclusive mandatory checks cannot produce admission or clearance. Default to rejection and removal of temporary copies. Any exceptional legally necessary evidence preservation requires purpose, qualified authority, secure custody, retention and Audit and is **not** a general quarantine of risky material inside the application. Previously admitted material may be held/removed later on new intelligence, reports or changes; that is a distinct post-admission Moderation/source-owner workflow.
- **CS-15 — Network-wide security (agreed).** Receiving Nodes and Hubs authenticate and qualify external evidence, revision/digest, provenance, detector/check coverage, policy, expiry and applicable permissions; never blindly inherit another Node's `clear`. Each receiver owns its exposure controls and local restrictions; original content stays under origin authority. Withdrawal, restriction propagation and remote receipt/reconciliation remain distinct facts.
- **CS-16 — Detection quality, uncertainty and correction (agreed).** Assessment outcomes identify check coverage and omissions, supported media/language, applicable dataset/model/provider and policy version, confidence where meaningful, false-positive/negative limitations, freshness, errors and uncertainty. Qualified challenge, reassessment, contextual human review and historical correction must be possible without exposing detectors or sensitive material. No malware-clean result is equivalent to legal or behavioural clearance.

**Deferred to implementation design (owner agreed):** scanner and provider selection, concrete thresholds/retention schedules, exact API/types/database model, concurrency/retry mechanisms, specific temporary ingress technology, detector benchmarks and qualified jurisdictional legal interpretation. These must honour accepted conceptual floors and be evidenced before operational acceptance.

**Implementation alignment (not authorised here):** verify/create independently usable root `CONTRACT.md`; compare real entry points, provider adapters, owned stores/outbox, test fakes, storage register and minimal consumer evidence; demonstrate per-modality failure and permission tests, independent source owner scenarios and 50-line Nuxt adapter if used. No implementation was modified or tested in this PR.

**Conceptual decision disposition:** CS-01–CS-16 are explicitly owner-approved at the conceptual level. This is not approval of implementation, final operational acceptance or merging. No assertion of implementation availability, verified package compatibility, deployed operations, provider certification or legal compliance.

---
## Earlier preserved reciprocal evidence
## Cross-capability note — Scanning outcomes and evidential accountability (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** Content Security owns scanning and safety verdicts; relevant domain owner owns content disposition and override. **Proposed:** trusted classified verdict/override assertions may pass to [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026), which records provenance, receipt and review without treating a scan flag as legal guilt or copying risky raw content. Missing scan or verifier results remain unknown. Content Security's conceptual review remains incomplete.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Detection, not adjudication:** Content Security owns classifier/hash/URL assessment requests and provenance-qualified verdicts, including provider/dataset/model version, scope, confidence, unknown/failure and retention. It must not declare criminal guilt, change Publisher/Media/Marketplace records or substitute its scan flag for the proposed Moderation case. Mandatory unknown verdicts require the source owner's risk-defined protective behaviour; no false `clear`. External IWF/NCII/classifier services need vetted lawful terms, sensitive-data minimisation, costs and alternative failure modes.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52), **not** an approved contract or implementation change. See [Comments Engine conceptual contract](../comments_engine/capability-record.md).

Comments Engine submits bounded candidate text/link evidence with comment/target revision, classification context and purpose. Content Security returns provenance/version-qualified assessment or explicit unknown; it does not approve publication or adjudicate legality. Comments Engine enforces risk-defined hold/pending/reject, reassesses material edits, and must not expose unscanned text when required checks are unavailable. Prohibit private reporter leakage and unrestricted foreign provider transfer.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not implemented or approved. [Conceptual interface](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Editor displays source-owned pending, unavailable, quarantine and held safety results; no client indicator substitutes for Publisher/Media server gating or Moderation decisions.

## Reciprocal conceptual note — Course (17 November 2026)

**Status: Proposed, pending owner approval.** [Course review](../course/capability-record.md), draft PR #56: Course submission and linked learning content must meet required Content Security checks before public exposure; Course owns curriculum publication, Content Security owns scanning verdicts. Failed/unknown required verdicts block exposure; concurrent Content Security PR #55 remains provisional. This does not complete content_security's own review.

## Moderation dedicated review — reciprocal conceptual boundary (19 November 2026, draft PR #96)

**Status: Proposed, not an accepted public implementation contract.** See [Moderation's dedicated idealised input/output contract](../moderation/capability-record.md#dedicated-conceptual-review--19-november-2026-pr-96). Content Security supplies revision-bound detection findings, limitations and provenance to Moderation; it owns scanning, not case adjudication. Moderation may submit scoped reassessment requests. Missing/unknown/stale detection is never clearance or guilt; source owners continue native emergency holds.

## Reciprocal boundary — Moderation dedicated review (19 November 2026, PR #96)

**Proposed; non-normative, no implemented port asserted.** Content Security owns revision-bound scan findings, confidence/limitations and provenance, never adjudication. Moderation owns case decisions and can request a scoped reassessment; stale/unknown scanner output is not clearance or guilt. Source owner alone enforces holds. See [Moderation conceptual contract](../moderation/capability-record.md#dedicated-conceptual-review--19-november-2026-pr-96). Public host-assembled contracts must remain acyclic, scoped and permission-checked.
