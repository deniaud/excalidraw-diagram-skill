---
name: excalidraw-diagram
description: Create Excalidraw diagram JSON files that make visual arguments. Use when the user wants to visualize workflows, architectures, or concepts.
disable-model-invocation: true
---

# Excalidraw Diagram Creator

Generate `.excalidraw` JSON files that **argue visually**, not just display information.

**Setup:** If the user asks you to set up renderer/dependencies, see [README.md](README.md).

## Rules (hard, non-negotiable)

These override stylistic preferences. Violating any of them is a defect.

1. **Palette only.** Every color in element JSON MUST come from [references/color-palette.md](references/color-palette.md). Ad-hoc hex literals are forbidden. If a concept doesn't fit an existing semantic slot, use Primary/Neutral or Secondary — do not invent.
2. **Research-receipt for technical diagrams.** Before emitting JSON for a technical diagram (protocol, API, real system), include a short receipt in the response: spec URLs, real event/method names, and the source you took them from. No generic placeholders like "Event 1".
3. **Pattern cap: ≤3.** No diagram uses more than 3 distinct visual patterns (fan-out, timeline, cycle, …). Each major concept uses a DIFFERENT pattern — no repeated pattern for two majors. See [references/PATTERNS.md](references/PATTERNS.md).
4. **Container budget: ≤2 boxes per 10 text elements.** Default to free-floating text; add a container only when it's a focal point, an arrow binds to it, or the shape itself carries meaning.
5. **Render after every section, not only at the end.** Use the render script and Read the PNG. Save `diagram.iterN.excalidraw` before each edit pass that follows a render. Details in [references/RENDER_LOOP.md](references/RENDER_LOOP.md).
6. **Stop-after-5.** Cap the render-fix loop at 5 iterations. If defects remain after iteration 5, escalate to the user with a concrete list of remaining issues — do not loop silently.
7. **Aesthetic defaults.** `fontFamily: 3`, `roughness: 0`, `opacity: 100` for every element. Element `text` contains only readable words.

## Core Philosophy

**Diagrams ARGUE, not DISPLAY.** A diagram is a visual argument that shows relationships, causality, and flow words can't. The shape IS the meaning.

- **Isomorphism Test:** if you removed all text, would the structure alone communicate the concept? If not, redesign.
- **Education Test:** could someone learn something concrete from this, or does it just label boxes? Good diagrams show actual formats, real event names, concrete examples.

## Depth Assessment (Step 0)

Before designing, decide:
- **Simple/Conceptual** — abstract shapes, labels, relationships. For mental models, philosophies, audiences who don't need technical specifics.
- **Comprehensive/Technical** — concrete examples, code snippets, real data. For real systems, tutorials, educational content. **MUST include evidence artifacts AND emit a research-receipt (Rule 2).**

## Evidence Artifacts (technical diagrams)

Concrete examples that prove your diagram is accurate. Pick what's relevant:

| Artifact Type | When to Use | How to Render |
|---|---|---|
| Code snippets | APIs, integrations | Dark rectangle + syntax-colored text (palette) |
| JSON / data | Schemas, payloads | Dark rectangle + colored text (palette) |
| Event sequences | Protocols, workflows | Timeline pattern (line + dots + labels) |
| UI mockups | Showing actual output | Nested rectangles mimicking real UI |
| Input samples | What goes IN | Rectangle with sample content visible |
| API/method names | Real function calls | Actual names from docs |

Principle: **show what things actually look like**, not what they're called.

## Multi-Zoom Architecture (comprehensive diagrams)

Operate at three levels simultaneously:
- **L1 Summary flow** — simplified overview of the full pipeline (`Input → Processing → Output`).
- **L2 Section boundaries** — labeled regions grouping related components (Backend / Frontend; Setup / Execution / Cleanup).
- **L3 Detail inside sections** — evidence artifacts, code snippets, concrete examples. Where the educational value lives.

## Design Process

**Step 0 — Assess depth.** Simple vs Comprehensive. If comprehensive: research first (emit receipt per Rule 2).

**Step 1 — Understand deeply.** For each concept: what does it DO (not what IS it)? What relationships exist? What would someone need to SEE?

**Step 2 — Map concepts to patterns.** Each major concept gets a pattern that mirrors its behavior. Respect Rule 3 (≤3 distinct, no repeats among majors). See [PATTERNS.md](references/PATTERNS.md).

**Step 3 — Sketch the flow.** Mentally trace how the eye moves. There must be a clear visual story.

**Step 4 — Build JSON section by section.** For comprehensive diagrams: one section per edit, descriptive string IDs, seeds namespaced by section, cross-section bindings updated as you go. Full procedure in [RENDER_LOOP.md](references/RENDER_LOOP.md). Element snippets in [element-templates.md](references/element-templates.md). Wrapper schema in [json-schema.md](references/json-schema.md).

**Step 5 — Render & validate.** Per Rule 5 and 6: render after every section AND at the end, save iterations, cap at 5.

**Step 6 — Run the checklist.** [references/CHECKLIST.md](references/CHECKLIST.md) before declaring done.

## JSON Wrapper (minimum)

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "https://excalidraw.com",
  "elements": [...],
  "appState": {"viewBackgroundColor": "#ffffff", "gridSize": 20},
  "files": {}
}
```

Text element template: `fontSize: 16`, `fontFamily: 3`, `textAlign: "center"`, `verticalAlign: "middle"`. `text` and `originalText` must match. Full templates in [element-templates.md](references/element-templates.md).

## References

- [references/PATTERNS.md](references/PATTERNS.md) — visual patterns, shape meaning, aesthetic defaults, bad/good comparison.
- [references/RENDER_LOOP.md](references/RENDER_LOOP.md) — render script, iteration bookkeeping, defect catalog, section-by-section workflow.
- [references/CHECKLIST.md](references/CHECKLIST.md) — full 30-point quality gate.
- [references/color-palette.md](references/color-palette.md) — single source of truth for all colors.
- [references/element-templates.md](references/element-templates.md) — copy-paste JSON per element type.
- [references/json-schema.md](references/json-schema.md) — top-level file structure.
