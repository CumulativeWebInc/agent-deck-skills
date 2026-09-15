---
name: first-spin
description: "Triage any track or demo with CWI's first-listen rubric — score five criteria, flag deal-breakers, ship a structured verdict JSON."
license: MIT
version: 1.1.0
---

# THE FIRST SPIN — talent evaluation

## What this accomplishes

THE FIRST SPIN turns a demo or catalog track into a structured, defensible verdict in one pass: five weighted criteria scores with confidence labels and cited sources, five deal-breaker flags, and a band verdict (`sign` / `advance` / `develop` / `pass`). It is honest-by-construction — no score ships without a cited source, uncited scores are capped, and a failing verdict ships with exactly what evidence would flip it. $0, no login, no API key.

## Prerequisites

- The rubric config: `GET https://cumulativewebinc.github.io/cwi-learn/first-spin/first-spin.json` (format `cwi-first-spin/v1`).
- The schema: `https://cumulativewebinc.github.io/cwi-learn/first-spin/first-spin-schema.json` (JSON Schema draft 2020-12; validates both the config and your verdict output).
- The empty verdict skeleton: `https://cumulativewebinc.github.io/cwi-learn/first-spin/verdict-template.json`.
- The worked example: `https://cumulativewebinc.github.io/cwi-learn/first-spin/sample-verdict.json`.
- The catalog evidence source for CWI tracks: `https://cumulativewebinc.github.io/cwi-learn/walkman/cartridge.json` (24 tracks: title, Spotify URL, verified credits, playlist placements, play counts, sync flags). For non-CWI tracks, evidence comes from the platforms themselves (Spotify/Apple/YouTube) — cite the listing URL.

## Procedure — run a First Spin

1. **Load the rubric.** Fetch `first-spin.json`. Confirm the five criteria and weights:
   `hook_density` 0.25 · `replay_pull` 0.25 · `lane_clarity` 0.15 · `sync_readiness` 0.15 · `momentum_evidence` 0.20.
2. **Gather evidence.** Collect only citable facts: catalog records (`cartridge.json`), scans, credits, release dates. Each score needs at least one source URL + observation date, or it gets capped.
3. **Score 0–5 per criterion.** Apply the confidence rules exactly:
   - A score based on listening judgment without a cited session = `estimated` → **capped at 3**.
   - A score with no citable evidence = `unverifiable` → **capped at 1**.
   - A criterion with zero citations is **unverifiable by definition**.
4. **Check the five deal-breaker flags**: `payola_adjacency`, `claimed_as_verified`, `rights_disputed`, `stream_inflation`, `no_verifiable_presence`. Each flag is `triggered: true/false` with notes. If any flag triggers, the verdict **caps at `develop`** — except `rights_disputed` or `no_verifiable_presence`, which cap at **`pass`**.
5. **Compute the verdict.** `weighted_total` = Σ(score × weight); `weighted_percent` = weighted_total × 20. Bands: **sign** 90–100 · **advance** 75–89 · **develop** 50–74 · **pass** 0–49.
6. **Ship the verdict JSON** (`format: "first-spin-verdict/v1"`) with: `subject`, `scores[]` (criterion, score, score_confidence, sources), `deal_breakers[]`, `weighted_total`, `weighted_percent`, `band`, `evidence_that_flips_it[]`, `evaluation_date`, `evaluated_by`. Validate against the schema before filing.
7. **(Optional)** Compose the ledger handoff line as in the sample verdict (`CWI-HANDOFF gear=first-spin verdict=<percent> band=<band> ...`) when filing to the Gear Ledger.

### On errors

- Schema validation fails → your verdict JSON is malformed or missing a required field. Diff against `verdict-template.json` and re-validate.
- Evidence is thin → do not inflate. File the honest low score with `evidence_that_flips_it` so the pipeline never re-litigates blind.
- A deal-breaker triggers on an A&R gut feeling → reject it. Flags need cited evidence, like scores.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/first-spin/ (200)
- Rubric config: https://cumulativewebinc.github.io/cwi-learn/first-spin/first-spin.json (200)
- Schema: https://cumulativewebinc.github.io/cwi-learn/first-spin/first-spin-schema.json (200)
- Verdict template: https://cumulativewebinc.github.io/cwi-learn/first-spin/verdict-template.json (200)
- Sample verdict: https://cumulativewebinc.github.io/cwi-learn/first-spin/sample-verdict.json (200)
- Item card / rubric / announce: linked from the product page's FILES block.

## Real examples

### Example 1 — The worked verdict: "Zooted Zone" triage for sync-readiness (cold-agent task)

Reproduce the sample verdict exactly. Scores from verified facts only:

| Criterion | Score | Confidence | Key source |
|---|---|---|---|
| hook_density | 3 | estimated | breakout-single fact, catalog.json (2026-09-14) |
| replay_pull | 5 | verified | 307,439 lifetime Spotify plays, observed 2026-09-14 |
| lane_clarity | 4 | verified | genre ['alternative rap','Post-Trap Futurism'], catalog.json (2026-09-15) |
| sync_readiness | 2 | derived | no clean/FCC-safe or instrumental versions exist; no one-stop or pre-cleared rights claim (catalog facts, 2026-09-15) |
| momentum_evidence | 5 | verified | New Rap Hits #21 Shaka Zulu / #30 Zooted Zone / #31 Doves & Diamonds — full 105-track scan 2026-09-15 |

Math: 3×0.25 + 5×0.25 + 4×0.15 + 2×0.15 + 5×0.20 = 0.75 + 1.25 + 0.60 + 0.30 + 1.00 = **3.90** → ×20 = **78** → band **advance**. No deal-breaker triggered. Sync-readiness triage verdict: **pitchable only with a legal caveat** (band-2 description verbatim) — uncapped only if clean/instrumental masters or documented pre-cleared splits land.

### Example 2 — Triage a track with no public record

A supervisor drops a brand-new demo with no Spotify presence and no credits on file.

1. Evidence gathered: none citable. `no_verifiable_presence` → **triggered: true** ("Artist and track not found on Spotify or any cited platform").
2. Every criterion has zero citations → all `unverifiable` → each capped at 1.
3. Weighted total ≤ 1.0 → percent ≤ 20, and the `no_verifiable_presence` flag caps the band at **pass** regardless.
4. Verdict ships with `evidence_that_flips_it`: "A live Spotify/Apple Music listing with verified metadata; documented credits; any scan-verified playlist hold." The pipeline now knows exactly what to ask for.

### Example 3 — Confidence-cap catch in practice

An evaluator scores `hook_density: 5` for a catalog deep cut based on "it slaps" with no listening-session record and no cited source.

1. Apply the confidence rule: no citations → `unverifiable` by definition → score caps at **1**, not 5.
2. Corrected contribution: 1×0.25 = 0.25 instead of 5×0.25 = 1.25 — a 20-point swing in the verdict percent.
3. Verdict notes: "attach a timestamped listening session to unlock the estimated band (cap 3) or verified band." The cap is the feature, not a bug.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
