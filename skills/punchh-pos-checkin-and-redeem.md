---
name: punchh-pos-checkin-and-redeem
description: Look a guest up at a POS terminal, show their applicable offers and balance, apply a redemption, and post the loyalty check-in — the core PAR Punchh POS flow.
api: Punchh POS API
generated: '2026-08-13'
method: generated
source: openapi/punchh-pos-api-openapi.yml, openapi/punchh-pos-redemptions-legacy-openapi.yml, openapi/punchh-pos-redemptions-v2-openapi.yml, https://developers.partech.com/docs/dev-portal-pos
operations:
  - pos_location_config
  - pos_user_search
  - get-api-pos-users-balance
  - pos_applicable_offers
  - pos_create_redemption
  - pos_void_redemption
  - post-api-pos-discounts-lookup
  - put-api-pos-discounts-unlock
  - pos_checkin
---

# Punchh POS: check in a guest and apply a redemption

Mirrors PAR's own POS API Certification Tutorial (modules 1-7). Every operationId
below is present in `openapi/punchh-pos-api-openapi.yml` or the POS redemptions
specs — do not invent others.

## Before you start

- **Base URL is templated.** `https://{server_name}.punchh.com` — the
  `server_name` is issued per brand and per environment by a Punchh
  representative. There is no public host.
- **POS is the one surface admitted at TLS 1.0+**; every other Punchh surface
  requires TLS 1.2+.
- POS calls authenticate with a location token / business token pair, **not** the
  mobile bearer + `x-pch-digest` pair. See `authentication/punchh-authentication.yml`.
- A `User-Agent` header is mandatory on every Punchh call. Requests without one
  are rejected outright.

## Steps

1. **Load location configuration.** `GET /api/pos/locations/configuration`
   (`pos_location_config`). Returns the loyalty program meta for this store — what
   currency the program uses, which redemption generation is enabled, and what the
   terminal is allowed to display. Cache it; do not call it per transaction.

2. **Find the guest.** `GET /api/pos/users/search` (`pos_user_search`). Accepts a
   scanned barcode/QR payload, a phone number, an email, or a card number. Generate
   the scan payload with PAR's published barcode algorithm
   (`https://developers.partech.com/docs/dev-portal-pos` → "Implement the Punchh
   Barcode and QR Code Algorithm"). A miss is a `404`, not an error state — offer
   enrollment via `POST /api/pos/users` (`pos_create_user`).

3. **Show the balance.** `GET /api/pos/users/balance`
   (`get-api-pos-users-balance`). Display points/currency and membership level on
   the terminal before the guest commits.

4. **Offer the discounts.** Which call depends on the redemption generation the
   brand is on — check step 1's configuration, do not guess:
   - **Redemptions 1.0 (legacy):** `POST /api/pos/redemptions/applicable_offers`
     (`pos_applicable_offers`) with the basket's menu items, then
     `POST /api/pos/redemptions` (`pos_create_redemption`) for the one the guest picks.
   - **Redemptions 2.0 (current):** `POST /api/pos/discounts/lookup`
     (`post-api-pos-discounts-lookup`) to build the server-side discount basket,
     then `PUT /api/pos/discounts/unlock` (`put-api-pos-discounts-unlock`) when the
     check needs to be reopened. The basket is the idempotency mechanism — a
     repeated apply mutates the basket rather than issuing a second redemption.

5. **Handle a void.** If the guest changes their mind or the check is cancelled,
   `DELETE /api/pos/redemptions` (`pos_void_redemption`) releases the redemption.
   Do this before the check-in, not after.

6. **Post the check-in.** `POST /api/pos/checkins` (`pos_checkin`). This is the
   earning event. Send the partner's own transaction identifier (`external_uid`)
   so a network retry does not double-award points.

## Failure handling

- Punchh does **not** use RFC 9457. Failures return `application/json` shaped
  `{"errors": "<human readable message>"}` with no machine-readable code — match on
  HTTP status first, message text only as a fallback. See
  `errors/punchh-problem-types.yml`.
- `412 Precondition Failed` and `422 Unprocessable Entity` are the two most common
  POS failures (35 and 123 documented occurrences across the specs); both mean the
  request was understood and rejected on business rules — do not retry blindly.
- Read `X-Request-Id` off every response and log it. It is the only handle Punchh
  support can act on.
- The POS certification track has a dedicated module — "Module 10: Handling POS
  Disconnections" — because terminals go offline mid-transaction. Implement it.

## Related

- `conventions/punchh-conventions.yml` — header contract, caching, tracing
- `lifecycle/punchh-lifecycle.yml` — Redemptions 1.0 is legacy; plan the 2.0 migration
- `asyncapi/punchh-webhooks.yml` — `Event - POS Scanner Check-in`, `Event - Check-in Void`
