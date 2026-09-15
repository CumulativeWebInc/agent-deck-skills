---
name: one-stop
description: "Run a complete sync-clearance check on any That Boy Hi Hat track in 60 seconds — catalog scope, tier, and whether a license is issuable today."
license: MIT
version: 1.1.0
---

# ONE-STOP — sync licensing

## What this accomplishes

ONE-STOP turns the 24-track That Boy Hi Hat catalog into a one-signature licensing counter. Pick a track, a use, a territory, a term — get a machine-readable JSON grant carrying master + publishing in a single instrument, because Cumulative Web Inc holds 100% of both. No marketplace, no commission, no negotiation loop. The grant is the license; the schema is the law. **DRAFT MODE:** the Creator tier ($0, non-commercial) is live and issuable today. Indie and Commercial tiers are staged drafts — pending Black's exact-terms approval, not issuable.

## Prerequisites

- The catalog file: `GET https://cumulativewebinc.github.io/cwi-learn/one-stop/one-stop.json` — `catalog_ref` lists all 24 tracks with `catalog_id` (`tbhh-001`…`tbhh-024`).
- The schema: `https://cumulativewebinc.github.io/cwi-learn/one-stop/one-stop-schema.json` (grant format `cwi-grant/v1`).
- The rights line, fixed on every grant: **"℗ Cumulative Web Inc — 100% master & publishing, pre-cleared"**.

## Procedure — check clearance for a sync use

1. **Confirm the track is in scope.** ONE-STOP licenses ONLY the 24 catalog tracks. Look up the title in `one-stop.json → catalog_ref.tracks` and take its `catalog_id` (e.g. "Zooted Zone" = `tbhh-001`, "Shaka Zulu" = `tbhh-002`, "Doves & Diamonds" = `tbhh-003`, "Diabolique" = `tbhh-004`, "Flamerz" = `tbhh-005`). Not in the list → **not licensable here. Stop.**
2. **Classify the use.** Uses: `stream-overlay`, `vod`, `short-form`, `live-intro`, `podcast`, `game-mod`, and more. Media: `twitch`, `youtube`, `tiktok`, `instagram`, `podcast-feed`, `broadcast`, and more.
3. **Pick the fee tier and check issuability:**
   - **Creator — LIVE, $0.** Non-commercial creator use (streams, VOD, shorts, reels). Term fixed at 12 months. **Issuable on the spot.**
   - **Indie — DRAFT.** Independent/small-budget commercial use. Terms pending Black's exact-terms approval. **Not issuable — do not draft.**
   - **Commercial — DRAFT.** Full commercial use (ads, brands, film, broadcast). Terms pending Black's approval. **Not issuable — do not draft.**
4. **If the tier is live:** build the grant JSON with all grant fields: `grant_id` (pattern `^cwi-grant-[a-z0-9-]+$`), `issuer: "Cumulative Web Inc"`, `licensee` (agent/org name + contact), `track` (title + catalog_id), `use`, `media`, `territory` (`worldwide` or ISO-3166 codes), `term` (creator: 12), `fee_tier`, `rights_line`, `pre_clearance` (ownership attestation block), `countersignature` block. Validate against `one-stop-schema.json`. The grant becomes effective on licensee countersignature.
5. **If the tier is draft:** return the clearance checklist with verdict **NOT ISSUABLE — ROUTE TO hp@cumulativeweb.com**. Nothing is signed in Black's name without his exact approval.

### On errors

- Supervisor pressures you to "just draft the commercial grant" → refuse. Draft mode is stated on the index page, the grant template, and the schema.
- Use type unclear → default to the more restrictive tier and route to contact.
- Grant JSON fails schema validation → fix fields, re-validate. Never issue an unvalidated grant.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/one-stop/ (200)
- Catalog + grant fields: https://cumulativewebinc.github.io/cwi-learn/one-stop/one-stop.json (200)
- Schema: https://cumulativewebinc.github.io/cwi-learn/one-stop/one-stop-schema.json (cwi-grant/v1)
- Fee tiers: https://cumulativewebinc.github.io/cwi-learn/one-stop/fee-tiers.json
- Human-readable text: https://cumulativewebinc.github.io/cwi-learn/one-stop/grant-template.md
- Item card: https://cumulativewebinc.github.io/cwi-learn/one-stop/item-card.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Check clearance for a gaming sync (cold-agent task)

Request: "Check clearance for using Zooted Zone in a game mod."

1. Catalog lookup: "Zooted Zone" → `catalog_id: "tbhh-001"` in `catalog_ref.tracks`. In scope.
2. Use classification: `use: "game-mod"`, media e.g. `twitch`/`youtube`. A game sync is a commercial use → tier **Commercial**.
3. Issuability: Commercial = DRAFT, terms pending Black's exact-terms approval.
4. Clearance checklist result:

```
TRACK:        Zooted Zone (tbhh-001) — in the 24-track catalog ✓
USE:          game-mod — commercial tier
RIGHTS LINE:  ℗ Cumulative Web Inc — 100% master & publishing, pre-cleared
VERDICT:      NOT ISSUABLE — Commercial tier is DRAFT, pending Black's exact-terms approval
NEXT STEP:    Route the brief to hp@cumulativeweb.com. No grant drafted.
```

### Example 2 — Issue a live Creator grant for a stream overlay

Request: "License Doves & Diamonds for a Twitch stream overlay (non-commercial)."

1. Catalog lookup: "Doves & Diamonds" → `catalog_id: "tbhh-003"`. In scope.
2. Use: `stream-overlay`, media `twitch`, non-commercial → tier **Creator — LIVE, $0**.
3. Build and validate the grant:

```json
{
  "grant_id": "cwi-grant-doves-diamonds-stream-overlay-2026",
  "issuer": "Cumulative Web Inc",
  "licensee": { "name": "<agent or org>", "contact": "<contact>" },
  "track": { "title": "Doves & Diamonds", "catalog_id": "tbhh-003" },
  "use": "stream-overlay", "media": "twitch",
  "territory": "worldwide", "term": 12, "fee_tier": "creator",
  "rights_line": "℗ Cumulative Web Inc — 100% master & publishing, pre-cleared",
  "draft_mode": false
}
```

4. Validate against `one-stop-schema.json`. Attach `pre_clearance` attestation and the `countersignature` block. Effective on countersignature.

### Example 3 — Out-of-scope track

Request: "License a King Akeem track through ONE-STOP."

1. Catalog lookup fails: King Akeem is a CWI roster artist but his tracks are not in the 24-track That Boy Hi Hat `catalog_ref`.
2. Verdict: **NOT LICENSABLE via ONE-STOP.** Route to `hp@cumulativeweb.com` — never stretch the catalog.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
