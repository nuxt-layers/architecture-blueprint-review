# **Capability Record**

## Capability Name:

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).

## Purpose

## Classification

## Dependencies

## Optional integrations

## Version

## Availability

## Capabilities offered

## Configuration




## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved direction for blueprint documentation only; not a completed capability review, implemented API or governing ADR. See [cross-capability review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

**Asset-specific safeguards:** Media owns uploaded media records, metadata, processing/derivative lifecycle and access to assets, with Storage providing byte-store operations through its port. Media must quarantine uploads/variants pending applicable safety gates, prohibit unapproved public/signed access, enforce removal and restoration, and issue authoritative lifecycle/outbox evidence. Content Security supplies detection; proposed Moderation handles reports/cases and appeals; Audit preserves minimal receipt evidence. Protect CSAM/NCII evidence by minimising access, transfers and retention; operator review requires independent safeguards.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed contract alignment in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not a completed media review, normative rule or implementation change. See [Content Editor conceptual boundary](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

The editor may request Media's authorised picker/asset metadata through public contracts; Media owns asset status, alt/access eligibility and quarantine, with Storage owning bytes. Unavailable or pending assets cannot silently become publishable Publisher references.

## Content Security — reciprocal conceptual interface (17 November 2026)

**Status:** Proposed in [Content Security draft PR #55](https://github.com/nuxt-layers/architecture-blueprint-review/pull/55), not an accepted implementation contract. See [Content Security conceptual record](../content_security/capability-record.md).

Media remains authoritative for uploads, image/file versions, variants and visibility; Content Security evaluates only properly authorised snapshot/byte references, links and applicable risks, returning revision/digest-bound evidence. Incomplete or stale checks never silently authorise derivative/public delivery; Media handles hold and CDN/original exposure, Storage bytes remain separately owned.

## Reciprocal conceptual note — Course learning offering (17 November 2026)

**Status: Proposed, not approved or implemented.** [Course conceptual review](../course/capability-record.md), draft PR #56: Course references versioned safe learning assets; Media owns asset metadata, quarantine, derivative lifecycle, Storage owns bytes. Course honours safety and access gates before exposure. This note does not complete the separate media review.

## Gallery reciprocal interface — 18 November 2026 (proposed; PR #70)

[Gallery's conceptual presentation contract](../gallery/capability-record.md#dedicated-conceptual-review--gallery-18-november-2026) consumes Media's current authorised variant metadata, alt text, safe thumbnail/lightbox delivery, asset picker/upload and original-download entitlement decisions; it holds no image bytes or authoritative asset state. Media must independently enforce member-only access, quarantine, removal and revocation for original and every derivative, URL, cache and CDN exposure; Gallery's visible button or Publisher publication does not grant access. Gallery's member submission intent is not a Media acceptance receipt. **Evidence gap:** Media's root `CONTRACT.md` was not retrieved; exact private delivery, picker and original-download public interfaces remain unverified. Existing online-safety and Content Editor findings are preserved.


## Dedicated conceptual review — Media (19 November 2026)

**Status: Proposed, awaiting owner conceptual approval. Non-normative; not an implementation contract or acceptance result.** [Draft PR #92](https://github.com/nuxt-layers/architecture-blueprint-review/pull/92) · [Opening baseline](../../../reviews/media-review-baseline.md). Governing `architecture-rules/master`: `b920ce0d8b361de000a6739a16123dbdc56df7a7`; blueprint opening `master`: `6dac83a03da8704f7945ee1bc894f2248300445a`.

### Identity, classification and evidence

**Platform capability; retain independent, state-owning Media responsibility.** Media makes tenant/group-owned images usable and safe for application content, manages asset metadata and revisions, processing derivatives, publication eligibility, revocation and retention, and exposes protected asset-resolution services. It is not a generic byte store or an editorial publication system. This aligns with the [accepted governing catalogue](https://github.com/nuxt-layers/architecture-rules/blob/master/docs/catalogue.md), Capability Standard and accepted ADR-0002, ADR-0009 and ADR-0012. The target implementation repo `nuxt-layers/media` exists at `6f68c8af248a9a349bc091a2162fbc5c695dba9a`, but **has no root `CONTRACT.md`**. Its README expressly says nothing is built; `docs/design.md` contains owner-agreed **25 October 2026 design intent**, not verified executable interfaces. Hence all interfaces below are *idealised proposed*, not actual exported functions. Related Publisher's root `CONTRACT.md` documents an optional `assets.resolve({ siteId, assetIds })` contract with URL/size-or-null outcomes; this is a verified **consumer expectation**, not a verified Media implementation.

**Prior conceptual evidence preserved:** Online Safety/Moderation, Content Security, Content Editor, Gallery and Course reciprocal notes above. These constitute status-marked proposals unless independently approved. Gallery, Publisher and Content Editor do not own Media records or storage bytes.

### Authority and excluded responsibilities

Media owns immutable asset identity, tenant/group owner reference, uploader identity reference, canonical image metadata, dimensions/format/checksums, alt/decorative designation, provenance/rights/credit attestation, authoritative asset revision, derivative manifest, processing state, safety eligibility, current disclosure/visibility state, archival/removal/tombstone state, own quota accounting and access/revocation evidence. Its own persistence schema and durable outbox are capability-owned; Storage supplies byte operations through ADR-0012's `storageFor('media')` Files shape. Identity owns tenant/group/member facts; Profile owns display names; Authorisation owns caller access decisions; Privacy and Legal Compliance determine applicable restrictions; Content Security owns detection evidence; proposed Moderation owns reports/cases and appeal adjudication, while Media executes only its own holds and takedowns. Publisher owns documents, published links and use context; Gallery owns neither photos nor album records except as Publisher types. Storage owns bucket/provider lifecycle, file-byte keys and signed access primitives, not Media eligibility or business policy. Media must never treat possession of a signed URL, CDN token, downstream document link or provider callback as authorisation.

Image asset contract is the minimum scope established by governing catalogue. Support for **video, audio, arbitrary document attachments, transcoding, OCR and DRM** is **deferred**; a generic name `media` does not silently confer them. Any scope expansion requires explicit owner decision and revised threat model, interfaces, costs and rights checks. The 25 October design gives JPEG/PNG/WebP/AVIF/HEIC input, 10 MB default / eligible 25 MB, 50 MP maximum, WebP widths 480/960/1920 and an optional cleaned private original; these are **historical agreed design defaults pending implementation/contract verification**, not runtime guarantees.

### Native service, state and failure model

1. **Prepare upload:** authorise tenant/group, scope, size/format/quota and rights/consent attestation; issue a short-lived, single-purpose staging grant via Storage. A grant is neither acceptance nor publishability.
2. **Claim and inspect:** verify stored object binding, measured bytes, actual content/MIME, digest, decompression/pixel limits, malware/unsafe format risks and ownership; reject suspicious or mismatched uploads. Enforce idempotent claim and a bounded staging expiry.
3. **Sanitise and transform:** strip embedded geolocation and hidden metadata; produce bounded web derivatives, optionally a separately protected cleaned original. Transform failure or incomplete safety verdict retains a non-deliverable state; do not silently expose unprocessed bytes.
4. **Eligibility:** `pending → processing → held/rejected | ready`; archived, quarantined, removed and erased/revoked are distinct states. Content Security evidence is tied to exact digest/revision and policy version; stale, unavailable, invalid or inconclusive checks cannot produce `ready/public`. Separate permitted *private review* access from release eligibility.
5. **Maintain:** authorised alt/decorative, credit, rights and usage updates carry revisions and provenance. A checked image may require revalidation after content-changing transformations or policy change. Archival hides discovery, not authorised existing references; removal revokes every original/derivative and delivery handle. Reinstatement rechecks current policy and content.
6. **Delete/erase:** check Publisher backlinks, legal holds, tenant policy and third-party rights; distinguish voluntary deletion (may be blocked by references) from mandatory takedown/erasure (must revoke exposure while retaining minimal legally required evidence). Preserve a safe non-disclosing tombstone for historical references. Restore/backup must replay revocation and erasure decisions; caches and signed URLs have bounded life and purge/invalidation contracts.
7. **Allowance:** expose measured/reserved/committed usage and entitlement-derived limit with reconciliation to Storage; deny new writes on exhausted allowance, do not erase existing assets merely because an entitlement expires. If entitlement authority is unavailable, no unverified increase in limit; keep an explicit conservative configured floor if permitted.
8. **Recover:** all operations distinguish requested/accepted, processing, completed, failed and unknown outcomes. Retry safely with operation key, reconcile orphaned objects, interrupted transformations and asynchronous delivery; no distributed exactly-once guarantee.

The service must remain useful for authorised manual image upload/management with a host-supplied storage service and essential IAM/policy decisions, without a commercial billing, external processing, Gallery or Content Editor provider. Essential persistence and Storage absence fail closed.

### Idealised inbound public contract

| Source | Facts/operation provided | Authority and requiredness | Validation / uncertainty |
|---|---|---|---|
| Caller/host via Authentication, Identity and Authorisation | Tenant, subject, assurance, target group; `decide(caller, action, resource)` for upload, read, manage, delete, download and review | Essential trusted server context/access decision; Identity owns group/membership | Never trust client group claims, infer hierarchy grants or upgrade assurance; deny missing/ambiguous decision |
| Client/editor/gallery/application | Prepare/claim upload, update alt/decorative/credit/rights, request variants, archive, remove, download original, inspect state; expected revision and idempotency key | Commands are intent only, never authority | Runtime check, limits, current policy, ownership and optimistic revision; stable conflict/refusal outcomes |
| Storage port | Signed staged upload/byte operation, metadata, object existence, derivative commit, deletion and delivery capabilities | Essential provider-supplied Files port; Storage owns bytes | Validate scope/expiry/size/digest, clean up orphans; uncertain provider response stays pending/inaccessible |
| Content Security | Scan verdict and provenance for specific asset digest, revision and policy | Conditional mandatory safety gate where applicable; detection owned by Content Security | Reject stale/partial/mismatched evidence; unavailable stays held |
| Proposed Moderation, legal/privacy policy | Enforcement case/appeal outcome, hold, removal or release request; legal retention/erasure constraints | Conditional; Moderation cases provisional, Legal Compliance/Privacy applicable constraints authoritative in their scope | Validate request authority and exact target; conflicting hold takes precedence pending reconciliation |
| Publisher and other domain owners | Authoritative backlinks and publication/access context; references in drafts or published documents | Conditional for referential deletion and use; Publisher owns document state | Absence/unknown links cannot be assumed unused; no permission inferred from public publication |
| Configuration/entitlements/administrators | Approved allowance, original retention, upload limits, feature/configuration version, effective date | Conditional provider; Media enforces bounds; admin fallback per prior design | Validate policy against non-configurable floors; stale/invalid limit cannot expand privilege |
| Clock and background execution | Authoritative time semantics, retry/expiry/retention scheduling, outbox delivery | Clock semantics; optional executor/transport via public ports | Expiry and revocation evaluated server-side; execution delay not a release |
| Uploader rights/consent attestation | Source ownership/licence/credit and applicable child-image consent claim | Required as policy dictates; claim is evidence of assertion, **not proof of legal compliance** | Refuse omitted required declarations; potentially sensitive evidence minimised and retained by policy |

### Idealised outbound public contract

| Public surface | Consumer and permitted meaning | Ownership, freshness and disclosure |
|---|---|---|
| Upload preparation receipt | Host/client receives scoped staging token, constraints and expiry; **not accepted media** | Storage grant plus Media policy version; no public URL |
| Accepted/processing result | Uploader sees asset ID, operation ID, state, revision and outstanding checks | Media authority for workflow state; does not guarantee ready/public |
| Asset descriptor and picker query | Content Editor, Gallery, Publisher adapters, domain applications see permitted ID, alt/decorative, credit, dimensions, format, variant/thumbnail availability, ownership scope, revision and eligibility | Media authoritative only for asset; current server-side access/visibility check; pagination and completeness stated; no private uploader Profile fields by default |
| Asset resolution/delivery grant | Publisher/renderers receive **only authorised** deliverable rendition/URL or explicit unavailable/removed/held placeholder and expiry | Audience/resource-specific authorisation, versioned immutable rendition, per-request private delivery; no long-lived public original or disclosure by cached stale URL |
| Original-download decision | Privileged requestor receives short-lived scoped private download or refusal | Never by public token; step-up as policy requires; all derivatives/originals separately revocable |
| Usage/allowance and cleanup candidates | Group administrators view committed/reserved bytes, cap, reconciliation freshness, unused candidates and restrictions | Media accounting, Storage byte figures distinguished; no automatic deletion based on 90-day candidate |
| Enforcement/removal receipt | Moderation, Content Security and authorised operators see applied hold/revoke/purge state with known incomplete cache outcomes | Media execution evidence, not a Moderation case verdict or legal interpretation |
| Immutable lifecycle events | MQ, Publisher, Search, Gallery, Audit, Reporting and revocation consumers receive committed `asset.claimed`, `asset.ready`, `asset.revised`, `asset.held`, `asset.archived`, `asset.revoked`, `asset.erased`, `allowance.changed` as appropriate | Capability-owned durable outbox; at-least-once relay, event ID/revision/tenant/correlation and redacted payload, duplicate/replay-safe |
| Export/erasure/reporting read models | Privacy requests, authorised administrators and Reporting receive bounded records, provenance and restricted retained evidence | Media supplies only own facts, with scope/retention and withheld-content markers; not Storage bytes as an unrestricted public export |

**Interaction rules:** commands are revision-checked and idempotent where retried; queries indicate freshness, partial availability, provenance and permissions; events follow committed authoritative changes and may be delivered more than once/out of order across consumers. Unknown provider result is not success. Distinguish archived from removed and erased; revoked URLs must not continue serving known content. Stable domain errors should cover unauthenticated, forbidden, insufficient-assurance, validation-failed, quota-exceeded, version-conflict, held, in-use, not-found, pending, unavailable and unsupported-operation. All protected actions are authorised server-side; client picker controls are presentation only.

**Shared context (not a universal request object):** tenant/site/group owner, subject/assurance and authorised resource, asset ID + revision + digest, operation/correlation/idempotency IDs, relevant policy/version/effective time, storage/provider provenance, audience/visibility, completion state and redacted safety evidence. Private storage keys and ephemeral grants are not normal published asset descriptors. Consumers must handle missing, unknown, stale, revoked and partial results without inventing approval.

### Cross-capability relationship register

| Cooperating capability | Media needs / supplies | Dependency and ownership |
|---|---|---|
| Storage | Need scoped bytes, staging, variants, revoke/delete, backup, usage; supply object lifecycle intent and binding | **Required** Files port, provider supplied by host; Storage owns bytes, Media owns asset records |
| Identity, Authentication, Authorisation | Need trustworthy group/subject/assurance and access decision; supply target resource/action | **Required** protected-operation access; no direct private IAM imports |
| Publisher | Need authoritative backlink/use/publication-context facts; supply eligible, audience-scoped asset resolution and revocation | **Conditional** integration; Publisher owns documents, Media owns images; avoid mutual package dependency via host-composed public ports |
| Content Editor, Gallery, Course | Supply picker, variants, alt, credit, status, protected delivery; receive use context where authorised | **Optional consumers**; no data transfer of asset authority |
| Content Security | Supply bounded authorised digest/scan handle; receive revision-bound detection | **Conditional required safety gate** for regulated exposure; no security bypass on absence |
| Moderation (proposed) | Receive case outcome/enforcement request; supply enactment receipts and state | **Conditional** provisional; Media not case owner |
| Privacy, Legal Compliance | Need applicable consent, rights, hold, retention/erasure constraints; supply minimal asset state and erasure evidence | **Conditional policy constraints**, independent of discretionary authorisation |
| Configuration, entitlements, billing | Need approved scopes and limits; supply usage; Media enforces, billing owns payments | **Optional/conditional**, conservative default/manual fallback; no subscription ownership |
| Audit, Logging, Observability | Supply minimal accountable events and separate diagnostic/health signals | **Conditional/optional integrations**; Audit authoritative receipts, Logging not evidence owner |
| Message Queue, Scheduler, Workflow | Relay Media outbox, execute maintenance, optional human review process | **Optional infrastructure/process ports**; Media owns state and handlers |
| Search, Federation, Reporting, Notifications | Supply eligible metadata/revocation changes and permitted aggregates; no source ownership | **Optional subscribers**; must retract on hold/removal |
| Profile, Localisation, Metadata, Theme Manager and UI | Resolve authorised uploader display name; translate UI, optional taxonomy; theme/accessibility for screens | **Optional presentation enrichments**; do not duplicate personal data or taxonomy authority |

Contract dependency direction must be declared, service orchestration through host-supplied ports, and any dependency/extension graph jointly acyclic under ADR-0016. Conditional cooperation does not mandate a compile-time package dependency.

### Security, privacy, legality and operational controls

Adopt OWASP ASVS 5 L2 baseline (L3 for critical admin/erasure paths), server enforcement, tenant/group/object isolation, no-public-by-default ingestion, origin/bucket segregation, strict MIME/content sniffing, decompression protection, image parser isolation, EXIF/GPS stripping, malware/content scanning, quotas, abuse/rate limiting, anti-CSRF for browser commands, expiry-bound grants, SSRF defence for any remote import, caching/CDN purge and audit of privileged original downloads. Protect child and other sensitive imagery: uploader attestations are not substitutes for lawfully assessed rights, data protection or safety controls. Use UK GDPR/Online Safety Act analysis where applicable, with Legal Compliance qualification; exact service obligations require jurisdictional verification. Avoid universal scanning of private E2EE content as an unexamined default. Keep provider region, processor agreements, keys and retention explicit; no hidden third-party transfer. On failure or ambiguity, do not expose bytes. Backups require erasure replay and measured restoration evidence.

### Conceptual GUI and headless host integration

**Optional separable presentation; full headless API must remain usable.** Host-owned sidebar Capabilities → Media dashboard and contextual picker in Content Editor/Gallery. Suggested screens: group asset library (search/filter, status, usage/allowance); upload wizard (rights, consent and metadata, progress, scan/processing); asset details (alt/decorative, credit, variants, provenance, backlinks, revision history); restricted original download; archive/delete with in-use/hold reasons; report/hold review queue for authorised operators; allowance/configuration view. Display explicit pending/quarantined/removed/unknown states and meaningful denial/remediation; no publish button for held material. Role-reduced simple uploader/picker vs supervisor/admin review, mobile responsive and low-training. WCAG 2.2 AA, keyboard/screen-reader, en-GB/i18n, localised dates via Clock, Theme Manager semantic tokens and no reliance on colour alone. Host controls routing, navigation, branding and permissions. `presentation: false` disables screens without disabling server-authorised operations; do not prescribe an automatic menu-registration contract.

### Conceptual acceptance scenarios (not executed)

| Input | Expected behaviour and output | Authority |
|---|---|---|
| Valid authorised image, within cap, required attestation | Staged upload then claimed/processed; only digest-bound safe ready variant resolves | Media + Storage; Content Security verdict where applicable |
| User forges another group ID or has no decision | No staging, read, rendition or original; stable forbidden, no asset existence leak | IAM decision + Media |
| Wrong MIME, >pixel limit, corrupt parser or quota exceeded | Refuse or hold; no publicly retrievable original/variant; cleanup/reconciliation | Media + Storage |
| Duplicate claim / lost processing callback | Idempotent same operation outcome; no duplicate charge, event or asset; unknown until reconciled | Media |
| Publisher references image; deletion attempted | In-use refusal with permitted backlink summary; archives do not break extant valid references | Publisher backlinks + Media |
| Member-only Gallery image | Audience-scoped grant only after server decision; public or cached URLs cannot bypass membership | Media + Authorisation |
| Safety verdict stale or scanner unavailable | Remains inaccessible pending/held; does not become ready through timeout | Content Security + Media |
| Moderation takedown, mandatory erasure or legal hold | Correct priority and revocation; minimal tombstone, private evidence, purge/restore replay | Media, policy owner, Moderation where adopted |
| Original entitlement expires | New intake/original privilege denied as configured; existing bytes not silently destroyed | Media + entitlements |
| Storage outage, restore or CDN lag | Explicit unavailable/partial purge state, idempotent retries, no false completed declaration | Storage + Media |
| Unsupported video/PDF upload | `unsupported-operation` or validation refusal, not implicit scope expansion | Media |

### Decision and delivery register

- **MEDIA-01 — Open owner decision:** Confirm image-only v1 scope versus a staged wider media-type charter. **Recommendation:** retain images only in this review; defer video/audio/files to separate evidence-based expansion.
- **MEDIA-02 — Open owner decision:** Confirm immutable rendition/version scheme and policy for replacing bytes versus creating a new asset. **Recommendation:** new immutable content revision/digest, re-scan and explicit cache invalidation; preserve audit history.
- **MEDIA-03 — Open owner decision:** Confirm visibility and safety release policy where scanner/moderation is unavailable. **Recommendation:** fail closed for public/member delivery until required gates pass; permit strictly controlled operator quarantine inspection.
- **MEDIA-04 — Open owner decision:** Confirm retained original eligibility, access/step-up, quota charging and private serving; **recommend** existing opt-in entitlement and strictly scoped original-download permission.
- **MEDIA-05 — Open owner decision:** Confirm public upload/report and child-image declarations against applicable legal advice and Content Security/Moderation interfaces; **recommend** records of assertions plus proportionate qualified independent controls, not a compliance claim.
- **MEDIA-06 — Open owner decision:** Confirm backlink deletion block versus mandatory erasure/removal priority and tombstone semantics; **recommend** fail-closed in-use voluntary deletion, immediate revocation for lawful mandatory takedown, controlled minimal tombstones.
- **MEDIA-07 — Open owner decision:** Confirm usage accounting, manual fallback and limit-update semantics; **recommend** conservative entitlement limits and no automatic deletion upon downgrade.
- **MEDIA-08 — Open owner decision:** Confirm conditional dependency model and owner of content report queue during transition to Moderation; **recommend** temporary Media report intake only if explicitly required, with future case ownership under Moderation and no duplicate authoritative case record.
- **Technical investigations:** publish an actual root `CONTRACT.md`; verify Storage's root published port and Publisher's optional resolver adapter; reconcile exact configuration, stable errors, digest-bound safety verdict, quota reservation, signed delivery/revocation and cross-capability reference/backlink contracts, including portability/backup tests and operational status.
- **Acceptance still required:** owner conceptual sign-off; public contract/API review; privacy/legal assessment; independent CI security, lifecycle, outage and minimal-host tests; application GUI tests. No runtime behaviour is claimed proven, and the PR remains draft.
