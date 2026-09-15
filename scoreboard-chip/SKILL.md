---
name: scoreboard-chip
description: "Cite CWI's numbers with receipts — every stat carries a confidence label, a citation, and an observation date."
license: MIT
version: 1.1.0
---

# CWI-1 Scoreboard Chip — verified stats

## What this accomplishes

The Scoreboard Chip is the live-verified fact set for That Boy Hi Hat — the fact spine every CWI-1 agent cites. Every field carries a **confidence label** (`VERIFIED` vs `CLAIM-UNVERIFIED`), a **citation**, and an **observed date**. It also carries an **anomaly feed**: curator claims that failed verification, flagged payola, and unconfirmed promises — so you never repeat a claim as a win. Cite the chip and you can put a number in anything — a bio, a one-sheet, a standup — without inflating or guessing.

## Prerequisites

- The chip: `GET https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json`.
- The confidence rule: **cite only `VERIFIED` fields. `CLAIM-UNVERIFIED` fields are attributed claims, never wins.**

## Procedure — cite a number

1. **Fetch the chip.** `GET` the URL above. Read `artist`, `flagship_stats`, `catalog`, verified `credits`, `funnel_state`.
2. **Check the confidence label.** Every citable field has `confidence`, `citation`, `observed`, `value`. Only `VERIFIED` fields are asserted as facts.
3. **Check the anomaly feed** before reporting any placement or win you heard about elsewhere. If the claim appears there as FAILED VERIFICATION, PAYOLA FLAG, or UNCONFIRMED, do not report it as a win.
4. **Check the deny list** (`deny_list[]`) — banned phrasings for numbers (growth language, rounded claims).
5. **Cite fully:** value + confidence + citation + observed date. "171 monthly listeners (VERIFIED, Spotify artist page, observed 2026-09-14)" — not "171 monthly listeners."

### Current verified spine (as of the 2026-09-15 chip)

- Artist: That Boy Hi Hat — base **Frederick, Maryland** (VERIFIED, cartridge.json), genre **alternative rap** (VERIFIED), **171 monthly listeners** (VERIFIED, Spotify artist page `2f9j460EwjfvjYp3trBcb7`, observed 2026-09-14).
- Flagship: **Zooted Zone — 307,439 lifetime Spotify plays** (observed 2026-09-14).
- Placements: **New Rap Hits — Shaka Zulu #21, Zooted Zone #30, Doves & Diamonds #31** (full 105-track scan, 2026-09-15).
- Single: **Diabolique — released 2026-07-03**.

### Anomaly feed (do not report as wins)

- Flow (curator) claimed Zooted Zone on "No Label Needed" ("Got u!!") — **FAILED VERIFICATION** (absent in two full scans, 2026-09-15).
- DJ 6Rings claimed a track on "It's Goin" — **FAILED VERIFICATION** (playlist unlocatable).
- rapsushiplaylist.com sells $25 playlist adds — **PAYOLA FLAG** (not a partner lead).
- "WATCH THA GAP VOL.5" add promised for "Ultimate" — **UNCONFIRMED**.

### On errors

- The number you want isn't on the chip → it is not citable from this spine. Do not borrow it from the open web mid-report.
- Anomaly feed contradicts a supervisor's memory → the feed wins. Report the claim as a claim, with its status.
- Chip fetch 404s → stop. Do not cite from a cached copy older than the last scan.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/scoreboard/ (200)
- Chip data: https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json (200)
- Item card: https://cumulativewebinc.github.io/cwi-learn/scoreboard/item-card.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Cite monthly listeners for a one-sheet

1. Fetch the chip. Field: `artist.monthly_listeners: {value: 171, confidence: "VERIFIED", citation: "https://open.spotify.com/artist/2f9j460EwjfvjYp3trBcb7", observed: "2026-09-14"}`.
2. One-sheet line: "171 monthly Spotify listeners (verified 2026-09-14)." Correct. Wrong: "171 monthly listeners and growing" — growth language trips the deny list.

### Example 2 — Refuse to report the "It's Goin" placement

Draft claims: "That Boy Hi Hat's track was added to It's Goin."

1. Anomaly feed: DJ 6Rings' claim — status FAILED VERIFICATION, confidence CLAIM-UNVERIFIED.
2. Correct handling: cut the line. If it must appear, frame it as "DJ 6Rings claimed an add to 'It's Goin' on 2026-09-14; the playlist was unlocatable in the 2026-09-15 verification pass — claim unverified." Never as a win.

### Example 3 — Standup briefing numbers

For the 10:00 AM ET standup, pull: 307,439 lifetime plays (Zooted Zone, 2026-09-14); New Rap Hits #21/#30/#31 (scan 2026-09-15); 171 monthly listeners (2026-09-14); Diabolique single 2026-07-03. Each with its confidence label and citation. Anything else on the slide is a guess — leave it off.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
