---
name: punchh-consume-webhooks
description: Stand up a consumer for the PAR Punchh Events Framework — pick an auth scheme, verify the endpoint, decode the envelope, and survive at-least-once delivery, out-of-order events and the circuit breaker.
api: Punchh Webhooks Manager
generated: '2026-08-13'
method: generated
source: asyncapi/punchh-webhooks.yml, https://developers.partech.com/docs/dev-portal-webhooks-manager
operations: []
---

# Punchh Webhooks Manager: build a consumer that survives

Punchh publishes 71 native event types across 8 families, plus 16 pre-shaped
adapter events for Braze and mParticle. There is **no AsyncAPI, no CloudEvents and
no JSON Schema** for this surface — the catalog in `asyncapi/punchh-webhooks.yml`
is the machine-readable index.

The framework must be enabled per business by a Punchh representative. It is not
self-service.

## 1. Register the endpoint

- HTTPS only. Punchh allows a **15 second** total request time.
- Pick one of four authentication schemes — Punchh discourages `none`:
  | Scheme | Headers |
  |---|---|
  | Basic | `authorization: basic base64(user:pass)` |
  | Bearer | `authorization: bearer <token>` |
  | HMAC-SHA1 | `authorization: hmac sha1(<URI+BODY>, <secret>)` + `x-pch-key: <client>` |
  | HMAC-SHA256 | `authorization: hmac sha256(<URI+BODY>, <secret>)` + `x-pch-key: <client>` |

  Choose HMAC-SHA256. `x-pch-key` identifies which secret to verify against; if you
  have no client identifier, use your system name in snake_case.
- Punchh calls your URL with **GET** to verify and activate it, and then again as a
  health check once a day or every 6 hours. Your GET handler must answer 200 —
  many consumers only implement POST and get deactivated.

## 2. Decode the envelope

Every event, regardless of type, arrives as:

```json
{
  "content_id": "<uuid>",
  "timestamp": 1619693178,
  "business_id": 6,
  "business_uuid": "<uuid>",
  "business_slug": "slugname",
  "event_name": "transactional_notifications",
  "event_type": "gift_card_auto_reload_payment_error",
  "action": "create",
  "payload": {}
}
```

Route on `event_name` + `event_type` + `action`. **All Punchh integer IDs are
int64** — parsing them as int32 will silently corrupt guest and business ids.

## 3. Assume at-least-once and out-of-order

Punchh states both explicitly:

- **Duplicates are expected.** Deduplicate on `content_id` and validate
  `timestamp`. Persist `content_id` for at least the retry horizon (a 5xx path can
  redeliver up to 2 hours after the first attempt).
- **Ordering is not guaranteed.** A later event can be processed before its parent.
  Never derive state from arrival order — reconcile against the REST API instead.

## 4. Answer correctly, because the retry ladder is unforgiving

| You return | Punchh does |
|---|---|
| `200` or `202` | Success |
| `429` | 3 retries at 15 / 45 / 180 seconds |
| `408` | 3 retries at 15 / 45 / 180 seconds |
| `5xx` | 7 retries at 60 / 120 / 300 / 600 / 1800 / 3600 / 7200 seconds |
| `3xx` | **Treated as a failure and never retried** — the event is lost |

Never redirect a webhook endpoint. A trailing-slash redirect silently drops events.

## 5. Know the circuit breaker

Past the retry window, once the failure counter exceeds **1000** the event and all
its queued events are **suspended** — no new deliveries at all. Recovery is a
successful response to a ping webhook, which an admin can send manually from the
Webhooks Manager. Punchh also auto-pings at 5 minutes, 10 minutes, then every 2
hours for 6 attempts; after that the webhook is **deactivated** and needs manual
re-enablement. Punchh emails the admin on the base URL when this happens — make
sure that address is a monitored alias, not a person who left.

## 6. Locale and transformation are yours

Messages are ENU-only with UTC timestamps, in Punchh's own JSON structure. Punchh
performs no transformation to your schema, and no locale conversion. If you need
Braze or mParticle shapes specifically, Punchh publishes dedicated adapter
documentation for both — use those rather than transforming the native events
yourself.

## Related

- `asyncapi/punchh-webhooks.yml` — the full event catalog
- `conventions/punchh-conventions.yml` — idempotency uses `content_id`, not an Idempotency-Key header
- `lifecycle/punchh-lifecycle.yml`
