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

**Status: Proposed for [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53), not an implemented contract.** See [Configuration conceptual public inputs](../configuration/capability-record.md#idealised-public-inbound-interfaces). Theme Manager owns the effective theme, selections and semantic tokens. Configuration's GUI consumes these; its setting registry cannot become a duplicate theme preference authority. Use public host-composed ports/events only; preserve all prior decisions and dependency acyclicity.


## Configuration decision reconciliation — CFG-05–08 (17 November 2026)

**Status: Owner-approved conceptual decisions in [Configuration PR #53](https://github.com/nuxt-layers/architecture-blueprint-review/pull/53); not an implemented or newly accepted governing contract.** See [Configuration decision register](../configuration/capability-record.md#decision-register-evidence-and-sign-off).

**Owner-approved CFG-05 (Option B):** Configuration may retain non-personal account-specific operational settings, but Theme Manager alone owns effective theme and relevant personal theme-selection semantics; generic Configuration account scope does not create a second theme authority.

Existing independently approved decisions are preserved; this note resolves Configuration's selected boundary rather than retroactively approving all prior proposals.

## Reciprocal conceptual note — Content Editor review (17 November 2026)

**Status:** Proposed contract alignment in [Content Editor draft PR #54](https://github.com/nuxt-layers/architecture-blueprint-review/pull/54); not a completed theme_manager review, normative rule or implementation change. See [Content Editor conceptual boundary](../content_editor/capability-record.md#dedicated-conceptual-review--content-editor-17-november-2026).

Content Editor uses Theme Manager's published semantic tokens and contrast/presentation preferences. The editor cannot create its own conflicting theme authority; host may mount or replace the screens, subject to WCAG 2.2 AA.
