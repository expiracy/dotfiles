---
name: uml-diagrams
description: Use when creating or editing LaTeX/TikZ UML diagrams for Markdown documentation, including sequence, activity, state machine, class, component, deployment and use case diagrams, or related software architecture views.
---

# UML Diagrams

Create Markdown diagram assets: editable TikZ source, an SVG or PNG preview, and a vector PDF when available.

## Choose the view

Support these seven common views:

| Scenario | Diagram |
|----------|---------|
| Ordered messages between participants | **Sequence** |
| Workflow steps, decisions and parallel branches | Activity |
| One entity's states and event-driven transitions | State machine |
| Types, fields, operations and relationships | Class |
| Subsystems, interfaces and dependencies | Component |
| Runtime placement on hosts and execution environments | Deployment |
| Actors and their goals within a system boundary | Use case |

Honour an explicitly requested supported type; otherwise choose a view and briefly explain why. Draw one focused view unless several are needed. Ask when the question is unclear or the requested type is outside this set. Label informal architecture views as informal.

Preserve supplied names, relationships, directions, multiplicities, message order, guards and timing. Mark illustrative assumptions; ask when missing semantics affect correctness. Do not infer ownership from pointer types or invent timing, cardinalities or failure policies.

## Reuse the canonical theme

Copy the shared preamble and `uml/` styles from [the template](assets/uml-class-template.tex) into self-contained source and replace its example body. Keep the blue/grey palette, sans-serif type, 0.65pt strokes, 10pt body and 9pt labels. [The preview](assets/uml-class-preview.png) shows the theme.

Use the correct UML symbols for the view. Read [the reference](references/uml-and-layout.md) for its notation and relevant compartment, arrow or layout details. Reserve space for labels and connector routes; reflow before shrinking text.

## Compile and deliver

Prefer an available native source editor/compiler. Use the [existing command-line workflow](references/uml-and-layout.md#portable-build-and-visual-check) when rendered asset export requires it. Do not install a toolchain for an ordinary diagram request.

Compile and check errors, missing glyphs and overfull boxes. Render and inspect at the intended Markdown width for notation, complete text, labels, connectors, overlaps and clipping. Fix the source and re-render after changes; compilation alone does not verify layout.

Keep existing asset paths. In Vault, use `features/assets/<feature-id>/` for new feature assets and the task's `assets/` for task-only media. Embed previews with relative Markdown image links and keep `.tex` source beside them.

Report source and preview paths, actual checks and limitations. If compilation, export or inspection is unavailable, retain the source and mark that scope unverified.
