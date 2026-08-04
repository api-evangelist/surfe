# Surfe (surfe)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Surfe (formerly Leadjet) is a B2B contact-data and sales-intelligence platform that syncs LinkedIn prospects into the CRM and exposes an API for people and company search plus enrichment. The Surfe API returns verified business emails and mobile phone numbers, company firmographics, and lookalike account recommendations, billed against a credit-based model.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/surfe/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/surfe/refs/heads/main/apis.yml)

## Tags

- B2B Data
- Contact Data
- Sales Intelligence
- Enrichment
- Lead Generation
- CRM
- Prospecting

## Timestamps

- **Created:** 2026-07-01
- **Modified:** 2026-07-01

## APIs

### Surfe People Search API

Searches for people by persona and company filters (job titles, seniorities, departments, industries, headcount, location). Job titles are expanded automatically with acronym and semantic matching, and results are paged with a nextPageToken.

- **Human URL:** [https://developers.surfe.com/public-009-search-people-v2](https://developers.surfe.com/public-009-search-people-v2)
- **Base URL:** `https://api.surfe.com/v2`

#### Tags

- People Search
- Prospecting
- Contacts

#### Properties

- [Documentation](https://developers.surfe.com/public-009-search-people-v2)
- [API Reference](https://developers.surfe.com/)
- [OpenAPI](openapi/surfe-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/surfe.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/surfe.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Surfe People Enrichment API

Asynchronous bulk enrichment of up to 10,000 people per request by LinkedIn URL or name plus company, returning verified professional emails, mobile phone numbers, LinkedIn URLs, and job history. Start with POST, then poll the GET job endpoint or receive a webhook callback.

- **Human URL:** [https://developers.surfe.com/public-015-create-people-bulk-enrichment](https://developers.surfe.com/public-015-create-people-bulk-enrichment)
- **Base URL:** `https://api.surfe.com/v2`

#### Tags

- People Enrichment
- Email
- Mobile Phone

#### Properties

- [Documentation](https://developers.surfe.com/public-015-create-people-bulk-enrichment)
- [OpenAPI](openapi/surfe-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/surfe.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/surfe.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Surfe Company Search API

Searches for companies against Ideal Customer Profile (ICP) filters such as industry, employee count, revenue, location, and keywords, returning matching organizations with domains and firmographic metadata.

- **Human URL:** [https://developers.surfe.com/public-011-search-companies](https://developers.surfe.com/public-011-search-companies)
- **Base URL:** `https://api.surfe.com/v2`

#### Tags

- Company Search
- Firmographics
- ICP

#### Properties

- [Documentation](https://developers.surfe.com/public-011-search-companies)
- [OpenAPI](openapi/surfe-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/surfe.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/surfe.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Surfe Company Enrichment API

Asynchronous bulk enrichment of companies by domain, returning firmographics including description, employee count, revenue range, founding year, HQ location, industry, keywords, funding rounds, IPO/stock details, LinkedIn URL and follower count. Start with POST, then poll the GET job endpoint.

- **Human URL:** [https://developers.surfe.com/public-014-get-bulk-enrichment-organizations](https://developers.surfe.com/public-014-get-bulk-enrichment-organizations)
- **Base URL:** `https://api.surfe.com/v2`

#### Tags

- Company Enrichment
- Firmographics
- Async

#### Properties

- [Documentation](https://developers.surfe.com/public-014-get-bulk-enrichment-organizations)
- [OpenAPI](openapi/surfe-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/surfe.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/surfe.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Surfe Recommendations API

Defines an Ideal Customer Profile and fetches lookalike account recommendations that resemble the best-fit companies, for account-based prospecting and list expansion.

- **Human URL:** [https://developers.surfe.com/](https://developers.surfe.com/)
- **Base URL:** `https://api.surfe.com/v2`

#### Tags

- Lookalikes
- Recommendations
- ICP

#### Properties

- [Documentation](https://developers.surfe.com/)
- [OpenAPI](openapi/surfe-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/surfe.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/surfe.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Surfe Credits API

Returns the remaining credit balance across the separate email, mobile, and search/ICP credit pools so integrations can check quota before spending on enrichment.

- **Human URL:** [https://developers.surfe.com/](https://developers.surfe.com/)
- **Base URL:** `https://api.surfe.com/v2`

#### Tags

- Credits
- Usage
- Balance

#### Properties

- [Documentation](https://developers.surfe.com/)
- [OpenAPI](openapi/surfe-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/surfe.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/surfe.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/surfe)
- [Website](https://surfe.com)
- [Documentation](https://developers.surfe.com/)
- [Plans](plans/surfe-plans-pricing.yml)
- [Rate Limits](rate-limits/surfe-rate-limits.yml)
- [Fin Ops](finops/surfe-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
