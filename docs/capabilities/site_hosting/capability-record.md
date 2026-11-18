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




## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53).** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Site Hosting owns domain verification, routing and trusted tenant-from-host resolution. Configuration's hostname/site descriptors must not confer domain ownership or trust forwarded headers without verified proxy controls. Public host-composed ports/events only; no direct package dependency or replacement of existing decisions is implied.

## Federation — reciprocal conceptual note (18 November 2026)

**Status:** Proposed in [Federation draft PR #69](https://github.com/nuxt-layers/architecture-blueprint-review/pull/69), not a published implementation contract or completed independent review. See [Federation conceptual contract](../federation/capability-record.md).

Site Hosting and host proxy supply verified endpoint, DNS and routing facts; Federation supplies scoped protocol and collection advertisements. Neither domain control nor TLS certs certify content truth or resource permissions. Remote address resolution, redirect, SSRF and rebinding checks remain mandatory. Public directional ports, explicit absence modes and acyclic package dependencies apply.


## Infrastructure reciprocal interface — 18 November 2026 (owner-approved infrastructure direction)

[Infrastructure's conceptual hosting and operational contract](../../../reviews/infrastructure-conceptual-architecture.md) owns reproducible host/proxy/TLS deployment tooling, approved installation and provider changes, host readiness and provider-evidenced operational outcomes. Site Hosting retains authoritative hostname/domain verification, site/tenant routing and request-address trust decisions under ADR-0014; operationally ready proxy/certificate infrastructure does **not** establish tenant domain ownership or authorise a hostname claim. Site Hosting supplies approved routing and certificate requirements to the host; Infrastructure returns verified applied/unknown/degraded deployment state without duplicating Site Hosting's source records. Infrastructure's administrative screens and APIs are accessible only to installation-scoped **host super-administrators**, not tenant or lower-level administrators. Internal site routing continues without an interactive super-administrator session. This is a conceptual reciprocal note, not a claimed implemented API.
