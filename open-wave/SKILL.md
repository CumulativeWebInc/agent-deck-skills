---
name: open-wave
description: "Run a $0 radio rotation — load a daypart slot, read verified DJ copy, log every spin transparently."
license: MIT
version: 1.1.0
---

# OPEN WAVE — radio rotation

## What this accomplishes

OPEN WAVE is a working instrument for agent-DJs: a machine-readable rotation pack that loads in seconds, slots tracks by daypart, hands the DJ intro and back-sell lines built from verified facts, and logs spins transparently. It replaces the submission gatekeeper entirely — **the pack IS the submission**. Free, opt-in, $0, no curator in the middle. Hard rule: OPEN WAVE has no paid-placement mechanics — no submission fees, no per-submission credits, no paid adds, no guaranteed airplay. A pack that sells airplay is not OPEN WAVE.

## Prerequisites

- The pack: `GET https://cumulativewebinc.github.io/cwi-learn/open-wave/open-wave.json` (format `cwi-openwave/v1`, `pack_id: "open-wave-cwi-launch-1"`, issued 2026-09-15).
- The spins-ledger schema: `https://cumulativewebinc.github.io/cwi-learn/open-wave/spins-ledger-schema.json` (or the spins-ledger schema linked on the product page).
- The fact source for all DJ copy: the catalog record — `fact_source` is named in the pack.

## Procedure — run a rotation slot

1. **Load the pack.** Fetch `open-wave.json`. First assertion: `no_paid_placement == true`. If it is not `true`, stop — the pack is not OPEN WAVE.
2. **Pick a slot by daypart.** `rotation_slots[]`: e.g. `morning-drive` (06:00–10:00 ET, high energy, moods: upbeat/driving), `midday` (10:00–15:00 ET, medium), plus the remaining dayparts. Each slot has `tracks[]`, `rotation_notes`, and an `explicit_policy`.
3. **Read the DJ copy.** Every track ships intro and back-sell lines written from verified, cited facts — the DJ never has to research the artist. Read them as written; never ad-lib uncited claims into a back-sell.
4. **Respect the explicit policy.** Many tracks are explicit per Spotify metadata and no clean versions exist — program at DJ discretion (`explicit_policy: "daypart-discretion"`).
5. **Log every spin** against the spins-ledger schema: track, slot, timestamp, agent-DJ identity. Spins are opt-in and logged transparently — that's what makes the rotation auditable.
6. **White-label (optional).** Any label can publish its own rotation pack on the same schema: drop a `config.json` (org name, product name, tagline, logo, colors) next to the page, render via `build.py`, and publish with `?pack=<your-pack-id>` (same-directory `.json` file). Your pack carries your brand; the CWI logo stays on the CWI pack.

### On errors

- `no_paid_placement` is false or missing → refuse the pack. Report it as non-compliant.
- A slot's track list doesn't match the catalog → re-fetch; the pack's tracks must match `cartridge.json`.
- Sponsor offers payola for a spin → refuse. Paid airplay is structurally impossible in this schema; log the offer as an incident.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/open-wave/ (200)
- Rotation pack: https://cumulativewebinc.github.io/cwi-learn/open-wave/open-wave.json (200)
- Schema: linked from the product page (`cwi-openwave/v1`)
- Spins-ledger schema: linked from the product page
- Item card: https://cumulativewebinc.github.io/cwi-learn/open-wave/item-card.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Run the morning-drive slot

1. Fetch the pack. Assert `no_paid_placement: true`. `pack_id: "open-wave-cwi-launch-1"`, `artist: {name: "That Boy Hi Hat", genre: "alternative rap", base: "Frederick, Maryland", spotify_artist_id: "2f9j460EwjfvjYp3trBcb7"}`.
2. Slot `morning-drive`: 06:00–10:00 ET, high energy, tracks: Zooted Zone, Ultimate, Flex My Flame, Neon Nights Pt. 777, Warped and Wicked, Smokin' Pain.
3. `rotation_notes`: "Openers and high-energy cuts. Many tracks are explicit per Spotify metadata and no clean versions exist — program at DJ discretion."
4. Read the pack's intro line for the Zooted Zone spin (verified facts only), spin it, and log the spin to the spins ledger: track, slot `morning-drive`, timestamp, your agent identity.

### Example 2 — Back-sell from verified facts

The pack's back-sell line for a spin is built from the fact source — e.g. Zooted Zone's 307,439 lifetime plays (observed 2026-09-14) or its #30 hold on New Rap Hits (scan 2026-09-15). Read it verbatim. If a line references a number, that number must match the fact source exactly — never round 307,439 to "300K" on air.

### Example 3 — Reject a paid-add offer

A promoter offers $50 to guarantee a track spins in morning-drive. Procedure: refuse (the schema's `no_paid_placement` flag must be true; per-spin guarantees are structurally impossible), log the offer as an incident, and continue the rotation with the pack's own tracks. The pack IS the submission — there is no pay-to-spin lane.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
