# Quality Checklist

Final gate before declaring a diagram done. SKILL.md states the Rules (hard, non-negotiable). This checklist is the broader review — pass everything here, not just the Rules.

## Depth & Evidence (technical diagrams)

1. Research done — actual specs, formats, event names looked up?
2. Research-receipt section emitted in the response before the JSON?
3. Evidence artifacts present — code snippets, JSON examples, or real data?
4. Multi-zoom — summary flow + section boundaries + detail all present?
5. Concrete over abstract — real content shown, not just labeled boxes?
6. Educational value — could someone learn something concrete from this?

## Conceptual

7. Isomorphism — does each visual structure mirror its concept's behavior?
8. Argument — does the diagram SHOW something text alone couldn't?
9. Variety — does each major concept use a different visual pattern?
10. Pattern cap — ≤3 distinct patterns used across the diagram?
11. No uniform containers — avoided card grids and equal-box layouts?

## Container Discipline

12. Container budget respected (≤2 boxes per 10 text elements)?
13. Lines as structure — tree/timeline using lines + text rather than boxes?
14. Typography hierarchy — font size and color creating hierarchy?

## Structural

15. Connections — every relationship has an arrow or line?
16. Flow — clear visual path for the eye to follow?
17. Hierarchy — important elements are larger / more isolated?

## Technical / JSON

18. `text` contains only readable words (no `originalText` ≠ `text` desync)?
19. `fontFamily: 3` everywhere?
20. `roughness: 0` for clean/modern (unless hand-drawn brief)?
21. `opacity: 100` for all elements (no transparency)?
22. All colors come from `color-palette.md` (no ad-hoc hex)?

## Visual Validation (rendered PNG)

23. Diagram rendered to PNG and visually inspected?
24. No text overflow — all text fits its container?
25. No unintentional overlaps?
26. Even spacing between sibling elements?
27. Arrows land on intended elements without crossing others?
28. Readable at export size — text legible in the PNG?
29. Composition balanced — no large voids or overcrowded regions?
30. Iteration count ≤5 OR escalated to user with concrete remaining issues?
