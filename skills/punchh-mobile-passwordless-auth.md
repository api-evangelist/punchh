---
name: punchh-mobile-passwordless-auth
description: Sign a guest in or up with a one-time password over email or SMS using PAR Punchh Advanced Authentication, including the PKCE exchange and refresh-token rotation.
api: Punchh Mobile API
generated: '2026-08-13'
method: generated
source: openapi/punchh-mobile-api-openapi.yml, https://developers.partech.com/docs/dev-portal-developer-resources/advanced-authentication-developer-guide
operations:
  - mobile_generate_otp_token
  - mobile_verify_token
  - oauth_token
  - mobile_fetch_user_balance
---

# Punchh Advanced Authentication: passwordless OTP sign-in

Advanced Authentication is a PAR Punchh platform feature that adds third-party
identity providers and **passwordless** login by email or SMS one-time password.
It must be enabled on your Punchh business by a PAR representative before any of
this works.

Sign-in and sign-up are the **same flow**. If the guest does not exist, calling
Send OTP and then Verify Token creates them. Do not branch.

## Steps

1. **Send the OTP.** `POST /api2/mobile/verify_token`
   (`mobile_generate_otp_token`). Arguments:
   - the business OAuth **client id**
   - the validation method
   - the **email address**, or the **phone number plus phone extension** (country code)
   - `terms_and_conditions=true` and `privacy_policy=true`
   - a **PKCE code challenge**

   Punchh looks the identifier up and sends the OTP to the guest by email or SMS.

2. **Verify.** `PUT /api2/mobile/verify_token` (`mobile_verify_token`) with the
   OTP the guest typed, the same identifier, the client id, both consent flags,
   and the **PKCE code verifier**. On success `response_body.data` carries
   `access_token` and `refresh_token`.

3. **Call the API.** Use the `access_token` as the bearer credential on Mobile and
   Online Ordering calls — e.g. `GET /api2/mobile/users/balance`
   (`mobile_fetch_user_balance`). The digest and device-id header rules still apply;
   OTP replaces the password, not the header contract.

4. **Refresh.** Both tokens expire. Exchange the `refresh_token` (with the OAuth
   client id) for a fresh pair rather than forcing a re-login, and **replace both
   stored tokens** with the new pair — Punchh rotates the refresh token.
   `POST /oauth/token` (`oauth_token`) is the published token endpoint.

## Consent is not optional

`terms_and_conditions=true` and `privacy_policy=true` are arguments on both calls.
Do not hard-code them — capture the guest's actual consent, because this flow
creates an account on first use.

## What Punchh does *not* publish

- No `/.well-known/openid-configuration` and no
  `/.well-known/oauth-authorization-server` — probed 404 on every host. There is no
  discoverable OAuth metadata to bootstrap from.
- No OAuth scopes. None of the 15 published specs declares an `oauth2`
  securityScheme, and there is no scopes/permissions reference page.
- Token lifetimes are not published; treat expiry as observed rather than known.

An ID token shape *is* published on the mobile User Authentication page:
`{"id": "<issuer>", "sub": "<subject>", "access_token": "<token>"}`.

## Testing it

PAR ships a **PAR Advanced Authentication** Postman collection in the
[PAR Tech APIs (Official)](https://www.postman.com/par-tech/par-tech-apis-official/collection/5p8ayn6/par-advanced-authentication)
workspace that runs the email-OTP and phone-OTP scenarios end to end and then
proves the resulting token against Mobile and Online Ordering calls. Fork it
before writing code. You still need keys from a Punchh representative.

## Related

- `authentication/punchh-authentication.yml`
- `conformance/punchh-conformance.yml` — oauth2 and oidc are both `partial` here, and this is why
- `rate-limits/punchh-rate-limits.yml`
