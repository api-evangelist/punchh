# Punchh (punchh)
Punchh, now part of PAR Technology and offered under the PAR Engagement brand, is an enterprise loyalty, offers, and customer engagement platform for restaurants. It unifies guest data from online ordering, mobile apps, POS, and kiosks into a single view so brands can run personalized loyalty and marketing programs. PAR exposes well-documented Punchh APIs through its developer portal covering platform functions, mobile, online ordering, POS and kiosk integration, and a webhooks manager, with sample collections published to Postman. Most integration surfaces require partner certification. Over 275 restaurant brands rely on Punchh to grow customer lifetime value.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/punchh/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

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

**Human URL:** [https://developers.partech.com/docs/dev-portal-mobile/bf6eddb435209-mobile-api](https://developers.partech.com/docs/dev-portal-mobile/bf6eddb435209-mobile-api)

#### Tags:

 - Mobile
 - Loyalty
 - Users
 - Offers

#### Properties

- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-mobile-openapi.yml)
- [JSONSchema](json-schema/mobile-access-token-schema.json)
- [JSONSchema](json-schema/mobile-create-user-request-schema.json)
- [JSONSchema](json-schema/mobile-login-request-schema.json)
- [JSONSchema](json-schema/mobile-mark-offers-read-request-schema.json)
- [JSONSchema](json-schema/mobile-transaction-details-request-schema.json)
- [JSONSchema](json-schema/mobile-transaction-details-schema.json)
- [JSONSchema](json-schema/mobile-update-user-profile-request-schema.json)
- [JSONSchema](json-schema/mobile-user-session-schema.json)
- [JSONStructure](json-structure/mobile-access-token-structure.json)
- [JSONStructure](json-structure/mobile-create-user-request-structure.json)
- [JSONStructure](json-structure/mobile-login-request-structure.json)
- [JSONStructure](json-structure/mobile-mark-offers-read-request-structure.json)
- [JSONStructure](json-structure/mobile-transaction-details-request-structure.json)
- [JSONStructure](json-structure/mobile-transaction-details-structure.json)
- [JSONStructure](json-structure/mobile-update-user-profile-request-structure.json)
- [JSONStructure](json-structure/mobile-user-session-structure.json)
- [JSON-LD](json-ld/punchh-mobile-context.jsonld)
- [Example](examples/mobile-access-token-example.json)
- [Example](examples/mobile-create-user-request-example.json)
- [Example](examples/mobile-login-request-example.json)
- [Example](examples/mobile-mark-offers-read-request-example.json)
- [Example](examples/mobile-transaction-details-example.json)
- [Example](examples/mobile-transaction-details-request-example.json)
- [Example](examples/mobile-update-user-profile-request-example.json)
- [Example](examples/mobile-user-session-example.json)
- [NaftikoCapability](capabilities/mobile-check-ins.yaml)
- [NaftikoCapability](capabilities/mobile-offers.yaml)
- [NaftikoCapability](capabilities/mobile-users.yaml)

### PAR Punchh Online Ordering and SSO API
SSO authentication, loyalty check-ins, and redemptions for online ordering platforms. Lets guests earn and redeem rewards against online order receipts. Requires partner certification.

**Human URL:** [https://developers.partech.com/docs/dev-portal-online-ordering/apis/online-ordering-and-sso-api](https://developers.partech.com/docs/dev-portal-online-ordering/apis/online-ordering-and-sso-api)

#### Tags:

 - Online Ordering
 - Loyalty
 - Redemptions
 - Single Sign On

#### Properties

- [GettingStarted](https://developers.partech.com/docs/dev-portal-online-ordering/apis/online-ordering-and-sso-api)
- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-online-ordering-openapi.yml)
- [JSONSchema](json-schema/online-ordering-online-order-checkin-request-schema.json)
- [JSONSchema](json-schema/online-ordering-online-order-checkin-response-schema.json)
- [JSONSchema](json-schema/online-ordering-online-order-redemption-request-schema.json)
- [JSONSchema](json-schema/online-ordering-online-order-redemption-response-schema.json)
- [JSONStructure](json-structure/online-ordering-online-order-checkin-request-structure.json)
- [JSONStructure](json-structure/online-ordering-online-order-checkin-response-structure.json)
- [JSONStructure](json-structure/online-ordering-online-order-redemption-request-structure.json)
- [JSONStructure](json-structure/online-ordering-online-order-redemption-response-structure.json)
- [JSON-LD](json-ld/punchh-online-ordering-context.jsonld)
- [Example](examples/online-ordering-online-order-checkin-request-example.json)
- [Example](examples/online-ordering-online-order-checkin-response-example.json)
- [Example](examples/online-ordering-online-order-redemption-request-example.json)
- [Example](examples/online-ordering-online-order-redemption-response-example.json)
- [NaftikoCapability](capabilities/online-ordering-check-in.yaml)
- [NaftikoCapability](capabilities/online-ordering-redemptions.yaml)

### PAR Punchh POS and Kiosk API
Point-of-sale and kiosk integration: guest lookup and balance, user and check-in creation, location/program configuration, and redemption processing. Authenticated with a location/business token pair. Requires partner certification.

**Human URL:** [https://developers.partech.com/docs/dev-portal-pos/1921e8b711e43-getting-started-with-pos-api-integrations](https://developers.partech.com/docs/dev-portal-pos/1921e8b711e43-getting-started-with-pos-api-integrations)

#### Tags:

 - Point Of Sale
 - Kiosk
 - Loyalty
 - Redemptions

#### Properties

- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-pos-openapi.yml)
- [JSONSchema](json-schema/pos-pos-checkin-request-schema.json)
- [JSONSchema](json-schema/pos-pos-user-schema.json)
- [JSONStructure](json-structure/pos-pos-checkin-request-structure.json)
- [JSONStructure](json-structure/pos-pos-user-structure.json)
- [JSON-LD](json-ld/punchh-pos-context.jsonld)
- [Example](examples/pos-pos-checkin-request-example.json)
- [Example](examples/pos-pos-user-example.json)
- [NaftikoCapability](capabilities/pos-check-ins.yaml)
- [NaftikoCapability](capabilities/pos-configuration.yaml)
- [NaftikoCapability](capabilities/pos-receipts.yaml)
- [NaftikoCapability](capabilities/pos-redemptions.yaml)
- [NaftikoCapability](capabilities/pos-users.yaml)

### PAR Punchh Platform Functions API
Core programmatic and headless access to the loyalty platform. The Headless Offers API lists offers (redeemables) defined on Punchh for browsing and selection in external platforms. Requires partner certification.

**Human URL:** [https://developers.partech.com/docs/dev-portal-platform-functions](https://developers.partech.com/docs/dev-portal-platform-functions)

#### Tags:

 - Platform Functions
 - Offers
 - Headless

#### Properties

- [Documentation](https://developers.partech.com/)
- [OpenAPI](openapi/punchh-platform-functions-openapi.yml)
- [JSONSchema](json-schema/platform-functions-redeemable-schema.json)
- [JSONStructure](json-structure/platform-functions-redeemable-structure.json)
- [JSON-LD](json-ld/punchh-platform-functions-context.jsonld)
- [Example](examples/platform-functions-redeemable-example.json)
- [NaftikoCapability](capabilities/platform-functions-offers.yaml)

## Common Properties

- [Website](https://punchh.com/)
- [Documentation](https://developers.partech.com/)
- [Portal](https://developers.partech.com/)
- [GettingStarted](https://developers.partech.com/docs/dev-portal-developer-resources)
- [Postman](https://punchh.com/blog/2024/07/12/par-punchh-apis-now-available-on-postman-workspace/)
- [GitHubOrganization](https://github.com/punchh)
- [Blog](https://punchh.com/blog/)
- [LinkedIn](https://www.linkedin.com/company/partechnology)
- [SpectralRules](rules/punchh-spectral-rules.yml)
- [Vocabulary](vocabulary/punchh-vocabulary.yaml)
- [Plans](plans/punchh-plans-pricing.yml)
- [RateLimits](rate-limits/punchh-rate-limits.yml)
- [FinOps](finops/punchh-finops.yml)
- [Webhooks](https://developers.partech.com/docs/dev-portal-webhooks-manager/8c18e3660f73f-event-guest)

## Features

| Name | Description |
|------|-------------|
| Loyalty Programs | Configurable points, rewards, tiers, and membership levels across channels. |
| Offers and Campaigns | Targeted offers, coupons, and personalized marketing campaigns driven by unified guest data. |
| Omnichannel Check-Ins | Earn loyalty across mobile, online ordering, POS, and kiosk channels. |
| Redemptions | Apply rewards, redeemables, and discounts against receipts with possible/create/void flows. |
| Webhooks Manager | Real-time event notifications for coupons, points, rewards, and guest lifecycle events. |
| Headless Offers | Surface Punchh-defined offers natively in external platforms via Platform Functions. |

## Use Cases

| Name | Description |
|------|-------------|
| Branded Mobile Loyalty App | Power a restaurant brand's mobile app with sign-in, profile, check-ins, and offers. |
| Online Ordering Rewards | Let guests earn and redeem loyalty on a digital ordering platform via SSO and check-in APIs. |
| POS Loyalty at the Counter | Look up guests, accrue points, and redeem rewards at the point of sale or kiosk. |
| External Offer Distribution | Pull Punchh redeemables into a CDP, messaging platform, or partner channel. |

## Integrations

| Name | Description |
|------|-------------|
| Point of Sale Systems | Integrations with restaurant POS platforms for in-store loyalty. |
| Online Ordering Platforms | Digital and online ordering platforms connect via the Online Ordering and SSO API. |
| Customer Data Platforms | Unify guest data with CDPs and CRMs. |
| Salesforce Marketing Cloud | Punchh Loyalty connector for Salesforce Marketing Cloud on AppExchange. |
| Messaging and Payment Gateways | Connects to messaging platforms, surveys, and payment gateways across dozens of categories. |

## Solutions

| Name | Description |
|------|-------------|
| Loyalty | Enterprise loyalty program management for restaurant brands. |
| Offers | Personalized offers and promotions engine. |
| Guest Engagement | Unified marketing and engagement across the guest lifecycle. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [punchh-mobile-openapi.yml](openapi/punchh-mobile-openapi.yml)
- [punchh-online-ordering-openapi.yml](openapi/punchh-online-ordering-openapi.yml)
- [punchh-platform-functions-openapi.yml](openapi/punchh-platform-functions-openapi.yml)
- [punchh-pos-openapi.yml](openapi/punchh-pos-openapi.yml)

### JSON Schema

- [mobile-access-token-schema.json](json-schema/mobile-access-token-schema.json)
- [mobile-create-user-request-schema.json](json-schema/mobile-create-user-request-schema.json)
- [mobile-login-request-schema.json](json-schema/mobile-login-request-schema.json)
- [mobile-mark-offers-read-request-schema.json](json-schema/mobile-mark-offers-read-request-schema.json)
- [mobile-transaction-details-request-schema.json](json-schema/mobile-transaction-details-request-schema.json)
- [mobile-transaction-details-schema.json](json-schema/mobile-transaction-details-schema.json)
- [mobile-update-user-profile-request-schema.json](json-schema/mobile-update-user-profile-request-schema.json)
- [mobile-user-session-schema.json](json-schema/mobile-user-session-schema.json)
- [online-ordering-online-order-checkin-request-schema.json](json-schema/online-ordering-online-order-checkin-request-schema.json)
- [online-ordering-online-order-checkin-response-schema.json](json-schema/online-ordering-online-order-checkin-response-schema.json)
- [online-ordering-online-order-redemption-request-schema.json](json-schema/online-ordering-online-order-redemption-request-schema.json)
- [online-ordering-online-order-redemption-response-schema.json](json-schema/online-ordering-online-order-redemption-response-schema.json)
- [platform-functions-redeemable-schema.json](json-schema/platform-functions-redeemable-schema.json)
- [pos-pos-checkin-request-schema.json](json-schema/pos-pos-checkin-request-schema.json)
- [pos-pos-user-schema.json](json-schema/pos-pos-user-schema.json)

### JSON Structure

- [mobile-access-token-structure.json](json-structure/mobile-access-token-structure.json)
- [mobile-create-user-request-structure.json](json-structure/mobile-create-user-request-structure.json)
- [mobile-login-request-structure.json](json-structure/mobile-login-request-structure.json)
- [mobile-mark-offers-read-request-structure.json](json-structure/mobile-mark-offers-read-request-structure.json)
- [mobile-transaction-details-request-structure.json](json-structure/mobile-transaction-details-request-structure.json)
- [mobile-transaction-details-structure.json](json-structure/mobile-transaction-details-structure.json)
- [mobile-update-user-profile-request-structure.json](json-structure/mobile-update-user-profile-request-structure.json)
- [mobile-user-session-structure.json](json-structure/mobile-user-session-structure.json)
- [online-ordering-online-order-checkin-request-structure.json](json-structure/online-ordering-online-order-checkin-request-structure.json)
- [online-ordering-online-order-checkin-response-structure.json](json-structure/online-ordering-online-order-checkin-response-structure.json)
- [online-ordering-online-order-redemption-request-structure.json](json-structure/online-ordering-online-order-redemption-request-structure.json)
- [online-ordering-online-order-redemption-response-structure.json](json-structure/online-ordering-online-order-redemption-response-structure.json)
- [platform-functions-redeemable-structure.json](json-structure/platform-functions-redeemable-structure.json)
- [pos-pos-checkin-request-structure.json](json-structure/pos-pos-checkin-request-structure.json)
- [pos-pos-user-structure.json](json-structure/pos-pos-user-structure.json)

### JSON-LD

- [punchh-mobile-context.jsonld](json-ld/punchh-mobile-context.jsonld)
- [punchh-online-ordering-context.jsonld](json-ld/punchh-online-ordering-context.jsonld)
- [punchh-platform-functions-context.jsonld](json-ld/punchh-platform-functions-context.jsonld)
- [punchh-pos-context.jsonld](json-ld/punchh-pos-context.jsonld)

### Examples

- [mobile-access-token-example.json](examples/mobile-access-token-example.json)
- [mobile-create-user-request-example.json](examples/mobile-create-user-request-example.json)
- [mobile-login-request-example.json](examples/mobile-login-request-example.json)
- [mobile-mark-offers-read-request-example.json](examples/mobile-mark-offers-read-request-example.json)
- [mobile-transaction-details-example.json](examples/mobile-transaction-details-example.json)
- [mobile-transaction-details-request-example.json](examples/mobile-transaction-details-request-example.json)
- [mobile-update-user-profile-request-example.json](examples/mobile-update-user-profile-request-example.json)
- [mobile-user-session-example.json](examples/mobile-user-session-example.json)
- [online-ordering-online-order-checkin-request-example.json](examples/online-ordering-online-order-checkin-request-example.json)
- [online-ordering-online-order-checkin-response-example.json](examples/online-ordering-online-order-checkin-response-example.json)
- [online-ordering-online-order-redemption-request-example.json](examples/online-ordering-online-order-redemption-request-example.json)
- [online-ordering-online-order-redemption-response-example.json](examples/online-ordering-online-order-redemption-response-example.json)
- [platform-functions-redeemable-example.json](examples/platform-functions-redeemable-example.json)
- [pos-pos-checkin-request-example.json](examples/pos-pos-checkin-request-example.json)
- [pos-pos-user-example.json](examples/pos-pos-user-example.json)

## Capabilities

Self-contained Naftiko capabilities, one per business surface, each exposing REST and MCP adapters.

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [PAR Punchh Mobile API — Check-Ins](capabilities/mobile-check-ins.yaml) | mobile | 1 | Integrator |
| [PAR Punchh Mobile API — Offers](capabilities/mobile-offers.yaml) | mobile | 1 | Integrator |
| [PAR Punchh Mobile API — Users](capabilities/mobile-users.yaml) | mobile | 3 | Integrator |
| [PAR Punchh Online Ordering and SSO API — Check-In](capabilities/online-ordering-check-in.yaml) | online | 1 | Integrator |
| [PAR Punchh Online Ordering and SSO API — Redemptions](capabilities/online-ordering-redemptions.yaml) | online | 1 | Integrator |
| [PAR Punchh Platform Functions API — Offers](capabilities/platform-functions-offers.yaml) | platform | 1 | Integrator |
| [PAR Punchh POS and Kiosk API — Check-Ins](capabilities/pos-check-ins.yaml) | pos | 1 | Integrator |
| [PAR Punchh POS and Kiosk API — Configuration](capabilities/pos-configuration.yaml) | pos | 2 | Integrator |
| [PAR Punchh POS and Kiosk API — Receipts](capabilities/pos-receipts.yaml) | pos | 1 | Integrator |
| [PAR Punchh POS and Kiosk API — Redemptions](capabilities/pos-redemptions.yaml) | pos | 3 | Integrator |
| [PAR Punchh POS and Kiosk API — Users](capabilities/pos-users.yaml) | pos | 2 | Integrator |

## Vocabulary

- [Punchh Vocabulary](vocabulary/punchh-vocabulary.yaml) — Unified taxonomy mapping 6 resources, 7 actions, 11 workflows, and 4 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [PAR Punchh Spectral Rules](rules/punchh-spectral-rules.yml) — 31 rules enforcing PAR Punchh API conventions

## Commercial

- [Plans and Pricing](plans/punchh-plans-pricing.yml) — API Commons Plans (enterprise / custom pricing, unreconciled)
- [Rate Limits](rate-limits/punchh-rate-limits.yml) — API Commons Rate Limits (partner-specific, unreconciled)
- [FinOps](finops/punchh-finops.yml) — FOCUS-aligned FinOps Framework artifact

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
