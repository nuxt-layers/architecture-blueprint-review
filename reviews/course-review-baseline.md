# Course conceptual review — opening baseline

**Status:** In progress; non-normative proposal, not approved.

- Target: `docs/capabilities/course/capability-record.md` (existing directory `course`).
- Review branch: `review/course-conceptual`.
- Governing `nuxt-layers/architecture-rules` master: `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`.
- Blueprint `nuxt-layers/architecture-blueprint-review` master: `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`.
- Protocol: `docs/review-protocol.md` at opening blueprint baseline.
- Target record presently an unfilled pro-forma; substantive ownership, interfaces and GUI remain to be reviewed.
- Initial PR search: no open PR matching `course`.

## Planned scope

Establish precise Course classification, native behaviour, authoritative course records and lifecycle, input/output public contracts, cross-capability boundaries and reciprocal notes, security and privacy, administrator/learner GUIs, acceptance scenarios, and open owner decisions. Validate consistency against current master before any future merge. No implementation changes, local testing or merge are authorised.


## Technical and architectural consistency checkpoint — 17 November 2026

**Compared with live master after substantive edits:** governing `architecture-rules/master` remains `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint `master` remains `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299`. `master...review/course-conceptual` comparison reports **ahead 22, behind 0**, with all changes confined to this branch. PR #56 is draft/open, **GitHub reported mergeable=false** at the checkpoint, so merging is not ready regardless of Git branch ancestry. The combined commit-status endpoint returned no statuses; this is **not** evidence of passing branch checks or CI. No tests/builds have been run.

**Document scope:** one substantive Course record, this baseline/checkpoint and additive notes in 20 related capability records; no implementation or governing repository files edited. Links use same-directory relative capability paths; `course`, `enrolment`, `training`, `content_editor`, `content_security`, `legal_compliance` are literal, verified directories. Catalogue/register already identify Course as Domain candidate and Enrolment/Training separately, so no classification promotion is made. No decision status is represented as approved.

**Architectural boundary challenge:** Course owns outcome **definitions** and frozen course revisions; Enrolment owns learner admissions and allocation; Training owns verified achievement/completion; Publisher owns learning-material documents; IAM retains identities and access. Course's downstream event subscribers are not reciprocal code imports; no required capability import cycle was introduced. Security/privacy/provider/GUI and error/unknown semantics are proposals rather than runtime claims. No Course implementation repository was found; actual CONTRACT.md and acceptance evidence are unavailable.

**Concurrent integration risks:** PR #53 Configuration, #54 Content Editor, #55 Content Security overlap reciprocal documents and remain **unmerged/provisional** at this checkpoint. Review their latest patches before integrating; reconcile additive notes without discarding other reviews, and repeat current-master checks if any base advances. There may be other publication, legal and training proposals not yet reconciled. Course's assessment/cohort/accreditation authority choices (COURSE-08–11) require owner discussion and/or future adjacent reviews.

**Outstanding pre-merge blockers:** GitHub mergeability currently reported false; protected branch/required checks not verified; no explicit owner conceptual approval or merge authorisation. Re-run technical conflict analysis, normative ADR and architectural consistency against fresh master immediately before any authorised squash merge. No merge attempted.


## Follow-up decision and current-master checkpoint — 17 November 2026 (late)

**Owner actions:** COURSE-08 approved three distinct responsibilities and expressly created Assessment candidate; COURSE-09 agreed Course/Enrolment/Events/Booking/Training boundary; COURSE-10 agreed separation of accreditation, individual achievement and legally authoritative formal awards, while the Credentials candidate was expressly requested later in this conversation; COURSE-11 approved independent course approval, safeguarding, retention and version migration principles. Course record has owner-agreed boundaries; other candidate designs/implementation remain provisional. `docs/capabilities/assessment/capability-record.md` and `docs/capabilities/credentials/capability-record.md` created as future-review pro-formas. Catalogue/register updated only to mark them candidates. Reciprocal notes and links added on the same original draft PR #56.

**External issuer distinction:** Accreditor owns recognition; authorised awarding body or evidenced scoped/time-bounded delegate owns formal award decision; Assessment owns results; Training owns verified achievements; Credentials owns representation/verification lifecycle, **not** original award decision. Provider-specific connectors belong to Integrations; an IAM permission is not external legal awarding power. Open dedicated Credentials review question: whether internal award decisions warrant a separate `qualification` or `awards` authority or can be legally and coherently represented within an explicit issuer-supplied contract.

**Fresh verification:** `architecture-rules/master` remains `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; `architecture-blueprint-review/master` advanced from opening `41ce9f3ffba9063407a6af0d0672dcbbd6a8b299` to `95c00d168c24af1767d0cc9c3c975925c97f72db`. Git compare now reports **ahead 46, behind 6, status diverged** for `master...review/course-conceptual`, and PR reports **mergeable=false**. Some touched documents overlap other concurrent reviews; resolve Git and conceptual conflicts together after inspecting the intervening master changes and provisional reviews. No claim of current merge readiness, CI success, or completed test coverage. No merge authorised or attempted.


## Owner approval of COURSE-12 — Qualification (18 November 2026)

**Scope:** The owner confirmed all five proposed Qualification responsibilities essential and explicitly approved creation of a distinct `qualification` Domain candidate. New [Qualification pro-forma](../docs/capabilities/qualification/capability-record.md) establishes qualification-definition/versions, multi-pathway evidence and credit equivalence, issuer/approved-centre/delegation governance with external provenance, authoritative award decisions, and appeals/withdrawal/teach-out. Credential issuance and technical credential status remain in Credentials; Course, Assessment, Training, Enrolment and IAM retain their domain boundaries. A separate generic awarding capability is not introduced. The full independent Qualification conceptual review and public contract still require future work.

**Changed files:** New Qualification record; candidate entries in blueprint catalogue/register; Course decision confirmation; bounded owner-approved reciprocal notes in Assessment, Training, Credentials, Integrations, Verification, Authorisation, Legal Compliance, Workflow, Audit and Privacy. Existing content retained; no implementation or governing repo modifications, local tests or CI execution by assistant.

**Live baseline check:** governing `architecture-rules/master` `2b5c0628e88b9698c9ad6ad57cc5315c8f879953`; blueprint `master` `95c00d168c24af1767d0cc9c3c975925c97f72db` (six commits newer than course branch's starting base). PR #56 remains open/draft and GitHub reported **mergeable=false**. Branch compare immediately before this checkpoint: ahead 62, behind 6. **Not merge-ready:** reconcile concurrent changes and recheck current governing authority, conflicts, checks, links, and reciprocal ownership before user-authorised squash merge. No merge attempted.
