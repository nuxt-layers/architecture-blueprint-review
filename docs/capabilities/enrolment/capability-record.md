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

## Reciprocal conceptual note — Course curriculum and learning outcomes (17 November 2026)

**Status: Proposed, pending owner approval; not a completed enrolment review or implementation contract.** [Course conceptual review](../course/capability-record.md) (draft PR #56): Course supplies immutable published course/version references, prerequisite definitions and entry constraints; Enrolment alone owns learner applications, admission, seat allocation, participation and standing. Enrolment must not infer that a public course is available to a particular learner, and Course must not record admissions. Missing or withdrawn course revisions must produce explicit unavailable/unknown outcomes, preserving lawful historical references.

## Course COURSE-08–11 approved conceptual reciprocity (17 November 2026)

**Status: Owner-agreed boundaries, no independently completed enrolment review or implemented API.** [Course](../course/capability-record.md) and [Assessment candidate](../assessment/capability-record.md): **COURSE-09 agreed:** Enrolment owns learner admission, cohort enrolment/waitlists and individual allocations referencing an immutable Course revision. Course provides teaching/prerequisite constraints, Events provides session/venue facts, Booking provides relevant reservations; Enrolment/host composition determines effective seat availability from authoritative constraints with unknown/stale semantics. Cohort-run operational identity is to be resolved in Enrolment's own review; Course does not own people or schedule. **COURSE-11 agreed:** learner transfer between course revisions requires explicit mapped outcomes/credits, gap review, authorised decision, original-version history and appropriate notification; never silently rewrite admissions.

## Reciprocal Assessment conceptual interface — 18 November 2026 (draft PR #64)

**Status: Proposed, not an independently approved enrolment contract.** [Assessment conceptual review](../assessment/capability-record.md): Enrolment supplies course-version-specific standing and verified candidate eligibility/attempt entitlement where applicable; Assessment owns authorised attempt and individual mark. A missing/stale/withdrawn Enrolment decision blocks dependent attempt creation, but lawful historical results retain their original source/version. Standalone examination need not invent an enrolment. Parallel Enrolment PR #60 is provisional. Conceptual cooperation does not require cyclic package imports; all protected reads and commands require public contracts, purpose/tenant permission and explicit unknown/failure handling. Preserve the enrolment owner's existing decisions.


## Qualification independent conceptual review — reciprocal interface (18 November 2026)

**Status: proposed detailed contract under [Qualification review](../qualification/capability-record.md), PR #65; COURSE-12 ownership remains owner-agreed.** Enrolment owns learner admission, cohort allocation and applicable Course revision. Qualification consumes those references only when the qualification pathway requires them; permitted RPL, direct assessment or external-award routes need not have enrolment. Qualification never assigns places or determines admission. Enrolment never independently confers qualification eligibility or an award. This note does not complete this adjacent capability's independent review or assert an implemented contract.

## Training TRAIN-01–08 reciprocal proposal (18 November 2026)

**Status: TRAIN-01–08 owner-approved in [Training conceptual review](../training/capability-record.md), PR #63; proposed public contract, not an implemented interface or completed enrolment review.** Enrolment supplies active learner standing, cohort and frozen Course reference for enrolment-controlled programmes; Training supplies verified participation and completion findings but never controls admission/waitlists. Independent approved prior-learning training need not require Enrolment. PR #60 is provisional and must be reconciled. All exchanges are public-contract scoped, tenant-authorised and provenance/version aware; avoid directed dependency cycles and treat unknown/stale external assertions explicitly.
