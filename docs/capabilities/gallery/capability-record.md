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

**Derived visual presentation:** Gallery may show Publisher/Media content only when source-publication and asset-delivery policies permit it. A source quarantine or takedown must affect galleries, thumbnails, variants and caches; Gallery owns no source moderation case or raw content. The host should show appropriately minimal removal notices rather than exposing harmful imagery or restricted case details.


## Dedicated conceptual review — Gallery (18 November 2026)

**Status:** Proposed contract reconciliation for owner approval; presentation classification is **established** by governing catalogue. Existing Gallery design was recorded as agreed with the owner on 25 October 2026; that earlier agreement is not proof of an implemented API. This review is non-normative. [Opening evidence](../../../reviews/gallery-review-baseline.md); [draft PR #70](https://github.com/nuxt-layers/architecture-blueprint-review/pull/70).

### Evidence, identity and classification

- Governing `nuxt-layers/architecture-rules` opening `master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`; blueprint `master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`. Accepted ADR-0001, 0009, 0012, 0016 and 0017/0018 and normative Architecture, Capability Standard, Security, Privacy, Presentation apply.
- Working and governing catalogues classify `gallery` **Presentation**: albums and photo of the week as Publisher types over Media images; **no data of its own**. This is an established boundary, not a proposed new domain.
- Actual implementation repository `nuxt-layers/gallery`, `master@8751fc168b7a7104442f52e9a25e6e796dbddf2e`: README says nothing is built; `docs/design.md` describes previously owner-agreed intended design. No root `CONTRACT.md` available. **Available / installed / configured / operational / enabled / authorised / released and consumer acceptance: unverified, not asserted.**
- Publisher root `CONTRACT.md` inspected on master: genuine published document lifecycle, type declaration, asset resolver, queries, version-conditioned transitions and outbox; no Publisher screens. `nuxt-layers/media` root `CONTRACT.md` not retrievable: Media capabilities and private-serving behaviour remain conceptual until verified.
- Concurrent Export, Federation, Events and Event Bus PRs #68, #69, #67 and #66 respectively are provisional; no conflicting ownership is adopted from them.

### Purpose, authoritative ownership and exclusions

Gallery presents and composes discoverable albums, individual image views, an authorised group-member submission experience and featured photos. Its purpose justifies reusable *screens and Publisher type declarations*, **not a second persistent album, photo, approval, safety, access-control or publication service**.

| Concern | Authority and limits |
|---|---|
| Album, members-only album, featured-photo record; order, caption, description, cover, credits, publication, revision, scheduling, addresses, moderation and removal | **Publisher** as host-registered document types, using type-specific validated fields; Publisher alone commits revisions/transitions |
| Asset identity, derivative variants, alt metadata, uploader association, upload, access eligibility, quarantine and original-download entitlement | **Media**, with Storage operating bytes through the host-provided port |
| Site, tenant, group, personal group, verified membership | **Identity/site host** as applicable; Gallery neither defines group membership nor grants identity |
| Caller assurance, permission, audience access | **Authentication/Authorisation and source owners**, enforced server-side; a gallery display flag is not authority |
| Safety detection, reports/appeals and enforcement | **Content Security**, proposed **Moderation** case lifecycle, with Media/Publisher performing their own holds/withdrawals |
| Gallery grid, album page, accessible lightbox, photo-of-week and optional submission UI | **Gallery presentation**; ephemeral UI state only, no authoritative persistent resource |
| Generic editorial forms, approval/review queue and Publisher document lifecycle dashboard | **Content Editor**, not duplicate Gallery administration |
| Search ranking, syndication, notifications, reporting/audit and delivery | Their respective owners; Gallery may offer public links/projections only via source contracts |

Historical `docs/design.md` defines types `album` (public), `members-album` (private, not in public feeds), and `featured-photo` (scheduled). **Proposed reconciliation:** preserve these display concepts, but verify supported Publisher type definitions, private access semantics and dedicated submission/review workflow rather than assume the old design's `publisher.<type>.moderate` permission or member-submission API exists. Publisher's published permission catalogue currently lists `view-draft`, `edit`, `publish`, `delete` only. A displayed image is independently access-checked by Media, including private variants and originals. No automatic public publication on upload.

### Native behaviour and lifecycle — presentation only

**Native when composed:** resolve configured Publisher document type and site context; fetch authorised published/preview listing and individual records; resolve each image against Media's current visibility and variants; render ordered accessible thumbnails/lightbox/featured content; route create/edit/review to Content Editor; provide a submission form only after source-owned submission contract is available. A presentation-only package can operate without Gallery state, database, message relay or scheduled jobs. The host may disable screens while Publisher and Media remain independently usable.

**Source-owned lifecycle:** proposed album draft → reviewed/approved where configured → published/scheduled → revised/withdrawn/archived/removed; images independently uploaded → held/processed/eligible → restricted/removed/restored. Gallery consumes these states, never owns transitions. A failed asset check yields omission/redaction with safe explanation, **not** an unsafe fallback to original. After a revocation or removal, stale page/cache/lightbox access must be suppressed at the owner delivery boundary; Gallery also refreshes its view.

**Absence:** no Publisher means no authoritative album records; no Media means no images or submission. Gallery should display controlled unavailable/empty states, never fabricate content. Search, Federation, Notifications, Reporting and Gallery-specific presentation are optional. Pending/unknown safety or access status fails closed.

### Idealised public inbound contract (presentation consumer)

| Public input / origin | Meaning, requiredness and validation |
|---|---|
| Host site, tenant, group/audience and routing configuration | Required trusted server-resolved scope; validate registered type/site and permitted route. Client-supplied scope never grants access |
| Publisher public document-type metadata, published listing/document, preview/admin queries, publication revisions, address/withdrawal changes | Required; Publisher is sole source of record/order/caption/featured period and publication eligibility. Missing, invalid, stale or withdrawn documents are not presented as live |
| Media public asset identifiers, authorised rendition/picker metadata, alt/caption provenance, delivery and current eligibility, original-download decision | Required to display/submit images; Media owns actual delivery and media policy. Missing, quarantined, forbidden, expired or unknown result does not expose bytes |
| Authenticated caller/assurance and Authorisation access decisions; Identity membership | Conditional for protected/member views, submission, admin actions and original downloads; verified on server and source action, not inferred from UI |
| Publisher create/save/transition public commands, Content Editor registry and submission/moderation intake | Conditional for editorial/submission flows; require validated type, revision preconditions, rights/consent and authorised actor. Do not claim legacy moderation endpoint is available |
| Source-owned Content Security/Moderation hold/reinstatement, Policy/Legal/Privacy disposition | Conditional whenever safety/legal duties apply; Gallery reads source-enforced availability, never adjudicates from a detector score |
| Configuration/Profile and Theme Manager semantic tokens, locale/Clock format, optional Search/SEO/Notifications | Optional or host-provided, subject to authorisation, privacy, provenance, missing preference defaults and publication eligibility |

All results must distinguish unknown, unavailable, unauthorised, stale, conflicting and unsupported values. Never treat an event payload or search index as permission to expose a record.

### Idealised public outbound contract

| Output / consumer | Promise and authority limit |
|---|---|
| `GalleryPresentation`: album list/grid, album detail, lightbox and featured-photo slots; host application | Accessible semantic UI driven by Publisher and Media; layout/navigation state and visibility of buttons **not** domain facts |
| `GalleryTypeDeclarations`: public, members-only and featured-photo type descriptors; host → Publisher composition | Proposed declarative schemas/field constraints and display adapters; registration and persistence occur **inside Publisher**. No extra Gallery database |
| `GallerySubmissionIntent`: image plus requested album, caption, rights/consent declarations; host → trusted intake → Media/Publisher | UI request only; accepted/queued/rejected/uncertain outcome must be returned by the authoritative receiver; **no committed Gallery submission event** |
| `GalleryEditorialIntent`: links to Content Editor and version-conditioned Publisher commands | Not an independent Gallery command API; actual confirmation, denial, conflict and auditability come from Publisher and relevant workflow |
| `GalleryViewResult`: authorised display status/empty/withheld/unavailable, image references, revision/freshness; host/assistive UI | Derived read model only; no independent guarantee of current media availability beyond source check |
| Shareable page metadata and safe links; SEO/Search/host | Derived from actually published, authorised source addresses and eligible media; no indexation or feed of protected member content |

**Commands / queries / events:** Gallery has *no independent domain commands, persistent authoritative queries or committed domain events*. Its view queries call Publisher and Media public contracts. User actions invoke those owners through host-wired ports. Publisher/Media committed outbox events drive invalidation, with at-least-once duplicate/out-of-order delivery, revision reconciliation and no exactly-once promise. Presentation telemetry must not be misrepresented as a domain event. Correlation/idempotency keys and expected Publisher revision belong on forwarded owner commands. Do not mandate a universal request object.

### Cross-capability relationship and absence matrix

| Peer | Information Gallery receives → supplies | Dependency and failure boundary |
|---|---|---|
| Publisher | Validated type schemas, document records, lifecycle and published addresses → presentation type declaration and authorised user intent | Essential for albums; direct contract port via host, not internal Publisher imports |
| Media / Storage | Safe current thumbnails, renditions, uploader metadata and download eligibility → asset references and authorised upload/picker intent | Media essential; Storage indirect through Media; no direct Storage capability import |
| Content Editor | Editor form/queue and authorised lifecycle UI → type-specific ordered image field and edit/deep links | Optional administration; Publisher still works headless |
| Identity, Authentication, Authorisation | Trusted context, membership, scopes/assurance and access decisions → target-specific request/action context via public ports | Conditional; protected access fails closed |
| Content Security, Moderation, Privacy, Legal Compliance | Source-owned restrictions, applicable obligations and notices → safe report and review entry points; source-owned removal updates | Conditional by content/risk; no Gallery case/safety authority |
| Configuration, Profile, Theme Manager, Clock, Localisation | Permitted display settings, safe attribution, semantic theme, locale/date formatting → contextual rendering | Optional presentation integration; minimise personal data |
| Search, SEO, Federation, Caching | Authorised source-derived discovery and invalidation → safe published links and version references | Optional; no Gallery indexing, publication or external federation authority |
| Audit, Logging, Observability, Reporting | Audit consumes Publisher/Media authoritative actions; operational logs/metrics reflect Gallery failures; reports use source records | No competing Gallery audit ledger; log opaque identifiers only |
| Scheduler, Workflow, Message Queue, Notification | Scheduled publication, approval, transport, notification via **source owners** → status presented when authorised | No direct Gallery job/queue ownership; an absent optional provider must not imply completion |

**Acyclicity:** Gallery is a leaf presentation consumer. Publisher and Media do not import Gallery; Publisher does not import Media internals (the host supplies the asset resolver). Cross-domain source events are delivered through interfaces and host composition. Viewer-level use of optional capabilities does not mandate package dependencies.

### GUI and host presentation

In `nuxt-layers-test/application-test-template`'s established shell, a host sidebar **Gallery** entry leads to a dashboard for authorised users, with album listing, private/public access indication, featured-photo preview and contextual action links. The host owns sidebar entry, routes and installation selection. Proposed screens: album index (filters/empty/withheld states), album detail with thumbnail grid, accessible lightbox with controls and conditional original download, featured-photo block, member upload/submission form and submit/status view where intake exists. Administration uses Content Editor's existing Publisher document forms/queue, with a custom ordered-media picker field; **no duplicate Gallery moderation dashboard**. Public pages may be host-mounted outside the admin shell. Optional presentation can be disabled; headless Publisher/Media stay operational.

Follow Theme Manager tokens, WCAG 2.2 AA (keyboard, dialog focus management/return, Escape, meaningful alt/figcaption, reduced motion, responsive grid, loading/errors), BCP 47/CLDR/ECMA-402 and safe semantic/schema.org metadata only for genuinely public resources. No hidden membership or consent information in URLs, titles, public previews, feeds or snippets. Admin pages no-store/no framing/no Referer. Lazy-load safe variants but do not rely on cache as an access decision.

### Provider, security, legal and privacy boundaries

No Gallery-specific external provider or store is essential. Hosting/image delivery, byte storage and processing are selected through Media/Storage/public host adapters; optional CDN, search and federation remain replaceable. Rights to upload and display, creator attribution, consent where required, copyright, UK GDPR and UK Online Safety Act applicability must be evaluated by the relevant owners and qualified policy inputs; the old design's blanket legal assertion does not constitute a compliance determination. Public galleries containing user-generated content need enforceable reporting, hold, takedown, appeal and restoration paths with clear source receipts. Scan/assessment unavailable or stale → **no unsafe public exposure**. Member-only images must not leak through direct URLs, responsive variants, image proxies, metadata, prefetch, CDN or search indexing. Signed URLs, if used, are owner-authorised and short-lived under governing Security controls. Do not emit raw originals without a fresh Media entitlement check.

Gallery holds no personal profile copies, uploaded image bytes, source audit records or durable gallery metadata; any future client-side preferences/cache/telemetry require storage-register and consent classification by the drawing implementation. Retention/export/erasure are performed by Publisher/Media and relevant owners. Privileged changes require appropriate assurance and Audit evidence from actual source operations; Logging captures technical failures without sensitive content.

### Conceptual acceptance cases (not executed)

| Input / situation | Required result and authority |
|---|---|
| Published album with eligible images | Correct ordered, accessible grid and safe variants sourced from Publisher + Media |
| Published album references newly quarantined image | Image blocked/removed across thumbnail, lightbox and caches; Media enforces byte denial; Publisher may withdraw album under applicable policy |
| Member requests member-only album | Verified site/group/member scope and server authorisation; hidden/not-found semantics for unauthorised viewers; Publisher/Media own eligibility |
| Authorised editor saves reordered album with current revision | Validated Publisher save and new document version; stale revision returns conflict, never overwrites |
| Member submits new photo | Media checks upload, rights and safety; authorised intake acknowledges pending/accepted/rejected/uncertain; no automatic album inclusion or assumed moderation API |
| Personal account publishes an album | Publisher validates publishing rights and lifecycle; Media checks media exposure; no silent bypass for self-publish |
| Image original download requested | Fresh Media-specific entitlement decision; forbidden original never substituted with a direct Storage URL |
| Duplicate/out-of-order withdrawal event | Read authoritative owner revisions and invalidate safe presentation; do not restore withdrawn content from stale event |
| Source timeout or unavailable Media/Publisher | Withheld/temporarily unavailable result, no leaked image data, explicit recovery/retry through owners |
| Cross-tenant query or forged client scope | Server-side refusal, no existence metadata leak, Audit where security-relevant |
| Album deletion, image erasure or expired consent | Source lifecycle and caches reconciled, no stale publication; lawful preservation handled by source owners |
| Gallery screen disabled or unsupported legacy moderation action | Publisher/Media remain operational; unsupported action is not invented or treated as successful |

### Decision and gap register

- **GAL-01 — Established:** Gallery remains presentation-only. No independent persistent album, featured-photo, moderation, event or document authority.
- **GAL-02 — Previously owner-agreed design (25 Oct), contract alignment proposed:** `album`, `members-album`, `featured-photo` are Publisher-registered types with Media asset references. Validate actual schema support before delivery.
- **GAL-03 — Proposed:** Use Published Publisher/Media contracts and host ports; Gallery's public contract exposes UI/type contributions, not a competing domain service.
- **GAL-04 — Proposed:** Restricted and public audiences are distinct publication/access paths; private assets require Media's independently enforced private delivery, no bypass by UI or URL.
- **GAL-05 — Proposed:** Submission/acceptance/rejection are owner-operated through explicit intake and approval/review contracts. Publisher's present root contract does not document `moderate`; reconcile the historical Gallery design before implementing.
- **GAL-06 — Proposed:** Source hold/withdrawal/revocation has precedence across variants, caches and all gallery presentations; uncertain access fails closed.
- **GAL-07 — Proposed:** Gallery screens are optional; Content Editor owns editorial workflow, and the host owns navigation. Respect accessibility/i18n/theme rules.
- **GAL-08 — Proposed:** No Gallery-specific business events, database, queue, scheduler, storage or independent legal compliance state.
- **GAL-09 — Open technical/contract investigation:** Verify Media's root contract and its private-image/variant/original entitlement surfaces; confirm Publisher's type-field extensibility and actual private document delivery; design a genuine member-submission / review path within source ownership.
- **GAL-10 — Open owner decision:** Should member contributions be included in v1 before an independently published intake/review contract exists, or should the initial release provide safe browsing and owner-editor publication only? Recommendation: **do not ship an implicit submission pathway**; make submission conditional until that contract is established.
- **GAL-11 — Acceptance gap:** No Gallery root `CONTRACT.md`, implementation, minimal host, WCAG/security/tenant/cross-capability acceptance, storage declaration or operational evidence verified. Preserve intended design but treat release/readiness as unproven.

**Conceptual sign-off:** Owner approved earlier proposed recommendations on 18 November 2026, including GAL-03–08 and the recommendation to make member submissions conditional until Publisher/Media intake and review contracts are verified (GAL-10). GAL-09 remains a technical verification gap; conceptual approval does not validate an implementation or resolve an absent source contract. Technical/integration alignment to actual root contracts and pre-merge reconciliation remain required. Do not amend governing rules, implementation repositories or merge without explicit approval.


## Follow-up review — published interfaces, supporting standards, GUI and permissive libraries (18 November 2026)

**Review status:** Owner approved the previous recommendations in this conversation. This section elaborates the conceptual contract, not a published Gallery root `CONTRACT.md` or evidence of a working package. Do not treat these candidate tools as mandatory packages. Governing `architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2` was rechecked; blueprint `master` had advanced to `258bb58e9b64987d1c6bd3e44716c6d3412726c0` at follow-up, and requires PR reconciliation before any later merge.

### Exact public contract distinction and host wiring

**Published and actually established elsewhere:** Publisher root `CONTRACT.md` exposes host-registered document types via `definePublisherDocumentType`, `composePublisher`, authorised `getPublishedDocument`, `listPublishedDocuments`, `getPublisherDocument`, `listPublisherDocuments`, version-conditioned `transitionPublisherDocument`, `createPublisherDocument`, history/backlinks, `assets.resolve` host port and publisher-owned identifiers/events. Its published type permissions are `view-draft`, `edit`, `publish`, `delete`. Publisher is headless; it does not supply Gallery screens. Gallery root `CONTRACT.md` is **absent** as checked. Media root `CONTRACT.md` was **not retrievable**; do not invent method names.

**Proposed Gallery public exports (names illustrative, not available API):**
1. `galleryPublisherTypes`: declarations for `album`, `members-album`, `featured-photo` for host registration with Publisher; never directly writes album data.
2. `GalleryDashboard`, `AlbumIndex`, `AlbumDetail`, `GalleryLightbox`, `FeaturedPhoto`: presentation components consuming host-wired authorised Publisher reads and Media safe rendition/eligibility results; publish no business outcome.
3. `GalleryAlbumField`: ordered media picker and captions for Content Editor's Publisher schema-driven forms; forward saves to Publisher under expected revision.
4. `GallerySubmitPhoto` and `SubmissionStatus` **conditional** on a real, source-owned intake contract. UI returns the source's pending/accepted/rejected/uncertain result; does not create `gallery.submitted` business events.
5. `galleryPresentationOptions`: host-controlled permitted feature visibility, routes, locale/labels, navigation context, Theme Manager tokens, download policy **display only**; cannot override source permissions.
6. Optional display callbacks for safe navigation and technical diagnostics; **no public Gallery data-store service, independent domain command/query/event, invented network endpoint or proprietary provider SDK**.

**Contract obligations:** A future root `CONTRACT.md` should enumerate actual imports, host ports, callable signatures and error codes, headless states and screens, permissions/absence modes, composition example within ADR-0012's ≤50-line host integration budget, accessibility, storage register/no-state declaration and independent consumer acceptance. Type registration must be host-coordinated rather than having Gallery import Publisher internals. Source version, tenant/site, audience and denied/unknown/unavailable states must be passed explicitly through the host's public adapters; never expose protected content because a UI control is visible.

### Logging, Audit and Reporting as contract consumers

| Capability | Input originating in Gallery or its cooperating owners | Its public result back / precise boundary |
|---|---|---|
| **Logging** | Optional structured *technical* signals: gallery rendering failure, image resolution timeout, unavailable external port, correlation ID, component/action code and severity; no bytes, bearer URLs, personal captions, search terms or private identifiers | Diagnostic record/acknowledgement and operational fault visibility; logging does **not** certify an upload, permission check, publication or audit evidence. Browser diagnostics must pass a trusted, privacy-limited host adapter, not send privileged records directly |
| **Audit** | Primarily **Publisher/Media authoritative** events: verified creation, publication, withdrawal, deletion, rights/permission-sensitive decisions and actual delivery-policy changes, with minimised source provenance, actor, outcome, correlation and revisions. A presentation-only Gallery operation is not itself an authoritative source change | Audit intake receipt, evidence/integrity and authorised audit history; the receipt is not the domain's business confirmation. Gallery may show an authorised owner-provided status, but neither reowns evidence nor sends duplicate success records. Where applicable, an independently meaningful sensitive presentation access attempt may be logged/audited by the security boundary |
| **Reporting** | Publisher/Media approved, versioned album, asset, publication and rights-constrained views and lifecycle facts; optionally Gallery aggregate presentation interaction counts **only if purpose and privacy/consent were assessed** | Authorised report, aggregation, freshness/coverage and error/unknown state. Published album count does not depend on Gallery's runtime; viewer telemetry is not authoritative proof of readership, a unique person or consent |

No mandatory Gallery runtime dependency on these three capabilities. Their provider implementations and event subscriptions are host composed; detailed reciprocal amendments should occur in those capabilities' dedicated reviews so their independent ownership remains clear.

### Established standards and how they apply

| Standard / guidance | Reuse instead of reinventing |
|---|---|
| **WCAG 2.2 AA and WAI-ARIA Authoring Practices** | Accessible gallery grid, keyboard-operable lightbox/modal, predictable focus and return, Escape, screen reader alt/caption, reduced motion and controls for any automatic carousel |
| **HTML Living Standard responsive media** (`picture`, `srcset`, `sizes`, lazy loading) | Browser-native responsive images, safe alternative text, download and performance behaviour; Media supplies authorised rendition sets |
| **BCP 47, Unicode CLDR and ECMA-402** | Locale, language direction and dates of featured-photo periods; don't bake UK text/date formats into business data |
| **Schema.org `ImageGallery`, `ImageObject`, `CollectionPage`** | Truthful structured public album metadata using Publisher/Media sources; never mark member-only albums public |
| **IPTC Photo Metadata / XMP, EXIF** | Image captions, credit/copyright, creator and location provenance handled by Media; avoid copying private location/device metadata into public Gallery outputs |
| **C2PA Content Credentials** (optional) | Portable provenance assertions if a use case warrants it; not evidence that subject consent, copyright licence or safety was established |
| **OWASP ASVS 5.0 L2; NIST and governing Privacy rules; UK GDPR / relevant online safety law** | Server-side audience/asset checks, safe URL/variant delivery, privacy minimisation, moderation source lifecycle and legal applicability without custom Gallery security policy |

Primary references: https://www.w3.org/TR/WCAG22/ ; https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/ ; https://www.w3.org/WAI/tutorials/carousels/ ; https://schema.org/ImageGallery ; https://iptc.org/standards/photo-metadata/iptc-standard/ ; https://spec.c2pa.org/ .

### Open-source library shortlist — permissive licence candidates, not approved dependencies

| Library | Licence and role | Qualification / selection |
|---|---|---|
| [PhotoSwipe](https://github.com/dimsemenov/PhotoSwipe) | **MIT**; framework-independent image lightbox with responsive zoom, gestures and navigation | **Preferred specialist viewer** if its public accessibility behaviour, SSR/client hydration and Nuxt integration are independently verified; wrap behind Gallery's own presentation contract |
| [VueUse](https://github.com/vueuse/vueuse) | **MIT**; Vue composables for responsive and keyboard/pointer interaction | Good optional utility for implementation only, not a domain or provider dependency |
| [Embla Carousel](https://github.com/davidjerleke/embla-carousel) | **MIT**; Vue-compatible carousel/swipe engine | Only if a photo strip or featured carousel is justified; no automatic cycling by default; WCAG controls essential |
| [SortableJS](https://github.com/SortableJS/Sortable), [vue.draggable.next](https://github.com/SortableJS/vue.draggable.next) | **MIT**; reordering albums/images in the editor | Optional for Content Editor's ordered images field; provide keyboard move-up/down alternatives, version-conditioned saves and accessible status |
| [Nuxt UI](https://github.com/nuxt/ui) | **MIT**; reusable Nuxt form/dialog/presentation primitives | Use only if aligned with existing platform `ui` and Theme Manager; do not introduce a second competing design system |

**Avoid:** `lightGallery` for this project's permissive-only dependency policy: GPLv3/commercial dual licensing may be legitimate open-source but is not permissive and proprietary distribution has different conditions. Do not confuse **MIT-licensed library availability** with verified maturity, release/security compatibility or accessibility certification. Inspect each transitive dependency, exact licence, project activity, vulnerability history, platform compatibility and maintenance at implementation selection time. Avoid `yet-another-react-lightbox` for this Vue/Nuxt stack even though MIT-licensed, due to framework mismatch. No vendor service, account, enterprise licence or freemium dependency is needed.

### Host dashboard, routes and GUI ownership

Representative host: `nuxt-layers-test/application-test-template` already provides top bar, home page, `/admin`, responsive sidebar and `/theme-manager`, with Theme Manager in **local-only test mode**. The host adds the **Gallery** sidebar item and chooses actual routes; the following paths are examples, **not implemented endpoints**:

| Entry / route concept | Screen, user and action | Data/decision owner |
|---|---|---|
| Sidebar **Gallery** → `/gallery` or `/admin/gallery` | Dashboard: authorised album tiles, featured image, browse/filter, contribution and admin actions where allowed | Gallery displays; Publisher/Media own data |
| Public album index → `/gallery/albums` | Cards, public metadata, search/filter/pagination, empty/unavailable states | Publisher listing + Media safe covers |
| Album detail → `/gallery/albums/:slug` | Title, credits, ordered responsive grid, captions, share link where public | Publisher publication/address; Media variants |
| Lightbox overlay within album | Focus-managed full-image view, close/next/previous, caption/alt, safe conditional original-download action | Gallery UI; Media authorises delivery |
| Featured-photo widget | Current photo of week, caption and optional album link | Publisher scheduled type + Media image |
| **Contribute photo** → host-configured flow | Upload/picker, rights confirmation, consent/alt/caption, pending/confirmed/failed receipts | Media and source-owned intake; **conditional**, not currently published |
| **Manage albums** → Content Editor | Create/edit album, order images, preview, approval and publication histories | Content Editor UI; Publisher lifecycle |
| Optional **Reports/Moderation** navigation | Case status and report action only via source/Moderation public interface | Moderation case owner; source state owners |

The dashboard must not reimplement Content Editor's full editing or Moderation case queue. Host route mounting and presentation enable/disable are configuration, not a new Gallery router authority. Users lacking permission see no privileged action; the server still checks every submitted operation. Member-only content must not appear in public index, feed, metadata, browser cache or prefetch. Mobile layouts, large image lists, low bandwidth, focus management, image loading/failure, captions, localisation and Theme Manager light/dark/high contrast require explicit conceptual and later CI/assistive technology acceptance.

### Follow-up decision alignment and remaining acceptance gates

- **GAL-12 — Owner direction incorporated (18 Nov 2026):** preserve Gallery as stateless Presentation; show the intended types, public input/output, reciprocal consumer boundaries, and no duplicate Logging/Audit/Reporting facts. Future `CONTRACT.md` remains an implementation deliverable.
- **GAL-13 — Library selection proposed:** PhotoSwipe first; VueUse/Embla/SortableJS or Nuxt UI only where needed, compatible and validated. MIT licences verified on upstream listings; no sole vendor dependency. Licence and security recheck at selection.
- **GAL-14 — GUI design proposed:** one host sidebar Gallery entry/dashboard, accessible public browsing and viewer, featured widget, editor deep-link, optional contribution/status UI. Do not create a duplicate administrative case/workspace.
- **Remaining technical contract gap:** Publisher's documented permissions lack old `moderate`; Media lacks an available independently inspectable root `CONTRACT.md`; private access and source-owned member contribution flows must be proven. No Gallery package/runtime acceptance is asserted.


## Media reciprocal conceptual interface — 19 November 2026 (proposed; PR #92)

**Status:** Provisional Media review, not approved as the gallery public implementation contract. See [Media dedicated conceptual review](../media/capability-record.md#dedicated-conceptual-review--media-19-november-2026).

Gallery is presentation over Publisher types and consumes Media-authorised descriptors, delivery, member-only variants, original-download eligibility and revoked states. Album selection never confers access; Media enforces each object and derivative, including short-lived/cached delivery, and Publisher owns albums/publication. Show accessible alt/credit and clear held/removed placeholders. Original download is separately privileged and never implied by membership alone.
