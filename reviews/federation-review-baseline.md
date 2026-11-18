# Federation — conceptual review baseline

**Date:** 18 November 2026  
**Status:** Work in progress, non-normative; owner approval pending.  
**Target directory:** `docs/capabilities/federation/`  
**Branch:** `review/federation-conceptual`

- Governing `nuxt-layers/architecture-rules` `master`: `0725f314abc9ad13f1a65247f54a7ff80772f0b2`.
- Blueprint `nuxt-layers/architecture-blueprint-review` `master`: `a4e40a5cd82a2f79e8edd872af55c22d472b61cb`.
- Current review protocol: `docs/review-protocol.md`; complete Phase 1 authority review follows.
- Active PRs specifically matching federation at opening: none returned by repository PR search; parallel related reviews may exist.

## Scope

Review Federation's independent justification, Node/Hub roles, source-of-truth and exchange boundaries, opt-in peer lifecycle, protocol neutrality, durable public inbound/outbound contracts, subscriptions, synchronisation and withdrawal, trust, privacy, authorisation, failure and replay, cross-capability reciprocal notes, headless and host GUI composition, acceptance scenarios, and outstanding owner decisions. Review existing Node–Hub architecture and adjacent conceptual records. No implementation edits, local tests, governing changes or merge are authorised.

## Baseline evidence

The working catalogue identifies Federation as a platform capability candidate, Node as a deployment/network participant rather than a capability, and Hub as an application composition/operator role; operational or implementation conformance is not verified. These remain provisional until the dedicated review and owner decision.

## Review disposition and consistency check — 18 November 2026

**Status:** Review documentation completed for owner consideration. No conceptual sign-off, implementation conformance or merge is asserted.

- **Candidate identity:** Existing directory `docs/capabilities/federation/` retained exactly. Node is a participant/deployment role; Hub is a composition/operator role; Federation is a reusable Platform candidate with its own peer/subscription/synchronisation decisions.
- **Public contracts:** The target record now describes all material inbound commands/evidence and outbound receipts/read models/committed events, own-state authority, source-owned origin projections, unknown/invalid/expired/replay outcomes, staleness, privacy controls, headless and UI use, and acceptance input-to-outcome examples.
- **Reciprocal conceptual notes:** Search, Publisher, Identity, Authorisation, Verification, Message Queue, Audit, Logging, Configuration, Moderation, Site Hosting, Integrations and Reporting. Notes are additive, linked to the target and explicitly provisional; no other capability's independent review is deemed complete.
- **Actual implementation evidence:** Publisher, Identity and Authorisation root `CONTRACT.md` were retrievable on master. Federation, Search, Message Queue, Verification and Site Hosting root `CONTRACT.md` were not retrievable at the examined names/locations; this is *not* evidence they are absent everywhere. No runtime Federation adapter was verified.
- **Architecture review:** Source business records never move into Federation; Search owns index state; Message Queue transports but does not own remote exchange; IAM decisions and Verification evidence remain separate; Hub composition cannot re-own source facts. An interchange request is not an authorisation. Direct network communication creates no local package dependency cycle. The core can operate headlessly and off-network.
- **Git check:** Compared draft PR #69 against blueprint master `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` and governing master `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. At this check branch was ahead, GitHub reported mergeable, and there were no deletions. Final checks must be repeated after any concurrent merge.
- **Shared files/concurrency:** Other parallel open capability reviews exist (including Export, Events, Event Bus, Gallery, Gaming and IAM Integration). Reciprocal notes use bounded additions only. Shared files may change independently before merge, so later conflict and semantic reconciliation is mandatory.
- **Documentation limitations:** Catalogue/register already designate Federation a candidate and Node/Hub separate roles; they have not been promoted to accepted governing classification. New review findings are proposals rather than accepted amendments to the working catalogue/register. Relative record links use the exact current directory names. This check did not mechanically validate every Markdown link.
- **Security/privacy:** Host/tenant identity and permissions are locally scoped, source-controlled opt-in is required, peer signatures are non-transitive, unknown delivery remains unknown, and remote fetches have SSRF/replay and abuse threats. These are architectural requirements, not audited controls or legal certification.
- **Implementation and CI:** No implementation repositories modified, no tests/builds run; CI/status checks and protected branch compliance must be verified again immediately before any approved merge.
- **Open owner disposition:** FED-11–FED-18 proposed for approval; FED-19–FED-20 unresolved owner choices alongside existing FED-Q01–FED-Q10. Protocol, trust root, signature profile and concrete staleness bounds are deferred for evidence-based selection. No claim of implemented or legal conformance.
- **Merge gate:** Not approved. Keep this PR as draft until conceptual decisions are explicitly approved; obtain separate explicit owner instruction before any merge.


## Final owner approval and reconciliation — 18 November 2026

**Owner decisions:** FED-11–FED-18 and the recommended approaches to FED-19 and FED-20 are approved conceptually, as captured in the Federation capability record. The owner subsequently explicitly authorised the squash merge subject to technical and architectural checks. FED-Q01–FED-Q10 remain evidence-based protocol/implementation investigations, not blockers to the *conceptual* boundary approval.

**Master reconciliation:** Governing `architecture-rules/master` remained `0725f314abc9ad13f1a65247f54a7ff80772f0b2`. Blueprint master advanced from opening `a4e40a5cd82a2f79e8edd872af55c22d472b61cb` to `258bb58e9b64987d1c6bd3e44716c6d3412726c0`. Feature and master modifications overlapped in Audit, Authorisation, Configuration, Identity, Integrations, Logging, Message Queue, Moderation, Publisher, Reporting and Verification; Search and Site Hosting were unaffected by upstream master. Every overlapping change was checked against original opening content and was additive on both sides; none of Federation's dated reciprocal notes was already present on master. The reconciled tree preserves current master text and Federation's additional notes on all 13 reciprocal paths and preserves the capability record/review baseline. The integration commit `5fab6ffb6f900b8ed197a03fe615632724156edf` includes the latest master as second parent and remains entirely on the initial feature branch; no direct master write or force push.

**Git/document scope after integration:** Git comparison reports 18 commits ahead, 0 behind, exactly 15 intended documentation paths, all additions and no deletions; newest Attendance, Events, Export, event_bus and other separately merged records on master remain intact. No change to architecture-rules or implementation repositories. Federation still owns exchange coordination, not domain source, IAM authority, Search index, Moderation adjudication, or transport infrastructure. Headless/host GUI boundary, privacy, replay, failure/unknown semantics and standard/vendor-neutral choices remain internally consistent.

**CI and merge gate:** Last inspected reconciled SHA `5fab6ffb6f900b8ed197a03fe615632724156edf` had no reported GitHub status contexts and zero check-runs; that does not prove CI passed. Raw GitHub mergeability temporarily returned `unknown` during calculation. Immediately before squash, recheck the final head, current governing and blueprint masters, required rules, CI visibility and GitHub mergeability. No local test/build executed.
