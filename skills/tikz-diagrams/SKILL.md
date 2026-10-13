---
name: tikz-diagrams
description: Use when creating or editing UML-style or software architecture diagrams with LaTeX/TikZ, especially class, component, and sequence diagrams that need consistent styling, readable labels, and carefully checked spacing and connector routes.
---

# TikZ Diagrams

Create clear, consistent diagrams and verify the rendered result. Deliver editable
TikZ source and a vector PDF when compilation is available. Follow the requested
diagram type, level of detail, page size, and existing document style.

## Start with the meaning

Identify the entities, relationships, arrow directions, labels, and multiplicities
the diagram must show. Preserve supplied names and facts. Mark illustrative
choices or unresolved relationships; do not invent ownership, cardinalities,
failure policies, or security requirements to fill space.

Choose formal UML notation when requested. For an informal architecture diagram,
use the appropriate UML-inspired visual language without claiming full UML compliance.

## Reuse one visual style

Start from [the standalone template](assets/uml-class-template.tex) and its
central `uml/` style block. Replace the example content with the requested model.
Keep the same typography, palette, stroke widths, padding, and arrow sizes across
related diagrams. Change shared styles when adapting a theme rather than styling
every node independently. [The preview](assets/uml-class-preview.png) shows the
default appearance.

Use aligned rows or columns, consistent box widths, muted fills, and clear dark
text. The template uses a 10pt body and 9pt labels at natural size. Keep text
readable at the final embedding size; reflow or simplify the diagram before
shrinking it. Use shape and line conventions as well as colour to convey meaning.

## Lay out boxes, then routes

1. Set the intended canvas and reading direction. Place the main nodes using
   positioning relative to their borders or named row/column coordinates.
2. Reserve whitespace for notes, labels, arrowheads, and routing corridors.
   Start with 12–20mm horizontal gaps and 20–26mm between class rows; adjust to
   actual rendered content. Long boxes need larger gaps or a different arrangement.
3. Set text widths and deliberate line breaks. Keep identifiers intact; break a
   long field or signature at meaningful boundaries. For rectangle-split classes,
   use the `two` and `three` compartments, not `second` and `third`.
4. Connect explicit border anchors through clear lanes and named waypoints.
   Place labels on a chosen straight segment and multiplicities beside the
   correct endpoints. Keep routes clear of unrelated boxes and annotations.

Relative positioning and `-|`/`|-` bends do not provide automatic collision
avoidance. Read [UML and layout details](references/uml-and-layout.md) for arrow
semantics, components, sequences, grouping, and crowded layouts.

## Compile, inspect, revise

Use the available LaTeX compiler and preview, or the reference's command-line
workflow. Check errors, missing glyphs, and overfull boxes, then render the PDF.
Inspect the entire diagram at its intended reading size and enlarge dense areas.

Check node and note separation; complete compartment text; intact identifiers;
label collisions; arrowheads and multiplicity placement; paths through unrelated
boxes, including paths hidden behind fills; and page margins or clipping.
Correct defects in the source, then compile and inspect the latest render again.
Compilation success alone is not a layout check.

Deliver only after this visual check finds no unintended overlaps. Report the
checks actually performed. If compilation or visual inspection is unavailable,
preserve the source and provide verification instructions; label the layout
unverified and do not claim it is overlap-free.
