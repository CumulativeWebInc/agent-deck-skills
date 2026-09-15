---
name: final-cut
description: "Ship publish-ready content in seconds — cut a content.json unit, gate every claim against verified facts, post with the report attached."
license: MIT
version: 1.1.0
---

# THE FINAL CUT — content publishing

## What this accomplishes

THE FINAL CUT is a publishing instrument, not a calendar. Every package is a machine-readable `content.json` unit — caption, hashtags, threads text, platform targets — that an agent can post in seconds. The difference from a scheduler: the content ships with the verified facts, and the **truth gate rejects any uncited claim before a package is issued**. Cut it. Gate it. Post it. Four launch packs are cut and gated; the Zooted Zone sample pack shows the standard.

## Prerequisites

- The authoring contract: `https://cumulativewebinc.github.io/cwi-learn/final-cut/final-cut-schema.json` (format `cwi-final-cut/v1`).
- The sample pack: "Zooted Zone" (linked from the product page's FILES block) — copy its structure.
- The verified fact set for gating: the 24-track catalog (`cartridge.json`), verified playlist placements (TALLY `tally.json` / Scoreboard Chip), release dates, studio credits (Compass passports).
- The nine standing `content.json` fields: `day`, `id`, `type`, `media_files`, `caption`, `hashtags`, `threads_text`, `post_order`, `platform_targets`.

## Procedure — cut, gate, post

1. **CUT.** Author the content unit against the nine standing fields. Nothing ships without all nine — a missing field is an incomplete package, not a minor gap.
2. **GATE.** Check every claim inside the unit against the verified CWI fact set. A claim without a fact source fails the gate. Produce the `truth_gate_report` — it is mandatory and travels with the unit.
3. **POST.** Copy the gated unit, pick the platform from `platform_targets`, paste. The premiere framing is the fun layer — the verified facts are the instrument.
4. **Cut your own pack.** Author against the schema, gate every claim, attach a `truth_gate_report` with `status: "pass"`. Anything that fails the gate is a rejected package — it never posts.

### The truth-gate rules

- Every number needs a source + date (e.g. "307,439 lifetime plays, observed 2026-09-14").
- Campaigns ≠ placements: Audiartist acceptances (#25818/#25820/#25821) vs New Rap Hits #21/#30/#31.
- No growth language. No invented quotes, bios, coverage, or lyrics.
- Spelling: "King Akeem" (never "Ahkeem"). Studio: Cue Recording Studios, Arlington, Virginia (official position).

### On errors

- `truth_gate_report.status` is not `pass` → the package is rejected. Fix the failed claims, re-gate.
- Schema validation fails → diff against the Zooted Zone sample pack and fix the structure.
- A claim is "probably true" but unsourced → it fails. Cut it or source it.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/final-cut/ (200)
- Schema: https://cumulativewebinc.github.io/cwi-learn/final-cut/final-cut-schema.json (cwi-final-cut/v1)
- Item card: https://cumulativewebinc.github.io/cwi-learn/final-cut/item-card.json (200)
- Sample pack (Zooted Zone): linked from the product page FILES block
- Fact sources: https://cumulativewebinc.github.io/cwi-learn/walkman/cartridge.json (200), https://cumulativewebinc.github.io/cwi-learn/tally/tally.json (200), https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json (200), https://cumulativewebinc.github.io/cwi-learn/compass/passports.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Cut a Diabolique anniversary pack

1. CUT: author the unit with all nine fields — `day: "2026-09-16"`, `id: "diabolique-spotlight-01"`, `type: "track-spotlight"`, `media_files: [<cover art>]`, caption, hashtags, `threads_text`, `post_order: 1`, `platform_targets: ["threads","instagram","tiktok"]`.
2. Claims inside: "Diabolique — single released 2026-07-03. Recorded at Cue Recording Studios, Arlington, Virginia. Produced by Hybrid, co-produced with Black Lansky." Each traces to the Compass passport / COPY DESK `diabolique-release` unit.
3. GATE: every claim sourced → `truth_gate_report: {status: "pass", claims_checked: 3, failed: []}`.
4. POST: copy, pick platform, paste. Package travels with its gate report.

### Example 2 — A gated rejection

Draft caption: "Zooted Zone just passed 400K streams and is climbing!"

1. GATE: "400K" has no fact source (registry says 307,439, observed 2026-09-14); "climbing" is growth language.
2. `truth_gate_report: {status: "fail", failed: ["unverified stream count 400K", "growth language 'climbing'"]}`.
3. Result: rejected package — never posts. Fix to "307K plays (observed 2026-09-14)" and re-gate.

### Example 3 — QA an incoming package before approval

1. Check all nine fields present. Check `truth_gate_report.status == "pass"`.
2. Spot-check two claims against the fact sources (a placement position, a date).
3. Anything missing or failed → return to the author with the exact failed claims. Approve only pass-gated packages.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
