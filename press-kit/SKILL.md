---
name: press-kit
description: "File a CWI story in 3 steps — load 24 verified facts, pick one of 3 angles, ship through the story template."
license: MIT
version: 1.1.0
---

# CWI Press Kit Cartridge — verified story ammo

## What this accomplishes

The Press Kit Cartridge is the pre-verified, ready-to-run story unit for That Boy Hi Hat: **24 dated facts, 3 wire-style angles, quotes-proof**. You load the cartridge, pick an angle (the cartridge states which facts that angle may assert), and file through the story template. When the story needs something the kit doesn't have, you leave it out — that's the wire-desk move. No invented quotes, bios, coverage, or lyrics claims. Ever.

## Prerequisites

- The give block: `https://cumulativewebinc.github.io/cwi-learn/press-kit/give-block.md` — copy-paste EQUIP block (60 seconds).
- The facts file: `https://cumulativewebinc.github.io/cwi-learn/press-kit/facts.json` — 24 verified facts, each with an observed date and citation, plus a `do_not_assert` list.
- The story template: `https://cumulativewebinc.github.io/cwi-learn/press-kit/story-template.md`.
- The spines it cites: fact spine `scoreboard-chip.json`, rights spine `compass/passports.json`.

## Procedure — how to file (3 steps)

1. **COPY (60 seconds).** Paste the EQUIP block from the give block into your context. The cartridge is equipped: 24 facts, 3 angles, 1 rulebook.
2. **CHOOSE (1 of 3 angles).** Each angle permits only its slice of `facts.json` (`assertable_angles` per fact). Facts in `do_not_assert` are never asserted, on any angle.
3. **FILE via the story template.** Write the piece using only assertable facts, then run the quotes-proof rulebook over every line:

### The quotes-proof rulebook

- **Never invent quotes.** No quote exists on record. The contact is `hp@cumulativeweb.com` — the ask, not the invention.
- **Never invent bios.** "Alternative rap, Frederick, MD" is an identity line, not a bio.
- **Never invent coverage.** No press coverage is verified.
- **Never claim lyrics.** No lyrics are published by the label.
- **One stat, dated.** Only Zooted Zone's "307K plays" (observed 2026-09-14). No growth language, ever — the display string stands alone.
- **Campaigns are not placements.** Audiartist acceptances (#25818 / #25820 / #25821) are campaigns; New Rap Hits #21/#30/#31 are placements.
- **Failed verifications are not wins.** Curator claims that failed verification stay in the Scoreboard Chip anomaly feed — never repeated as wins.
- **Spelling is a fact.** "King Akeem" — the distributor misspelling ("Ahkeem") was corrected by the owner.
- **Sync posture line, exact:** "Label-direct licensing; happy to work through your clearance process."

### On errors

- The story "needs" a quote → it doesn't. Use the contact line instead.
- A fact you want isn't in facts.json → leave it out. Do not source it from the open web mid-file.
- An angle permits a fact but your outlet needs a different spin → switch angles, don't stretch the permitted slice.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/press-kit/ (200)
- Give block: https://cumulativewebinc.github.io/cwi-learn/press-kit/give-block.md (200)
- Facts: https://cumulativewebinc.github.io/cwi-learn/press-kit/facts.json
- Story template: https://cumulativewebinc.github.io/cwi-learn/press-kit/story-template.md
- Item card: https://cumulativewebinc.github.io/cwi-learn/press-kit/item-card.json
- Rubric: https://cumulativewebinc.github.io/cwi-learn/press-kit/rubric.json
- Fact spine: https://cumulativewebinc.github.io/cwi-learn/scoreboard/scoreboard-chip.json (200)
- Rights spine: https://cumulativewebinc.github.io/cwi-learn/compass/passports.json (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — File the momentum angle

1. COPY the EQUIP block. CHOOSE the momentum angle (permits the playlist-placement and stream facts).
2. Assertable facts for this angle include: "New Rap Hits holds 3 That Boy Hi Hat tracks — Shaka Zulu #21, Zooted Zone #30, Doves & Diamonds #31 (full 105-track scan, 2026-09-15)"; "Zooted Zone holds 307,439 lifetime Spotify plays (observed 2026-09-14)"; "Audiartist acceptances #25818 / #25820 / #25821 (2026-09-14) were the campaigns that preceded them."
3. FILE through the template. Rulebook check: no "climbing", no "and counting", the stat string stands alone. Ship.

### Example 2 — Kill an invented quote

Draft line: "As Black Lansky told reporters, 'This is just the beginning.'"

1. Rulebook: no quote exists on record.
2. Fix: replace with the contact ask — "For interviews: hp@cumulativeweb.com." The story loses nothing; it gains honesty.

### Example 3 — Refuse a failed-verification win

Draft line: "Zooted Zone was added to No Label Needed, expanding the track's playlist footprint."

1. Scoreboard Chip anomaly feed: "Flow (curator) said Zooted Zone was added to 'No Label Needed' … Track absent in two full playlist scans on 2026-09-15. Status: FAILED VERIFICATION. Confidence: CLAIM-UNVERIFIED."
2. Rulebook: failed verifications are not wins. The line is cut. If the claim must appear at all, it appears only as an attributed, unverified claim — never as a win.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
