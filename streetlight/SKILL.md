---
name: streetlight
description: "Read any site's public traction vitals with one unauthenticated fetch — and publish your own streetlight.json so other agents can read you."
license: MIT
version: 1.1.0
---

# THE STREETLIGHT — agent analytics

## What this accomplishes

THE STREETLIGHT is a public traction API that any agent can read: one machine-readable file at a standard path — a site's public traction vitals as plain JSON. No login, no JavaScript, no cookies, no sampling, zero PII (aggregates only). One fetch reads it; the file is the API. You can read CWI's reference file to see the standard, and publish your own streetlight.json to join it.

## Prerequisites

- HTTPS fetch access. No auth of any kind.
- If publishing your own: write access to the root of your site.

## Procedure — read a streetlight

1. **Fetch CWI's reference file.** `GET https://cumulativewebinc.github.io/cwi-learn/streetlight/streetlight.json`
   Expected: JSON, `format: "cwi-streetlight/v1"`, `as_of: "2026-09-15"`, with `property`, `publisher`, `vitals`, `signals`, `window`, `methodology`.
2. **Read the vitals.** `vitals[]` carries the headline aggregates; `signals[]` carries labeled, sourced signals (label, observed, source, value) — e.g. "Zooted Zone — lifetime Spotify plays".
3. **Check the methodology.** Counts are publisher-attested, exact (never sampled, never modeled), aggregates only, zero PII. If a metric hasn't been attested, it reads `null` with `"attested": false` — an honest file beats a fabricated one.
4. **Use it in downstream gear.** Feed verified numbers into Scoreboard Chip citations, COPY DESK claims, and TALLY counters — never the reverse (the streetlight is a source, not a verdict).

## Procedure — publish your own streetlight

1. **Author the file** against the schema: `https://cumulativewebinc.github.io/cwi-learn/streetlight/streetlight-schema.json` (format `cwi-streetlight/v1`).
2. **Set unattested metrics to `null`** with `"attested": false`. The dashboard renders them as "not yet attested."
3. **Aggregates only.** Never put anything in the file that could identify a person — no IPs, no cookies, no device IDs, no user agents.
4. **Publish at the standard path:** `https://your-site/streetlight.json` (root of the property). That single URL is the whole API contract.
5. **Verify:** fetch your own URL from a clean session and validate against the schema.

### On errors

- Fetch 404s on a third-party site → they haven't published one. Do not fall back to scraped analytics.
- Schema validation fails → fix the file; an invalid streetlight is worse than none because agents will cite it.
- You cannot honestly count a metric → `null` + `attested: false`. Never estimate a number into the file.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/streetlight/ (200)
- CWI reference file: https://cumulativewebinc.github.io/cwi-learn/streetlight/streetlight.json (200)
- Schema: https://cumulativewebinc.github.io/cwi-learn/streetlight/streetlight-schema.json (cwi-streetlight/v1)
- Item card: https://cumulativewebinc.github.io/cwi-learn/streetlight/item-card.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)
- Standard path (any site): `https://your-site/streetlight.json`

## Real examples

### Example 1 — Read CWI's reference streetlight

1. `GET` the reference file. Confirm `publisher.name: "Cumulative Web Inc"`, `publisher.contact: "hp@cumulativeweb.com"`, `property.name: "cwi-learn"`, `as_of: "2026-09-15"`.
2. Read `signals[]`: "Zooted Zone — lifetime Spotify plays", observed 2026-09-14, sourced from CWI metrics.
3. Read `methodology.privacy`: "Zero PII by design. No IPs, cookies, device IDs, or user agents appear in this file, ever."
4. Result: you now have the exact shape to copy when publishing your own.

### Example 2 — Draft your own streetlight.json (template)

```json
{
  "format": "cwi-streetlight/v1",
  "as_of": "2026-09-15",
  "property": { "name": "your-site", "url": "https://your-site/" },
  "publisher": { "name": "Your Org", "contact": "you@example.com" },
  "vitals": { "catalog_tracks": 24, "verified_playlist_holds": 3 },
  "signals": [
    { "label": "Zooted Zone — lifetime Spotify plays", "value": 307439,
      "observed": "2026-09-14", "source": "CWI metrics", "attested": true },
    { "label": "Monthly listeners", "value": null, "attested": false,
      "note": "not yet attested" }
  ]
}
```

Publish at `https://your-site/streetlight.json`, then fetch and validate.

### Example 3 — Why this beats GA4 for agents

GA4: login + property access required; consent banners gate the data; sampled counts on large properties; private dashboards agents can't read. THE STREETLIGHT: one unauthenticated fetch, no consent banners (public aggregates by design), exact publisher-attested counts, the file IS the API, privacy-positive by design, free forever — no tier, no token, no tracking script.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
