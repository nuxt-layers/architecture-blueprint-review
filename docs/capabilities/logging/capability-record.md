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

## Cross-capability note — Logging versus Audit (14 November 2026)

**Established:** The governing catalogue distinguishes Logging's structured technical diagnostics/correlation/sinks from Audit's proposed tamper-evident business/security evidence and review. **Proposed:** Logging may provide correlation and operational failure signals to [Audit](../audit/capability-record.md), but debug logs are not by default authoritative evidential records. Audit does not own Logging's sinks or general log lifecycle. **Open:** event mapping, classifications, sensitive-data minimisation and failure alerts. Logging's full conceptual review remains incomplete.

## Cross-capability note — Authentication operational logging (15 November 2026)

**Established:** [Authentication](../authentication/capability-record.md) owns credentials, sign-in attempts and outcomes, session lifecycle, security controls and authenticated principal assertions; Logging supplies structured technical diagnostics and correlation, not authoritative security-event custody or the originating Authentication facts. **Agreed conceptual direction:** Authentication emits only purpose-limited, sanitised operational signals for authentication errors, provider outages, throttling, maintenance and degraded health, with suitable correlation references and controlled diagnostic access. Logs must not expose passwords or verifiers, session/bearer tokens, passkeys or recovery secrets; IP addresses, user agents and identifiers require data minimisation, classification, access controls and retention. Authentication's significant security outcomes flow through its owned durable event mechanism for [Audit](../audit/capability-record.md), not by promoting ordinary logs into authoritative evidence. **Open:** diagnostic taxonomy, correlation/redaction policy, retention, outage behaviour and whether Logging is an independent capability rather than an infrastructure integration. Logging's own conceptual review remains incomplete.
