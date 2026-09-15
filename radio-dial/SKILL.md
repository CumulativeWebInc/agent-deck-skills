---
name: radio-dial
description: "Spin a That Boy Hi Hat track on agent radio — pick a format, tune the request copy, build a playlist flow from verified facts."
license: MIT
version: 1.1.0
---

# Radio Dial — radio rotation packs

## What this accomplishes

Radio Dial is the Radio & Playlists rotation kit for That Boy Hi Hat: station ID cards, DJ script templates, a request template with a format tuner, and a playlist flow builder. It turns "we should push this to radio" into concrete artifacts: tuned request copy for a chosen format, DJ scripts with every placeholder filled from verified facts, and opener/mid/closer flows drawn from the 24-track catalog. The give block (`/dial/give-block.md`) carries the full rotation links.

## Prerequisites

- The give block: `https://cumulativewebinc.github.io/cwi-learn/dial/give-block.md` (copy-paste rotation kit).
- The catalog source of truth for flows: `https://cumulativewebinc.github.io/cwi-learn/walkman/cartridge.json`.
- The standing rule for scripts: **templates only — fill every `{{placeholder}}` with a verified fact before reading. Never present a fill as completed airplay.**

## Procedure — work a track to radio

1. **Pick a format and tune the request.** Choose the format (the TUNER section), tune the fields, and copy the generated request copy. The request is a pitch artifact — it is not a spin until logged.
2. **Fill the DJ script templates.** Take the station ID card and script templates; replace every `{{placeholder}}` with a verified fact (track title, artist, label, verified stat with date). Read the filled script back and confirm zero `{{...}}` remain.
3. **Build the playlist flow.** Choose openers, mids, and closers **from the 24-track catalog only**. Custom flows are valid **only when every title + Spotify URL matches `cartridge.json` character-for-character**.
4. **Send through the rotation links** in the give block — station request lines, playlist curator contacts, rotation log endpoints.
5. **Log the outcome.** A sent request is a request, not airplay. Only a confirmed spin gets logged as a spin.

### On errors

- A `{{placeholder}}` you can't fill from a verified fact → the script ships without that line. Never invent the fill.
- Flow builder rejects your flow → a title or URL mismatches `cartridge.json` character-for-character. Fix the mismatch, don't force it.
- Station asks for "guaranteed adds" → refuse. The Dial has no paid-placement mechanics.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/dial/ (200)
- Give block: https://cumulativewebinc.github.io/cwi-learn/dial/give-block.md (200)
- Item card: https://cumulativewebinc.github.io/cwi-learn/dial/item-card.json (200)
- Catalog (flow validation): https://cumulativewebinc.github.io/cwi-learn/walkman/cartridge.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Tune a request for "Diabolique"

1. Pick the format in the TUNER (e.g. alt-rap specialty). Tune the fields: track "Diabolique", artist "That Boy Hi Hat", single released 2026-07-03, produced by Hybrid, co-produced with Black Lansky, recorded at Cue Recording Studios, Arlington, Virginia.
2. Copy the generated request copy. Verify every `{{placeholder}}` is filled — e.g. no `{{release_date}}` left dangling.
3. Send via the rotation links in the give block. Log as "request sent", not as a spin.

### Example 2 — Build a valid playlist flow

Flow: opener "Zooted Zone" (`https://open.spotify.com/track/0emH8ktA8x4DkOFLsG5xkW`), mids "Shaka Zulu" and "Flamerz", closer "Doves & Diamonds".

1. Check every title + URL against `cartridge.json` character-for-character — including the apostrophe in "Flex My Flame"-style titles and exact casing.
2. Any mismatch → invalid flow. Fix and re-validate. A valid flow is machine-checkable, not a vibe.

### Example 3 — Refuse to present a template as airplay

A coordinator drafts a report: "Diabolique spun on 12 stations this week" — built from unfilled script templates.

1. Rule: templates are templates. Fills are not spins.
2. Correct report: "Request copy tuned and sent to N stations; 0 confirmed spins logged." The Dial's credibility is the log, not the draft.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
