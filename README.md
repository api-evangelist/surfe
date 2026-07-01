# Surfe (surfe)

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
