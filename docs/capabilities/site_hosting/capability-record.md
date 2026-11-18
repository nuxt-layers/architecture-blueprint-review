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
