# Phronesis — Design Spec

**Status:** v0.2 — direction locked, v2 mockups shipped
**Date:** 2026-06-14
**Mockups:** [`docs/mockups/design_mockups.html`](./mockups/design_mockups.html)

---

## 1. Aesthetic Direction

**The Cool Kaffeehaus.** The intellectual warmth of a Viennese coffeehouse, filtered through Nous-Research-grade restraint, served on cream paper — and signed, in a small way, by the Greeks.

> *What would a serious intellectual salon feel like if it were designed today by people with good taste and restraint?*

### Cultural Anchors

- **Kaffeehauskultur** — the Viennese tradition where economics was debated
- **Nous Research** — duotone discipline, monospace metadata, generous whitespace, dashed system dividers
- **Hayek’s library** — restrained, classical, intellectually serious
- **The Platonic dialogue** — philosophy written as conversation; the walk-and-talk is structural to Phronesis
- **Classical Greek mathematics** — Euclid, Archimedes, and the tradition of using Greek letters (α, β, γ) for equation numbers

### Why the Greeks

Phronesis is a Greek word (φρόνησις). The phi (φ) in the wordmark is **doing real work** — three meanings at once:

1. The first letter of *phronesis* itself
2. The Golden Ratio (φ ≈ 1.618…) — symbol of proportion and natural elegance
3. Aristotle’s distinction between *phronesis* (practical wisdom) and *sophia* (theoretical wisdom) — exactly the persona

Greek is therefore not decoration. It is cultural alignment. The aesthetics lean into this through:

- The Greek-key (meander) hairline divider
- Greek letters (α, β, γ) as equation and page numbers
- Greek transliterations (φρόνησις, φιλοσοφία) in microcopy
- A subtle Greek-key ring around the home voice button

### What This Is Not

- ❌ LITERAL Viennese kitsch (no coffee cups, no landmarks, no mottos)
- ❌ Greek kitsch (no columns, no statues, no faux papyrus textures)
- ❌ Generic SaaS dashboard (no metric tiles, no left-border accent cards)
- ❌ Trendy gradients, glassmorphism, or playful illustrations
- ❌ Flashy animations or scroll-jacking

---

## 2. Color Tokens

### Cream Theme (primary)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#F5EFE3` | Primary background (paper-like, sun-readable) |
| `--surface` | `#EDE5D2` | Cards, panels (subtle depth) |
| `--surface-2` | `#E4DBC3` | Hover, layered surfaces |
| `--ink` | `#1B2A4A` | Primary text (Nous echo) |
| `--ink-soft` | `#2A3B5E` | Secondary text |
| `--mute` | `#A8A195` | Metadata, timestamps |
| `--mute-2` | `#C7BDA9` | Hairline dividers, dashed borders |
| `--accent` | `#7A2E2E` | Oxblood — emphasis, voice-active state |
| `--accent-2` | `#B08A52` | Brass — hover, secondary highlights |
| `--espresso` | `#3D2A20` | High-contrast text on cream |
| `--meander` | `#8C7B5A` | Greek-key hairline pattern |

### Espresso Theme (dark)

| Token | Value | Use |
|---|---|---|
| `--bg-d` | `#1A130C` | Primary background (after-hours café) |
| `--surface-d` | `#251A12` | Cards |
| `--surface-2-d` | `#2E2014` | Layered surfaces |
| `--ink-d` | `#F0E6D2` | Primary text (cream on espresso) |
| `--ink-d-soft` | `#D8CDB6` | Secondary text |
| `--mute-d` | `#8A7864` | Metadata |
| `--mute-2-d` | `#5C4D3E` | Hairline dividers |
| `--accent-d` | `#C3975A` | Brass lit — primary accent in dark |
| `--accent-2-d` | `#B08A52` | Brass — secondary highlight |
| `--meander-d` | `#6B5A3F` | Greek-key hairline in dark |

**Rule:** Never have more than **two** accents visible at a time. Choose either `--accent` OR `--accent-2` as the day's accent.

---

## 3. Typography

**Five-voice system. Each voice has a job.**

| Voice | Font | Weight | Job |
|---|---|---|---|
| **Editorial** | *Fraunces* (Google Fonts, variable, optical sizing) | 500, italic | Brand, headings, concept intros, model names |
| **Reading** | *Source Serif 4* | 400, 400 italic | Long-form explanations, math context, retrieved page chunks |
| **Classical** | *Cormorant Garamond* | 400, 500, italic | Greek transliterations, ceremonial moments |
| **Working** | *Inter* | 400, 500, 600 | UI, buttons, navigation, system messages |
| **Technical** | *JetBrains Mono* | 400, 500 | Tool outputs, code, retrieval metadata, status indicators |

**Type hierarchy rules:**
- **Editorial** = emotional/conceptual moments (mode names, model names, key concepts)
- **Reading** = content the user is *studying*
- **Classical** = Greek transliterations and ceremonial typography
- **Working** = content the user is *operating*
- **Technical** = content the user is *inspecting*

**Type scale (mobile):**
- Display (Fraunces italic): 22–28px
- Heading: 17–20px
- Body: 13–15px
- Caption: 11–12px
- Mono micro: 9–10px (uppercase, +0.12em letter-spacing)

**Google Fonts link:**
```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;0,9..144,600;1,9..144,400&family=Source+Serif+4:ital,opsz,wght@0,8..60,400;0,8..60,500;1,8..60,400&family=Cormorant+Garamond:ital,wght@0,400;0,500;1,400;1,500&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

---

## 4. Layout & Spacing

### Grid
- 12-column asymmetric editorial grid
- 8pt baseline grid
- **Greek-key meander pattern** (6px tall, hairline, repeating) for major system boundaries
- **1px dashed** dividers in `--mute-2` for minor boundaries
- No drop shadows (use 1px ink borders for depth)

### Spacing scale
- 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 (px)
- Page padding (mobile): 22–24px edges
- Stage padding: 50px top (status bar) + 20px bottom

### Content width
- Mobile: 100% width with 22px gutters
- Desktop: 720px (reading) or 880px (controls)
- Math card: 100% width, 14–18px padding

### Greek-key Meander Pattern

A 6px tall pattern rendered as hairline horizontal bars. Used:
- Above and below the main content on every screen
- Replaces the heavier section dividers

```css
.meander {
  height: 6px;
  background-image:
    linear-gradient(90deg, var(--meander) 50%, transparent 50%),
    linear-gradient(90deg, var(--meander) 50%, transparent 50%);
  background-size: 6px 1px, 6px 1px;
  background-position: 0 0, 0 5px;
  background-repeat: repeat-x;
}
```

---

## 5. Component Library

### Voice Button
- **Size:** 96×96px (phone), 132×132px (tablet)
- **Shape:** Perfect circle
- **States:**
  - **Idle:** 1.5px solid `--ink` border, transparent fill, ink mic icon
  - **Idle + Greek ring (home only):** surrounded by a 1px solid + 1px dashed concentric ring in `--meander`
  - **Listening:** `--accent-2` fill, white mic icon, soft 2.4s pulse animation
  - **Thinking:** 1.5px **dashed** `--ink` border (Nous echo), ink mic icon
  - **Speaking:** `--accent` fill, white mic icon
  - **Paused:** `--accent` border only, transparent fill
- **Inline (history strip):** 56×56px compact variant for the sticky voice strip

### Status Label
- Font: *Source Serif 4* italic, 14px
- Below voice button
- Examples:
  - "Listening…"
  - "Considering…"
  - "Looking through your materials…"
  - "Take your time."

### Status Sub-label
- Font: *JetBrains Mono* 10px, uppercase, +0.10em letter-spacing
- `--mute` color
- Shows real-time data: captured time, retrieval source, etc.

### Wordmark
- *Fraunces* italic, 21px
- The leading "φ" (Greek phi) is **oxblood** (`--accent`), non-italic, semibold, 24px
- The rest of "phronesis" is ink, italic, weight 500
- Renders as: **φphronesis**

### Mode Tag
- Right-aligned, top-bar
- Small mono uppercase 9px
- 6px colored dot prefix (oxblood for Tutor, brass for Research, etc.)
- "TUTOR" / "RESEARCH" / etc.

### Top Bar
- 12px padding bottom, then meander pattern
- Wordmark on left, mode tag on right

### Bottom Bar
- Meander pattern above, then 14px padding
- Mono micro text
- Left: tool affordances (DOCS, EXPORT, PAUSE)
- Right: page/session indicator ("PAGE 1 / 4" or "φιλοσοφία" on home)

### Page Counter
- Top-left of math page
- Mono micro 9px
- `PAGE α · 1 / 4` (Greek letter for page number)

### Marginalia (decorative)
- Right edge of screen, 10px from edge
- *Source Serif 4* italic, 9px
- `--mute` color
- `writing-mode: vertical-rl`
- Carries a small editorial note about the current session/focus
- Decorative, not critical

### Quote Hero (home/empty state)
- Centered on the home screen
- Bracket marks (⌜⌝) in `--accent`, 22px Fraunces
- Quote text in Fraunces italic 13.5px, max-width 250px
- Attribution in JetBrains Mono 8.5px uppercase
- Default quote: **F. A. Hayek, *The Fatal Conceit* (1988)**
- See §10 for the quote library

### Math Card
- Background: `--surface` (cream) or `--surface-d` (espresso)
- Border: 1px solid `--ink` (or `--ink-d`)
- Border-radius: 3px (subtle, almost square)
- Padding: 16×14px
- **Equation:** centered, *Source Serif 4* 13px, KaTeX-rendered LaTeX
- **Subtitle:** centered, italic 10px
- **Equation number:** top-right, **Greek letter** (α, β, γ) in `--accent`, *Fraunces* italic 11px
- **Source badge:** mono 8.5px, dark background with cream text (e.g., "STOKEY-LUCAS")
- **Page reference:** mono 8.5px, mute color ("ch. 4 · p.142")

### Spoken Version (callout)
- Left border: 2px solid `--accent` (or `--accent-d`)
- No background
- Padding: 10×12px
- Label: "Phronesis says" — mono 7.5px uppercase, oxblood color
- Body: *Source Serif 4* italic 11px

### History Sheet (pull-up)
- Bottom sheet, drag handle at top (36×4px pill in `--mute-2`)
- Header: session title in Fraunces italic 16px
- Meander divider below header
- Turn list with:
  - Role label (mono 8.5px uppercase) + color dot prefix + timestamp
  - Body: *Source Serif 4* 11px (italic for Phronesis, regular for user)
  - Hairline dashed dividers between turns
- **Sticky voice strip at bottom** with:
  - Current state text (italic)
  - Compact 56px voice button (listening state inline)

---

## 6. Iconography

**Style:** 1.5px stroke, line-art, geometric but slightly hand-drawn
**Color:** single-color (ink or accent); duotone optional
**Size:** 30px in voice button; 18px in compact voice button; 14–18px in UI; 10–12px in metadata

**Custom icons needed:**
- 🎙 Microphone (default)
- 🔖 Book (retrieving)
- 〰 Sound wave (speaking)
- ⊙ Concentric circle (listening pulse)
- ⌖ Dashed line (thinking)
- ✕ Pause/close
- ↑ Export/share
- ⌥ Mode switcher

---

## 7. Motion

| Property | Value | Notes |
|---|---|---|
| Default easing | `cubic-bezier(0.4, 0, 0.2, 1)` | Calm, no bounce |
| Default duration | 200–350ms | Considered, not slow |
| Page transitions | Cross-fade 250ms | No slides |
| Listening pulse | 2.4s loop, ease-in-out | Box-shadow 0→12px transparent |
| Math object appear | 250ms fade-in | No slide |
| Voice button hover | 250ms | Subtle background fill |
| Sheet drag | Native | 200ms ease-out on snap |

**Reduced motion:** All non-essential animations disabled under `prefers-reduced-motion: reduce`.

---

## 8. Microcopy

### Voice
Witty, not cute. Curious, not commanding. Rigorously honest. Refined.

### Examples
| State | Label |
|---|---|
| Empty | *(Hayek quote as hero — see §10)* |
| Listening | *"Listening…"* |
| Thinking | *"Considering…"* |
| Retrieving | *"Looking through your materials…"* |
| Speaking | (no label, audio is the signal) |
| Paused | *"Take your time."* |
| Context near limit | *"We're approaching the edge of context. Consider exporting or starting a new session."* |
| Out of context | *"Sorry, we ran out of context, but we can continue in a new session. I'll try to remember what we discussed."* |

### Tone rules
- No exclamation marks unless earned
- No emoji in chrome
- No "AI" or "as an AI" disclaimers
- Acknowledge uncertainty honestly: "I don't have a confident answer here"
- Refined classical references allowed in marginalia

---

## 9. Walk-and-Talk States (Mobile-First)

| State | Voice button | Status label | Status sub |
|---|---|---|---|
| **Idle** | Outlined ink + Greek ring | (Hayek quote) | (none) |
| **Listening** | Brass fill, pulse | "Listening…" | "Captured 12s · 184 wpm" |
| **Thinking** | Dashed ink border | "Considering…" | (none) |
| **Retrieving** | Dashed ink border | "Looking through materials…" | "Stokey-Lucas · p.142" |
| **Speaking** | Oxblood fill | (no label) | (audio only) |
| **Paused** | Oxblood outline | "Take your time." | (none) |

**Glanceability rule:** A user walking must understand the state within 1 second. Status label + button visual must do the job without sound.

---

## 10. Quote Library (Empty-State Hero)

The home screen features a rotating quote from the Austrian intellectual tradition. Default and alternates:

### Primary
> *“The curious task of economics is to demonstrate to men how little they really know about what they imagine they can design.”*
> — F. A. Hayek, *The Fatal Conceit* (1988)

**Why this is the default:** The meta-statement of intellectual humility. Echoes Phronesis' role as a tutor. Self-referentially apt for a tool that didn't exist this morning. Signals culture immediately.

### Alternates (rotate in future)

**Schumpeter:**
> *“Creative destruction is the essential fact about capitalism.”*
> — *Capitalism, Socialism and Democracy* (1942)

**Mises:**
> *“Economics is not about goods and services, it is about human action.”*
> — *Human Action* (1949)

**Menger:**
> *“All things are subject to the law of cause and effect.”*
> — *Grundsätze der Volkswirtschaftslehre* (1871)

**Böhm-Bawerk:**
> *“The present is always the true standard of value.”*
> — *Capital and Interest* (1884)

**Aristotle (the founder of phronesis):**
> *“Practical wisdom is concerned with things human and with questions about what is to be done.”*
> — *Nicomachean Ethics* (c. 340 BC)

### Greek Word Substitutions (footer)

The home bottom bar shows Greek transliterations in place of session number:
- `φιλοσοφία` (philosophia — "love of wisdom") on home / session 0
- `διάλογος` (dialogos — "dialogue") during active session
- `σοφία` (sophia — "theoretical wisdom") in deep research mode

---

## 11. Math Display

**Signature visual moment.**

### Speech
Verbalized naturally by MisoTTS, transformed by `create_math_object` tool.

### Display
- LaTeX-rendered via **KaTeX** (fast, mobile-friendly)
- Custom font: *Source Serif 4* for body math, italic for variables
- **Equation number** top-right: **Greek letter** (α, β, γ) in `--accent`
- Source citation bottom: book badge + chapter/page
- Spoken-version callout below in oxblood-bordered box

### Tap behavior
- Tap card to expand: shows derivation history (future)
- Long press: copy LaTeX

---

## 12. Page-Based UI Update Model

**Core principle:** Each substantive turn or concept becomes a **page** in a session journal. The voice conversation flows through these pages.

### Flow
1. User speaks: *"Walk me through the Bellman equation"*
2. A **new page appears** (centered, parchment surface, the math/quote/concept)
3. **The voice button stays sticky** at the bottom — never moves
4. As the conversation continues, **the current page updates in place**:
   - Math objects appear on the current page
   - Retrieval citations become marginalia
   - Spoken version callout expands
5. When the topic shifts, a **new page** is created; the previous page scrolls up

### Why This Works
- Combines the **calm of voice-pure** UI
- The **focus of object-highlight**
- The **continuity of chat** (history is preserved as pages)
- The voice button is always one tap away, in the same position

### History Sheet
- Drag handle at top
- **Journal-style transcript** of all turns in the session
- Sticky voice strip at bottom (always accessible)
- Tap to dismiss and return to current page

---

## 13. Accessibility

- **Contrast:** All text combinations meet WCAG AA minimum (4.5:1 for body, 3:1 for large)
- **Touch targets:** Minimum 44×44px (Apple HIG)
- **Voice button:** 96×96px primary, 56×56px inline (well above minimum)
- **Focus states:** Visible 2px ink border + 4px offset
- **Screen reader:** All state changes announced via aria-live
- **Reduced motion:** Honored throughout
- **Font scaling:** Layouts reflow gracefully up to 200% zoom

---

## 14. Open Questions (to confirm before implementation)

1. **Light vs. dark primary mode?**
   - Recommendation: **Cream primary, dark mode as refined secondary**
2. **Brand mark:** wordmark with **lowercase φ** as accent — confirm
3. **Loading/empty states:** Hayek quote as default hero — confirm
4. **Equation numbering:** Greek letters (α, β, γ) like classical mathematics — confirm
5. **Dark mode palette:** espresso + brass, not Nous-blue — confirm
6. **Greek transliterations in footer** (φιλοσοφία, διάλογος, σοφία) — confirm

---

## 15. Reference Mockups

A working HTML mockup file is included in this repository:

`docs/mockups/design_mockups.html`

It contains **5 phone mockups** (Home with Hayek quote, Listening, Math Page in cream, Math Page in espresso, History Pull-up Sheet) plus a design tokens strip showing the full palette and typography.

To view: serve the folder locally (`python3 -m http.server` from the `docs/mockups` directory) and open `http://localhost:8000/design_mockups.html`. The mockups include a real pulse animation on the listening state.

---

## 16. Next Steps

1. Lock the 6 open questions above
2. Build a proper component library
3. Add motion studies
4. Build the actual frontend
