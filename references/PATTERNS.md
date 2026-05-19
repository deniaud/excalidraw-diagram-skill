# Visual Patterns, Shape Meaning, Aesthetics

Concrete vocabulary the diagram chooses from. Read this when planning Step 2 (Map Concepts to Patterns).

## Pattern → Concept Mapping

| If the concept... | Use this pattern |
|-------------------|------------------|
| Spawns multiple outputs | **Fan-out** (radial arrows from center) |
| Combines inputs into one | **Convergence** (funnel, arrows merging) |
| Has hierarchy/nesting | **Tree** (lines + free-floating text) |
| Is a sequence of steps | **Timeline** (line + dots + free-floating labels) |
| Loops or improves continuously | **Spiral/Cycle** (arrow returning to start) |
| Is an abstract state or context | **Cloud** (overlapping ellipses) |
| Transforms input to output | **Assembly line** (before → process → after) |
| Compares two things | **Side-by-side** (parallel with contrast) |
| Separates into phases | **Gap/Break** (visual separation between sections) |

## Pattern Sketches

### Fan-Out (one-to-many)
```
        ○
       ↗
  □ → ○
       ↘
        ○
```
Use for: sources, PRDs, root causes, central hubs.

### Convergence (many-to-one)
```
  ○ ↘
  ○ → □
  ○ ↗
```
Use for: aggregation, funnels, synthesis.

### Tree (hierarchy)
```
  label
  ├── label
  │   ├── label
  │   └── label
  └── label
```
Use `line` elements for the trunk and branches, free-floating text for labels.

### Spiral / Cycle
```
  □ → □
  ↑     ↓
  □ ← □
```
Use for: feedback loops, iterative processes, evolution.

### Cloud (abstract state)
Overlapping ellipses with varied sizes. Use for: context, memory, conversations, mental states.

### Assembly line (transformation)
```
  ○○○ → [PROCESS] → □□□
  chaos              order
```
Use for: transformations, processing, conversion.

### Side-by-Side (comparison)
Two parallel structures with visual contrast. Use for: before/after, options, trade-offs.

### Gap/Break
Visual whitespace or barrier between sections. Use for: phase changes, context resets, boundaries.

### Lines as Structure
- **Timelines**: vertical/horizontal line with 10–20px dot markers, free-floating labels beside each.
- **Tree**: vertical trunk + horizontal branches, no boxes around nodes.
- **Dividers**: thin dashed lines between sections.
- **Flow spine**: central line that elements relate to.

```
Timeline:           Tree:
  ●─── Label 1        │
  │                   ├── item
  ●─── Label 2        │   ├── sub
  │                   │   └── sub
  ●─── Label 3        └── item
```

## Shape Meaning

| Concept Type | Shape | Why |
|--------------|-------|-----|
| Labels, descriptions, details | none (free-floating text) | Typography creates hierarchy |
| Section titles, annotations | none (free-floating text) | Font size/weight is enough |
| Markers on a timeline | small `ellipse` (10–20px) | Visual anchor, not container |
| Start, trigger, input | `ellipse` | Soft, origin-like |
| End, output, result | `ellipse` | Completion, destination |
| Decision, condition | `diamond` | Classic decision symbol |
| Process, action, step | `rectangle` | Contained action |
| Abstract state, context | overlapping `ellipse` | Fuzzy, cloud-like |
| Hierarchy node | lines + text (no boxes) | Structure through lines |

## Aesthetics Defaults

- `roughness: 0` for modern/technical diagrams. `roughness: 1` only for explicit hand-drawn brief.
- `strokeWidth`: `1` for dividers/subtle lines, `2` for shapes and arrows, `3` only for the main flow line.
- `opacity: 100` for every element. Create hierarchy via color, size, stroke width — never transparency.
- Hero element 300×150, primary 180×90, secondary 120×60, small 60×40. Hero gets ≥200px of empty space.

## Container vs Free-Floating Text — Decision

Add a container only when at least one is true:
- It is a focal point of a section.
- It needs visual grouping with other elements.
- An arrow needs to bind to it.
- The shape itself carries meaning (decision diamond, start/end ellipse).

Otherwise: free-floating text. The hard cap is in SKILL.md (Rules).

## Bad vs Good (quick comparison)

| Bad (Displaying) | Good (Arguing) |
|------------------|----------------|
| 5 equal boxes with labels | Each concept has a shape that mirrors its behavior |
| Card grid layout | Visual structure matches conceptual structure |
| Icons decorating text | Shapes that ARE the meaning |
| Same container for everything | Distinct visual vocabulary per concept |
| Everything in a box | Free-floating text with selective containers |
| Generic labels (Input/Process/Output) | Specific: shows what input/output actually looks like |
| "Events" or "Messages" label | Timeline with real event/message names from the spec |
| "UI" or "Dashboard" rectangle | Mockup showing actual UI elements and content |
