# Combined prompt + upload

A single prompt box that invites the user to type a prompt **or** drop in a file — replacing what used to be a separate text box and upload button.

## Getting started

```sh
python3 -m http.server 8765
open http://localhost:8765/combined-prompt-upload.html
```

## Layout

A single 1280×720 screen. Content is centered in a 600px column.

- **Top bar** — back and close icon buttons.
- **Heading** — two centered lines: *Let's create your first presentation* (grey) and *Describe your deck, or upload a file* (black).
- **Toolbar above the box** — Upload Files on the left · Slides / Standard / Settings on the right.
- **Prompt box** — outer black border + inner dashed frame signal the whole area is a drop target.
  - Auto-focused textarea at the top
  - Two-line placeholder: pencil icon + *Type here or* · upload icon + *drop in a file*
  - Sample-prompts ticker inside, at the bottom
- **Create Presentation →** — wide dark button below the box; **hidden until something is typed**.

## Behaviours

| Trigger | What happens |
|---|---|
| Page load | Textarea auto-focuses, native cursor blinks |
| Page load | Cascade reveals the screen (see Animations) |
| User types | Custom placeholder fades out; *Create Presentation* fades in |
| User clears text | Placeholder returns; CTA fades back out |
| Hover the ticker | Chip ticker pauses |
| Hover any toolbar button | Border darkens slightly |

## Animations

### Entrance cascade (runs once on page load)

| Element | Start | Duration | Travel |
|---|---|---|---|
| Intro line ("Let's create…") | 0s | 1.5s | 40px ↑ |
| Action line ("Describe your deck…") | 1.2s | 1.5s | 40px ↑ |
| Toolbar above the box | 1.6s | 1.5s | 40px ↑ |
| Prompt box | 1.8s | 1.5s | 40px ↑ |
| Intro line slow fade-out | 4.0s → 8.0s | 4s | none |

Each element starts before the previous one finishes, so the cascade feels overlapping rather than mechanical. Easing is `cubic-bezier(0.16, 1, 0.3, 1)` (snappy ease-out); the intro's lifecycle uses `cubic-bezier(0.4, 0, 0.2, 1)`.

### Looping micro-animations

| Element | Motion | Cycle |
|---|---|---|
| Upload icon — arrow | Lifts up 3px | 1.4s |
| Upload icon — bracket | Dips down 0.6px in opposition | 1.4s |
| CTA arrow | Nudges right 3px | 1.4s |
| Sample-prompts ticker | Scrolls right-to-left, full loop | 70s |
| Textarea cursor | Native blink | 1s |

The two halves of the upload glyph move in opposition so the icon reads as a small "lift and release" — the arrow does the work, the bracket gives slightly under it. The bracket motion is deliberately tiny so the arrow stays the focal point.

## Files

| File | What it is |
|---|---|
| `combined-prompt-upload.html` | The self-contained design (HTML + CSS, no build step). |
| `README.md` | This file. |
