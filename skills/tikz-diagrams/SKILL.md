---
name: tikz-diagrams
description: Use when creating or editing LaTeX/TikZ UML diagrams for Markdown documentation, including sequence, activity, state machine, class, component, deployment and use case diagrams, or related software architecture views.
---

# TikZ Diagrams

Create diagram assets for Markdown: editable TikZ source plus a rendered SVG or PNG for embedding, and a vector PDF when compilation supports it. Preserve the requested diagram type, model, detail and final reading size. A diagram request does not require a prose LaTeX document.

## Choose the UML view

Support these seven common views. Choose one that answers the document's question:

| Scenario or question | Diagram |
|----------------------|---------|
| Who calls whom, in what order, during one request or interaction? | **Sequence** |
| What steps, decisions and parallel branches form a workflow? | Activity |
| How does one entity change state in response to events? | State machine |
| What types, fields, operations and structural relationships exist? | Class |
| What subsystems, interfaces and dependencies form the software? | Component |
| What runs where, across hosts and execution environments? | Deployment |
| Which actors pursue which goals through the system? | Use case |

For an explicit supported type, use it. Otherwise select the best view and briefly state why. Sequence shows exchanges between participants; activity shows the process; state machine shows one entity's lifecycle. Component shows software organisation; deployment shows runtime placement. Use case shows goals, not execution order. Draw one focused view unless the request needs several; ask when the intended question is unclear. For a requested type outside this set, explain the supported scope and ask about a suitable supported view rather than silently substituting.

Consult the [notation table](references/uml-and-layout.md#diagram-types) for the selected view. Use formal UML notation for UML requests; label informal architecture views as informal.

Identify supplied entities, relationships, direction, multiplicity, message order, guards and timing. Preserve names and facts. Mark illustrative choices or unresolved relationships; ask when missing semantics affect correctness. Do not infer ownership from pointer types or invent timing, cardinalities or failure policies.

## Reuse the canonical theme

The shared preamble and `uml/` style block in [the template](assets/uml-class-template.tex) are the canonical visual source for every type. Copy those definitions into a self-contained diagram, then replace the class-example body with the requested view's appropriate glyphs. [The preview](assets/uml-class-preview.png) shows the theme.

Keep its blue/grey palette, sans-serif typography, 0.65 pt strokes, padding and arrow proportions consistent across diagrams. Use the existing class, component, action, state, actor, lifeline, interface, frame and final-node primitives. Deployment cube faces and sequence frame headings use normal TikZ geometry with the same styles. Correct UML notation takes precedence over making every symbol look like a class box.

The default body is 10pt and labels 9pt at natural size. Reflow or simplify before shrinking text; check the final Markdown embedding width. The theme is a local visual convention, not an OMG-mandated colour scheme.

## Place symbols, then route connectors

1. Set canvas, reading direction and meaningful event/time order. Align related nodes and reserve lanes for routes, notes and labels.
2. Set widths and deliberate line breaks. Use border-relative positioning and size the next row from actual content. Start with 12–20mm horizontal gaps and 20–26mm between class rows, then adjust.
3. Use the relationship and flow styles for their actual meaning. Keep open activity-flow heads, final symbols, lifeline headings and message arrowheads distinct. Distinguish standard UML keywords from defined stereotypes; use plain explanatory text for other connector labels.
4. Connect explicit anchors through clear waypoints. Place labels on straight segments and multiplicities beside the endpoints they count. Check self-calls, nested frames, group boundaries and underlying paths.

TikZ bends and positioning do not automatically avoid collisions. [The reference](references/uml-and-layout.md) covers compartments, groups, arrows and type-specific geometry.

## Compile, inspect, deliver

Prefer an available native LaTeX source editor/compiler for standalone diagram editing and diagnostics. Use the existing [command-line workflow](references/uml-and-layout.md#portable-build-and-visual-check) when rendered asset files are needed and native export is unavailable. Native standalone compilation needs a self-contained source. Installing a toolchain is outside an ordinary diagram request.

Check compilation diagnostics, missing glyphs and overfull boxes. Render and inspect the entire diagram at its intended size, then enlarge dense areas. Verify notation, arrowheads, complete text, labels, borders, connectors and clipping. Correct the source and re-render after changes; compilation alone is not a layout check.

In Vault, follow its guide: keep feature assets in `features/assets/<feature-id>/`, task-only assets in that task's `assets/`, and existing media at their current paths. Embed the SVG/PNG using a relative Markdown image link and retain the `.tex` source beside it. Do not turn the Markdown document into a LaTeX report.

Report source and preview paths, actual compile/render checks and limitations. If compilation, export or inspection is unavailable, preserve the source and label the missing scope unverified rather than claiming a checked image.
