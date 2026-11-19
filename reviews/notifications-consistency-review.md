# Notifications — technical and architectural consistency review (19 November 2026)

**Status:** completed initial pre-merge review, **not** merge approval; repeat if governing/blueprint master or overlapping drafts change.

## Verified baselines and evidence

- Governing `architecture-rules/master`: `b920ce0d8b361de000a6739a16123dbdc56df7a7` at opening and recheck. Accepted ADR-0012, ADR-0017 and ADR-0018 inspected; Capability Standard and governing catalogue classify Notifications as Platform. Governance status is not inferred from normative references alone.
- Blueprint `architecture-blueprint-review/master`: `6dac83a03da8704f7945ee1bc894f2248300445a` at opening and recheck.
- Target implementation `nuxt-layers/notifications` exists; `master` at `89c43c04c86e8eb8a1034394f69da26186a5cbc4`, but root `CONTRACT.md` fetch returned 404. This does **not** prove there is no implementation or interface. No implementation changes/tests or actual behaviour assertions.
- [Draft PR #97](https://github.com/nuxt-layers/architecture-blueprint-review/pull/97) comparison from current `master`: ahead 8, behind 0; eight changed files, additive rather than destructive; head `1656719f381ae62db65268ebb047215d3d180144` at first review. A subsequent commit to this review note will advance the head. GitHub PR was draft, open and marked non-mergeable at check, with no commit statuses returned. Cause not determined; no clean-merge/CI/protection success claimed.

## Technical and architectural challenge

1. **Ownership:** source domains own the event/decision and durable origin outbox; Notifications owns accepted notice, scoped audience policy/routing, channel attempt/evidence, inbox and its own outbox; Mailer owns email transport; Message Queue owns message transport only; Scheduler executes due tasks. No provider response becomes human receipt or domain completion.
2. **Public contract:** every inbound source, authorisation/consent/policy version, provider uncertainty and revalidation requirement is described; output meaning distinguishes durable acceptance, queued attempt, hand-off, delivery evidence, inbox read and legal effectiveness. Commands/queries/events expose scoped, idempotent, duplicate-tolerant behaviour without universal request type or private persistence access.
3. **Failure, isolation and security:** tenant-parent access is not implied; late revocation, unresolved legal duties, unsafe templates, duplicate callbacks, idempotent retries, unsupported provider and already-transmitted cancellation are explicit. Potential risk remains around mandatory-notice policy, statutory service and preference ownership (NOT-07–NOT-10).
4. **Relationships:** direct draft overlap is material in Mailer PR #90 and Message Queue PR #94; this PR only adds proposed bounded reciprocal notes to their master records. Their current branch designs must be reconciled at integration and not silently treated as approved. Existing historical notes for Billing, Booking, Course, Authorisation etc were retained unchanged.
5. **Documentation:** target path `docs/capabilities/notifications/capability-record.md` preserves the existing pro-forma/notes and adds explicit non-normative status. Relative links are scoped from target record to `docs/review-protocol.md`, `reviews/notifications-review-baseline.md` and adjacent capability records. No catalogue/register classification change required because governing catalogue and blueprint already identify Notifications as Platform. Proposed NOT-01–NOT-10 have no claimed owner approval.
6. **GUI:** optional accessible user inbox and operator dashboard, including headless absence, safe contextual host access and Theme Manager semantics, without taking application navigation or peer domain ownership.

## Outstanding gates before any merge

- Owner decision on NOT-01–NOT-10 and any consequential scope changes; reconcile competing Mailer, Message Queue, Privacy/Profile and domain-owner drafts.
- Check current `master` and accepted governing changes again, update/rebase preserving concurrent edits, and verify GitHub mergeability and protected-branch checks. Investigate current `mergeable: false` and absent statuses rather than declaring ready.
- Future implementation-owned work: independently usable root `CONTRACT.md`, storage inventory, public errors/ports and minimal consumer, security/provider acceptance, CI evidence. The conceptual review neither delivers nor verifies those obligations.
- **Explicit owner approval required before merge; only squash under protected master policy.**
