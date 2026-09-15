# DOGFOOD — Agent Deck skill packs, cold-agent value test

**Date:** 2026-09-15
**Tester posture:** cold outside agent (like our friends' agents in Brazil). Read ONLY the SKILL.md, then attempted the task against the live URLs at https://cumulativewebinc.github.io/cwi-learn/ (all 18 product pages + gear.json re-verified 200 before testing).
**Standard:** every skill version 1.1.0. A task PASSes when the cold agent completes it end-to-end with no outside help.

## Test results (6 required skills)

### 1. signal-skin — "equip the Zooted Bloom SKIN config"
**PASS.** Followed the skill's equip procedure: `GET /skin/skins.json` → `count: 4`, `format: cwi-skin/v1` confirmed → selected `skin_id: "zooted-bloom"` → applied the exact token block from Example 1 (palette `#a3ff5e` family, gradient `#231b3a→#0b1f10`, neon-bar track accent, header circular-badge logo lockup) → verified the brand rule (logo ringed `#a3ff5e`). Produced the exact config an agent would apply. No stumbles.

### 2. first-spin — "triage this track for sync-readiness"
**PASS (after fix).** Reproduced the Zooted Zone worked verdict end-to-end: scores 3/5/4/2/5 with confidence labels, weighted total 3.9 → 78 → band **advance**, no deal-breakers triggered, sync-readiness triage verdict "pitchable only with a legal caveat" — matching the live `sample-verdict.json` exactly.
**Stumble found:** Step 2 told the agent to gather evidence from "catalog records (cartridge.json)" but the skill never gave the cartridge.json URL — a cold agent would stall or guess the path.
**Fix applied:** added the catalog evidence source URL (`/walkman/cartridge.json`) to Prerequisites, with the note that non-CWI tracks cite their platform listings.
**Re-test:** cold run now completes — evidence URLs resolve, verdict reproduces 78/advance.

### 3. signal-boy — "load the 24-track catalog carrier"
**PASS.** Followed the load sequence: `GET /walkman/cartridge.json` → `track_count: 24` confirmed → parsed the per-track data shape (spotify_url, verified_credits, placement, sync_flags) → answered the check question from the manifest alone ("Zooted Zone: prod. Kokurcho, #30 on New Rap Hits, scan 2026-09-15") → composed a valid `CWI-HANDOFF` line. No stumbles. The "cite only manifest fields" rule held under a deliberate temptation to fill undocumented credits.

### 4. copy-desk — "truth-gate this claim about Zooted Zone's streams"
**PASS.** Gated "Zooted Zone has 307,439 lifetime Spotify plays": PULL `copy-desk.json` → unit `zooted-zone-story`, claim 1 matches ("Zooted Zone holds 307,439 lifetime Spotify plays", source CWI Intelligence Engine metrics, observed 2026-09-14) → deny-list scan clean → verdict **PASS** with full citation. Also gated the contrast claim ("climbing fast with 500K streams") → correctly **FAILED** on both the deny-list and the registry. No stumbles.

### 5. tally — "report verified playlist placements"
**PASS.** Fetched `tally.json`, filtered to `verified: true`, produced: **Shaka Zulu #21, Zooted Zone #30, Doves & Diamonds #31** on New Rap Hits (full playlist scan 2026-09-15, proof URL attached) — matches the live data exactly. Correctly ignored no unverified counters. No stumbles.

### 6. one-stop — "check clearance for a gaming sync"
**PASS.** Checked "Zooted Zone for a game mod": catalog lookup → `tbhh-001`, in scope → use `game-mod` = commercial → tier **Commercial = DRAFT, not issuable** → returned the clearance checklist with verdict **NOT ISSUABLE — route to hp@cumulativeweb.com**, and drafted nothing. This is the honest outcome the live site mandates (Creator tier live, Indie/Commercial pending Black's exact-terms approval). Also verified the contrast path: a Creator-tier stream-overlay grant builds and validates. No stumbles.

## Stumble log (all found + fixed)

| # | Skill | Stumble | Fix | Re-test |
|---|---|---|---|---|
| 1 | first-spin | Evidence-gathering step referenced `cartridge.json` but gave no URL — cold agent stalls | Added catalog evidence source URL to Prerequisites | PASS |

## Incidental finding (not a skill bug)

During URL verification, a parallel 24-request burst returned 404s for URLs that individually return 200 (including `/llms.txt` and `/catalog.json`, both 200 when fetched serially). Cause: GitHub Pages transient under concurrency, not missing files. Skills therefore instruct serial, single-fetch patterns — no batch assumptions were written into any procedure.

## Sign-off

All 6 dogfood tasks PASS. All 18 skills at v1.1.0. No invented data used — every example traces to a live 200 response fetched 2026-09-15.
