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

## Conceptual presentation and application navigation — 15 November 2026

**Status:** Existing pages and components are documented by the published [Authentication root `CONTRACT.md`](https://github.com/nuxt-layers/authentication/blob/ffb92d8c033ebb8bcb5043e3fa5acadac9e1d825/CONTRACT.md); additional dashboard, user journeys and operator surfaces below are **proposed**, not claimed implemented. No routes, component names or authorisation APIs are invented beyond the contract.

### Representative host presentation pattern

**Verified reference:** `nuxt-layers-test/application-test-template` `master` at `8b7b142b84b5ec2379d4e2e727914fe344187d64`. Its `README.md`, `nuxt.config.ts`, `app/app.vue` and relevant public application-shell components demonstrate a separate public home page (`/`), local administration dashboard (`/admin`), shared responsive/collapsible side navigation with a **Capabilities** group and a link to the Theme Manager (`/theme-manager`). The application owns the navigation, branding, appearance control, header, content shell and active-link/mobile behaviour. Its authentication-status indicator explicitly says **Not signed in** and is not a functioning Authentication integration. Its Theme Manager **test** mode is unauthenticated and must never be assumed suitable for production.

**Proposed Authentication integration:** A derived test application (not the shared template itself) explicitly composes Authentication through its published contract and, after sign-in, offers a **Security / Authentication** item in the same host-owned **Capabilities** sidebar leading to a capability overview at a host-chosen path (illustrative `/authentication`). An optional card on `/admin` provides the same entry. This is an application navigation decision, **not** a new automatic registration mechanism, mandatory route or reason for Authentication to depend on the shell. Capability overview and management views should open in the existing shared content area and use the host's trusted viewer/context; a menu item must not imply permission.

**Crucial two-context distinction:** public/anonymous sign-in, sign-up, recovery, second-factor challenge and emergency enrolment screens must be usable **without first entering an authenticated administration shell**. The host may present them in a public/minimal access layout. Once authenticated, personal security settings can be accessed from a user/account menu as well as an optional sidebar entry. Privileged credential/service and policy management must be separately authorised; do not put service secrets, emergency credentials or all-tenant controls on an ordinary account security dashboard.

### Existing published screens and components

The current contract describes **optional, configurable** presentation with `presentation: false` (no capability pages/components) or `pages.enabled: false` (components only), plus host-moveable routes:

| Existing screen key | Current contract default route | Primary audience and purpose |
|---|---|---|
| `signIn` | `/sign-in` | Anonymous person: password, passkey, federated sign-in, challenge progression |
| `signUp` | `/sign-up` | Prospective person: initiate approved sign-up and verification |
| `forgotPassword` | `/forgot-password` | Anonymous claimant: request non-enumerating recovery |
| `resetPassword` | `/reset-password` | Holder of valid bounded recovery proof: complete password reset |
| `mfa` | `/mfa` | Signed-in/partly authenticated person: enrol or complete second factor/step-up |
| `security` | `/account/security` | Authenticated account holder: manage password, TOTP, backup codes, passkeys, provider links and personal sessions |
| `breakGlassEnrol` | `/break-glass/enrol` | Specifically designated operator: one-time emergency passkey enrolment using the approved restricted process |

**Established reusable presentation pieces** include `AuthenticationSignInForm`, `AuthenticationSignUpForm`, `AuthenticationForgotPasswordForm`, `AuthenticationResetPasswordForm`, `AuthenticationMfaPanel`, `AuthenticationTotpEnrolment`, `AuthenticationBackupCodes`, `AuthenticationReauthenticate`, `AuthenticationSecuritySettings`, `AuthenticationBreakGlassEnrolment`, `AuthenticationProviderButtons`, `AuthenticationField` and `AuthenticationAlert`. The public `useAuthentication()` client contract includes sign-in/out, passkey/provider/MFA operations, session listing/revocation and provider linking; those functions do not establish any undisclosed administration screen. The contract offers no evidence of a published unified Authentication dashboard, tenant-wide service-credential console, security-policy editor or audit investigator console. **Implementation/rendering and host acceptance remain unverified.**

### Proposed screen inventory and journeys

The following are conceptual screen purposes; names and paths are illustrative and **not implemented** unless expressly listed in the existing screen table above.

| Proposed screen or journey | Audience / permissions | Information and presentation responsibilities | Status |
|---|---|---|---|
| **Authentication overview/dashboard** | Authenticated viewer, scoped to their account; optional separately authorised operations overview | Clear personal security posture, enrolled methods, active-session summary, recent important security notices, actionable warnings and links to existing settings; avoid implying that locally authenticated means authorised for every app resource | **Proposed** |
| **Personal account security** | Account holder, with fresh reauthentication for sensitive mutations | Existing `/account/security` functions: credential management, linked providers, MFA, backup codes and own-session revoke controls; one-time recovery material never appears again after display | **Existing contractual screen**, conceptual presentation refinement |
| **Sessions and recognised devices** | Account holder | Session list, last activity where available, current-session identification, revoke one/others, expiry and unknown-session response; no cross-tenant leak | **Existing in security page/client surface**; a separate screen is **optional proposal** |
| **Authenticator and account recovery** | Account holder, or constrained unauthenticated claimant as appropriate | Status of passkeys/TOTP, backup-code regeneration, recovery verification and clearly separated pending/succeeded/expired steps; do not elevate recovered sessions without proof | **Existing functions/screens**, improvements **proposed** |
| **Federated account links** | Account holder | Trusted providers and linked accounts, explicit link/unlink confirmation and provider errors; email equality does not authorise linking | **Existing functions/security screen**, presentation refinement **proposed** |
| **Service-identity credential management** | Separately authorised service-identity managers in the owning group; elevated recent authentication required | List/issue/rotate/revoke service credentials, show newly issued secret once, group scope, expiry and revocation status; never offer unrestricted all-tenant views | **Proposed standard operator UI**; existing contract documents server/HTTP services but not a supplied screen |
| **Authentication policy and provider configuration** | Appropriately privileged tenant/application operators, subject to host governance | Effective required assurance/MFA and session policy, allowed providers and policy provenance, safe status/validation and controlled change workflow; secrets must not be displayed through public config | **Proposed**, may be a Configuration/host-owned management presentation rather than Authentication-owned UI |
| **Security-event overview and operational health** | Authorised security operators | Sanitised sign-in and revocation trends, throttling/provider outages and event-delivery degradation; link to Audit for evidential review and Logging/Observability for diagnostics, without copying their authoritative records | **Proposed integration view**, not Authentication-owned Audit/Logging UI |
| **Emergency access enrolment and use** | Individually designated emergency operator and separate authorised approvers | Existing restricted enrolment, explicit warnings, bounded activation, post-use rotation and evidence; keep emergency governance/approval with IAM/Authorisation | **Existing enrolment screen**; wider operator journey **proposed** |
| **Presentation-disabled / bespoke host UI** | Application designers | Reuse protected public client/server contracts without installing capability screens or duplicated enforcement; support components-only or entirely headless composition | **Existing documented modes** |

**Minimum proposed reusable experience:** retain the seven existing optional routes and account-security components; supply an optional **Authentication overview** as a capability landing screen where useful, reusing existing personal security functionality rather than duplicating it. Separately consider a genuinely authorised **service-credential management** presentation. A generic Authentication dashboard is *not* a prerequisite for sign-in and should not block independent native/headless operation.

### Screen-to-capability responsibility and access boundaries

- **Host application:** selects whether Authentication is composed, whether its optional presentation is enabled, routing/location, sidebar and user-menu placement, capability card, branding, responsive shell, localised navigation text and trusted server caller context. A capability must not modify the application's global sidebar implicitly.
- **Authentication core:** validates credential and session operations and assurance/freshness requirements on the server; supplies only safe, documented personal/session/credential data and status to presentation. Sign-in success never grants privileged management permission.
- **Identity and IAM integration:** own principal standing and cross-capability lifecycle choreography. A security page must not expose membership, tenant administration or personal-profile records as Authentication-owned data.
- **Authorisation:** decides resource-specific permissions for service credentials, privileged policy access, emergency controls and evidence views. Hiding a sidebar item is not enforcement; direct-route/API requests must fail closed independently.
- **Audit versus Logging/Observability:** Audit owns accountable security evidence; Logging owns operational diagnostics/correlation; Observability owns health/traces/metrics. Authentication may display authorised, minimised summaries through public contracts but cannot become a competing record store or investigation console.
- **Configuration/Privacy/Legal Compliance:** effective policy, provenance, notices/retention and holds must be obtained from the appropriate owner; a screen may explain them but cannot authoritatively redefine those owners' rules.
- **Theme/accessibility/internationalisation:** reuse published Theme Manager semantic presentation vocabulary and optional generic `ui` components; do not require Theme Manager for the headless core. Follow WCAG 2.2 AA, keyboard/screen-reader support, responsive mobile presentation, focus management after route/challenge changes, accessible errors independent of colour, reduced motion and host locale/message override behaviour.
- **Safe disclosure:** consistent masked/non-enumerating recovery outcomes, no credentials/cookies/tokens in screen URLs or telemetry, one-time display for backup codes/new service secrets, fragment-based break-glass enrolment token, reauthentication before sensitive changes, strong confirmation of revocation and safe provider redirects. Empty, loading, partial-assurance, account-restricted, rate-limited, stale, provider-failed and unavailable states must be explicit and recoverable without unverified success.

### Conceptual host acceptance scenarios

1. A test-host sidebar shows an explicitly selected Authentication capability entry and optionally an `/admin` card, and opens a capability landing page inside the existing shell; installation alone adds no navigation.
2. A signed-out visitor can reach sign-in, sign-up, password recovery and second-factor completion without first being authenticated into `/admin`. The host's previously static authentication-status placeholder is replaced only by consuming the published Authentication interface.
3. A signed-in person reaches their personal security page from the account menu or permitted sidebar, lists/revokes only their own sessions, manages verified methods, and reauthenticates for protected changes.
4. A person without service-credential management rights cannot see privileged controls or invoke their underlying endpoints directly; a recently authenticated authorised operator can act only within an appropriate service identity's owning-group scope.
5. Enabling `presentation: false` preserves full headless capability operation; components-only and relocated-route modes behave as described in the public contract.
6. Anonymous/partial-assurance, unavailable provider, expired challenge, revoked session, blocked account, unknown recovery identifier and expired break-glass token states fail safely and do not disclose secrets or falsely imply success.
7. Keyboard-only and screen-reader users can traverse sidebar, public authentication flows, method-management and confirmation dialogs; mobile layouts, focus order, light/dark contrast and localisation meet accepted baseline requirements.
8. No user, operator or host can obtain cross-tenant account/security, service credential or Audit evidence from client-supplied identifiers, hidden navigation or an unguarded direct URL.
9. Derive the implementation acceptance app from `nuxt-layers-test/application-test-template` rather than changing that common reference template; verify independently through CI/user acceptance at the later implementation stage, with ADR-0012 single-call/50-line host budget preserved.

**Review disposition:** This presentation addition is a **non-normative concept and existing-contract inventory**. It does not authorise new Authentication APIs, automatic menu registration, an Authentication implementation change, a new generic dashboard capability or a change to the shared application-test-template. Detailed layouts, route choice, component architecture and tests belong to subsequent design/implementation.

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

## Agreed conceptual directions — 15 November 2026

**Review decision:** The platform owner agreed the recommended directions for AUT-01–AUT-10 and AUT-12, and explicitly approved AUT-11 on the five privacy/retention principles below. These are *conceptual directions*, not verified implementation, a published contract revision or amendments to governing ADRs. Detailed acceptance thresholds and qualified legal/assurance validation remain to be specified.

| ID | Agreed conceptual direction |
|---|---|
| AUT-01 | Maintain a mandatory platform assurance/security floor; permit stricter scoped tenant, application and operation policies, never weaker mandatory protections. |
| AUT-02 | Derive achieved authentication assurance from independently verified evidence and trusted methods; do not promote an external provider's unverified MFA assertion. |
| AUT-03 | Adopt a risk-based credential/session revocation matrix; suspected compromise and high-risk recovery invalidate affected credentials, sessions and remembered-device trust. |
| AUT-04 | Security-critical operations require immediate authoritative denial after applicable revocation; other consistency intervals must be explicit and measurable, never presumed. |
| AUT-05 | Adopt an Authentication-owned durable security-event outbox for significant authentication and credential lifecycle events, reconciled through the owning public contract with Audit; event transport does not establish business success. |
| AUT-06 | Configuration manages scoped setting declarations, values and precedence where its published contract permits; Authentication validates and enforces authentication-specific security meaning and constraints. |
| AUT-07 | Define service/workload authentication assurance separately from human AAL claims; service tokens cannot impersonate people or claim phishing-resistant human authentication. |
| AUT-08 | Provide configurable, bounded session concurrency, secure credential/session rotation and reliable local logout; disclose limitations and reconciliation needs for federated logout. |
| AUT-09 | Account recovery, compromise response and provider migration require independently verifiable, risk-appropriate authorisation, evidence and account-linking safeguards. |
| AUT-10 | Preserve restricted, phishing-resistant emergency authentication with independent approval/governance, attributable use, post-use rotation and separation from ordinary permissions. |
| AUT-11 | Apply the five approved privacy and retention principles immediately below. |
| AUT-12 | Retain ADR-0012 without amendment; separately migrate Authentication to a single documented composition call, shared caller/access shapes, a minimal independent host and verification of the 50-line budget without weakening assurance or fail-closed behaviour. |

### AUT-11 — approved privacy, retention and legal-hold principles

1. **Data minimisation:** Authentication collects and retains only the personal information needed for documented authentication and security purposes.
2. **Configurable retention:** Different information classes have justified retention periods, configurable within mandatory security and legal constraints, coordinated with Privacy and Legal Compliance.
3. **Coordinated account closure:** Identity/IAM integration orchestrate closure; each owning capability independently disposes of, anonymises or lawfully retains its own records through published contracts. No direct cross-schema deletion.
4. **Legal holds:** Preserve only records subject to a valid, applicable restriction, with limited access, review, expiry or release and no blanket indefinite retention.
5. **External services:** Document disclosures, relevant provider responsibilities and deletion/retention obligations; never claim third-party erasure without confirmed evidence.

**Security invariant:** Routine personal-data exports and Audit submissions must not include password verification material, authentication secrets, private keys, bearer/session tokens or recovery codes. Necessary retained credential-verification material remains protected and is disposed of under the credential lifecycle.

**Outstanding detailed design rather than unresolved ownership:** Agree exact revocation timing/guarantees, which Audit events require durable acknowledgements, assurance evaluation against the applicable NIST release, policy precedence, retention periods and legal applicability, incident recovery proofs, minimal host acceptance and public-contract compatibility in separately authorised implementation work. No universal Audit dependency, invented interface or normative amendment follows automatically.

## Review disposition and architectural consequences

**Established:** Authentication remains a Foundation (IAM) capability with its own state and contract. Current catalogue/register ownership text remains correct; no classification or governing ADR change is recommended. No implementation repository edits are authorised by this review.

**Agreed conceptual directions:** the eleven proposed logical surfaces, native/federated/service modes, ownership and failure invariants, durable Authentication security-event ownership, policy resolution and AUT-01–AUT-12 directions are approved for conceptual purposes; the specific APIs and performance/assurance claims remain unverified. Reciprocal notes preserve related capabilities' separate incomplete-review status. An approved conceptual record does not certify the existing implementation or modify `Authentication` version `1`.

**Next work after conceptual sign-off:** a separate contract reconciliation and independent acceptance review for Authentication/IAM integration, with explicit revocation, assurance mapping, durable security evidence, privacy controls and ADR-0012 composition gates. Security and legal specialists must validate applicable regulatory and assurance claims. 

**Alphabetical sequence:** `authentication` follows `audit`; determine the next capability from the actual directory list rather than inferring that a related IAM capability is next.


## Cross-capability note — Tenancy, policy and commercial onboarding (16 November 2026)

**Status:** ORG-01–ORG-08 owner-approved conceptual direction; TEN/COM/OWN and policy refinements proposed pending governing review, not implemented interfaces.

Trusted subject standing, sufficient assurance, recency and phishing-resistant step-up for protected organisation creation, new owners, ownership recovery, policy changes, payer changes and sensitive commercial operations. Credentials and session recovery must not itself confer legal-company authority or transfer Identity ownership. Incomplete/unverified claim fails closed.

**Conceptual interfaces and acceptance:** [tenancy/governance](../../proposals/organisational-tenancy-and-governance.md), [commercial onboarding](../../proposals/commercial-onboarding-and-entitlements.md), [policy boundaries](../../proposals/policy-and-governance-boundaries.md), [hostile-administrator recovery](../../reviews/organisational-ownership-and-recovery.md). Review relevant input owners, authoritative outputs, absence, revocation and evidence here during this capability's full alphabetical review; no package dependency inferred.

## Reciprocal note — trusted UTC assurance and expiry after clock adjustments (17 November 2026)

**Approved Clock conceptual boundary; Authentication implementation unchanged.** [Clock's CLK-03/CLK-04 review](../clock/capability-record.md#final-completeness-review--eight-concerns-resolved-17-november-2026) distinguishes an instant from proof that the current server clock is sufficiently assured. Authentication continues to own session/credential validity, expiry, step-up and fail-closed security decisions; the host/Infrastructure must supply approved trusted UTC and independently check relevant assurance state. Stale/unverified health cannot silently authorise access; a backward wall-clock correction must not automatically resurrect expired or revoked sessions. Monotonic elapsed-time measurements may be used for local timeout budgets but are not durable UTC expiry timestamps. This note does not revise Authentication's published root contract or invent a shared runtime package.


## Online Safety and Content Governance — reciprocal conceptual note (17 November 2026)

**Status:** Review-approved documentation direction, not an implemented interface or governing ADR. See [safety review](../../../reviews/online-safety-content-governance.md) and [Moderation candidate](../moderation/capability-record.md).

Authentication owns credentials, sessions, assurance, and phishing-resistant protection, not merchant eligibility or moderation. Sensitive moderation and evidence access should require bounded authentication assurance and recency. Proposed privacy-preserving age assurance must verify issuer, credential evidence, freshness and resistance to transfer; no default trust in a ZKP token solely because it is cryptographic.


## Identity, Age and Eligibility Assurance — reciprocal conceptual note (17 November 2026)

**Status:** Owner-approved cross-capability review direction only, not a changed published contract or accepted ADR. See [dedicated assurance review](../../../reviews/identity-age-eligibility-assurance.md).

Authentication owns authenticator/session proof, session assurance, method and freshness; this is distinct from age threshold proof, civil identity proofing and merchant standing. A privacy-preserving age or identity credential requires qualified issuer trust, claim/audience binding, replay resistance, expiry/revocation and accessible fallback. Never treat a cryptographic signature, provider callback or successful authentication as age, legal representation or access permission.


## Verification candidate — reciprocal boundary (17 November 2026)

**Conceptual only:** VER-01–VER-12 approved in [Verification's record](../verification/capability-record.md); see [jurisdiction comparison](../../../reviews/verification-international-jurisdictions.md). No new implementation, published API or governing ADR.

Verification candidate owns proofed attributes and trusted issuer attestation lifecycle; Authentication retains credentials, sessions, authenticator assurance and sign-in recency. Signed external identity/age proof does not automatically authenticate a session or create elevated credential assurance. Provider-neutral status/expiry and replay/holder-binding decisions must remain explicit.

## Comments Engine — reciprocal conceptual proposal (17 November 2026)

**Status:** Proposed for owner review in [Comments Engine PR #52](https://github.com/nuxt-layers/architecture-blueprint-review/pull/52); not an accepted public contract. See [conceptual record](../comments_engine/capability-record.md).

Comments Engine must consume trusted session/subject assurance and recency where risk requires, never authenticate from client-supplied names or treat successful login as permission, age proof or safety clearance. Guests/pseudonyms require explicit policy and traceable, minimised provenance. Authentication owns credential/session state; Comments Engine owns authored attribution references and comment lifecycle.


## Configuration reciprocal interface — 17 November 2026

**Status: Proposed, non-normative, pending Configuration PR #53 approval.** [Configuration conceptual contract](../configuration/capability-record.md#idealised-public-inbound-interfaces). Authentication owns assurance, recency, MFA and sessions. Configuration may supply approved bounded policy selections, but never weakens mandatory floors or decides how existing sessions are handled; high-risk settings changes require independent effective assurance checks. Cooperate via public host-composed ports/events; no mandatory new package import or cyclic dependency. Preserve existing owner approvals.


## Reciprocal conceptual note — IAM Integration (18 November 2026)

**Status: Proposed under [IAM Integration draft PR #73](https://github.com/nuxt-layers/architecture-blueprint-review/pull/73); not a new published implementation contract or owner approval.** Authentication remains authoritative for credentials, verified sessions/assurance, reauthentication and session revocation. IAM Integration consumes its trusted principal, recency, phishing resistance, recovery and revocation outcomes; it supplies Identity provisioning/service-governance/hold adapters through public contracts. The proposed common caller interface must preserve risk, assurance and session continuity; legacy best-effort delivery requires alignment with source-owned durable events. See [IAM Integration conceptual public contract](../iam_integration/capability-record.md).
