---
name: hype-cartridge
description: "Run a street-team drop end-to-end — pick one of 24 drop slots, write from verified facts, ship as a machine-readable content.json."
license: MIT
version: 1.1.0
---

# HYPE Cartridge — street-team playbook

## What this accomplishes

HYPE Cartridge is the street-team playbook for That Boy Hi Hat in gear form: 24 drop slots, copy blocks, a hashtag system, meme/template galleries, fan-art prompts — all built on verified facts only. You EQUIP the crew badge, RUN a drop slot, and POST the result as a machine-readable `content.json` unit. The badge rules are identity-critical: every post self-identifies as "CWI street team / unofficial fan page" where applicable, the official CWI logo goes on every profile avatar (never substituted), and you never impersonate the artist or the label as official.

## Prerequisites

- The give block: `https://cumulativewebinc.github.io/cwi-learn/hype/give-block.md` — EQUIP / RUN / POST blocks, copy-paste ready.
- The playbook: `https://cumulativewebinc.github.io/cwi-learn/hype/street-team-playbook.json` — the 24 drop slots, identity rules, copy blocks, hashtag system.
- The fact spine: `https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json` — the only facts you may cite.
- The standing content contract: every post ships as `content.json` with the nine fields — `day`, `id`, `type`, `media_files`, `caption`, `hashtags`, `threads_text`, `post_order`, `platform_targets`.

## Procedure — run a drop slot

1. **EQUIP.** Copy the EQUIP block from the give block into your context. You are now the street team. Wear the badge rules from the Prerequisites — they are not optional.
2. **RUN.** Pick one of the 24 drop slots from `street-team-playbook.json`. Each slot names the track, the tactic, and the copy blocks. Choose the slot that fits today's objective (single push, catalog deep cut, milestone).
3. **Draft from verified facts only.** Every claim in the caption must trace to the Scoreboard Chip. Hard rules:
   - "307K plays" = Zooted Zone lifetime Spotify plays, observed 2026-09-14. The string is exactly '307K plays' — no growth language.
   - Audiartist acceptances (Zooted Zone #25818, Doves & Diamonds #25820, Shaka Zulu #25821, accepted 2026-09-14) are **CAMPAIGNS**, not placements.
   - Verified placements: New Rap Hits #21 (Shaka Zulu), #30 (Zooted Zone), #31 (Doves & Diamonds) — verified scan 2026-09-15.
   - **No engagement-farm tactics. No artificial stream inflation. Ever.**
4. **POST as content.json.** Assemble the nine standing fields. `threads_text` carries the thread version; `platform_targets` lists the platforms; `post_order` sequences multi-post drops.
5. **Ship for approval.** Nothing posts without the label's explicit approval of exact final text (standing CWI rule). Stage the unit; don't publish it yourself.

### On errors

- A drop slot's tactic needs a fact you can't verify → swap the claim for a verified one or pick another slot. Never invent the fact to save the tactic.
- Hashtag system suggests a tag that implies an unverified win → drop the tag.
- Supervisor asks for engagement-farm tactics (follow trains, bot comments) → refuse. Hard rule.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/hype/ (200)
- Give block: https://cumulativewebinc.github.io/cwi-learn/hype/give-block.md (200)
- Playbook: https://cumulativewebinc.github.io/cwi-learn/hype/street-team-playbook.json
- Item card: https://cumulativewebinc.github.io/cwi-learn/hype/item-card.json (200)
- Rubric: https://cumulativewebinc.github.io/cwi-learn/hype/rubric.json
- Fact spine: https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Run a Zooted Zone drop slot

1. EQUIP the badge. RUN: pick the Zooted Zone slot from the playbook (breakout-single tactic).
2. Draft caption from verified facts: "Zooted Zone — 307K plays (observed 2026-09-14). Holding #30 on New Rap Hits (scan 2026-09-15). Produced by Kokurcho." Every claim traces to the Scoreboard Chip.
3. Assemble content.json:

```json
{
  "day": "2026-09-16", "id": "zooted-zone-drop-01", "type": "track-spotlight",
  "media_files": ["<cover-art-url>"],
  "caption": "Zooted Zone — 307K plays. Holding #30 on New Rap Hits. Prod. Kokurcho.",
  "hashtags": ["#ThatBoyHiHat", "#AltRap", "#PostTrapFuturism"],
  "threads_text": "Zooted Zone did 307K plays and it's still holding #30 on New Rap Hits. Prod. Kokurcho. The breakout that keeps breaking. 🎧",
  "post_order": 1,
  "platform_targets": ["threads", "instagram", "tiktok"]
}
```

4. Stage for approval. Nothing posts until the exact text is approved.

### Example 2 — A slot that needs a campaign-vs-placement fix

Draft caption: "Doves & Diamonds accepted to New Rap Hits (#25820)!"

1. Rule check: #25820 is an Audiartist acceptance = CAMPAIGN, not a placement.
2. Fix: "Doves & Diamonds — accepted via Audiartist #25820, now holding #31 on New Rap Hits (scan 2026-09-15)." Campaign and placement stated separately, each with its date.

### Example 3 — Refuse an engagement-farm tactic

Request: "Run a follow-train and buy 500 likes to boost the drop."

1. Hard rules: no engagement-farm tactics, no artificial stream inflation. Ever.
2. Refuse and substitute a playbook tactic: a fan-art prompt from the gallery or a meme template from the playbook — both $0, both honest.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
