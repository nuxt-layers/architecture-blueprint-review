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

## Review notes — staff, contractors, payroll and accounting (14 November 2026)

**Provisional conceptual notes only.** Employment and payroll ownership have not been independently established.

- Identity group membership **does not establish employment**, contract terms, payroll enrolment, worker status, employer obligations or permission to see pay.
- Employment may govern employment engagements, contract type, assignment, working status and effective dates. Contractors may instead be counterparties supplying services under commercial agreements; one person can have distinct roles for different legal entities.
- **Payroll** would calculate gross/net pay, deductions, employer contributions, accruals, payslips, payment instructions and statutory reporting under applicable law, potentially through a configured external provider. Do not put raw personal payroll data into Accounting or generic Profile.
- Accounting consumes authorised aggregate or attributable financial facts for wages, benefits, employer liabilities, contractor invoices/payables and allocation of qualifying direct labour to production/WIP; it does not determine employment rights or calculate statutory deductions.
- Utilities, leases, subscriptions and outsourced services create other recurring operating costs that belong to supplier/contract/billing evidence and Accounting posting; purchase commitments, accruals, invoices and bank settlements are distinct.
- **Open:** do we need a dedicated Payroll conceptual candidate; how are privacy, jurisdiction, employer identity, contractor status, time tracking and per-tenant external payroll authority governed?

### Cross-capability relationships and evidence status

- **Established evidence:** This record remains an uncompleted pro forma plus discussion notes; its corresponding repository, if any, and root `CONTRACT.md` have **not been independently audited for this capability**. No implementation readiness is asserted. Governing catalogue and accepted ADRs take precedence over these notes.
- **Proposed responsibility boundary:** Employment and contractor-engagement facts must be distinct from payroll calculations and Accounting postings; membership is not employment.
- **Related capability notes:** [accounting](../accounting/capability-record.md), [asset](../asset/capability-record.md), [order](../order/capability-record.md), [billing](../billing/capability-record.md), [integrations](../integrations/capability-record.md).
- **Open architectural questions:** Whether Payroll is a separate domain, how personnel privacy and employment status are handled, and payroll provider authority.
- **Review gate:** At this capability's alphabetical turn, verify current organisation repositories and the public root `CONTRACT.md` if present; reconcile authority and evidence, then define its own conceptual record. Keep other domains' internal implementation out of scope.
