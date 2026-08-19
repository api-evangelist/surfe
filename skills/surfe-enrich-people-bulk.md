---
name: surfe-enrich-people-bulk
description: >-
  Bulk-enrich a list of contacts with verified professional emails and mobile
  phone numbers using the Surfe API, without double-charging credits.
api: openapi/surfe-people-api-openapi.yml
operations: [startPeopleEnrichment, getPeopleEnrichment, getCredits]
method: generated
source: openapi/surfe-people-api-openapi.yml + https://developers.surfe.com/public-015-create-people-bulk-enrichment
generated: '2026-08-13'
---

# Bulk-enrich people with Surfe

Turn a list of contacts into verified emails and mobile numbers. This is an
**asynchronous, metered** flow: the start call returns a job id, and every
resolved email or phone spends a credit from a separate pool.

## Before you start

- Auth: `Authorization: Bearer {api-key}`. Keys come from
  <https://app.surfe.com/api-settings>; one key per user.
- Base URL: `https://api.surfe.com/v2`.
- **There is no idempotency key.** Retrying `startPeopleEnrichment` starts a
  second job and spends credits again. Deduplicate your input list before you
  send it, and store the returned `enrichmentID` before doing anything else.

## Steps

1. **Check the budget first — `getCredits`**

   `GET /credits` returns `emailCredits`, `mobileCredits` and `searchCredits` as
   three independent meters. If the pool you are about to spend is empty, stop:
   the enrichment call will fail rather than partially succeed.

2. **Start the job — `startPeopleEnrichment`**

   `POST /people/enrich`, up to 10,000 people per request.

   - Each entry needs **either** `linkedinUrl` **or** `firstName` + `lastName` +
     (`companyName` or `companyDomain`).
   - Set `externalID` on every entry. It is echoed back on the enriched record
     and on every webhook — it is the only way to reconcile results to your own
     rows, because Surfe issues no person id.
   - `include` is **required** and must carry at least one of `email`, `mobile`,
     `linkedInUrl`, `jobHistory`. `include` is a billing control: `email: true`
     debits the email pool, `mobile: true` debits the mobile pool.
   - Use `enrichmentOptions.skipMobileEnrichmentIfNoEmailFound: true` to avoid
     spending mobile credits on contacts you could not resolve at all.
   - Use `enrichmentOptions.acceptedEmailType` (`professional` | `personal`) to
     pick the cascade. Personal email is priced separately.
   - If you can receive callbacks, set `notificationOptions.webhookUrl` now —
     see step 4.

   A `202 Accepted` returns `enrichmentID`, `enrichmentCallbackURL` and a
   `message` with an estimated completion time. **Persist `enrichmentID`
   immediately.** If you lose it there is no way to list jobs and recover it,
   and the credits are already committed.

3. **Collect the results — `getPeopleEnrichment`**

   `GET /people/enrich/{id}`. Read `status` (`PENDING`, `IN_PROGRESS`,
   `COMPLETED`, `FAILED`) and `percentCompleted`. Poll only if you have no
   webhook, and poll slowly: every poll counts against the same daily request
   quota the enrichment does.

   Each `EnrichedPerson` carries `emails[]` (with `validationStatus`),
   `mobilePhones[]` (with `confidenceScore`), optional `jobHistory[]`, and its
   own `status` — a person can come back unresolved inside a `COMPLETED` job, so
   check per record, not just per job.

4. **Prefer the webhook over polling**

   With `notificationOptions.webhookUrl` set, Surfe POSTs
   `person.enrichment.completed` per contact and
   `person.batch-enrichment.completed` once for the batch. Respond `200 OK` to
   acknowledge. Note that Surfe **does not sign webhook payloads**, so treat the
   callback as a trigger to call `getPeopleEnrichment` yourself rather than as
   trusted data, and never expose the callback URL publicly.

## Errors and limits

- `401` — missing/wrong key. Every path on `api.surfe.com` returns 401 when
  unauthenticated, including paths that do not exist.
- `403` — quota exceeded **or** insufficient credits (per the responses
  reference). The changelog also documents `402` for insufficient search
  credits, so treat **both 402 and 403** as "out of budget", not as retryable.
- `429` — rate limited. The ceiling is 10 req/s per user with bursts to 20; the
  limiter resets every minute. **No `Retry-After` or `RateLimit-*` header is
  returned**, so back off on a fixed schedule with jitter rather than reading a
  hint from the response.
- `500` — may mean a malformed body, not a server fault. Surfe's own CLI notes
  that a wrong v2 request shape returns 500. Re-check `include` is present and
  the array field is `people`.
- Errors are `{"code": <int>, "message": <string>}` — no error type, no field
  paths. You cannot branch on anything finer than the status code.

## Related

- Conventions: `conventions/surfe-conventions.yml`
- Errors: `errors/surfe-problem-types.yml`
- Webhooks: `asyncapi/surfe-webhooks.yml`
