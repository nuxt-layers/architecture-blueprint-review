# Attendance capability — opening conceptual review baseline

**Date:** 18 November 2026. **Status:** owner-requested *capability creation and conceptual documentation*, **not** a separately approved runtime authority or implementation. **Target:** `docs/capabilities/attendance/capability-record.md`. **Branch:** `review/attendance-conceptual-20261118`.

**Governing:** `nuxt-layers/architecture-rules/master@0725f314abc9ad13f1a65247f54a7ff80772f0b2`. **Blueprint:** `nuxt-layers/architecture-blueprint-review/master@5b6f67be3263586ffea5156f7b23135373ccd734`. **Protocol:** [review-protocol](../docs/review-protocol.md).

**Finding motivating review:** Event attendee registration/invitations/RSVPs and verified presence should be examined as a reusable participant/attendance capability, independent of Events, Booking, Enrolment and Training. The user requested a new Attendance capability record and reciprocal Booking/Enrolment notes, while expressly seeking pros/cons of Attendance as the shared “people record”. Distinguish **Identity/Profile person master**, **Attendance per-activity participant register**, **Booking per-reservation party/beneficiary**, **Enrolment learner standing** and **Training educational evidence**. Replacing another capability's approved authoritative ledger is **not** automatically approved.

**Review deliverables:** idealised public input/output contract, actor/participant data model and verification lifecycle, generic activity references, capacity and entitlement separation, corrections/outbox, data minimisation, provider/integrations, reciprocal relationships, optional GUI, approval gates and future independent contract/CI checks. No separate implementation repo, local tests or automatic merge.
