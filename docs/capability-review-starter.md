# **Nuxt Layers — Capability Conceptual Review**

**Target capability:** `[CAPABILITY]`  
**Working repository:** `nuxt-layers/architecture-blueprint-review`  
**Governing repository:** `nuxt-layers/architecture-rules`

Read and follow the **current** [Parallel Capability Conceptual Review Protocol](review-protocol.md) in the working repository.

**Constraints.** Do not modify implementation repositories, run local tests or builds, assume normative adoption, or merge without explicit approval. Use British English.

## **Phase 0: start now**

1. Find the target’s actual directory name. Do not assume its punctuation.
2. Inspect the current master baselines of the governing and blueprint repositories, and any active PR for the target.
3. Create a dedicated branch, commit a meaningful review-baseline note and open a draft PR immediately.
4. Report the PR link before any substantive analysis.

## **Phase 1: evidence**
Read the current accepted governing authority and the working blueprint evidence. Review the existing implementation through its root CONTRACT.md if one exists. Review related repositories only through their public root contracts, unless broader inspection is expressly authorised.

## **Conceptual specification**
Complete the capability’s:  

* purpose and classification
* authoritative ownership and exclusions
* native behaviours
* commands, queries and events
* provider-neutral interfaces
* security and legal constraints
* failure and recovery
* accessibility (WCAG)
* acceptance scenarios

As part of this, answer each question below briefly and in plain English, covering every issue that must be considered:

1. **Public contract:** What published input and output interfaces does the capability have? This is its mandatory, idealised contract.
2. **Information exchange:** What information does it need from other capabilities, and what does it supply to them, as its likely or existing CONTRACT.md would state?
3. **Logging, audit and reporting:** How does it relate to the logging, audit and reporting capabilities? Answer in terms of its contract and theirs: what it emits, what each one consumes, and what must never pass between them.
4. **Standards:** Which established standards (specifications, formats, protocols, NIST, W3C, ISO or government published standards) can it adopt instead of reinventing them?
5. **Libraries:** Which mature, actively maintained and stable libraries could support its development?
  * Each must be genuinely open source under a commercially permissive licence, such as MIT, Apache-2.0, BSD or ISC.
  * Exclude source-available and open-core products whose free edition leads to vendor lock-in, as with Neo4j, Redis and Elasticsearch.
  * For each library, give its licence and say why it qualifies.
  * Record these as proposals, not adoptions.

Throughout, mark each item as established, owner-approved, proposed, open or unverified.

## **Records**
Keep all documentation commits on the original draft PR. Update the catalogue, register, findings and decisions where justified. Add dated reciprocal notes to related capability records where warranted, including those under parallel review, without silently rewriting their accepted work.

## **GUI**
Identify the screens the capability is likely to need and explore how they would be presented. Use `nuxt-layers-test/application-test-template` as the representative host: a side-menu option opens a capability dashboard, in the same way theme-manager is enabled. You may read that repository’s navigation and dashboard wiring for this purpose only, without changing it.

## **Acceptance and merge**
Complete the target capability's conceptual purpose, classification, authoritative ownership/exclusions, native behaviours, **mandatory idealised input/output contract**, commands/queries/events, cross-capability information exchange, provider-neutral interfaces, security/legal constraints, failure/recovery, conceptual GUI, accessibility and acceptance scenarios. Use dated reciprocal notes in related capability records whenever warranted, including parallel reviews, without silently rewriting their accepted work.

Keep all documentation commits on the **original draft PR**, updating catalogue/register/findings/decisions where justified. Distinguish established, owner-approved, proposed, open and unverified material.

1. If you are satisfied that the conceptual specification is sufficiently complete, mark it as accepted. This is acceptance of the conceptual review, not normative adoption.
2. Run the final pre-merge checks:
  * the latest master in both architecture repositories
  * newly merged or open overlapping PRs
  * Git conflicts
  * architectural contradictions
  * ownership and contract consistency
  * links and filenames
  * required CI
3. Fix any conflicts, errors or other problems preventing the squash merge from happening.
4. Obtain explicit approval.
5. Immediately before the squash merge, recheck mergeability and approvals.
6. After merging, verify that GitHub reports the PR as merged and closed.


