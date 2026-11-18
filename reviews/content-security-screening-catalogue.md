# Content Security — comprehensive screening and control catalogue

**Status:** Proposed technical/conceptual classification under Content Security draft [PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), 17 November 2026. **Not** an approved list of installed detectors, a claim of universal scanning capability or an automatically applicable legal duty. Owner-approved **CS-09/10/11/12 Option C** govern coverage, disclosure, retention and emergency isolation. The specific catalogue/check matrix below is proposed for review, not silently approved.

**Reference baseline:** Governing `architecture-rules/master@2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint `master@b0b026931c4b66ec4bfc445489147045497db890` at last read. Current PR branch diverges from the latter after merged Configuration #53 and Content Editor #54; reconcile before merge.

## Screening versus controls

A **security control** is not necessarily a content scan. Safe SQL parameterisation, escaped output, safe markdown/rich-text rendering, malware-safe isolated processing, server-side access control, quotas and storage isolation are **enforced by the capability, host or relevant specialist owner**. Content Security supplies *reusable classification/detection assessments* where justified; scanning neither replaces those controls nor guarantees an unexploitable application. The conceptual public contract may publish common check identifiers, evidence, coverage and versioned results without becoming a universal application-security/firewall/authorisation engine.

**Required vocabulary:**
- `B` **baseline mandatory:** a protective control applies to every untrusted instance of that kind; executor may be source owner/platform rather than a scanner.
- `F` **format/feature mandatory:** check is required if the specific format, action, feature or processing risk exists (e.g. macros, archives, uploads, public URL).
- `R` **risk/policy mandatory:** risk assessment, audience, jurisdiction and legally qualified service duties decide applicability. A configured requirement may not silently be disabled.
- `O` **optional/defence in depth:** additional checks where justified; missing optional checks must be represented accurately.
- `N/A` unsupported or inapplicable is recorded and never represented as passed.

The **effective check manifest** for a source operation specifies requirement class, modality/content class, source/tenant/audience/jurisdiction and purpose, input revision/digest, check and detector versions, pre-exposure/background timing, freshness/expiry, required independent controls, on-error behaviour, disclosure and evidence retention. `B` does **not** mean every item is sent to every external scanner.

## S1 — Text, structured input and rendering / application threats

| ID | What must be checked or controlled | Applicability | Executor / ownership |
|---|---|---|---|
| S1-01 | Input schema/type, length, size, field allowlist, character/encoding validity, invalid Unicode, resource bounds | B, all untrusted fields/API/imports | Source owner/input validator |
| S1-02 | SQL/NoSQL/LDAP/template/OS-command injection, path traversal and unsafe dynamic queries through parameterisation, context-specific validation and safe API design | B, all untrusted inputs reaching interpreter/sink | Source owner/implementation security; scanner never substitutes |
| S1-03 | XSS, HTML/SVG/script/style injection, event handlers, unsafe embeds, dangerous attributes, rich-text and markdown rendering | B where user text can be rendered; F for formatted text | Source owner + `rich-text` safe tree + secure renderer; Content Security may detect indicators |
| S1-04 | Prompt injection, malicious instructions in retrieved documents/imports/tool results, data exfiltration instructions and indirect tool abuse | F where AI/automation/tool execution consumes untrusted text | AI/tool execution boundary, authorisation, source owner; optional Content Security signals |
| S1-05 | Unsafe regular expressions, malformed/recursive parsers, XML external entities, entity expansion and denial-of-service payloads | F for parsing/structured import | Safe parser/host and owner; isolated execution and limits |
| S1-06 | Active formula/external references and spreadsheet/CSV formula injection on import/export/open, leading special characters | F for spreadsheets/CSV/tabular input and export | Document/spreadsheet/import/export owner |
| S1-07 | URLs, URI schemes, redirects, punycode/homograph or confusable domains, shorteners, tracking redirects, malicious destination and phishing indicators | F for any link in text or metadata; R reputation check by exposure | Source owner sanitises and constrains; Content Security URL reputation assessment |
| S1-08 | Credential/secret exposure, tokens, API keys, private personal identifiers, doxxing indicators | R when publicly shared/imported; sensitive false positives | Content Security signal; Privacy, source owner and Moderation for disclosure decision |
| S1-09 | Spam, unsolicited advertising, mass repetition, bot-driven submissions, abusive volume, rate/deduplication/cost quotas | B for public submission abuse controls; R classifier | Source owner/rate limiting; Content Security optional spam classification |
| S1-10 | Dangerous or untrusted iframe/embed origins, remote resources, SVG/HTML rendered as executable content, CSP and safe isolation | F for embeds/previews | Publisher/Document/Media host and security policy |
| S1-11 | Hidden instructions in Unicode control characters, bidirectional markers, zero-width obfuscation, disguised links, text embedded in metadata | F input canonicalisation; R abuse context | Owner preserves faithful text and limits unsafe presentation; scanner reports limitations |
| S1-12 | Misuse of permitted file paths/URL references (SSRF, internal service probes, DNS rebinding, cloud metadata endpoints) | F for server-side fetch/import/preview | Host/importer network/egress isolation; Content Security may assess URL threat |

**Important:** Most S1 controls are **not** delegated to Content Security. For normal text fields, do *not* run blanket third-party language toxicity classification or store duplicate personal data.

## S2 — Files, images, documents and other media

| ID | Threat/check | Applicability | Owner |
|---|---|---|---|
| S2-01 | Allowlisted type, extension/MIME/signature consistency, true format parsing, disguised/polyglot files | B for untrusted uploads; F format parser | Media/Document/source owner and isolated validator |
| S2-02 | Antivirus/signature malware, trojans, ransomware, worms, embedded executables, exploit payloads, malicious downloader/script | F for untrusted file ingestion and distribution; risk-based scan depth | Content Security malware detector; source holds until mandatory check |
| S2-03 | Suspicious archive contents, nesting, compression bombs, decompression ratio/limits, recursive traversal, symlinks, special file entries | F for archives/container formats | Source owner sandbox + scanner when appropriate |
| S2-04 | Macros, OLE/embedded objects, PDF JavaScript/actions, active document content, remote external references, embedded fonts/scripts | F for office/PDF/e-book/templates | Document/Publisher owner safe preview; Content Security scanner/CDR adapter |
| S2-05 | Raster image decoder exploits, malformed headers, extreme dimensions/pixel counts, malicious image data, unsafe SVG | F for images | Media safe decoder/rewriter + scanner |
| S2-06 | Image EXIF/XMP/IPTC/GPS, author/device/location details, embedded thumbnails/comments and privacy-sensitive metadata | F for uploaded/public images | Media metadata policy/stripping, Privacy constraints; Content Security flags anomalous metadata |
| S2-07 | Steganographic/hidden payloads, embedded executables, encoded data, suspicious metadata, data exfiltration payloads | R targeted detection, limitations explicit | Content Security specialist detector; source owner enforces |
| S2-08 | Exact/robust hashes and permitted trusted matching for known high-risk imagery (e.g. CSEA/NCII) with legally/contractually approved datasets | R according to qualified policy; tightly restricted | Content Security approved hash-provider, Moderation cases; never assume match is final legal finding |
| S2-09 | Classifiers for potentially unlawful sexual imagery, intimate imagery, synthetic non-consensual material, exploitation, graphic violence and other risk signals | R according to exposure/service/audience and law | Content Security scoped model; Moderation investigates; Media enforces |
| S2-10 | OCR/extracted text, QR codes and embedded links in images/screenshots/document scans | R for relevant contexts; link controls F if extracted links are used | Content Security/OCR provider or safe extraction; source owner controls previews |
| S2-11 | Audio/video container, codecs, decoder defects, file malware, embedded tracks, captions/transcripts, thumbnails, time/rate/size limits | F if audio/video supported; R content classifiers | Media/source owner + Content Security supported modality; no claims if unsupported |
| S2-12 | Generated thumbnail/preview, conversion, export, derivative variants and transformations for retained threats or new active content | F for transformations | Media/Document/Publisher; rebind assessment to derivative/revision |
| S2-13 | Remote hosted file/download malware, link changes, content-type or digest drift after assessment, mutable originals | F when fetched/served; R reputation recurrence | Source/Integration/Federation owner with Content Security recheck |
| S2-14 | Block executability/dangerous inline hosting, use safe content disposition, no sniffing, controlled downloads and URL expiry | B when delivering untrusted files | Storage/Media/source + host; not proof supplied by scanner |

A hash match is a **signal tied to a particular dataset and method**; a negative hash match does not mean an image is lawful or safe. Never copy especially sensitive source imagery into routine logs, audit, training sets or provider requests without qualified lawful purpose and approvals.

## S3 — Human safety, conduct and contextual content risks

| ID | Category to assess when risk policy applies | Relevant distinctions |
|---|---|---|
| S3-01 | CSEA, sexual grooming, exploitation, child abuse facilitation and related contact risk | High-priority specialist safeguards and statutory referral review; private spaces need separate legal/privacy classification |
| S3-02 | Non-consensual intimate images, intimate-image threats, synthetic intimate imagery, sexual harassment, cyberflashing | Consent/context and provenance matter; no definitive guilt by classifier |
| S3-03 | Illegal sexual content and age-inappropriate or adult imagery | Adults-only material and unlawful imagery differ; explicit nudity alone is not proof of offence |
| S3-04 | Hate speech, targeted abuse, identity-based harassment, discriminatory hostility and incitement | Do not conflate legally protected discussion, quotations and actual threats; jurisdictions differ |
| S3-05 | Bullying, dogpiling, harassment, stalking, coercive control, intimidation and repeated unwanted contact | Behavioural pattern and context may be decisive, not merely single-text toxicity |
| S3-06 | Credible threats of violence, incitement, targeted threats and dangerous coordination | Assess immediacy and context; urgent escalation may be required |
| S3-07 | Terrorist content, extremist recruitment, support/financing instructions and violent propaganda | Legal assessment and qualified obligations distinct from technical match |
| S3-08 | Suicide/self-harm encouragement, dangerous encouragement and exploitation of vulnerable users | Avoid treating support requests or crisis discussion as abuse |
| S3-09 | Fraud, phishing, impersonation, romance/investment scams, financial manipulation, counterfeit or prohibited trade | Marketplace/Payment/Order retain business fraud and seller decisions |
| S3-10 | Illegal goods/services promotion, exploitation, illicit transactions or facilitation | Listing owner enforces product/marketplace constraints, qualified by law |
| S3-11 | Malicious disclosure of private information, doxxing, blackmail, sexual extortion, threats to release private content | Access and privacy constraints apply; reporter/witness identity must be protected |
| S3-12 | Misinformation, manipulated content, authenticity/AI provenance or impersonation indicators | Not automatically unlawful; no universal factual arbiter, guard against false censorship |
| S3-13 | Profanity, obscenity, offensive language, insults, spam and uncivil behaviour | **Separate configurable community policy category**, not inherently illegal or always warranting blocking |
| S3-14 | Graphic violence, cruelty, abuse imagery and age- or context-inappropriate media | Contextual educational/news/reporting exceptions, audience/access settings |
| S3-15 | Copyright, trademark, IP claims, plagiarism and licence violations | Specialist claim/rights evidence and dispute workflow; detectors are indicators, not legal determinations |
| S3-16 | Sexualised content involving minors, age-targeted exploitation and inappropriate minor/adult contact patterns | Distinguish safety signals, qualified age assurance and domain restrictions |
| S3-17 | Spam/deceptive marketing, coordinated manipulation, sockpuppetry or mass-produced abusive content | Behavioural risk may require source/domain account and network evidence, not text scan alone |
| S3-18 | Public safety/public health or other jurisdiction-specific regulated categories | Only add verified service-specific duties and lawful policies; no blanket political/opinion censorship |

**Applicability:** S3 is R (risk/policy mandatory), never an assertion that automated algorithms can or should decide every reported category. Use sensitive matching services only with vetted sources, qualified legal terms, privacy limitation, traceable model/dataset revisions and false-positive correction. Moderation owns cross-domain investigations and appeals; source content owner owns immediate holds and actual source restrictions.

## S4 — Supply-chain, import, federation and provenance risks

| ID | Check | Applicability / owner |
|---|---|---|
| S4-01 | Authenticity, trust level and integrity of source feed, provider API and imported packages; signatures/identities where supported | F external imports; Integrations/Federation/importer |
| S4-02 | Import schema and size limits, nested data, injection, unsafe URLs/media, malformed and mixed-format content | B all imported data + F by format; destination owner |
| S4-03 | Content owner/resource revision, digest, signed attestations, claim source, trust/expiry and permission | F federated intake and attestations; Federation/source owner |
| S4-04 | Known malicious URL/domain/hash/blocklist signals with source/expiry/appeal; defend against poisoned feeds and false reports | R threat-intelligence use; Content Security + Federation |
| S4-05 | Duplicate, replay, stale or substituted content and origin-hub divergence, revoked peer/content claims | B events/replay control; F federation; Federation/domain owners |
| S4-06 | External AI/model outputs, generated markup/files/links, third-party rendered previews and embedded remote content | F for generated/third-party content; destination owner |
| S4-07 | Remote scan verdict claims: trust scope, detector evidence, policy equivalence, signature, version and expiry | R when trusting foreign scan evidence; never uncritically reuse `clear` |
| S4-08 | Publication/distribution rights, licence, audience/age restriction and privacy/export consent | F when redistributing; source owner, Privacy/Legal Compliance; not technical malware classification |
| S4-09 | Supply-chain compromise of scanning libraries, provider datasets, reputation feeds, classifier models and plugin adapters | B operational assurance, updates/integrity verification; infrastructure/security operations |

Federation must treat other Nodes and Hubs as distinct trust boundaries. A Hub may restrict its own index; it cannot remove source Node content. External provider API credentials, egress and legal disclosure stay controlled by the host and applicable owner.

## S5 — Ongoing assessment and revalidation

| ID | Trigger | Responsibility |
|---|---|---|
| S5-01 | Content revision, attachment replacement, derived variant, mutable file bytes or digest mismatch | Source owner invalidates bound verdict; Content Security reassesses where policy requires |
| S5-02 | URL redirect/destination/domain/reputation changes | URL owner and Content Security apply freshness/recurrence based on risk |
| S5-03 | Newly published malware intelligence, changed hash dataset, classifier/rules or vulnerability disclosures | Content Security exposes version/expiry and schedules targeted reassessment |
| S5-04 | Source visibility/audience/tenant or jurisdiction changes | Source owner recomputes required checks and publication eligibility |
| S5-05 | Provider outage, timeout, budget exhaustion, false-positive incident or compromised scanner | CS-12 isolation/recovery; never issue `clear` for missing checks |
| S5-06 | Quarantine/hold release, appeal/reinstatement, re-publication and content restoration | Source owner verifies current authorisation, revision and checks; Moderation owns case decision |
| S5-07 | Search/cache/CDN/preview/feed/hub withdrawal propagation and stale remote copies | Source/Federation/Search/Media reconcile independent receipts; scanner cannot certify global deletion |
| S5-08 | Retention expiry, rights requests, provider data deletion, statutory hold and audit evidence review | Content Security owns scan job/evidence disposal; source owner retains content lifecycle; Privacy/Legal Compliance constrain |

## Input entry points and minimum routing matrix

| Entry point and examples | Baseline controls | Extra content checks / timing | Owner |
|---|---|---|---|
| Plain text fields (names, headings, titles, references, addresses, notes, form fields, support messages) | S1 input/rendering and permitted-field validation **always**; never turn text into executable code | S3 only for publish/share/audience risk; credential/PII leakage where justified; never universal external toxicity scanning of private forms | Each form/domain owner |
| Free-text comments, replies and reviews | S1 baseline, anti-abuse/rate controls | Public/group policy S3 hate/harassment/threats, links S1-07 and applicable fraud/child-safety rules, before exposure when mandatory | Comments Engine / Reviews |
| Articles, blogs, pages, rich-text and publication drafts | S1 baseline, safe rich-text tree and embeds | External links, abuse/fraud and relevant S3 before public release; recheck revised versions | Publisher |
| Templates, office documents, spreadsheets, presentations, PDFs, CSV/XML/HTML and attached files | S1 baseline, S2 format/decompression/malware/active-content and safe preview/export; CSV formula controls where applicable | Extracted text/URLs and image content S3/R only by audience, context and purpose | Actual document owner (Publisher/Document classification unresolved), Content Editor as presentation |
| Image uploads, screenshots, scanned documents, thumbnails, albums, profile pictures | S2 format/size/decoder/malware/privacy metadata, safe transforms and downloads | S3 relevant imagery/known-harm hash checks, optional OCR/QR/link inspection; before public delivery when required | Media; domain owner for image's publication context |
| Audio/video uploads, transcripts/subtitles | Format/codec/resource validation and safe processing when supported | Transcript, imagery/voice and user conduct signals only with supported detectors and justified policy; otherwise unsupported/hold as necessary | Media/source; future support conditional |
| Product/listing descriptions, merchant media and marketplace imports | S1/S2 baseline | Scam/phishing, illicit sale, abuse, prohibited images according to seller/listing/service risk | Marketplace/Product and other source owners |
| Third-party imports, feeds, API/webhook payloads and AI-generated content | S1/S2 baseline, trust/provenance/replay checks S4 | S3 only where audience/exposure policy needs; never trust an external `clear` automatically | Integrations/Federation/destination owner |
| Federated content or content exposed on Hubs | Trust/revision/permission/provenance checks and supported safe-preview controls | Hub-local policy and service-specific duties; classification may use scans and remote evidence with qualification | Origin owns source; Hub owns own index/presentation |
| Private/E2EE content | Local validation and access enforcement where technically feasible without breaking confidentiality | No blanket content extraction or compulsory external scanner assumption; separate lawful, risk-qualified reporting and safeguarding design | Source/host and specialised policy owners |

**Boundary reminder:** S1 common controls must not be misconstrued as a synchronous round trip to Content Security for every database field. Validators and safe rendering must work with Content Security unavailable. A reusable scanner is invoked by the owning capability when appropriate.

## Contract and results requirements

Each check entry must publish: `checkId`, `classification` (S1–S5), `mechanism`, `executorOwner`, `appliesTo`, `requirement` (B/F/R/O), `purpose`, `preExposureRequired`, `inputsAndPermissions`, `supportedModality`, `providerCapability`, `policyRevision`, `detectorVersion`, `dataFreshness`, `retentionClass`, `disclosureClass` and `unavailableBehaviour`. Logical fields only; not a universal required host request shape.

The outcome vocabulary must separate `passed_named_check`, `detected_indicator`, `inconclusive`, `unsupported`, `not_run`, `not_applicable`, `stale`, `failed`, `provider_unknown`; include job accepted/running/completed status and check-set coverage. A technical detector finding does not itself decide illegality. A scanner performing only S2 malware checks cannot claim S3 image-safety clearance. Security-control compliance (S1/S2 host measures) also requires independent security/CI evidence, not self-declared scan results.

## Assured failure boundaries and operational design

1. For mandatory checks, source owner must enforce pending, restricted, quarantined or rejected exposure when results are missing, failed, unknown, unsupported or stale; choose policy proportional to service/legal risk. No auto-publish on timeout.
2. Preserve versioned reports for checks actually run; do not imply that an untested modality is safe. Control evaluation of re-used results by exact resource/digest, audience and effective policy.
3. Bound file size, processing time, archive depth, concurrent jobs, egress and provider cost while preserving required safeguards; capacity pressure must be visible.
4. Quarantine files before unsafe preview/serving; scanners run with low privilege/isolation, never giving untrusted payloads access to private system/network resources.
5. Cross-tenant access, reviewer evidence, minors, intimate imagery and reporter identity need scoped authorisation, minimisation and audit; no unnecessary retention of raw evidence.
6. Permit provider-neutral antivirus, file parser/CDR, URL intelligence, approved image hash feeds, classifiers and OCR only when qualified, licensed and transparent about provenance, jurisdiction, limitations and fallback.
7. Confirm actual OWASP ASVS 5 baseline and independently validate technical security controls; content scanning cannot replace ordinary security engineering.
8. Establish false positive/negative review, red-team and adversarial-evasion acceptance, and safe restoration without global undelete claims.

## Concrete conceptual acceptance scenarios

- An ordinary private name field is safely stored and rendered without external abusive-language classification; injection remains impossible by construction.
- Public comment contains an XSS payload: safe input/rendering behaviour stops execution even if Content Security is offline; harmful-content assessment is separate.
- Harassing public text is flagged by qualified classifier: owner holds or routes to Moderation under policy; no automatic criminal finding.
- A valid-looking image with malicious/polyglot payload cannot bypass file validity checks by extension/MIME; no dangerous public serving before mandatory checks.
- An image with a licensed known-harm dataset match goes to tightly restricted safety handling; no unrestricted evidence preview, no blanket guilt inference.
- An uploaded spreadsheet has formulas that would execute in downstream spreadsheet applications: importer/exporter treats them as active content and prevents unsafe interpretation.
- An uploaded DOCX/PDF containing macros/scripts or embedded malicious attachment remains restricted and receives appropriate supported checks/CDR; unsupported checks not marked passed.
- A web article containing an unsafe URL is rechecked on material change; source owner prevents publication if a currently required check failed.
- A federated item carrying remote `clear` evidence cannot bypass Hub-local/authorisation rules or source revision checks.
- A flagged quotation of hate speech in legitimate research is routed for qualified contextual review rather than treated as proof of criminal hate offence.
- Required image classifier is unavailable while public exposure is requested: result `unknown/incomplete`, the owning capability holds exposure; a scanner fallback may be applied only when equivalently approved.
- New dataset release renders older scans stale where policy requires; owner checks current eligibility before restoration or subsequent exposure.
- Content Security's technical scan history contains only necessary risk and provenance receipts; sensitive files remain with the authorised owner unless justified evidence capture is explicitly permitted.

## Open implementation/owner matters

Detailed baseline check applicability per supported initial media types, initial service legal/risk classification, first-release modality support (especially audio/video/office/collaboration), precise URL freshness and metadata handling, classifier quality/false-positive tolerances, and licence/provider vetting remain open. This catalogue **does not impose a universal content prohibition on profanity** or a legally unqualified universal scanning mandate. Do not automatically classify authors, quoted texts or private messages as illegal. No implementation or mandatory database schema is prescribed.
