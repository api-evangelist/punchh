# Punchh (punchh)

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

Punchh, now part of PAR Technology and offered under the PAR Engagement brand, is an enterprise loyalty, offers, and customer engagement platform for restaurants. It unifies guest data from online ordering, mobile apps, POS, and kiosks into a single view so brands can run personalized loyalty and marketing programs. PAR exposes well-documented Punchh APIs through its developer portal covering platform functions, mobile, online ordering, POS and kiosk integration, and a webhooks manager, with sample collections published to Postman. Most integration surfaces require partner certification. Over 275 restaurant brands rely on Punchh to grow customer lifetime value.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/punchh/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/punchh/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- Restaurant
- Loyalty
- Marketing
- Guest Engagement
- Online Ordering
- Mobile
- Point Of Sale
- Webhooks

## Timestamps

- **Created:** 2026-06-02
- **Modified:** 2026-06-03

## APIs

### PAR Punchh Mobile API

Guest-facing loyalty functions for business-branded mobile apps and websites: registration and sign-in, profile management, check-in transaction details, and offer management. Calls are HMAC-SHA256 signed and require partner certification.

- **Human URL:** [https://developers.partech.com/docs/dev-portal-mobile/bf6eddb435209-mobile-api](https://developers.partech.com/docs/dev-portal-mobile/bf6eddb435209-mobile-api)
- **Base URL:** `https://{server_name}.punchh.com`

#### Tags

- Mobile
- Loyalty
- Users
- Offers

#### Properties

- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-mobile-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/punchh-mobile.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/punchh-mobile.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/mobile-access-token-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-create-user-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-login-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-mark-offers-read-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-transaction-details-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-transaction-details-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-update-user-profile-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/mobile-user-session-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/mobile-access-token-structure.json)
- [JSON Structure](json-structure/mobile-create-user-request-structure.json)
- [JSON Structure](json-structure/mobile-login-request-structure.json)
- [JSON Structure](json-structure/mobile-mark-offers-read-request-structure.json)
- [JSON Structure](json-structure/mobile-transaction-details-request-structure.json)
- [JSON Structure](json-structure/mobile-transaction-details-structure.json)
- [JSON Structure](json-structure/mobile-update-user-profile-request-structure.json)
- [JSON Structure](json-structure/mobile-user-session-structure.json)
- [J S O N- L D](json-ld/punchh-mobile-context.jsonld)
- [Example](examples/mobile-access-token-example.json)
- [Example](examples/mobile-create-user-request-example.json)
- [Example](examples/mobile-login-request-example.json)
- [Example](examples/mobile-mark-offers-read-request-example.json)
- [Example](examples/mobile-transaction-details-example.json)
- [Example](examples/mobile-transaction-details-request-example.json)
- [Example](examples/mobile-update-user-profile-request-example.json)
- [Example](examples/mobile-user-session-example.json)

### PAR Punchh Online Ordering and SSO API

SSO authentication, loyalty check-ins, and redemptions for online ordering platforms. Lets guests earn and redeem rewards against online order receipts. Requires partner certification.

- **Human URL:** [https://developers.partech.com/docs/dev-portal-online-ordering/apis/online-ordering-and-sso-api](https://developers.partech.com/docs/dev-portal-online-ordering/apis/online-ordering-and-sso-api)
- **Base URL:** `https://{server_name}.punchh.com`

#### Tags

- Online Ordering
- Loyalty
- Redemptions
- Single Sign On

#### Properties

- [Getting Started](https://developers.partech.com/docs/dev-portal-online-ordering/apis/online-ordering-and-sso-api)
- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-online-ordering-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/punchh-online-ordering.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/punchh-online-ordering.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/online-ordering-online-order-checkin-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/online-ordering-online-order-checkin-response-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/online-ordering-online-order-redemption-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/online-ordering-online-order-redemption-response-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/online-ordering-online-order-checkin-request-structure.json)
- [JSON Structure](json-structure/online-ordering-online-order-checkin-response-structure.json)
- [JSON Structure](json-structure/online-ordering-online-order-redemption-request-structure.json)
- [JSON Structure](json-structure/online-ordering-online-order-redemption-response-structure.json)
- [J S O N- L D](json-ld/punchh-online-ordering-context.jsonld)
- [Example](examples/online-ordering-online-order-checkin-request-example.json)
- [Example](examples/online-ordering-online-order-checkin-response-example.json)
- [Example](examples/online-ordering-online-order-redemption-request-example.json)
- [Example](examples/online-ordering-online-order-redemption-response-example.json)

### PAR Punchh POS and Kiosk API

Point-of-sale and kiosk integration: guest lookup and balance, user and check-in creation, location/program configuration, and redemption processing. Authenticated with a location/business token pair. Requires partner certification.

- **Human URL:** [https://developers.partech.com/docs/dev-portal-pos/1921e8b711e43-getting-started-with-pos-api-integrations](https://developers.partech.com/docs/dev-portal-pos/1921e8b711e43-getting-started-with-pos-api-integrations)
- **Base URL:** `https://{server_name}.punchh.com`

#### Tags

- Point Of Sale
- Kiosk
- Loyalty
- Redemptions

#### Properties

- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-pos-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/punchh-pos.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/punchh-pos.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/pos-pos-checkin-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/pos-pos-user-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/pos-pos-checkin-request-structure.json)
- [JSON Structure](json-structure/pos-pos-user-structure.json)
- [J S O N- L D](json-ld/punchh-pos-context.jsonld)
- [Example](examples/pos-pos-checkin-request-example.json)
- [Example](examples/pos-pos-user-example.json)

### PAR Punchh Platform Functions API

Core programmatic and headless access to the loyalty platform. The Headless Offers API lists offers (redeemables) defined on Punchh for browsing and selection in external platforms. Requires partner certification.

- **Human URL:** [https://developers.partech.com/docs/dev-portal-platform-functions](https://developers.partech.com/docs/dev-portal-platform-functions)
- **Base URL:** `https://{server_name}.punchh.com`

#### Tags

- Platform Functions
- Offers
- Headless

#### Properties

- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-platform-functions-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/punchh-platform-functions.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/punchh-platform-functions.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/platform-functions-redeemable-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/platform-functions-redeemable-structure.json)
- [J S O N- L D](json-ld/punchh-platform-functions-context.jsonld)
- [Example](examples/platform-functions-redeemable-example.json)

## Common Properties

- [Website](https://punchh.com/)
- [Documentation](https://developers.partech.com/)
- [Portal](https://developers.partech.com/)
- [Getting Started](https://developers.partech.com/docs/dev-portal-developer-resources)
- [Postman](https://punchh.com/blog/2024/07/12/par-punchh-apis-now-available-on-postman-workspace/) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [GitHub Organization](https://github.com/punchh)
- [Blog](https://punchh.com/blog/)
- [LinkedIn](https://www.linkedin.com/company/partechnology)
- [Spectral Rules](rules/punchh-spectral-rules.yml)
- [Vocabulary](vocabulary/punchh-vocabulary.yaml)
- [Plans](plans/punchh-plans-pricing.yml)
- [Rate Limits](rate-limits/punchh-rate-limits.yml)
- [Fin Ops](finops/punchh-finops.yml)
- [Webhooks](https://developers.partech.com/docs/dev-portal-webhooks-manager/8c18e3660f73f-event-guest)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)
- [Solutions](undefined)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
