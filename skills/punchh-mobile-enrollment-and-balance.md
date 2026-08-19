---
name: punchh-mobile-enrollment-and-balance
description: Enrol a guest from a branded mobile app, sign them in, read their balance and offers, and post a scan-based loyalty check-in against the PAR Punchh Mobile API.
api: Punchh Mobile API
generated: '2026-08-13'
method: generated
source: openapi/punchh-mobile-api-openapi.yml, https://developers.partech.com/docs/dev-portal-mobile
operations:
  - mobile_sign_up
  - mobile_signin
  - mobile_fetch_user_information
  - mobile_update_user_profile
  - mobile_fetch_user_balance
  - mobile_list_applicable_offers
  - mobile_create_redemption_using_redeemable
  - mobile_create_loyalty_checkin_by_qr_code
---

# Punchh Mobile: enrol, authenticate, earn

The Mobile API is the largest published Punchh surface — 116 operations across 28
tags (badges, beacons, challenges, check-ins, collectibles, coupons, drive-thru,
feedback, games, gift cards, invitations, locations, loyalty transfers,
notifications, offers, passcodes, payment cards, payments, referrals, single scan
code, social cause campaigns, surveys, swag, users, WiFi acquisition).

## The header contract is the hard part

Punchh rejects mobile requests on headers more often than on payloads. All four of
these are required:

| Header | What it carries |
|---|---|
| `Authorization` | `Bearer <access_token>` from sign-in |
| `x-pch-digest` | HMAC-SHA256 of URI + body — tamper protection |
| `punchh-app-device-id` | Stable per-device GUID; must survive a device reset (iOS keychain / Android permanent storage) |
| `User-Agent` | `AppName/Version/Build (OS; Model; MANUFACTURER; MODEL; OS Version)` — requests without it are **rejected** |

Also honour the ceilings: total request headers ≤ 32 KB, any single header ≤ 16 KB,
and send **no** header the spec did not ask for. Over-limit messages are dropped
server-side and never processed.

`punchh-app-device-id` is an anti-fraud control, not telemetry — sign-up rewards
are granted per device so a guest cannot re-register repeatedly on one handset.
Rotating it looks like fraud.

## Steps

1. **Enrol.** `POST /api2/mobile/users` (`mobile_sign_up`). Unauthenticated mobile
   calls also pass the business OAuth `client` id in the request body.
2. **Sign in.** `POST /api2/mobile/users/login` (`mobile_signin`). Returns the user
   record including the access token. For passwordless, see
   `skills/punchh-mobile-passwordless-auth.md`.
3. **Read the profile.** `GET /api2/mobile/users/profile`
   (`mobile_fetch_user_information`); update with `PUT /api2/mobile/users`
   (`mobile_update_user_profile`).
4. **Read the balance.** `GET /api2/mobile/users/balance`
   (`mobile_fetch_user_balance`).
5. **Show what they can use.** `GET /api2/mobile/redemptions/applicable_offers`
   (`mobile_list_applicable_offers`).
6. **Redeem.** `POST /api2/mobile/redemptions/redeemable`
   (`mobile_create_redemption_using_redeemable`).
7. **Earn.** `POST /api2/mobile/checkins/qrcode`
   (`mobile_create_loyalty_checkin_by_qr_code`). Receipt-image and barcode variants
   exist on the same spec if the brand supports them.

## Caching and localisation

- Honour `Cache-Control`, `Expires` and `Etag` — Punchh sets them deliberately and
  sends conservative values based on the response body.
- Send `Accept-Encoding: gzip`. Responses are materially smaller.
- Send `Accept-Language` (`en` default, `es` supported) and `Accept-Timezone` with
  an Olson/IANA zone. Punchh generates timestamps in the zone you supply — omit it
  and your timestamps drift.
- `x-max-ios` / `x-max-android` come back on responses carrying the latest known
  app version; use them to drive in-app upgrade prompts.

## Failure handling

`401` is the single most common documented failure on the mobile surface (134
occurrences). Distinguish "token expired" from "digest wrong" before retrying — a
bad `x-pch-digest` will fail forever. See `errors/punchh-problem-types.yml`.

## Related

- `conventions/punchh-conventions.yml`
- `rate-limits/punchh-rate-limits.yml` — 10 failed authentications in 10 minutes gets the IP blocked for an hour
