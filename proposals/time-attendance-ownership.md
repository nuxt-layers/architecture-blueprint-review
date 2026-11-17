# Time & Attendance — approved conceptual ownership boundary

**Status:** Owner-approved conceptual separation following EMP-03 on 17 November 2026; **candidate Domain capability**, not a completed independent capability review, governing ADR, authorised implementation repository or published contract.
**Proposed identifier:** `time-attendance`.
**Origin:** [Employment draft PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59) and [Employment record](../docs/capabilities/employment/capability-record.md).

## Purpose and unique authority
Time & Attendance is the proposed authoritative business boundary for **actual time and attendance evidence** across employees, workers, contractors, volunteers and other appropriately authorised participants. It must work without requiring an Employment record when an eligible context is established independently.

Its own records would cover clock-in/clock-out observations, break periods, submitted time entries, timesheet periods, evidence sources, corrections, disagreements, approvals/rejections, overtime as a *recorded quantity* (not automatically approved or payable), completeness and integrity/provenance. Distinguish **observed, declared, submitted, disputed, approved, corrected and passed downstream**. It does not silently delete or rewrite historical approved entries.

## Explicit boundaries
- **Employment** owns employer/worker legal relationship, contracted hours, agreed patterns, leave entitlements, relevant employer-side approvals and eligibility conditions; it does not own actual time observations. Employment can provide authorised approval policy context and consume approved time/exception references.
- **Workforce Scheduling (proposed separate responsibility)** owns intended shifts, rosters, shift assignments and alterations, not proof of attendance. Whether it warrants a dedicated capability is a separate review.
- Existing **`scheduler`** is platform timed/background execution; it owns neither staff shifts nor actual hours.
- **Payroll** owns pay eligibility calculations, gross/net pay, statutory deductions and payslips, consuming qualified, versioned approved time as needed. Worked time is not automatically payable overtime.
- **Project/Task** own activity/task/work allocation, not all-person attendance. They may supply attributable activity evidence and consume permitted approved allocation references; avoid counting the same interval twice across payroll and billing.
- **Clock** owns date/time/time-zone/DST semantics; Time & Attendance owns business interval validation and measured/declared record states.
- **Identity/Authorisation/Privacy/Legal Compliance** provide identity/scope/decision/rights/qualified legal constraints, with purpose-limited, tenant-safe access and explicit statutory uncertainty handling.
- **Integrations** supplies external terminal/timesheet provider transport and provenance; Time & Attendance selects per-scope source authority and reconciles duplicates, errors and uncertain provider outcomes.
- **Audit** owns independent accountability evidence; Time & Attendance retains its own source revision history and outbox.

## Preliminary idealised public interfaces — not the final contract

| Input | Proposed meaning / failure |
|---|---|
| Trusted participant/activity and scope reference | Validate tenant, legal/work context and source authority; person need not have an Employment engagement |
| Clock event, timesheet claim or correction | Include event interval, source, observed/declaration distinction, provenance, version, idempotency and correction reason; hold conflicting/invalid intervals |
| Work pattern/entitlement and approval constraints | Employment supplies employer-related requirements conditionally; other participation owners supply their own approval policies |
| Planned shift / task attribution | Workforce Scheduling or Project/Task supply references, not proof that hours were worked |
| Authorised reviewer decision | Validate field/purpose access, independence where required, expected revision and applicable legal rules |
| Provider evidence | Explicit remote source/version and status; uncertainty remains held for reconciliation |

| Output | Proposed consumers / meaning |
|---|---|
| Time entry and attendance record with state/history | Authorised worker, manager, employer or relevant participant owner; no universal personnel directory |
| Approved time statement / correction reference | Payroll, Project/Task, authorised billing/cost allocation as applicable; approval of evidence is not approval of wages or invoices |
| Exception/overlap/missing entry and dispute state | Participant, manager, authorised compliance/reconciliation |
| Committed state-change event | Minimised revisioned outbox events; subscribers deduplicate and use independently authorised detail queries |
| Rights/retention and provider reconciliation result | Privacy and authorised administrators with effective policy/scope and provenance |

## Open questions for the future dedicated alphabetical review
1. Whether attendance presence, job/task effort allocation and external billable consulting time share one authority or require separately owned source records with reconciliation.
2. Which actor can approve hours for a non-employed contractor, volunteer or external engagement, and when approval must be independent.
3. Overlapping intervals, travel, breaks, absence, overnight work, cross-border assignments, daylight saving transitions and correction of previously paid periods.
4. Time-device trust, offline capture, attestation, fraud and audit, source priority and external provider reconciliation.
5. Jurisdiction-specific employment/working-time law, worker visibility/disputes, sensitive location/biometric data minimisation and retention.
6. The [pro-forma capability record](../docs/capabilities/time-attendance/capability-record.md) now exists; complete its full independent review and capability-start gate before considering any `nuxt-layers/time-attendance` implementation repository.

**Acceptance status:** The separate Domain boundary and creation of the blueprint pro-forma are approved; the detailed contract, GUI, provider/retention choices, dependency architecture and implementation packaging remain unapproved.
