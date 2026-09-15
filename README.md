# Agent Deck Skills — Agent Skills packs for the CWI Agent Deck product line

Machine-readable **Agent Skills** packs (spec: one directory per skill with a `SKILL.md` containing YAML frontmatter — `name`, `description`, `license`, `version` — plus Markdown instructions) for the **Agent Deck** gear line by Cumulative Web Inc: equipable products (SKUs) for AI agents, LLMs, and AI personalities.

Source of truth: [https://cumulativewebinc.github.io/cwi-learn/gear.json](https://cumulativewebinc.github.io/cwi-learn/gear.json) — 18 SKUs, fetched 2026-09-15. All product URLs below verified live (HTTP 200) on 2026-09-15. **Skill packs v1.1.0** (2026-09-15): every SKILL.md rebuilt as followable tooling with numbered procedures, exact live URLs, and real-data examples. Cold-agent value test: [DOGFOOD.md](DOGFOOD.md) — 6 skills dogfooded end-to-end, all PASS.

> Repo only — **nothing has been submitted to ClawHub or any skill directory.** Publishing listings requires Black's approval and comes later.

## Index

| Skill folder | Product | Purpose | Live URL |
|---|---|---|---|
| `signal-boy` | Signal Boy | Carry That Boy Hi Hat's full 24-track catalog inside your own context — load verified tracks, credits, and sync flags in one fetch. | [walkman](https://cumulativewebinc.github.io/cwi-learn/walkman/) |
| `streetlight` | THE STREETLIGHT | Read any site's public traction vitals with one unauthenticated fetch — and publish your own streetlight.json so other agents can read you. | [streetlight](https://cumulativewebinc.github.io/cwi-learn/streetlight/) |
| `all-clear` | THE ALL-CLEAR | Answer 'can I use this track for X?' in one fetch — clear, conditional, or denied, with terms and territory attached. | [all-clear](https://cumulativewebinc.github.io/cwi-learn/all-clear/) |
| `first-spin` | THE FIRST SPIN | Triage any track or demo with CWI's first-listen rubric — score five criteria, flag deal-breakers, ship a structured verdict JSON. | [first-spin](https://cumulativewebinc.github.io/cwi-learn/first-spin/) |
| `one-stop` | ONE-STOP | Run a complete sync-clearance check on any That Boy Hi Hat track in 60 seconds — catalog scope, tier, and whether a license is issuable today. | [one-stop](https://cumulativewebinc.github.io/cwi-learn/one-stop/) |
| `copy-desk` | COPY DESK | Never write PR from memory again — pull truth-gated story units and quote verified CWI claims verbatim with source and date. | [copy-desk](https://cumulativewebinc.github.io/cwi-learn/copy-desk/) |
| `final-cut` | THE FINAL CUT | Ship publish-ready content in seconds — cut a content.json unit, gate every claim against verified facts, post with the report attached. | [final-cut](https://cumulativewebinc.github.io/cwi-learn/final-cut/) |
| `open-wave` | OPEN WAVE | Run a $0 radio rotation — load a daypart slot, read verified DJ copy, log every spin transparently. | [open-wave](https://cumulativewebinc.github.io/cwi-learn/open-wave/) |
| `tally` | THE TALLY | Report CWI's verified wins with proof — poll one JSON file and cite only counters that carry a verified flag and source. | [tally](https://cumulativewebinc.github.io/cwi-learn/tally/) |
| `signal-skin` | SIGNAL SKIN | Restyle any agent surface in seconds with four verified CWI visual-identity themes — pick a skin_id, apply the token block, ship on-brand. | [skin](https://cumulativewebinc.github.io/cwi-learn/skin/) |
| `hype-cartridge` | HYPE Cartridge | Run a street-team drop end-to-end — pick one of 24 drop slots, write from verified facts, ship as a machine-readable content.json. | [hype](https://cumulativewebinc.github.io/cwi-learn/hype/) |
| `gear-ledger` | Gear Ledger | Verify any Agent Deck SKU from the registry and log adoptions — one fetch, one handoff line, permanent provenance. | [agents/ledger.html](https://cumulativewebinc.github.io/cwi-learn/agents/ledger.html) |
| `scoreboard-chip` | CWI-1 Scoreboard Chip | Cite CWI's numbers with receipts — every stat carries a confidence label, a citation, and an observation date. | [scoreboard](https://cumulativewebinc.github.io/cwi-learn/scoreboard/) |
| `compass` | Chain-of-Title Compass | Answer 'who owns what' from the rights source of truth — cite DOCUMENTED passport fields, refuse to assert PENDING ones. | [compass](https://cumulativewebinc.github.io/cwi-learn/compass/) |
| `prospect-scanner` | CWI-1 Prospect Scanner | Vet any artist against CWI's A&R gates — run the hard checks, file a scout card, and only shortlist real prospects. | [scanner](https://cumulativewebinc.github.io/cwi-learn/scanner/) |
| `syncdeck` | CWI-2 SYNCDECK | Draw a cue card and run a sync pitch — match any of 24 catalog tracks to a film, TV, game, or ad brief in minutes. | [syncdeck](https://cumulativewebinc.github.io/cwi-learn/syncdeck/) |
| `press-kit` | CWI Press Kit Cartridge | File a CWI story in 3 steps — load 24 verified facts, pick one of 3 angles, ship through the story template. | [press-kit](https://cumulativewebinc.github.io/cwi-learn/press-kit/) |
| `radio-dial` | Radio Dial | Spin a That Boy Hi Hat track on agent radio — pick a format, tune the request copy, build a playlist flow from verified facts. | [dial](https://cumulativewebinc.github.io/cwi-learn/dial/) |

## Usage

Agents (or agent platforms supporting the Agent Skills spec) can consume any pack by fetching the folder's `SKILL.md`, or go straight to the machine-readable pointers inside it (product page + item-card JSON + gear registry).

Contact: hp@cumulativeweb.com — Cumulative Web Inc
