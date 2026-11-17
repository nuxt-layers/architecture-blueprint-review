# Online Safety and Content Governance — Cross-capability Blueprint Review

**Status:** Owner-approved conceptual findings for documentation, 17 November 2026. **Non-normative**; the current accepted `architecture-rules` and actual public `CONTRACT.md` remain authoritative. No implementation, compliance certification or new repository is approved.  
**Scope:** Public, semi-public and (where introduced) private messaging, marketplace activity, independent Nodes and Hub services.  
**Related:** [Moderation candidate](../docs/capabilities/moderation/capability-record.md), [Moderation pro-forma/report](../docs/capabilities/moderation/capability-report.md), [Node–Hub federation](node-hub-federation-architecture.md).

## Problem and legal applicability boundary

An ecosystem publishing articles, comments, images, forum posts, products, vacancies and federated discovery results must provide proportionate, measurable controls against illegal content and conduct, not merely a collection of scanners or an editorial approval button. The UK Online Safety Act 2023 duties vary by service classification (user-to-user, search/combined and other relevant services), functions, risk and audience, and do not mean that every flagged act is a priority offence or that all content must be proactively pre-screened. Legal Compliance must present qualified, source-verified applicability, applicable effective dates, service-specific obligations and regulatory-reporting duties; qualified legal review remains necessary. Operators retain statutory accountability: deployment of capabilities alone does not certify compliance.

**Risk taxonomy to maintain (with legal vs service-policy classification):** CSEA/grooming; controlling/coercive conduct; cyber-flashing; non-consensual intimate images including synthetic content; bullying, harassment and stalking; threats/incitement/hate offences; suicide/self-harm content; extreme sexual material; terrorism; fraud/phishing/scams; illegal-goods trading. Distinguish harmful but lawful conduct, evidence of suspicion, qualified illegality assessment and formal legal finding. Not all categories are legally identical.

**Regulatory reference review before implementation:** Ofcom illegal-harms risk assessment, Codes of Practice and implementation dates; child-safety duties, highly effective age assurance when applicable; applicable CSEA reporting and other statutory referral duties; section 121 notices and safeguards; UK GDPR/PECR and lawful evidence processing. This working review does not assert definitive duties for any particular future service. Reverify current law and guidance at deployment.

## Ownership matrix — separation of detection, case and enforcement

| Responsibility and authoritative records | Owner | What that owner must not take over |
|---|---|---|
| Drafts, revisions, publish/unpublish, addresses, approval state, published feed | Publisher | Detection classifier or external regulatory authority |
| Upload asset identity, metadata, transformations/variants, visibility, controlled delivery | Media with Storage for bytes | Case adjudication; ordinary gallery UI is not asset owner |
| Generic authoring/review screens | Content Editor, presentation only | Content and source lifecycle |
| Gallery/albums presentation | Gallery, presentation (Publisher/Media data) | Safety state or source bytes |
| Comments, threading, local comment visibility/moderation actions | Comments Engine | Cross-domain moderation cases and evidence custody |
| Scanning/technical classifier runs, policy-referenced detection verdicts and provider evidence | Content Security | Original content, final legal guilt, unrelated domain lifecycle |
| Reports, cross-domain cases, triage, decisions, appeal, action requests and reconciliation | **Moderation — candidate** | Source-content mutation or universal security scanning |
| Source listing and seller participation, seller restriction, marketplace commercial risk | Marketplace | Identity credentials, authoritative Product/Order/Payment state |
| Payments/transactions and fraud indicators | Payment Gateway / Order / domain owner | Market-wide case governance |
| Legal rules, jurisdiction and service classification, legal holds and statutory obligations | Legal Compliance | Domain writes; blanket claim of legal accuracy |
| Effective policy configuration and provenance | Configuration; owning domain interprets/enforces | All policy enforcement or universal legal interpretation |
| Access/identity/assurance and scoped delegations | Identity, Authentication and Authorisation | Moderation decisions and source ownership |
| Hub peer/subscription exchange, remote publication/withdrawal | Federation | Source Node business records, Search index ownership |
| Derived discovery index and ranking | Search, composed into Hub | Origin-source authoritative transaction |
| Trusted independent evidence intake, integrity, review and disclosure record | Audit | Raw source-content master, business decision or arbitrary evidence hoard |
| Technical failures/health and aggregate trend metrics | Logging, Observability, Reporting respectively | Authoritative legal determination or source case |
| Timed orchestration, notice delivery, specialist external gateways | Workflow, Scheduler, Notifications, Integrations | Source domain state, statutory report truth by default |

**Core invariant:** Content Security detects, Moderation evaluates cases, domain owners enforce changes, Legal Compliance provides qualified duties, Audit preserves attributable receipts and evidential integrity. A scanner detection, moderator decision, requested restriction and actually enforced removal are distinct outcomes.

## Publication, quarantine and enforcement

1. Authorised user/application submits to authoritative content owner (Publisher, Comments Engine, Marketplace, Media). Content Editor/Gallery merely render or submit through public interfaces.
2. Required pre-publication controls, risk policy and data minimisation determine pending/quarantine/review/eligible state. Media original and derived URLs remain protected until required clearance; no private object-store URL bypass.
3. Content Security assesses applicable inputs with provider/version, classification, confidence/limitations, timestamps and policy ID. External provider failures yield `unknown` with a risk-appropriate hold/review/allowed alternative, never false `clear`.
4. Where human/cross-domain review is needed, Moderation takes a reference to the content/revision, not unrestricted bytes, and records a case and qualified determination.
5. Authorised source capability executes hold, publish, remove or reinstate under its own invariant, including TOCTOU/revision checks. Moderation records request and separate confirmation/failure/unknown and coordinates retries. Critical immediate holds must work without a functioning Moderation service.
6. Domain-owned outbox events provide committed outcome signals; Audit accepts minimised attributable evidence independently; Reporting derives measurable statistics; Notification and disclosure follow scoped consent/statutory policies.
7. Appeals, correction, legal holds and expiry follow separate controlled lifecycles; publication refusal, case completion, evidence preservation and technical deletion never silently collapse into a single state.

**Prevent orphaned variants and external exposure:** Media's originals/derivatives, Publisher feeds, Search indexes, CDN/public caches and Federation Hub indexes must reconcile withdrawal. A domain hold is not proof that every cache/Hub has ceased serving the material; track receipts/freshness/expiry and surface discrepancies.

## Conceptual shared contract requirements

- Safety policy applicability: service/tenant/host/collection classification, audience/age risk, jurisdiction, source, effective version, mandatory/optional controls and unknown/fail-closed treatment.
- Source assessment request: trustworthy owner and resource ID/revision, visibility, content class, permitted material reference, sensitivity and expected decisions.
- Assessment result: provider/model/dataset version, detection category, confidence/provenance, explanation where possible, errors, uncertainty and effective period; no assertion of criminal guilt.
- Moderation case: reporter/source, grouped targets, restricted evidence references, severity, reviewer assignment, bounded decision, versioned policies, protective steps, appeal and status.
- Enforcement: authorised requester, exact target/action/revision/expiry/idempotency, domain-source receipt, actual state/result and error/unknown code.
- Evidence: stable correlation/source event IDs, actor role and assurance, receipt timestamps, source revision, decision/appeal versions, disclosure authority, retention and complete/missing outcomes.
- Registry of specialist provider abilities: detection scope, supported languages/modalities, data processing locations/purposes, applicable licences, assurance, service costs, timeouts, fallback, monitoring and provider exit.

No fixed API types or universal mandatory service are imposed by these conceptual surfaces; preserve ADR-0012 and ADR-0016 directional public contracts.

## Private communication and confidentiality

Public/semipublic publications can normally be assessed by the hosting service, but a closed group is **not automatically outside UK OSA scope**. E2EE messaging, if implemented, requires distinct threat model and operational requirements. Prefer user-driven reporting, local safety settings, blocking and abuse-resistant account controls. Do not mandate universal client-side hash matching of private plaintext or introduce silent backdoors as a safety prerequisite; hashes and client scanners introduce endpoint abuse and privacy risks. Cryptographic message franking may be evaluated for authenticated reports but is not assumed to prove illegality. On-device nudity blurring can be optional and local, with accessibility protections. Section 121 technology-notice duties must be assessed separately with qualified statutory analysis, not guessed as a universal exemption.

## Fraud, verification and marketplace safety

Identity is not equivalent to merchant eligibility. Separate human/company identity evidence, authority to represent a merchant, seller-participation standing, listing legality, transaction risk and payment/escrow provider outcomes. Marketplace owns seller participation and listing restrictions, Identity/Authentication/Authorisation establish local principals/access, Product owns product facts, Order owns accepted orders, Payment Gateway owns payment/provider evidence. Provider-specific KYB/KYC, anti-fraud and phishing signals should arrive through verified specialist interfaces and scoped adapters. Do not require universal KYC or blockchain smart-contract escrow purely under the Online Safety Act. Escrow, if ever added, needs separate regulated-service/payment and dispute review.

## Nodes and Hubs

Originating Node remains authoritative for its resources, publication and local user/merchant sanctions. A Hub Node is independently accountable for its own derived index, search results, peer participation and local moderation policy. Hub may suppress its own index item/peer without deleting origin content. Origin withdrawal and Hub removal are independent states, with delayed/missing acknowledgements visible. Shared signed threat/malicious-URL/peer feeds are attributed, expiry-controlled input evidence, not obligatory consensus or self-validating proof. Guard against malicious/incorrect blocklisting, rogue peer reports, content laundering, index poisoning and stale or misleading public commerce results. Hub regulatory classification may differ from an origin Node and needs independent applicability review.

## External services, costs, privacy and failure

Provider-neutral adapters may be needed for known-illegal-image hash datasets, NCII services, text/video/image classifiers, URL threat intelligence, age assurance, merchant verification, fraud detection and legal submission gateways. Qualify vendors, lawful sharing/bases, operator access, retention, processing locality, dataset limitations, response quality, contract/price, audit evidence and exit routes. Do not copy extremely sensitive content broadly to unvetted services. Mandatory safeguards are not silently disabled upon budget exhaustion; record charge attribution without embedding sensitive content in financial records. Failure policy is domain- and risk-specific: hold, alternate approved review, deny or indeterminate as appropriate.

## Quantified evidence and operational dashboards

Define scoped, measurable indicators: applicable submission assessment coverage (numerator/denominator), detection and exposure latency, confirmed enforcement lag, high-risk backlog and age, appeal timeliness/reversal, false-positive estimation, service/provider failures and fallbacks, regulatory referral status, evidence gaps, downstream Hub/cache withdrawal acknowledgements. Counts alone and 100% scan coverage do **not** establish accuracy or legal compliance. Audit owns accepted evidence receipts and integrity; Reporting derives authorised metrics and historical dashboards; source owner is authoritative about actual enforcement.

GUI pattern: host-owned sidebar to capability dashboards, with Mod queue/detail/appeals and restricted evidence, Content Security scanner results/provider health, Publisher/Media/Marketplace source-specific review, operator-level risk assessment/reporting, and Hub peer/index action views where relevant. Server-side authorisation and step-up for sensitive access, low-bandwidth accessible (WCAG 2.2 AA) and internationalised UX; headless capabilities need not acquire business-state-owning UI.

## Statutory reporting and security incidents

Legal Compliance qualifies reporting duty, scope, recipients, deadlines and disclosure constraints. Moderation coordinates case-linked disclosure preparation and approvals. A designated reporting record owner (to be decided) owns authoritative submission state; Integrations handles transmission/acknowledgement without assuming report truth; Audit preserves minimised evidence and provenance. Separate general cybersecurity incident handling (compromise, phishing infrastructure, malicious software, infrastructure attacks) from content/conduct case moderation; Authentication, Authorisation, Logging and Observability retain their responsibilities.

## Acceptance scenarios and unresolved decisions

1. Safe publication flow from Content Editor/Media/Publisher, with quarantine until applicable mandatory review outcome; no visible derivative or cached bypass.
2. Domain owner continues immediate emergency hold when Moderation or an external scanner is unavailable; required unknown results never become clearance.
3. Automated detection yields scoped referral with policy/version and provenance but no automatic statement of criminal guilt.
4. One case spans multiple comments/media/listings; each authoritative owner executes its own action and returns independent receipt.
5. Appeal reverses mistaken moderation and source recovery is confirmed; Audit preserves correction history.
6. External detector unavailable or too costly: approved risk-specific fallback with disclosed gap and no silent disabling of required checks.
7. Federation Hub and source Node disagree: Hub suppresses only its derivative; originating Node preserves local independence, withdrawal propagation is tracked.
8. Regulator reporting occurs only on validated applicability and authorised disclosure; transmission failure and legal hold remain observable.
9. Private E2EE reports have tightly limited, user-initiated evidence disclosure without routine operator access to messages.
10. Host dashboard metrics and evidence prove denominator, decision time, actuation and outstanding exceptions without exposing sensitive material.

**Open:** formal service-by-service OSA scope and Ofcom code version; independent case vs comment-specific moderation owner; legal filing owner; evidential custody of high-risk imagery; age assurance standards; identity/KYB ownership; acceptable scan provider disclosures; trust feed appeal; source-to-Hub withdrawal guarantees; public policy vs technical enforcement versioning.

## Disposition

Approve the conceptual responsibility map and create `moderation` as a **candidate** in this working blueprint only. Add reciprocal review notes to affected capability records; defer runtime design, legal assurance and any governing ADR amendments pending full architectural review. Preserve original capability ownership and the current latest accepted governing authority.
