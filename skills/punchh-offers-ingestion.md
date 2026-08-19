---
name: punchh-offers-ingestion
description: Create, update and distribute offers and redeemables into PAR Punchh from an external CDP, CRM or offer-management system using the Platform Functions and Offers Ingestion APIs.
api: Punchh Platform Functions API
generated: '2026-08-13'
method: generated
source: openapi/punchh-platform-functions-api-openapi.yml, openapi/punchh-platform-functions-offers-ingestion-openapi.yml, openapi/punchh-platform-functions-headless-offers-openapi.yml, https://developers.partech.com/docs/dev-portal-platform-functions
operations:
  - dashboard_get_location_list
  - get-api2-dashboard-offers-redeemable
  - post-api2-dashboard-offers-redeemable
  - patch-api2-dashboard-offers-redeemable
  - get-api2-redeemable-list
  - post-api2-redeemable-distribution
---

# Punchh Platform Functions: push offers in from an outside system

Platform Functions is the admin surface — 63 operations across 14 tags, plus
separate Offers Ingestion (10 operations) and Headless Offers (5 operations)
specs. This is the API a CDP, CRM, offer engine or agency platform integrates
against, and it is a different security posture from the guest-facing APIs.

## Before you start

- Platform Functions authenticates with an **admin** bearer token, not a guest
  token. Do not reuse a mobile access token here.
- Punchh requires `x_true_client_ip` on Platform Functions calls, and — unusually —
  the security guidelines say for this surface it must be *"a string variable equal
  to the customer brand name (e.g., IHOP, MOD Pizza)"*, not an IP. Send what PAR's
  documentation says, not what the header name implies.
- TLS 1.2+.
- Certification is required before production access.

## Steps

1. **Resolve locations first.** `GET /api2/dashboard/locations`
   (`dashboard_get_location_list`). Offers are scoped to locations and location
   groups; ingesting against a stale location list is the most common cause of an
   offer that never surfaces to a guest. Location group and franchisee ids
   (`location_group_id`, `franchisee_id`) are the scoping keys — see
   `data-model/punchh-data-model.yml`.

2. **Read the existing redeemables before writing.**
   `GET /api2/dashboard/offers/redeemable` (`get-api2-dashboard-offers-redeemable`)
   or `GET /api2/dashboard/redeemables` (`get-api2-redeemable-list`). Punchh has no
   upsert — you must decide create-vs-update yourself.

3. **Create.** `POST /api2/dashboard/offers/redeemable`
   (`post-api2-dashboard-offers-redeemable`).

4. **Update.** `PATCH /api2/dashboard/offers/redeemable`
   (`patch-api2-dashboard-offers-redeemable`). PATCH, not PUT — sending PUT here
   will fail.

5. **Distribute.** `POST /api2/dashboard/campaigns`
   (`post-api2-redeemable-distribution`) commits the redeemable distribution to a
   guest population. This is the step that actually puts the offer in guests'
   accounts; creating a redeemable alone does nothing visible.

## Offers Ingestion vs Headless Offers

These are separate published specs and they are not interchangeable:

- **Offers Ingestion** (`openapi/punchh-platform-functions-offers-ingestion-openapi.yml`)
  — bulk ingestion of externally-authored offers, with 29 component schemas
  covering item qualifiers, line-item selectors, aggregator groupings and
  alternate-locale name/description pairs. Use this when another system owns offer
  authoring. PAR ships a dedicated "Offers Ingestion Developer Guide" and a
  separate certification track.
- **Headless Offers** (`openapi/punchh-platform-functions-headless-offers-openapi.yml`)
  — distribution of offers Punchh already holds, for brands rendering their own
  offer UI. See "Headless Offers Management - Distribution".

## Pagination and filtering

Platform Functions is the only Punchh surface with published pagination — `page`
and `per` query parameters on user search — and the only one with a `filter`
parameter (three operations). Assume everything else returns an unpaged array and
size your requests accordingly.

## Failure handling

`403 Forbidden` matters here in a way it does not on the guest surfaces (22
documented occurrences, mostly on Platform Functions and Offers Ingestion) — it
means the admin token lacks the entitlement, not that the object is missing. `422`
on an ingestion call is a qualifier/schema rejection; log the whole `errors` string
because there is no error code to switch on.

## Related

- `data-model/punchh-data-model.yml` — redeemable, location_group, custom_segment
- `asyncapi/punchh-webhooks.yml` — `Event - Redeemables`, `Event - Coupon Campaign`, `Event - Redeemable Unlocked`
- `errors/punchh-problem-types.yml`
