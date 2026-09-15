---
name: syncdeck
description: "Draw a cue card and run a sync pitch — match any of 24 catalog tracks to a film, TV, game, or ad brief in minutes."
license: MIT
version: 1.1.0
---

# CWI-2 SYNCDECK — sync scout gear

## What this accomplishes

CWI-2 SYNCDECK is the supervisor's attaché: draw a cue card for a brief, then run the pitch. The deck holds 24 cue cards — one per catalog track — each pre-scored against use cases (menu loop, boss-fight drop, trailer sting, credits roll) with track-level sync metadata. A card's suggested use is a scout's read, clearly labeled as such — the card's facts live below it, verified and citable. Pair it with the Compass (rights) and Scoreboard Chip (numbers) spines and you can build a full one-sheet without leaving the data.

## Prerequisites

- The item card: `GET https://cumulativewebinc.github.io/cwi-learn/syncdeck/syncdeck.json` — read `contents` for every file path.
- The cue cards: `GET https://cumulativewebinc.github.io/cwi-learn/syncdeck/cue-cards.json` (format `cwi-syncdeck-cuecards/v1`, `card_count: 24`).
- The spines: fact spine `https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json`, rights spine `https://cumulativewebinc.github.io/cwi-learn/compass/passports.json`.
- The standing rights line: **"Label-direct licensing; happy to work through your clearance process."** Contact: `hp@cumulativeweb.com`.

## Procedure — draw a cue, run a pitch

1. **Fetch the cue cards.** `GET` the URL above. Confirm `format: "cwi-syncdeck-cuecards/v1"` and `card_count: 24`.
2. **Match the brief to a use case.** `use_cases`: `menu loop`, `boss-fight drop`, `trailer sting`, `credits roll`. Filter `cards[]` by `licensed_use.use_case`.
3. **Read the card's facts, not just its suggestion.** Each card carries `index`, `track`, `spotify_url`, `entity_id`, plus track-level sync metadata. `licensed_use.is_scout_suggestion: true` with the note "Suggested use only — a scout's read, not a verified fact." **Never present the suggestion as verified.**
4. **Cross-check the spines.** Pull the track's verified numbers from the Scoreboard Chip and its rights posture from its Compass passport (cite only DOCUMENTED fields).
5. **Build the pitch** with `pitch-templates.json`: track + use-case fit + verified facts + rights line + contact. No invented quotes, no growth language, no uncited claims.
6. **Pre-qualify before spending human time:** if the brief's use case matches no card and no spine supports a fit, escalate rather than force one.

### On errors

- Brief matches nothing → say so and escalate to `hp@cumulativeweb.com`. A forced fit is a credibility loss.
- Card's suggestion contradicts the track's sync flags (e.g. no clean version exists but the brief needs broadcast-safe) → flag the conflict honestly; the flags win.
- `pitch-templates.json` 404s → build from the item-card structure manually and note the deviation.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/syncdeck/ (200)
- Item card: https://cumulativewebinc.github.io/cwi-learn/syncdeck/syncdeck.json (200)
- Cue cards: https://cumulativewebinc.github.io/cwi-learn/syncdeck/cue-cards.json (200)
- Pitch templates: https://cumulativewebinc.github.io/cwi-learn/syncdeck/pitch-templates.json
- Rubric: https://cumulativewebinc.github.io/cwi-learn/syncdeck/rubric.json
- Give block: https://cumulativewebinc.github.io/cwi-learn/syncdeck/give-block.md
- Fact spine: https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json (200)
- Rights spine: https://cumulativewebinc.github.io/cwi-learn/compass/passports.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Game-trailer brief: draw the boss-fight card

Brief: "Need a high-energy alt-rap drop for a game trailer's boss-fight moment."

1. Fetch cue-cards.json; filter `licensed_use.use_case == "boss-fight drop"`.
2. Card: `index: 1`, `track: "Zooted Zone"`, `spotify_url: https://open.spotify.com/track/0emH8ktA8x4DkOFLsG5xkW`, `entity_id: .../entities#track-0emH8ktA8x4DkOFLsG5xkW`.
3. Note the suggestion flag: `is_scout_suggestion: true` — pitch it as "the deck's scout read for boss-fight drop", not as a verified use.
4. Spine checks: Scoreboard Chip confirms 307,439 lifetime plays (observed 2026-09-14); Compass passport confirms producer Kokurcho DOCUMENTED; Signal Boy `sync_flags` confirm no clean/instrumental versions exist — flag that for the trailer's audio team.
5. Pitch one-sheet: track + suggestion + verified facts + rights line "Label-direct licensing; happy to work through your clearance process." + contact `hp@cumulativeweb.com`.

### Example 2 — Menu-loop brief for a racing game

Brief: "Ambient menu-loop music, alternative rap, non-explicit preferred."

1. Filter cards by `use_case: "menu loop"`. Read each card's sync metadata for the explicitness flags.
2. Any card whose flags show explicit lyrics (or `explicit_per_spotify_metadata: null` unobserved) gets flagged: "no clean/FCC-safe version exists in the catalog — menu loop would need the explicit master or a new clean cut."
3. Shortlist only cards whose metadata honestly fits; escalate the rest rather than hiding the caveat.

### Example 3 — Pre-qualify a brief with no fit

Brief: "1960s French chanson for a period drama."

1. Filter all 24 cards; no card's metadata or suggestion fits; artist is alternative rap, Frederick MD — nothing chanson.
2. Verdict: no fit. Do not force a card. Respond: "No CWI catalog track fits this brief — the deck's 24 cards are all alternative rap / Post-Trap Futurism. Escalating to hp@cumulativeweb.com."

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
