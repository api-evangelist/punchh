---
name: punchh-online-ordering-loyalty-checkout
description: Attach PAR Punchh loyalty to an online ordering checkout — sign the guest in over SSO, build a Redemptions 2.0 discount basket, and post the loyalty check-in when the order is placed.
api: Punchh Online Ordering and SSO API
generated: '2026-08-13'
method: generated
source: openapi/punchh-online-ordering-sso-api-openapi.yml, openapi/punchh-online-ordering-redemptions-v2-openapi.yml, https://developers.partech.com/docs/dev-portal-online-ordering
operations:
  - oauth_token
  - sso_signup
  - sso_login
  - sso_fetch_user_informaton
  - sso_fetch_user_balance
  - sso_auth_fetchavailableoffers
  - get-api-auth-discounts-active
  - post-api-auth-discounts-auto_select
  - delete-api-auth-discounts-unselect
  - put-api-auth-discounts-unlock
  - sso_create_online_redemption
  - sso_loyalty_checkin
  - sso_update_loyalty_checkin
  - sso_void_loyalty_checkin
---

# Punchh Online Ordering: loyalty on an online checkout

Mirrors PAR's Online Ordering API Certification Tutorial (modules 1-7). Every
operationId is verified present in the published Online Ordering specs.

## Before you start

- Requires an `x-pch-digest` HMAC-SHA256 signature over URI + body on every call,
  alongside the bearer token. PAR publishes a digest generator on the developer
  portal; there is also a "Generating x-pch-digest Header for Online Ordering
  APIs" page.
- If you proxy guest traffic (the "indirect access" topology), you **must** send
  `x_true_client_ip` with the real guest IP. Punchh rate-limits and bot-mitigates
  on that header, not on your load balancer's IP. Requests without it are filtered
  and ignored.
- TLS 1.2+.

## Steps

1. **Get the SSO token.** `POST /oauth/token` (`oauth_token`) using the business
   OAuth client credentials.

2. **Sign the guest in, or enrol them.**
   - `POST /api/auth/customers/sign_in` (`sso_login`) for email + password.
   - `POST /api/auth/customers.json` (`sso_signup`) to create a new guest.
   - SAML SSO and passwordless OTP are also supported — see
     `skills/punchh-mobile-passwordless-auth.md` for the OTP path.

3. **Read the account.** `GET /api/auth/users` (`sso_fetch_user_informaton`) and
   `GET /api/auth/users/balance` (`sso_fetch_user_balance`) so the checkout can
   show who the guest is and what they have banked.

4. **Fetch what they can use.** `GET /api/auth/offers`
   (`sso_auth_fetchavailableoffers`).

5. **Build the discount basket (Redemptions 2.0).** This is the current
   generation; prefer it over Redemptions 1.0 on any new build.
   - `POST /api/auth/discounts/auto_select` (`post-api-auth-discounts-auto_select`)
     lets Punchh pick the best-value discount for the basket.
   - `GET /api/auth/discounts/active` (`get-api-auth-discounts-active`) reads the
     basket back — call this to render the cart, never your own cached copy.
   - `DELETE /api/auth/discounts/unselect`
     (`delete-api-auth-discounts-unselect`) removes an item the guest declined.
   - `PUT /api/auth/discounts/unlock` (`put-api-auth-discounts-unlock`) releases a
     locked basket. Punchh locks the basket during checkout on purpose — read
     "Redemptions 2.0 - Discount Basket Locking" before you build retry logic.
   - `POST /api/auth/batch_redemptions` (`sso_create_online_redemption`) commits a
     batch redemption.

6. **Post the check-in when the order is placed.**
   `POST /api/auth/checkins/online_order` (`sso_loyalty_checkin`). Send your own
   order identifier as `external_uid` — this is the idempotency key, and it is the
   only thing standing between a network retry and a double-award.

7. **Amend or reverse.** `PUT /api/auth/checkins/online_order`
   (`sso_update_loyalty_checkin`) for a modified order;
   `DELETE /api/auth/checkins` (`sso_void_loyalty_checkin`) for a cancellation or
   refund. Do not leave a cancelled order's points standing.

## Failure handling

- `412` and `422` dominate. A `422` on a discount call usually means the basket no
  longer qualifies — re-fetch `discounts/active` rather than retrying the same body.
- `500` is documented on exactly one online-ordering operation; treat it as
  transient and retry with backoff, but never retry a check-in without the same
  `external_uid`.
- Error bodies are `{"errors": "..."}` — see `errors/punchh-problem-types.yml`.

## Related

- `conventions/punchh-conventions.yml`
- `asyncapi/punchh-webhooks.yml` — `Event - Check-in - Gift and Loyalty`, `Event - Redemption Applied`
