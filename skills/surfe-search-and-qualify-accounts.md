---
name: surfe-search-and-qualify-accounts
description: >-
  Build a target account list with Surfe company search, enrich the firmographics,
  and find the right people at each account — spending search credits deliberately.
api: openapi/surfe-companies-api-openapi.yml
operations: [searchCompanies, startCompanyEnrichment, getCompanyEnrichment, searchPeople, getCredits]
method: generated
source: openapi/surfe-companies-api-openapi.yml + https://developers.surfe.com/public-011-search-companies
generated: '2026-08-13'
---

# Build and qualify a target account list with Surfe

Go from an ICP description to a list of accounts with firmographics and named
contacts. Search is **metered by results returned**, so the shape of the query
decides the bill.

## Before you start

- Auth: `Authorization: Bearer {api-key}`, base `https://api.surfe.com/v2`.
- **Request-shape trap, published by Surfe in its own CLI repo:**
  `searchCompanies` requires filters nested under a top-level `filters` object,
  and the employee filter is `employeeCount` with `from`/`to`. `searchPeople`
  has **no** `filters` wrapper — it takes top-level `people` and `companies`
  objects. Getting this wrong returns **HTTP 500, not 400**.

## Steps

1. **`getCredits`** — read `searchCredits` before you start. Search credits are
   opt-in: without them, search is capped at a low daily result quota (200
   results/day); with them, up to 100,000/day. They are enabled by contacting
   `api.support@surfe.com`, not from the dashboard.

2. **`searchCompanies`** — `POST /companies/search`.

   - Body: `{ "filters": { ... }, "limit": <1–200>, "pageToken": "<optional>" }`.
   - `CompanyFilters` supports `industries`, `employeeCount` (`from`/`to`),
     `revenue`, `countries`, `domains`, `keywords`.
   - Page with `nextPageToken` from the response. Stop when it is absent.
   - **Set `limit` to what you will actually use.** Search credits are deducted
     per result returned, so an oversized page is money spent on rows you
     discard.

3. **`startCompanyEnrichment` → `getCompanyEnrichment`** — for the accounts that
   survive qualification.

   - `POST /companies/enrich` with `{"companies": [{"domain", "externalID"}]}`.
     The array field is `companies`, **not** `organizations`.
   - Use `include` to ask only for `firmographics` and/or `phoneNumbers`.
   - The call returns `202` with an `enrichmentID`; poll
     `GET /companies/enrich/{id}` until `status` is `COMPLETED`, or take the
     `company.enrichment.completed` webhook.
   - Enriched `Company` carries `description`, `employeeCount`, `revenue`,
     `founded`, `hqCountry`, `hqAddress`, `industry`, `keywords`,
     `linkedInUrl`, `linkedInFollowersCount`, `fundingRounds[]`, `isPublic`,
     `stockExchange`/`stockSymbol` and `parentOrganization`.

4. **`searchPeople`** — find the buying committee inside those accounts.

   - Body: top-level `people` (`jobTitles`, `seniorities`, `departments`,
     `countries`) and `companies` (`domains` from step 2/3), plus `limit` and
     `peoplePerCompany`.
   - Job titles are expanded automatically with acronym and semantic matching —
     if you need literal matching, use the `exactJobTitles` filter documented on
     the people-search page rather than fighting the expansion.
   - Carry your own keys through `organizationIDMappings` so results come back
     already tagged with your `externalID`.

5. **Hand off to enrichment** — the people returned by search have no contact
   details. Feed them to `startPeopleEnrichment` (see
   `skills/surfe-enrich-people-bulk.md`), which spends the email/mobile pools,
   not the search pool.

## Cost model to keep in mind

Three independent meters: **email credits**, **mobile credits**, **search
credits**. Search consumption changed on 2026-06-09 from `ceil(results / 25)` to
`ceil(results / 10)` — a 2.5x increase — so any cost model built before that
date is wrong. Daily quotas reset at midnight in the account's local time.

## Errors

`401` unauthenticated · `403` quota or credits exhausted (`402` also published
for insufficient search credits) · `429` rate limited, 10 req/s per user, burst
20, no `Retry-After` header · `500` frequently means a malformed body. Envelope
is `{"code", "message"}`.

## Related

- Conventions: `conventions/surfe-conventions.yml`
- Data model: `data-model/surfe-data-model.yml`
- Plans and credits: `plans/surfe-plans-pricing.yml`
