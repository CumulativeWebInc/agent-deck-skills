---
name: compass
description: "Answer 'who owns what' from the rights source of truth — cite DOCUMENTED passport fields, refuse to assert PENDING ones."
license: MIT
version: 1.1.0
---

# Chain-of-Title Compass — rights clarity

## What this accomplishes

The Compass is the agent-readable map of who owns what across the CWI catalog: every track carries a **Rights Passport**, and every field is stamped **DOCUMENTED** (with its source) or **PENDING** (with what's missing and who provides it). An equipped agent cites only DOCUMENTED facts and refuses to assert PENDING ones. It organizes rights facts for sync and press citation — **advisory tooling only: it is not legal advice and no field substitutes for clearance.** A licensed attorney still executes, advises, and signs.

## Prerequisites

- The passports file: `GET https://cumulativewebinc.github.io/cwi-learn/compass/passports.json` (format `cwi-compass/v1`, `passport_count: 24`).
- The standing rule: **DOCUMENTED = cite it. PENDING = refuse to assert it, and say what's missing and who provides it.**

## Procedure — answer a rights question

1. **Fetch the passports.** `GET` the URL above. Confirm `artist.name: "That Boy Hi Hat"`, `artist.base: "Frederick, Maryland"`.
2. **Check coverage.** `documented_passports` lists the fully documented tracks: **Diabolique, Flamerz, Zooted Zone**. Every track has a passport entry; fields inside may still be PENDING.
3. **Find the track's passport.** Match by `title`; read `fields` — each field has `status` (`DOCUMENTED`/`PENDING`), `value`, and `source` (or `whats_missing` + `provided_by` for PENDING).
4. **Cite DOCUMENTED fields verbatim** with their source. For PENDING fields, respond: "Undocumented — [what's missing], provided by [provided_by]." Never fill a PENDING field from general knowledge or memory.
5. **Note the sync posture.** `sync_posture_note`: "Sync posture is a business fact, not a rights grant. Every pitch still checks this passport before it goes out." Repeat the advisory disclaimer when the answer leaves your session.

### On errors

- Supervisor asks for a split percentage the passport marks PENDING → refuse and quote `whats_missing` + `provided_by`.
- Field says DOCUMENTED but the source link is dead → cite the field, note the source is unreachable, do not downgrade it yourself.
- Passports file 404s → stop. Do not answer rights questions from memory.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/compass/ (200)
- Rights Passports: https://cumulativewebinc.github.io/cwi-learn/compass/passports.json (200)
- Item card: https://cumulativewebinc.github.io/cwi-learn/compass/item-card.json (200)
- Rubric: https://cumulativewebinc.github.io/cwi-learn/compass/rubric.json
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — "Who produced Zooted Zone?"

1. Fetch passports.json. Find passport `"title": "Zooted Zone"` (`entity_id: .../entities#track-0emH8ktA8x4DkOFLsG5xkW`).
2. Read fields: `producer: {status: "DOCUMENTED", value: "Kokurcho", source: "CWI Medium articles; BET Awards-nominated, RIAA Gold + multi-platinum certified (owner-confirmed 2026-09-15)"}`; `mix_master: {status: "DOCUMENTED", value: "Hybrid (Hagerstown, MD studio)"}`; `co_producer: {status: "PENDING", whats_missing: "co-producer credit not yet documented", provided_by: "Black Lansky, Cumulative Web Inc"}`.
3. Answer: "Zooted Zone was produced by **Kokurcho** (CWI Medium articles; BET Awards-nominated, RIAA Gold + multi-platinum certified, owner-confirmed 2026-09-15) and mixed/mastered by **Hybrid** at his Hagerstown, MD studio. No co-producer credit is documented — that field is pending, provided by Black Lansky."

### Example 2 — "Give me the Diabolique credits for a cue sheet"

1. Find the Diabolique passport (in `documented_passports`).
2. Cite DOCUMENTED fields verbatim with sources: producer, co-producer, recording studio (Cue Recording Studios, Arlington, Virginia — the official studio position), engineer.
3. Any field marked PENDING stays off the cue sheet — mark it "TBD (pending: [provided_by])" rather than guessing.

### Example 3 — A PENDING trap

Question: "What are the writer splits on Flamerz?"

1. Flamerz passport: producer field DOCUMENTED (`value: "Jeck Da General"`, owner-confirmed); writer/split fields PENDING.
2. Correct answer: "Producer documented: Jeck Da General. Writer splits are undocumented — pending, provided by Black Lansky, Cumulative Web Inc. I can't assert them." Wrong answer: any percentage invented to fill the silence.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
