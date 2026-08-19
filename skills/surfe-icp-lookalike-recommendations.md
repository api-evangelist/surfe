---
name: surfe-icp-lookalike-recommendations
description: >-
  Define an Ideal Customer Profile in Surfe and pull daily-refreshed lookalike
  account recommendations from it.
api: openapi/surfe-recommendations-api-openapi.yml
operations: [upsertICP, fetchRecommendations, getCredits]
method: generated
source: openapi/surfe-recommendations-api-openapi.yml + https://developers.surfe.com/public-019-v2-recommendations-icp-post
generated: '2026-08-13'
---

# Define an ICP and fetch lookalike accounts

Surfe's Recommendations product turns a saved Ideal Customer Profile into a
refreshed list of companies that resemble your best-fit accounts. Unlike search,
the ICP is **stateful** — you save it once and fetch against it repeatedly.

## Before you start

- Auth: `Authorization: Bearer {api-key}`, base `https://api.surfe.com/v2`.
- This product is **REST-only**. It is not exposed on Surfe's MCP server and has
  no `surfer` CLI command, so an agent must call the API directly.
- The ICP is scoped to a user. Surfe's documented `GET /v2/recommendations/icp`
  takes an optional `externalUserId` query parameter to read the ICP belonging
  to a specific user in your own system.

## Steps

1. **`upsertICP`** — `POST /recommendations/icp`.

   Body is an `ICPDefinition`: a `name` plus `filters` using the same
   `CompanyFilters` value object that company search uses (`industries`,
   `employeeCount` with `from`/`to`, `revenue`, `countries`, `domains`,
   `keywords`). Because the filter object is shared, an ICP you validated
   through `searchCompanies` will behave the same way here.

   This is an **upsert**: calling it again replaces the saved profile for the
   user. There is no version history and no diff — snapshot the body you sent if
   you need to explain a change in recommendations later.

2. **`fetchRecommendations`** — `POST /recommendations/fetch`.

   Body takes `limit` (1–200) and an optional `pageToken`. The response carries
   `companies[]` (the standard `Company` schema — same type as search and
   enrichment, so you can reuse one mapper across the whole API) and
   `nextPageToken`.

   Surfe describes these as **daily-refreshed**, so poll on a daily cadence, not
   per request. Re-fetching within a day spends quota for a list that has not
   changed.

3. **Enrich what you keep.** Recommendations return firmographics, not contacts.
   Feed the domains you keep into `startCompanyEnrichment` for deeper
   firmographics, and into `searchPeople` + `startPeopleEnrichment` for named
   contacts.

## Reading the recommendation reason

The recommendation payload carries a `reason` whose `data` became a typed object
on 2026-04-21 with `changesAmount`, `currentJobTitle` and `previousJobTitle` —
i.e. some recommendations are driven by **job-change signals** at the account,
not only by firmographic similarity. Surface that reason to the user; a
lookalike explained by a champion changing jobs is a different play than one
explained by industry fit.

## Errors and limits

`401` unauthenticated · `403` quota or credits exhausted · `429` rate limited
(10 req/s per user, burst 20, resets every minute, **no `Retry-After` header**)
· `500` may indicate a malformed body rather than a server fault. Envelope is
`{"code", "message"}` with no error taxonomy.

## Related

- Conventions: `conventions/surfe-conventions.yml`
- Changelog (this product shipped 2026-04-07): `changelog/surfe-changelog.yml`
- Data model: `data-model/surfe-data-model.yml`
