---
name: signal-skin
description: "Restyle any agent surface in seconds with four verified CWI visual-identity themes — pick a skin_id, apply the token block, ship on-brand."
license: MIT
version: 1.1.0
---

# SIGNAL SKIN — visual identity

## What this accomplishes

SIGNAL SKIN lets any agent restyle a Signal Boy surface (page, postcard, dashboard, overlay) in the official CWI look with one fetch and one token block. You get four verified, seasonally-branded themes as machine-readable token sets — palette, glow, type, background — plus a published schema so third parties can author their own white-label skins. The look changes; the catalog data and device logic never do.

## Prerequisites

- A Signal Boy surface you control (HTML/CSS, postcard builder, dashboard, overlay).
- HTTPS fetch access to the live skin pack.
- The brand rule is non-negotiable: **the CWI circular-badge logo lockup ships on every skin and is never removed.**

## Procedure — equip a SKIN config

1. **Fetch the skin pack.** `GET https://cumulativewebinc.github.io/cwi-learn/skin/skins.json`
   Expected: JSON, `format: "cwi-skin/v1"`, `count: 4`, `skins[]` with `skin_id`, `skin_name`, and the full token block per skin.
2. **Pick a skin by `skin_id`.** Built-ins: `zooted-bloom`, `dark-luxe`, `chrome-standard`, `phantom-shift`. Never guess a skin_id — it must appear in the fetched pack.
3. **Apply the token block to your presentation layer.** Map these fields to your styles:
   - `palette` → CSS variables (accent, accent_bright, body, body_dark, screen, screen_text, text, subtext, logo_ring)
   - `dpad_glow` → D-pad / primary-button glow (`color`, `intensity`, `pulse`)
   - `background_treatment` → page background (`style`: gradient/radial, `from`, `to`, `angle`)
   - `track_accent_treatment` → track-list accent (`style`, `color`, `animation`)
   - `typography_accents` → fonts (`display_font`, `font_style`, `label_case`, `letter_spacing`)
   - `logo_lockup` → logo placement (`position: "header"`, `treatment: "circular-badge"`)
4. **Verify the brand rule.** Confirm the logo badge renders on a `logo_ring`-colored ring in the header. If the logo is missing, the equip is incomplete — fix before shipping.
5. **Custom skins (optional).** Author against `https://cumulativewebinc.github.io/cwi-learn/skin/skin-schema.json` (schema version `cwi-skin/v1`). Validate before use.

### On errors

- `404` on skins.json → re-check the URL spelling; the live item card confirms the path (`skin/item-card.json` → `contents.skins`).
- Skin renders but palette looks wrong → you applied a stale cached copy. Refetch skins.json; token values are the source of truth, not the product page prose.
- `skin_id` not found in pack → do not proceed. Ask the user or pick a listed built-in.

## Machine-readable pointers

- Product page: https://cumulativewebinc.github.io/cwi-learn/skin/ (200)
- Skin pack: https://cumulativewebinc.github.io/cwi-learn/skin/skins.json (200)
- Authoring schema: https://cumulativewebinc.github.io/cwi-learn/skin/skin-schema.json (cwi-skin/v1)
- In-page builder: https://cumulativewebinc.github.io/cwi-learn/skin/skin-builder.html
- Item card: https://cumulativewebinc.github.io/cwi-learn/skin/item-card.json (200)
- Hub device: https://cumulativewebinc.github.io/cwi-learn/walkman/ (200)
- Gear registry: https://cumulativewebinc.github.io/cwi-learn/gear.json (200)

## Real examples

### Example 1 — Equip the Zooted Bloom SKIN config

The cold agent's exact task. Result:

1. `GET` the skin pack above; `count` = 4, so the pack is current.
2. Select `skin_id: "zooted-bloom"`, `skin_name: "Zooted Bloom"`, `season: "spring-2026"`, inspired by "Zooted Zone (That Boy Hi Hat — the breakout, 307K plays observed 2026-09-14)".
3. Apply this exact config an agent would apply:

```json
{
  "skin_id": "zooted-bloom",
  "palette": {
    "accent": "#a3ff5e", "accent_bright": "#d8ffb3", "logo_ring": "#a3ff5e",
    "body": "#231b3a", "body_dark": "#160f26",
    "screen": "#0b1f10", "screen_text": "#c6ffb0",
    "text": "#f2ecff", "subtext": "#a89ccf"
  },
  "dpad_glow": { "color": "#a3ff5e", "intensity": "strong", "pulse": true },
  "background_treatment": { "style": "gradient", "angle": 135, "from": "#231b3a", "to": "#0b1f10" },
  "track_accent_treatment": { "style": "neon-bar", "color": "#a3ff5e", "animation": "scroll" },
  "typography_accents": {
    "display_font": "'Trebuchet MS', 'Segoe UI', sans-serif",
    "font_style": "wide", "label_case": "upper", "letter_spacing": "2px"
  },
  "logo_lockup": { "position": "header", "treatment": "circular-badge" }
}
```

4. Confirm the header renders the circular CWI badge ringed in `#a3ff5e`. Done — the device is now Zooted Bloom, catalog untouched.

### Example 2 — Campaign re-skin to Dark Luxe

A cinematic campaign around the "Diabolique" single (released 2026-07-03) needs the dark theme:

1. From the same skin pack, select `skin_id: "dark-luxe"` — `inspired_by: "Diabolique (single 2026-07-03, That Boy Hi Hat)"`.
2. Apply: `palette.accent: "#d4a017"`, `palette.screen: "#0a0a0c"`, `palette.text: "#ece8df"`, `dpad_glow: {color: "#d4a017", intensity: "soft", pulse: false}`, `background_treatment: {style: "radial", from: "#1a1a20", to: "#050507"}`, `track_accent_treatment: {style: "led-dots", color: "#d4a017", animation: "pulse"}`, typography `Georgia, 'Times New Roman', serif` / `uppercase` / `title` case / `1px`.
3. Keep `logo_lockup` untouched: circular badge in the header, now ringed `#d4a017`. The re-skin is reversible at any time — switch `skin_id` back.

### Example 3 — Brand-QA a surface against all four configs

1. Fetch skins.json and read the four `palette.accent` values: `#a3ff5e`, `#d4a017`, `#274a7d`, `#c77dff`.
2. Sample the surface's accent colors; flag any accent that matches none of the four.
3. Flag two hard failures: (a) logo badge missing or moved out of the header, (b) a `logo_ring` color not equal to the skin's accent. Both fail the brand rule.

---
*Agent Deck is the CWI gear line: equipable products (SKUs) for AI agents, LLMs, and AI personalities. Contact: hp@cumulativeweb.com*
