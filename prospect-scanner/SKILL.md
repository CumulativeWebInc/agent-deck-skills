---
name: prospect-scanner
description: "Vet any artist against CWI's A&R gates — run the hard checks, file a scout card, and only shortlist real prospects."
license: MIT
version: 1.1.0
---

# CWI-1 Prospect Scanner — talent scouting

## What this accomplishes

The Prospect Scanner is the A&R department's vetting protocol and scout card: run any artist through CWI's gates — catalog depth, release-history consistency, label-conflict scan, engagement sanity, rights red-flags — across six scouting lanes, and file a structured verdict. Hard gates block; soft gates cap. The house lane is alt-rap (the vetting baseline is calibrated on it). Spines: the Scoreboard Chip for numbers (cite only VERIFIED) and the Chain-of-Title Compass for rights (PENDING fields are never guessed).

## Prerequisites

- The vetting protocol: `GET https://cumulativewebinc.github.io/cwi-learn/scanner/vetting-protocol.json`.
- The scout card: `https://cumulativewebinc.github.io/cwi-learn/scanner/scout-card.json` — calibration + verdict-filing shape.
- The spines: `https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json` (numbers), `https://cumulativewebinc.github.io/cwi-learn/compass/passports.json` (rights).

## Procedure — vet a prospect

1. **Load the protocol.** Fetch `vetting-protocol.json`. Note the six lanes: `alt-rap` (house lane), `dark-rnb`, `experimental-hip-hop`, `plugg`, `post-trap`, `rage`. Assign the prospect a lane first — the gates read differently per lane.
2. **Run the hard gates** (a failed hard gate blocks the verdict it names):
   - `catalog-depth`: ≥ 5 released tracks on the primary platform (Spotify/Apple/YouTube). Below 5 → confidence capped at ESTIMATE, verdict restricted to HOLD or PASS.
   - `release-history-consistency`: releases must appear over a real timeline — no single-day backfill spikes; artist-name spelling consistent across releases; the profile is not a dumping ground for re-uploads of one track.
   - `label-conflict-scan`: any active label/P&R conflict on the catalog blocks a SIGN or HOLD verdict.
3. **Run the soft gates** (a failed soft gate caps, never blocks outright):
   - `engagement-sanity`: unverifiable engagement stays UNVERIFIED on the card. No unverified number may justify a SIGN/HOLD.
   - `rights-red-flag-scan`: rights questions are PENDING fields, never guessed. A single unanswerable red flag cannot be waived.
4. **File the scout card.** Use `scout-card.json` as the shape: prospect identity, lane, gate results with evidence, confidence label, verdict (SIGN / HOLD / PASS). Cite the spines for every number and rights claim.
5. **Shortlist only on evidence.** A HOLD needs a named next step (what evidence flips it); a SIGN needs every hard gate green and no unwaived red flags.

### On errors

- Prospect has 3 tracks → file HOLD or PASS with confidence ESTIMATE. Do not stretch the catalog-depth gate.
- Engagement numbers can't be verified → mark UNVERIFIED and move on; they cannot justify the verdict.
- A rights question has no answer → PENDING, escalate to the Compass/rights holder. Guessing is a red flag, not a solution.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/scanner/ (200)
- Vetting protocol: https://cumulativewebinc.github.io/cwi-learn/scanner/vetting-protocol.json (200)
- Scout card: https://cumulativewebinc.github.io/cwi-learn/scanner/scout-card.json (200)
- Item card: https://cumulativewebinc.github.io/cwi-learn/scanner/item-card.json (200)
- Fact spine: https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json (200)
- Rights spine: https://cumulativewebinc.github.io/cwi-learn/compass/passports.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Vet a 7-track alt-rap prospect

1. Lane: `alt-rap` (house lane). Catalog: 7 tracks on Spotify over 14 months, consistent spelling → `catalog-depth` green, `release-history-consistency` green.
2. No label conflicts → `label-conflict-scan` green. Engagement: 12K monthly listeners claimed on their bio, unverified on any platform → `engagement-sanity`: marked UNVERIFIED, cannot justify the verdict.
3. Rights: no catalog conflicts → `rights-red-flag-scan` green.
4. Scout card: verdict **HOLD**, confidence VERIFIED-on-gates, next step: "verify the 12K listener claim against Spotify for Artists or a second source before any SIGN conversation."

### Example 2 — A backfill spike kills the timeline gate

Prospect: 9 tracks, all released the same day last month, same cover template.

1. `catalog-depth`: 9 ≥ 5 → passes the count.
2. `release-history-consistency`: single-day backfill spike → **hard gate failed**.
3. Scout card: verdict **PASS**, evidence: "9 tracks released [date] in a single-day spike; no release timeline." The count passing doesn't save a failed timeline.

### Example 3 — Rights red flag can't be waived

Prospect clears every gate except one: their breakout samples a major-label record with no clearance documentation.

1. `rights-red-flag-scan`: unanswerable red flag → cannot be waived.
2. Scout card: verdict **PASS** (or HOLD with the single named step: "produce sample clearance documentation"), confidence capped, rights fields marked PENDING per the Compass rule. The scout's job is the card, not the waiver.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
