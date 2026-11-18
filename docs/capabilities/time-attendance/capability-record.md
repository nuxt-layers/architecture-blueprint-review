# **Capability Record**

## Capability Name:
Time & Attendance (`time-attendance`).

## Status: (Available, Installed, Configured, Operational, Enabled, Authorised and Proposed).
**Proposed Domain capability; conceptual ownership approved under Employment EMP-03 on 17 November 2026.** Dedicated conceptual review not started or completed. No implementation repository, published `CONTRACT.md`, runtime availability, operational status or blanket authorisation is asserted.

## Purpose
Maintain authoritative, attributable evidence of **actual attendance and time worked** for eligible employees, workers, contractors, volunteers and other participants, including where no Employment relationship exists. Distinguish observed attendance from declared hours, approved evidence, payable time and time allocated to particular activities.

## Classification
**Domain capability candidate** with a separately approved conceptual responsibility and potentially independent data/lifecycle. Its final packaging, contracts and implementation remain subject to the normal capability review and governance gates. This record is a pro-forma with review notes, **not** a completed architecture or permission to create a package.

## Dependencies
To be established through its dedicated review. Expected conceptual cooperation: Identity, Authentication, Authorisation, Clock, Privacy and Legal Compliance; conditional Employment, Workforce Scheduling (proposed), Project, Task, Payroll (proposed), Accounting and Audit. Public contracts, not private stores or cyclic dependencies.

## Optional integrations
To be reviewed: approved external time clocks, attendance terminals, timesheet providers and mobile/offline capture through Integrations. Establish scoped provider authority, provenance, duplicates, offline reconciliation, trust and withdrawal before implementation.

## Version
No public contract or implementation version assigned.

## Availability
No implementation established. Blueprint pro-forma only.

## Capabilities offered
**Approved ownership boundary, not yet a completed service design:** actual clock-in/out observations, attendance intervals, breaks, submitted timesheets, evidence of actual hours, corrections, disputes, approvals and source/history integrity. Future review must explicitly distinguish observed, declared, submitted, disputed, approved, corrected and downstream-consumed states.

**Does not own:** contractual hours or leave entitlement (Employment); planned shifts and rosters (prospective Workforce Scheduling); infrastructure triggers (existing `scheduler`); payroll eligibility, pay or statutory deductions (Payroll); or project/task activity ownership (Project/Task). A planned shift, scheduled trigger or task entry is not evidence of worked hours, and approved worked hours are not automatically payable hours.

## Configuration
To be determined: authorised per-organisation/engagement approval policies, source/provider preferences, time rounding and overlap rules where lawful, exception handling, retention and evidence requirements, restricted presentation settings and jurisdiction/effective-date applicability. Configuration does not override statutory or security floors.

## Deferred dedicated conceptual review — required questions (17 November 2026)
**Evidence and decision status:** [Employment PR #59](https://github.com/nuxt-layers/architecture-blueprint-review/pull/59) records the owner's approval that Time & Attendance is **independently owned** rather than an Employment subfunction. [Ownership proposal](../../../proposals/time-attendance-ownership.md) contains preliminary input/output ideas. The complete Time & Attendance contract, GUI and implementation choices **have not been approved**.

1. **Owned records and lifecycle:** distinguish attendance presence, actual worked time, employer-approved time, project/task allocation and externally billable consultant time. Decide whether all belong here or require independently owned evidence with reconciliation.
2. **Inputs:** source actor, participant/engagement or other authorised activity, employer/group/tenant context, observed vs declared events, timestamps/zones, breaks, source assurance, approval policy, expected revision and idempotency; define required/conditional fields and stale/missing/contradictory handling.
3. **Outputs:** validated entries, period summaries, approved statements, corrections, disputes and events to Employment, Payroll, Project/Task, Accounting/Reporting and authorised participant views; specify lawful field disclosure, provenance, completeness, version and freshness.
4. **Authority and approvals:** who may attest/approve time for employees, self-employed contractors and volunteers; delegation, independence/separation of duties, corrections after payroll, disputes and protected records.
5. **Workforce Scheduling:** rosters and planned shifts belong to a **different prospective business responsibility**; never treat existing infrastructure `scheduler` as workforce rostering. Clarify shift hand-offs, absences, overlapping schedules and discrepancies.
6. **Legal/security/privacy:** jurisdictional working-time and break rules, child/safeguarding cases where applicable, record retention, worker access/challenge, fraud, location tracking/biometrics, cross-border work and minimisation.
7. **Integration/recovery:** time-device trust, clock drift/DST, offline submission, duplicates, delayed callbacks, remote provider authority, corrections and synchronisation without dual authoritative sources.
8. **GUI and headless contract:** employee/contractor self-service timesheet and correction views; role-restricted reviewer queues, approvals, disputes and audit history; WCAG 2.2 AA, localisation and Theme Manager. Confirm host sidebar integration and independent headless operation.
9. **Acceptance scenarios:** no Employment record, valid clock events, overlapping claims, denied cross-tenant read, incorrect/expired approver, offline replay, disputed attendance, corrections after payroll, jurisdictional break violations, export/retention constraints and provider failure.
10. **Capability-start gate:** confirm final public input/output surfaces, commands/queries/events, dependency direction, independent ownership, provider-neutral composition, security guarantees, reciprocal documentation, contractual acceptance and whether a separate implementation repository is justified.

## Cross-capability and review notes
- [Employment](../employment/capability-record.md) owns terms and entitlements, consumes authoritative time evidence only as authorised, and never becomes the owner of clock events.
- [Scheduler](../scheduler/capability-record.md) executes background tasks; it does not plan staff shifts or prove work attendance.
- Payroll remains a separate proposed domain; it may consume qualified approved hours but must make its own wage and statutory decisions.
- Project/Task activity allocations must be reconciled without inventing additional attendance or double-counting the same interval.
- All independent capability dependencies must be explicit, directional and acyclic; commands/events do not confer access.
- The full conceptual review must follow [review-protocol.md](../../review-protocol.md) in its own dedicated branch and draft PR, and update reciprocal records and the catalogue/register as warranted.

**Sign-off:** Independently owned Domain boundary agreed; **detailed review, contract, GUI and packaging pending**. No implementation, no local tests, no merge or change to `architecture-rules` authorised by this pro-forma.

## Training TRAIN-01–08 reciprocal proposal (18 November 2026)

**Status: TRAIN-01–08 owner-approved in [Training conceptual review](../training/capability-record.md), PR #63; proposed public contract, not an implemented interface or completed time-attendance review.** Training owns attendance at learning activities and verified training progress; Time & Attendance owns actual work-time intervals/breaks/payable-time evidence. Mapping one interval to training does not automatically prove working hours or vice versa; separate consent/authorisation and revision reconciliation apply. All exchanges are public-contract scoped, tenant-authorised and provenance/version aware; avoid directed dependency cycles and treat unknown/stale external assertions explicitly.
