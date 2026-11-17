# Verification and Assurance — International Jurisdiction Comparison

**Status:** Conceptual research note, 17 November 2026; not legal advice and not a legal classification of a particular Node, Hub or operator. Local counsel and current primary legislation must establish actual deployment applicability.  
**Related:** [Verification candidate](../docs/capabilities/verification/capability-record.md), [Identity, Age and Eligibility Assurance](identity-age-eligibility-assurance.md).

## Purpose

Compare the design pressures of **China, Russia and Saudi Arabia** for verification and age/merchant eligibility. Differentiate a credential's technical interoperability, proofing effectiveness, national legal obligations, lawful processing and geographical deployment. **No standard, government connector or paid provider is selected.**

## Comparative working matrix

| Jurisdiction | Verified identity ecosystem | Age and minors safeguards | Residency/data protection and commerce | Implication for our provider-neutral architecture |
|---|---|---|---|---|
| China | National internet identity authentication service began July 2025, with online identity numbers/credentials and qualified disclosure; separate services must comply with applicable real-name duties | Sector-specific minors obligations such as age-linked livestream publisher restrictions, parental consent and age attributes | Personal Information Protection Law, data-security and cross-border rules; anti-fraud controls; assess host/provider operation | Adapter for lawful national identity and qualified age attributes, avoid raw documents and distinguish legally mandated real-name checks from voluntary national credential use |
| Russia | Gosuslugi and other national digital identity mechanisms; requirements vary by type of service; MAX age-check mechanism recognised by late-2025 legislation | Law 436-FZ age classifications and service-specific controls; do not claim universal live age check on all sites | 2025 tightened Russian citizen personal-data localisation requirements; cross-border impact and service operation must be specifically reviewed | A foreign-hosted Node must not assume lawful operation merely because signed national identity evidence is accepted; separate residency and service obligations |
| Saudi Arabia | National digital identity through Nafath, Absher and related services; approved government/private app verification | National digital identity can support identity-backed age-check flows, while exact age mandates depend on goods/service category | PDPL and e-commerce/merchant registration obligations; commercial bank/merchant verification can be relevant | National provider adapter yields only permitted qualified claims; keep merchant eligibility and age access separate, do not assume ZKP or anonymous outputs |

## Source evidence and dates

### China

- **Measures on the Management of the National Internet Identity Authentication Public Service**, effective 15 July 2025. Official CAC: https://www.cac.gov.cn/2025-05/23/c_1749711107835487.htm . The public service distinguishes network identity numbers/credentials from plaintext civil identity, provides for voluntary application and use in the statutory framework, limits extra plaintext collection in defined circumstances and can provide age indicators for minors/elderly. See Law Library of Congress: https://www.loc.gov/item/global-legal-monitor/2025-07-09/china-centralized-internet-id-system-officially-launched/
- **Protection of minors online** contains service-specific verification and guardian provisions; the source legal scope should be reviewed before assuming broad applicability: https://www.chinalawtranslate.com/en/online-protection-of-minors/
- Architectural inference: signed/qualified attribute results can minimise service-level disclosure without eliminating real-name obligations where law imposes them. Do not infer universal anonymity, provider availability to overseas Nodes or unrestricted cross-border data transfers.

### Russia

- **Law 436-FZ** regulates age-related information classification. **Law 149-FZ** includes duties for certain online information and social network services; exact coverage differs by service: https://agegating.org/ru and https://www.consultant.ru/document/Cons_doc_LAW_61798/ .
- **Federal Law 569-FZ, 29 December 2025**, recognises an age-check mechanism associated with the MAX multifunctional messenger (verify actual service availability, permitted integration and effective requirements): https://base.garant.ru/483423156/
- **Personal Data law amendments, 2025** strengthened localisation of Russian citizens' personal data on collection; qualified interpretation, exceptions and lawful cross-border flows remain service-specific: https://epam.ru/en/media/view/lokalizaciya-personalnyh-dannyh-i-osobaya-kategoriya-subuektov
- Architectural inference: transportable attestations cannot override rules about where a Node's personal-data processing/storage may lawfully take place.

### Saudi Arabia

- **National digital identity / Nafath / Absher:** Saudi official government information https://my.gov.sa/en/content/165 and https://my.gov.sa/en/services/20936 . National identity-backed authentication may be integrated with permitted government and private sector services.
- **Personal Data Protection Law:** official SDAIA guidance https://dgp.sdaia.gov.sa/ . **E-Commerce Law:** https://misa.gov.sa/app/uploads/2025/07/E-Commerce-Law.pdf ; commercial verification example: https://mc.gov.sa/en/mediacenter/News/Pages/03-09-23-01.aspx
- Architectural inference: verified identity, verified age for particular commercial products and merchant standing are separate claims; Nafath does not imply zero-knowledge/non-disclosing tokens in every provider integration.

## Shared design conclusions

1. **Issuer/protocol adapter** is different from **legal applicability**. Legal Compliance qualifies which scheme, evidence quality, identity/age requirement and data handling is mandated for the specific service, audience, region and operator.
2. **Evidence-minimising outcomes** are preferable where lawful; do not assume they can replace real-name verification, retained records, disclosure or national registration legally required in particular circumstances.
3. **Local independent decision:** a Hub's trust in a national issuer is not transitive to all other Nodes; each Node checks issuer, audience, subject binding, assurance, freshness, revocation and applicable restrictions.
4. **Deployment residence is independent of proof validity:** a Hetzner VPS/Coolify deployment cannot be assumed suitable for every jurisdiction; residency, restricted cross-border transfers and national connectivity must be evaluated separately.
5. **No single global provider:** permit independent adapters and sensible alternative methods. Conformance to W3C/OpenID standards is not proof that an issuer's age estimation or business proofing satisfies local statutory requirements.
6. **Recheck on change:** document expiry, provider compromise, legal mandate changes, officer revocation and high-risk actions, without turning status checks into cross-platform tracking.
7. **Ethical safeguards:** limit surveillance and linkability, preserve accessible recourse, forbid automatic rights derived from provider claims, and make denial and failed verification explainable at appropriate security-sensitive granularity.

## Open verification items

Confirm official current legal text, service categorisation, enforcement dates, national provider onboarding and availability, legitimate international transfers, local hosting restrictions, child safeguards, proofing accuracy/accreditation and retained evidence obligations separately for each intended deployment. This comparison is research, not certification.
