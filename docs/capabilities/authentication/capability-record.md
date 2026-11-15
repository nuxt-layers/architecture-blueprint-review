# Capability Record — Authentication

**Capability:** `authentication` — **Foundation (IAM), established architectural responsibility**.  
**Conceptual review:** Proposed for sign-off; implementation readiness is separate.  
**Review date:** 15 November 2026.  
**Governing baseline:** `nuxt-layers/architecture-rules` `master` at `2eea557fa3acbf9412fea065d2a3cdda42a764fc`.  
**Blueprint baseline:** `nuxt-layers/architecture-blueprint-review` `master` at `88557906cab4799599a66974f2411aa572f01ac5`.  
**Implementation evidence:** [`nuxt-layers/authentication`](https://github.com/nuxt-layers/authentication) `master` at `ffb92d8c033ebb8bcb5043e3fa5acadac9e1d825`; root [`CONTRACT.md`](https://github.com/nuxt-layers/authentication/blob/ffb92d8c033ebb8bcb5043e3fa5acadac9e1d825/CONTRACT.md), published contract `Authentication` version `1`, development status, no supported release. The public contract, not private source, was inspected. An independently verified complete implementation, host acceptance or production deployment is **unverified**.

## Architectural authority and decision status

**Established:** [Platform Charter](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/platform-charter.md), [Architecture](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/architecture.md), [Capability Standard](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/capability-standard.md), [Catalogue](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/catalogue.md), [Identity and Access](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/identity.md), [Security](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/security.md) and [Privacy](https://github.com/nuxt-layers/architecture-rules/blob/2eea557fa3acbf9412fea065d2a3cdda42a764fc/docs/privacy.md). Accepted ADR-0001, 0002, 0003, 0004, 0005, 0006, 0007 (break-glass as referenced by the current contract), 0008, 0009, 0010, 0012, 0014, 0015 and 0016 are relevant where applicable. The accepted ADR-0005 defines the IAM suite and its inviolable separation of members; accepted ADR-0012 defines shared structural ports and single-call/50-line composition; ADR-0016 permits controlled specialisation, not private coupling. This record does not approve normative changes or certify standards compliance.

**Evidence hierarchy:** accepted ADRs → normative governing standards → approved public capability contracts → current implementation evidence; this blueprint is non-normative. Historical findings in `records/findings.md` identify Authentication assurance and revocation as integration invariants. The completed [Audit review](../audit/capability-record.md) proposes a governed, minimised evidence interface. Authentication must not silently claim that its presently best-effort events meet Audit completeness guarantees.

## Purpose and conceptual definition

**Established:** Authentication proves an asserted principal's control of accepted authenticators, governs credential enrolment and recovery, establishes authenticated sign-in and service-credential outcomes, and manages authenticated sessions, assurance, reauthentication, expiry and revocation. It publishes a trustworthy, time-scoped authentication assertion for consumers; it does **not** decide whether the principal may act on a particular resource.

**Why separate:** Credentials and session trust have distinct security rules and lifecycles from Identity's opaque principals, memberships and tenants; Profile's personal records; and Authorisation's resource-specific decisions. Authentication is a genuinely independent, security-critical Foundation capability, not a theme, screen, SDK or application composition. It can operate headlessly using its own records and provider-neutral host services. A federation provider is optional and never acquires control of the local application's access decisions.

**Consumers:** people signing into applications, non-human service principals, IAM composition, protected domain/platform capabilities, administrators managing their own authentication methods, and authorised security operations. A principal assertion is evidence of authentication, *not* evidence of tenant membership, group ownership, user consent or permission.

## Responsibility and authoritative ownership

| Dimension | Authentication owns | Explicitly elsewhere |
|---|---|---|
| Sign-in identifiers | Authentication-specific identifier verification, uniqueness and linkage to opaque principal IDs | Identity owns the principal and its standing; Profile owns ordinary personal/contact attributes |
| Authenticators | Password verifiers, passkeys, MFA credentials, recovery/backup credentials, external provider account links, service credential verification and revocation | External providers own their external credentials; Identity owns service-identity existence |
| Sessions | Issue, refresh, rotation, inactivity/absolute expiry, concurrent-session policy, logout, account-wide revocation, reauthentication evidence | Authorisation owns operation-specific access decisions and changes resulting from memberships |
| Assurance | Methods and independently justified strength, authentication time, phishing resistance, proof freshness and constrained assertion | An external provider's assurance claims require explicit verified trust; no automatic elevation |
| Abuse prevention | Authentication attempt throttling, suspicious sign-in safeguards, account-safe failure and recovery restrictions | Audit owns accepted evidence and integrity review; Logging/Observability own technical diagnostics |
| Account authentication lifecycle | Credential enrolment, verification, lockout, recovery and credential disposal, correlated to Identity identifiers | Identity owns creation, suspension, closure and account standing |
| Emergency access | Restricted authenticators, authentication of designated emergency principal and session revocation | Identity/Authorisation/IAM integration own emergency identity provisioning, permission and approval governance |
| Service access | Service authenticators, limited-lifetime tokens and their authentication evidence | Identity owns service principals; Authorisation checks requested resources and privileges |

**Invariant:** never use email, a provider subject, a session ID, a client-supplied tenant/group or an authentication method as an independent permission or authoritative membership. Credential changes never silently mutate Identity, Profile or Authorisation storage. Authentication holds only personally identifying information necessary for sign-in and risk controls, subject to classification, retention and lawful rights.

## Native functionality and conceptual lifecycle

**Established public-contract functionality:** password enrolment/change/reset, verified sign-in identifiers, account verification, session issuance and management, MFA using TOTP/backup codes, passkeys, reauthentication, session risk controls, account restriction, administrator break-glass passkeys, service credentials and time-limited tokens. Optional federation providers and remembered devices are described in the public contract. Optional screens can be disabled entirely.

**Proposed minimum independent behaviours:**
1. Accept a clearly scoped account/authenticator enrolment request; verify required proof; reject duplicative/untrusted linkage and unsupported methods; produce an authenticated session only on successful verification.
2. Verify authenticators securely, mitigate brute force, enumeration and replay, apply adaptive or policy-bound friction without silently locking out lawful users indefinitely, and distinguish an attempted sign-in from an authenticated result.
3. Issue an opaque authenticated principal assertion with principal ID, principal kind, bounded validity, authentication time, method/assurance and standing evidence; refuse invalid, expired, revoked or insufficiently assured sessions.
4. Manage all authenticator transitions: pending enrolment → verified/active → replaced, restricted, revoked or expired; recovery is a separately justified high-risk transition, not proof of pre-existing high assurance.
5. Manage session transitions: anonymous → partly authenticated/challenge pending → authenticated at an evidenced assurance → stepped up/rotated → expired, signed out or revoked. Distinguish credential lifecycle from session lifecycle; revoking a credential should trigger the session invalidation required by policy.
6. Offer self-service visibility of active sessions and relevant authenticators, selective/account-wide revocation, recovery and documented administrative controls. Constrain recovery and break-glass with provenance and non-impersonation.
7. Support service-to-service authentication separately from person sessions: a service credential or bearer token cannot inherit a person's phishing-resistant assurance or be upgraded by a user session cookie.
8. Provide safe error categories, secure user-facing sign-in and recovery flows and headless equivalents; preserve anti-enumeration, CSRF/origin and redirect protections.
9. Honour lifecycle signals from Identity, including account pause/suspension/closure, and fail closed for sensitive operations if required standing or revocation evidence cannot be established.
10. Provide operator-safe maintenance, retention, expiry, recovery and reconciliation; keep authentication records authoritative even if mail, Audit delivery or external federation is unavailable.

**Proposed additional lifecycle states to make explicit:** challenge issued/expired/consumed; credential pending proof/active/compromised/revoked; federated link pending/linked/unlinked; recovery requested/authorised/consumed/expired; session assurance downgraded or no longer fresh; service secret rotation with bounded overlap and retirement; lockout and appeal/recovery; emergency enrolment pending/activated/rotated/revoked. These are conceptual distinctions, not claims about existing database enumerations.

**Failure semantics:** distinguish invalid proof, insufficient assurance, expired or revoked session, account restriction, consent or policy refusal, temporary provider outage and undetermined result. Never turn a timeout, missing standing response, failed verification or third-party callback into a successful assertion. A notification failure does not reverse a successful credential mutation, but must be observable and recoverable.

## Conceptual public contract — input and output boundaries

The following are *logical contract surfaces*. Their proposed naming is **not** an assertion that matching functions or endpoints exist; see the implementation's root contract for the actual published functions.

| Surface | Inputs received from consumers/providers | Outputs and guarantees provided |
|---|---|---|
| **AUC-01 Authentication policy** | Scoped, validated requirements for permitted authenticators, required assurance, session lifetime, risk throttling and reauthentication | Effective non-secret policy, version/provenance and explainable restrictions; never ownership of general Configuration settings |
| **AUC-02 Credential enrolment and management** | Opaque Identity principal reference, authenticated proof, method, verified challenge and authorised operation | Method metadata, enrolment/revocation status, one-time recovery material where applicable; no persisted secret exposed through routine reads |
| **AUC-03 Sign-in and challenges** | Sign-in identifier or trusted provider response, authentication proof, client context and bounded challenge reference | Unauthenticated failure, pending challenge or authenticated outcome with explicit assurance and timing |
| **AUC-04 Session and principal resolution** | Server-side request credentials or validated token, freshness/assurance requirements | Stable opaque authenticated-principal assertion, or deny/null with reason; never access rights |
| **AUC-05 Session and account revocation** | Session/principal reference, verified Identity lifecycle signal, authorised revocation instruction, correlation | Authoritative revocation decision, propagation/completion state and safe idempotent retry |
| **AUC-06 Step-up and recovery** | Existing authenticated context or recovery evidence, action-risk context, independent confirmation when needed | Renewed/rotated session or restricted credential recovery with actual achieved assurance; no false preservation of pre-recovery assurance |
| **AUC-07 Federation and provider connections** | Explicitly configured provider/trust rules, state/nonce-bound callback, verified issuer, subject, audience and protocol metadata | Mapped local principal only after verified or explicitly authorised linking; failure/reconciliation status; no implicit email-based linking |
| **AUC-08 Service authentication** | Identity-owned service ID, appropriately authorised credential-management instruction, service proof, intended audience/scope | Service-principal assertion or short-lived service token with bounded claims and expiry; no impersonation or human passkey assurance |
| **AUC-09 Security evidence and events** | Authentication-owned outcome and provenance, causal identifiers, emission requirements and retention class | Minimised typed events and receipt/replay/reconciliation evidence where guaranteed; delivery outcome distinct from authentication outcome |
| **AUC-10 Operational and data-subject services** | Authorised maintenance, export, legal restriction and data-disposal/recovery requests | Bounded retention/disposal results, classified subject export, safety/exception reports; no password verifiers or raw credential secrets in export |
| **AUC-11 Emergency authentication** | Identity-owned emergency-principal designation, separate approval evidence, secure enrolment and rotation requests | Passkey-only constrained authentication assertion and revocation/rotation outcomes; never independent emergency authorisation |

**Established implementation examples:** `AuthenticatedPrincipal` includes `principalId`, `kind`, `sessionId`, `authenticatedAt`, `expiresAt`, `assurance` and `standing`. The contract offers `getAuthenticatedPrincipal`, `requireAuthenticatedPrincipal`, `revokeAuthenticationSessions`, recovery and export functions, service-credential operations, optional `AuthenticationEvent` sink, client composable, HTTP routes and configurable presentations. Its errors expose stable `code` and `messageKey`, with OAuth-specific errors for the service-token route. Existing event delivery is explicitly **best effort**, and current host composition requires multiple `provideAuthentication*` registrations.

**Proposed evolution:** harmonise the Authentication host contract with ADR-0012's shared caller/access/mail/events/tasks/clock shapes, one composition call and the measured minimal-host budget; preserve the exact assurance, freshness, service-vs-person and fail-closed behaviour while adapting. Publish the required absence mode for each provider. Do not invent a second generic session, credential or trust broker.

## Cross-capability input/output and dependency matrix

| Peer | Authentication receives | Authentication supplies | Nature / ownership rule |
|---|---|---|---|
| [Identity](../identity/capability-record.md) | Opaque principal and service identity references; standing and verified lifecycle signals; emergency principal provisioning | Authentication result, credential recovery evidence, session revocation result, account clean-up acknowledgement | **Essential conceptual IAM relationship**; Identity owns principals and lifecycle, no direct private-code dependency |
| [Authorisation](../authorisation/capability-record.md) | Server-side decision for restricted credential management; resource-specific decisions remain in that owner | Authenticated principal, assurance, recency and request context | Essential to protected actions; no permission inferred from being signed in |
| Profile | Authorised presentation/contact delivery requirements where suitable | No ordinary personal-profile ownership; limited references/subject export for rights process | Optional contextual integration; Profile owns personal data |
| IAM integration | Suite composition, provisioning, recovery, account lifecycle choreography and adapters | Public Authentication assertions, revocation, export and recovery interfaces | Suite integration without circular imports or duplicated IAM records |
| Configuration | Validated effective scoped configuration and change provenance if adopted | Authentication-specific schemas, constraints and safe public effective policy | Proposed policy integration; Authentication validates and enforces security minima |
| [Audit](../audit/capability-record.md) | Configured evidence requirement, accepted producer and evidence acceptance/reconciliation contracts | Minimised outcome assertions, attempted/denied/succeeded distinctions, assurance and revocation provenance | Proposed; Audit owns evidential custody, Authentication owns fact/outcome and its outbox |
| Privacy / Legal Compliance | Applicable retention, disclosure, data-subject and legal-hold constraints | Classified authentication data inventory, permissible exports/disposal/exception evidence | Required policy constraints where applicable, no transfer of credentials or account ownership |
| Clock | Trusted current-time semantics | Timestamped authentication, expiry and freshness requirements | Shared time shape; Clock does not own session time policy |
| Notifications / mail | Host-provided delivery and optional channel preference | Authenticated notification request (verification, recovery, security notice), no assumption that sending confirms reading | Optional transport choice; secure delivery may be mandatory for an enabled recovery method |
| Message Queue / Scheduler | Optional execution/relay providers and scheduled maintenance trigger | Owned events/outbox relay and owned maintenance handler definitions | Transport/execution do not own Authentication facts or tables |
| Integrations / external IdPs | Verified provider assertion, trust metadata and transport status | Scoped federation request, outcome and verified local linkage | External account does not become authoritative Identity, tenant or permission record |
| Logging / Observability | Technical telemetry collection | Sanitised failures, health, performance and correlation | Diagnostic evidence is not Audit evidence |
| Presentation / Theme Manager | Optional semantic theme, language and layout configuration | Accessible, localisable, replaceable sign-in/security UI or headless contract | Presentation never enforces server-side security |

**Dependency constraint:** cross-capability relationships are not automatically package dependencies. IAM foundational packages remain independent and meet through the application's or IAM suite's public port composition. Verify the combined declared graph, including any Nuxt extension edges, is acyclic.

## Configuration, governance, security and privacy

**Established governance baseline:** OWASP ASVS 5.0 Level 2 minimum with relevant Level 3 requirements for security-sensitive operations, including Authentication; NIST SP 800-63-4 identity assurance guidance, phishing-resistant methods for elevated-risk accounts and privileged administration, secure cookies, expiry/rotation/revocation, anti-enumeration, CSRF/origin checks, least privilege, tenant isolation, server enforcement, classified personal data and necessary legal retention controls. `NIST SP 800-63B-4` governs authenticator lifecycle/assurance guidance and `800-63C-4` is relevant to federation; mappings do not themselves certify AAL compliance.

**Proposed policy partition:**
- **Mandatory security invariants:** trustworthy server verification, non-forgeable session state, explicit assurance freshness, strong isolation, no unauthorised access or privilege escalation, safe provider trust, credential secrecy, applicable minimum standards, emergency restrictions and attributable revocation.
- **Permitted organisation/tenant policy:** stricter assurance requirements, allowed authenticator families where lawful and technically justified, scoped session durations, recovery procedures, concurrency limits, threat/risk responses, federation allow-list and enrolment permissions.
- **Operational configuration:** trust boundary for reverse proxies, mail delivery, secret/key rotation, provider connectivity, health, expiry/maintenance, event/outbox relay, retention and recovery operations.
- **User preferences:** language, accessible presentation and optional trusted-device choice; these must not weaken mandatory assurance or override privileged risk policy.

**Open:** effective policy precedence across platform, tenant, group, application, risk class and resource action; lifecycle/versioning of policy changes; policy impacts on active sessions; reliable historical proof of applied policy. Configuration may manage declarations and scoped values, but Authentication must own validation of security meaning and enforcement. Legal Compliance/Privacy retain their own authority. An external security provider may supply evidence, not silently replace these owners.

**Privacy and resilience:** sign-in identifiers, recovery contacts, provider IDs, session metadata, IP-derived throttle records and user agents may be personal data; minimise, classify, retention-limit, avoid presenting them to unrelated tenants and never place passwords, session tokens, authenticator secrets, recovery codes or private keys in diagnostic/audit records. Preserve protected recovery under outage and incident response; back up authentication-owned records with appropriate key management without treating object storage for application images/files as authentication persistence.

**Trust and claims:** do not label a password-plus-remembered-device combination compliant AAL2 without checking the actual NIST requirements for the configured authenticator; do not equate a provider's self-reported MFA with locally verified phishing resistance. Distinguish authenticator strength, account recovery strength, session age, federation assertion strength, token binding and resource authorisation. External sign-in needs explicit trusted issuer/audience/nonces/state validation and careful linking/unlinking, with account takeover threat modelling.

## Integration modes and recovery of authority

- **Native mode:** local Authentication verifies accepted native authenticators, owns local sessions and supplies principal assertions without an external social or enterprise identity provider.
- **Federated mode:** external IdPs authenticate at their boundary; Authentication verifies the assertion under configured trust, maps it through an approved account-link relationship and issues/maintains the local session. The IdP does not own the local principal, application session, group graph or permissions.
- **Service mode:** service identities are established through Identity; Authentication verifies service credentials and issues bounded service authentication evidence. It does not mint a new independent service identity.
- **Headless mode:** all substantive operations remain available without Authentication pages or styling.
- **Emergency mode:** narrowly scoped, independently authorised break-glass identity using phishing-resistant authentication, with explicit enrolment, use, notification, expiry, revocation and post-use rotation.

Provider enabling, connection health, verified assertion, linked-account confirmation, local session issuance and authorised business action are distinct results. Switching providers or returning to native mode requires verified ownership and safe recovery; matching an email address cannot transfer local account authority. Suspended or closed Identity standing continues to constrain all modes.

## Conceptual acceptance scenarios

1. **Native person sign-in:** enrol an allowed authenticator, prove control, complete required second factor, receive a bounded local principal assertion, and gain no domain permissions until a separate Authorisation decision.
2. **Partial assurance:** password sign-in creates only the evidenced lower-assurance context; a protected operation requiring higher assurance fails until legitimate step-up; step-up rotates/refreshes applicable session evidence.
3. **Session expiry/revocation:** idle expiry, absolute expiry, selective logout, account-wide sign-out and Identity suspension each make further protected use fail; stale cache or asynchronous delivery cannot silently restore access.
4. **Federation:** a validated trusted provider assertion authenticates only its explicitly linked principal; unknown, mismatched, replayed or unlinked assertions do not create an accidental link; provider outage does not falsify local success.
5. **Account recovery:** an authorised recovery is bounded, auditable and does not magically inherit previous high assurance; other authenticators/sessions are retired or revalidated according to risk policy.
6. **Service principal:** an authorised service credential obtains short-lived service proof; cannot be used as a human passkey session, gain a tenant context by self-assertion or bypass a critical-resource decision.
7. **Break-glass:** two distinct stages of identity/governance approval and verified emergency authentication; successful use is attributable to the actual emergency identity, triggers rotation and produces appropriately protected evidence.
8. **Tenant and group isolation:** neither sign-in identifier, provider identity nor browser-supplied group/tenant causes cross-tenant access; protected resources are always rechecked by Authorisation.
9. **Audit failure:** an authenticated outcome remains accurately classified even if an optional best-effort event sink fails; where a policy mandates durable capture before a privileged action, the operation fails or follows a separately approved degraded-mode contract.
10. **Time and provider failure:** unreliable clock, invalid policy, missing mandatory service or ambiguous provider response does not grant authentication; failures expose safe and distinguishable codes.
11. **Privacy and data-subject lifecycle:** subject export omits credentials and secrets; retention and erasure are bounded by Privacy/Legal Compliance controls; lawful holds and restricted disposal are explicit.
12. **Headless accessibility:** host screens using public contracts preserve anti-enumeration, safe redirects, MFA, localisable messages and WCAG 2.2 AA; a presentation widget cannot substitute for server enforcement.
13. **Integration compatibility:** consume Authentication through published interfaces in a minimal host within governing composition budget after the documented ADR-0012 migration; no private imports or host-authored domain adapters.
14. **Concurrency and replay:** concurrent authentication, one-time challenges, backup codes, service credential rotation and revocation are race-safe and idempotent where appropriate; delayed events do not resurrect revoked state.

## Completeness challenge and unresolved decisions

| ID | Question | Assessment |
|---|---|---|
| AUT-01 | Must every host use the same minimum authenticator/assurance policy, and which stronger scoped overrides are allowed? | **Open** — preserve governing risk-based minimum and explicit treatment |
| AUT-02 | What evidence demonstrates federation-provider authentication strength, and how is local achieved assurance assigned? | **Open** — avoid unverified AAL elevation |
| AUT-03 | When does credential replacement/recovery invalidate other methods and sessions, including remembered devices? | **Open** — specify risk-governed revocation matrix |
| AUT-04 | What is the maximum tolerated revocation propagation delay from Identity and membership-related Authorisation changes? | **Open** — align fail-closed behaviour with IAM |
| AUT-05 | Which authentication events require durable capture, receipt and source reconciliation rather than today's best-effort sink? | **Open** — jointly reconcile with Audit and ADR-0012 outbox |
| AUT-06 | How are shared platform/tenant/group policies resolved and overridden without duplicate Configuration ownership? | **Open** — agree provenance, version and activation |
| AUT-07 | How are non-human identities, service tokens, workload identities and privileged automation classified for assurance? | **Open** — distinguish machine authentication from human AAL |
| AUT-08 | What is the complete concurrent-session and token/credential rotation policy, including logout/federated logout semantics? | **Open** — do not assert single sign-out from remote IdPs |
| AUT-09 | How are account recovery, suspected compromise and provider migration independently authorised and evidenced? | **Open** — account takeover and lockout scenarios |
| AUT-10 | What are binding baseline requirements for emergency access, operator separation, approvals and rotation? | **Open** — preserve accepted break-glass restrictions |
| AUT-11 | How are minimum privacy, retention, export, erasure and legal holds enforced across metadata, mail, IdPs and event delivery? | **Open** — jurisdiction-specific validation |
| AUT-12 | What exactly is the post-migration ADR-0012 shared public contract and acceptance evidence? | **Open implementation alignment**, not a reason to change conceptual ownership |

**Important gaps in the present root contract versus the conceptual target:** explicit session-concurrency maximum and behaviour; durable event/outbox guarantees; detailed cross-provider logout/reconciliation; a complete privilege/revocation propagation guarantee; trustworthy assurance mapping for external federation and remembered devices; host-independent composition; and proof of the operational/acceptance status. The present contract's `aal2` labels describe its published behaviour and are **not independently validated NIST conformance claims**.

**Industry reference points, not automatic legal obligations:** [OWASP ASVS 5.0](https://owasp.org/www-project-application-security-verification-standard/), [NIST SP 800-63-4](https://csrc.nist.gov/pubs/sp/800/63/4/final), [NIST SP 800-63B-4](https://csrc.nist.gov/pubs/sp/800/63/b/4/final), NIST SP 800-63C-4 for federated assertions, W3C WebAuthn/FIDO2 for passkey ceremonies, OAuth 2.0 security best current practice for bearer/service credentials, and OIDC Core for federation semantics. Map actual controls to exact published versions/requirements in the owning security programme; do not claim compliance or certification without evidence. UK GDPR and other legal duties require qualified applicability assessment.

## Review disposition and architectural consequences

**Established:** Authentication remains a Foundation (IAM) capability with its own state and contract. Current catalogue/register ownership text remains correct; no classification or governing ADR change is recommended. No implementation repository edits are authorised by this review.

**Proposed for conceptual approval:** adopt the eleven logical surfaces above, native/federated/service modes, ownership and failure invariants, conditional durable Audit integration and explicit policy resolution. Record reciprocal boundary notes in Identity and Authorisation without completing those separate reviews. An approved conceptual record does not certify the existing implementation or modify `Authentication` version `1`.

**Next work after conceptual sign-off:** a separate contract reconciliation and independent acceptance review for Authentication/IAM integration, with explicit revocation, assurance mapping, durable security evidence, privacy controls and ADR-0012 composition gates. Security and legal specialists must validate applicable regulatory and assurance claims. 

**Alphabetical sequence:** `authentication` follows `audit`; determine the next capability from the actual directory list rather than inferring that a related IAM capability is next.
