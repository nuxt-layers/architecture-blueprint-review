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

## Cross-capability note — Audit evidence attachments and custody (15 November 2026)

**Status: Proposed reciprocal relationship; not a completed capability design.** Storage owns bytes and provider-agnostic file delivery, not Audit evidence ownership. **Proposed:** [Audit](../audit/capability-record.md#completeness-review--further-interfaces-and-relationships-15-november-2026) may use the published StorageService shape for protected attachments, keeping evidence associations, integrity manifests, holds/disposal decisions and disclosure in Audit. Missing bytes yield explicit unavailable/partial verification, not fabricated authenticity. No assumption that generic object storage provides immutable audit custody. Storage's conceptual review remains incomplete.

## Cross-capability note — Authorisation of protected files (15 November 2026)

**Status:** Proposed relationship; no new Storage access-decision ownership. [Authorisation](../authorisation/capability-record.md#completeness-challenge--further-authorisation-interfaces-and-relationships-15-november-2026) may evaluate owner-supplied verified file/resource context and requested read/write/share/export permission. Storage remains responsible for file bytes and provider-neutral file operations, while the content/domain owner retains business metadata and disclosure rules. Signed links, caches, derivatives and file exports need tenant scoping, bounded lifetime and revocation semantics; a storage success does not itself prove lawful or authorised disclosure. Storage's conceptual review remains incomplete.
