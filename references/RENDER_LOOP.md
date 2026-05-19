# Render & Validate — Full Workflow

You cannot judge a diagram from JSON alone. Render to PNG, view it, fix it — in a loop. SKILL.md states the hard rules; this file is the procedure.

## Setup (first-time only)

```bash
cd .claude/skills/excalidraw-diagram/references
uv sync
uv run playwright install chromium
```

## Render Command

```bash
cd .claude/skills/excalidraw-diagram/references && \
  uv run python render_excalidraw.py <path-to-file.excalidraw>
```

Outputs a PNG next to the `.excalidraw` file. Then use the **Read tool** on the PNG to actually view it.

## Iteration Bookkeeping (mandatory)

Before every edit pass that follows a render, copy the current file to a numbered iteration so you can diff and roll back:

```bash
cp diagram.excalidraw diagram.iter1.excalidraw   # before first edit pass
cp diagram.excalidraw diagram.iter2.excalidraw   # before second edit pass
```

Keep iterations until the diagram ships, then delete `*.iter*.excalidraw`.

## The Loop (per section AND at the end)

For comprehensive diagrams: render after **each section is added**, not only at the end. Catching an overlap after section 2 costs one edit; catching it after section 7 may force a re-layout.

**1. Render & view** — Run the render script, then Read the PNG.

**2. Audit against the original vision.** Before hunting for bugs, ask:
- Does the visual structure match the conceptual structure planned in Step 1-4?
- Does each section use the pattern intended (fan-out, convergence, timeline, etc.)?
- Does the eye flow through the diagram in the designed order?
- Is hierarchy correct — hero elements dominant, supporting elements smaller?
- For technical diagrams: are evidence artifacts readable and properly placed?

**3. Defect check:**
- Text clipped by or overflowing its container.
- Text or shapes overlapping other elements.
- Arrows crossing through elements instead of routing around them.
- Arrows landing on the wrong element or pointing into empty space.
- Labels floating ambiguously (not clearly anchored to what they describe).
- Uneven spacing between elements that should be evenly spaced.
- Sections with too much whitespace next to cramped ones.
- Text too small to read at the rendered size.
- Composition feels lopsided or unbalanced.

**4. Fix.** Common operations:
- Widen containers when text is clipped.
- Adjust `x`/`y` to fix spacing and alignment.
- Add intermediate waypoints to arrow `points` to route around elements.
- Reposition labels closer to the element they describe.
- Resize elements to rebalance visual weight across sections.

**5. Re-render & re-view.** Same script, Read the new PNG.

**6. Repeat — but cap at 5 iterations.** If after the 5th iteration the diagram still has unresolved defects, STOP. Surface to the user with a concrete list of remaining issues and a question (e.g. "the timeline overlaps the convergence section — should I drop the convergence, shrink the timeline, or restructure?"). Do not keep looping silently.

## Stop Conditions

Done when ALL of these hold:
- Rendered diagram matches the conceptual design from planning.
- No text is clipped, overlapping, or unreadable.
- Arrows route cleanly and connect to the right elements.
- Spacing is consistent and the composition is balanced.
- You'd show it to someone without caveats.

If fewer than 5 iterations: continue. If 5 reached and still not done: stop and escalate.

## Section-by-Section JSON Build

**Phase 1: Build each section**
1. Create the base file with the JSON wrapper (`type`, `version`, `appState`, `files`) and section 1.
2. Add one section per edit. Each section gets a dedicated pass.
3. Use descriptive string IDs (`trigger_rect`, `arrow_fan_left`) so cross-section references are readable.
4. Namespace seeds by section (section 1 → 100xxx, section 2 → 200xxx) to avoid collisions.
5. Update cross-section bindings as you go — when a new arrow binds to a previous element, edit the earlier element's `boundElements` array in the same pass.
6. **After each section: render + audit + fix. Save iteration before the next section.**

**Phase 2: Review the whole**
- Are cross-section arrows bound correctly on both ends?
- Is overall spacing balanced?
- Do IDs and bindings reference elements that actually exist?

**Phase 3: Final render & validate**
Run the loop above. Cap at 5 iterations.

## What NOT to Do

- Do not generate the entire diagram in one response — output token limit will truncate.
- Do not delegate JSON generation to a coding agent — coordination overhead exceeds benefit.
- Do not write a Python generator script — templating + coordinate math creates a debugging layer of indirection. Hand-crafted JSON with descriptive IDs is more maintainable.
- Do not skip render after a section "because it's a small section" — small sections are how overlaps sneak in.
