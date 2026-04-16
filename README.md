# Combined prompt + upload

A single prompt box that invites the user to **either type a prompt or drop a document** — replacing the older "type OR upload" split where those were two separate affordances.

## Overview

The page shows two variants stacked, separated by a thin divider:

| Variant | Purpose |
|---|---|
| Primary (top) | The default screen with the **sample-prompts ticker** above the input. |
| Clean (bottom) | The same layout **without sample prompts** — for teams who want a simpler first-run view. |

## Getting started

```sh
python3 -m http.server 8765
open http://localhost:8765/combined-prompt-upload.html
```

---

## Components

### 1. Top bar

- Back button (left) and close button (right).
- Progress indicator from the original Figma was dropped — it wasn't earning its space at this step.

### 2. Heading

Two lines, centered:

> **Let's build your first deck.** *(grey)*
> **Enter a prompt, or upload a file.** *(black)*

The grey lead-in adds personality without needing a subtitle.

### 3. Sample prompts ticker

- Label **"PROMPTS CURATED FOR YOU"** between two faded horizontal dividers.
- Chips auto-scroll **right-to-left** at `40s / cycle` — slow enough not to distract.
- **Hover pauses** the ticker.
- Edges fade into the background via a CSS mask.
- Each chip is a clickable starter prompt.

### 4. Prompt box

The main input. Uses a **dashed inner frame** to signal the entire area is a drop target — type to write, or drop a file anywhere inside.

#### 4a. Upload chip (top-right)

The `PDF, DOCX or PPT` pill inside the prompt box.

**Purpose**
Secondary affordance to the text input. Tells the user which file types are accepted, and gives a clickable shortcut to the file picker without needing to drag.

**Visual style**

| Property | Value |
|---|---|
| Shape | Small dashed pill (echoes the drop-zone frame) |
| Fill | White |
| Border | `1.5px dashed rgba(26, 26, 26, 0.2)` |
| Text | 12px, secondary grey, uppercase off |
| Position | Top-right of the box, 12px from edges |

**Hover state**

- Border darkens → `rgba(26, 26, 26, 0.35)`
- Text darkens → primary
- No background or heavy shadow — keeps it calm.

**Micro-interaction — the "lift"**

The upload glyph is built from two independently-animated parts that share a `1.4s ease-in-out infinite` loop:

| Part | Motion | Amplitude |
|---|---|---|
| Arrow | Rises up, then settles | `-3px` |
| Bracket / tray | Dips down in opposition | `+0.6px` |

The opposing motion gives the icon a tiny sense of weight and physics — the arrow looks like it's pushing off the tray. The bracket dip is deliberately **subtle** so the arrow remains the focal point. Together they reinforce the "drop here" metaphor without ever becoming noisy.

### 5. Bottom toolbar

| Button | Purpose |
|---|---|
| `Slides: Auto ▼` | Slide count / auto |
| `🧠 Standard ▼` | Thinking-mode / model selector |
| Settings icon | Advanced controls |
| `→` *(dark, right)* | Submit — starts generating the deck |

All four sit `12px` from the bottom edge of the box, matching the side padding.

---

## Layout notes

- Canvas width: **1280px**.
- Content column at `left: 340px`, width `600px` — prompt box, heading, and chips share one vertical axis.
- **All insets inside the prompt box are 12px** (padding, toolbar offsets) so every edge aligns to the same grid.
- Main screen height: `720px`. Iteration sits directly below, separated only by a 1px divider.

## Files

| File | What it is |
|---|---|
| `combined-prompt-upload.html` | The self-contained design (HTML + CSS, no build step). |
| `README.md` | This file. |
