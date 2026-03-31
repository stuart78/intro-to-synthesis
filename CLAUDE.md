# Intro to Synthesis - Slide Deck

Interactive single-file HTML slide deck for a workshop at Synth Library Portland (March 29, 3PM). Uses VCV Rack for demos.

## File Structure

- `intro-to-synthesis-slides.html` - the entire deck (single file, HTML + CSS + JS)
- `intro-to-synthesis-outline.md` - workshop outline

## Browser Testing

The slide deck cannot be loaded or previewed via the Chrome browser tool (neither `file://` URLs nor localhost servers work). The user tests visually using the native file preview in Cowork mode, which Claude cannot see. Rely on JS syntax checking (`node -c`) and code review for validation.

## Slide Numbering

Slides are **1-indexed** in conversation (matching the on-screen navigator), but **0-indexed** in code (`data-slide="0"` = slide 1).

| Slide | Code Index | Title |
|-------|-----------|-------|
| 1 | 0 | Intro to Synthesis (title) |
| 2 | 1 | What is Synthesis? |
| 3 | 2 | Three Questions |
| 4 | 3 | Voltage Basics |
| 5 | 4 | CV = Audio |
| 6 | 5 | Four Waveforms |
| 7 | 6 | Fundamentals & Overtones |
| 8 | 7 | The Filter |
| 9 | 8 | Pitch & Frequency |
| 10 | 9 | Noise |
| 11 | 10 | 1 Volt per Octave |
| 12 | 11 | Controlling Pitch |
| 13 | 12 | Gates & Triggers |
| 14 | 13 | Envelopes |
| 15 | 14 | The VCA |
| 16 | 15 | The LFO |
| 17 | 16 | Envelope as Modulation |
| 18 | 17 | Building the Classic Voice |
| 19 | 18 | Breaking the Paradigm |

## Chart / Visualization Style

All canvas-based charts should follow these conventions consistently:

### Layout
- Use `initCanvas(id, w, h)` helper (handles DPR scaling)
- Standard margins: `mL = 72, mR = 30–60, mT = 40–52, mB = 40–64` (adjust per chart; left margin needs room for y-axis labels)
- Plot area: `pW = w - mL - mR`, `pH = h - mT - mB`

### Border & Grid
- **Light grey thin border** around plot area: `ctx.strokeStyle = '#bbb'; ctx.lineWidth = 1; ctx.strokeRect(mL, mT, pW, pH)`
- **Zero/center line**: `ctx.strokeStyle = '#bbb'` or `'#999'`, lineWidth 1–1.5
- No dark backgrounds, no scope-style green grids - keep it clean on white

### Axes
- **Y-axis labels**: `ctx.font = '600 12–13px Source Code Pro, monospace'; ctx.fillStyle = '#1a1a1a'`, right-aligned at `mL - 10`
- **Y-axis title** (vertical, rotated): `700 12px Source Code Pro`, colored by meaning (green for amplitude)
- **X-axis labels**: centered, `'600 13px Source Code Pro'`, `#1a1a1a` for primary, `#888` for secondary
- **X-axis title**: `700 12px Source Code Pro`, colored by meaning (blue for time/frequency)
- **Tick marks**: `#1a1a1a`, lineWidth 2

### Color Coding (semantic)
- **Blue `#0066cc`**: pitch, frequency, time - anything related to "how fast"
- **Green `#2e7d32`**: amplitude, level, dynamics - anything related to "how loud"
- **Orange `#cc4400`**: waveshape, timbre, control signals - anything related to "what shape"
- Waveform-specific colors are defined in `WAVE_HARMONICS` objects with `.color` and `.rgb` properties

### Signal Traces
- Line width: 2–2.5 for primary traces, 1.5 for secondary
- Optional subtle fill under curves: `rgba(r, g, b, 0.06–0.1)`

### Annotations
- **Period brackets** (top or bottom): colored line with end caps showing one cycle width, labeled with period/frequency
- **Amplitude brackets** (right side): green vertical bracket with voltage label
- Font for annotations: `'600 11–12px Source Code Pro, monospace'`

### Do NOT use
- Dark/black scope backgrounds
- Green phosphor glow effects
- Shadow/blur effects on traces
- Non-standard color schemes

## Typography Tiers

All text sizes are standardized. Do NOT add inline `font-size` overrides - use the CSS classes instead.

| Tier | Size | CSS | Usage |
|------|------|-----|-------|
| h1 | 56px | `h1` | Title slide only |
| h2 | 24px | `h2` | Slide titles |
| h3 | 28px | `h3` | Major sub-headings (rarely used) |
| h4 | 20px | `h4` | Sub-headings within slides |
| Body | 20px | inherited from `body` | Primary slide text (paragraphs, explanations) |
| Callout | 18px | `.slide-callout` | Bottom-of-slide takeaway lines |
| Description | 15px | `.desc-text` | Helper text below controls, secondary descriptions |
| UI controls | 13px | `.wave-btn`, `.audio-btn`, `.slider-row label/val` | Buttons, slider labels, value readouts |
| Micro-label | 11px | `.micro-label` | Uppercase faint section labels ("Time Domain", "Target:", etc.) |
| Section marker | 13px | `.section-marker` | "Part 1 · Timbre" etc. |

### Fonts
- **EB Garamond** (serif): all body/heading text
- **Source Code Pro** (monospace): UI controls, data readouts, canvas labels, section markers

### Special-purpose (OK to inline)
- Pitch note display: 32px (data readout, slide 8)
- Pitch freq readout: 16px (monospace data, slide 8)
- Envelope ADSR labels: 12px (tight control panel, slide 13)
- Canvas axis/annotation labels: 10–13px Source Code Pro (chart-specific)

## HTML Slide Style Rules

These rules apply when writing slide HTML. Follow them for every new or modified slide to avoid recurring issues.

### Text sizing
- **Primary explanatory text** uses bare `<p>` tags (inherits 20px body size). Do NOT use `desc-text` for substantive content - only for genuinely secondary helper text (e.g. "Sweep the cutoff to hear harmonics disappear").
- **Never add inline `font-size`** unless listed in Special-purpose above. Use the CSS classes.
- If two adjacent paragraphs look like different sizes, one probably has `desc-text` when it shouldn't.

### Color in HTML
- **Do NOT use `style="color: var(--accent-blue)"` or any inline color** on body text, `<strong>`, or `<span>` tags. Body text is always `#1a1a1a` (inherited).
- `<strong>` is for bold emphasis only, never colored.
- Headings (`h3`, `h4`) use inherited color by default. The **only exception** is the Timbre/Pitch/Rhythm semantic headings (slides 2, 3, 17) which use orange/blue/green to match diagram color coding. Do not add color to headings elsewhere.

### Canvas text color
- **Data labels** (voltages, notes, values): `#1a1a1a`
- **Secondary values** (frequencies, dim info): `#888`
- **Column/axis headers**: `#999`
- **Semantic color** (blue/green/orange) is reserved for chart elements: signal traces, axis titles describing a dimension, annotation brackets. Never use semantic color on table data text.

### `.slide-callout em` pattern
- Used for the key takeaway phrase at the bottom of a slide.
- The `<em>` highlights a short phrase (2-5 words), not single words like "the" or "a".
- CSS makes it non-italic with slightly heavier weight. No color - callouts stay dim.

### Punctuation
- **No em dashes.** Use a regular hyphen with spaces (` - `) instead of `—` everywhere: HTML text, JS strings, comments, canvas labels.

### Checklist before finishing a slide
1. No inline `font-size` except special-purpose items
2. No inline `color` on body text, `<strong>`, `<h3>`, or `<h4>`
3. Canvas text uses `#1a1a1a` / `#888` / `#999` only (no semantic color on data)
4. `desc-text` only on genuinely secondary helper text, not main content
5. No em dashes anywhere
6. JS syntax validates: `sed -n '/<script>/,/<\/script>/p' file | sed '1d;$d' | node -c`
