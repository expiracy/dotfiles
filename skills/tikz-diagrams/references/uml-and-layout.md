# UML notation and TikZ layout

Use the template's common `uml/` styles. Preserve the requested model and its
semantics while adapting the layout. These are practical defaults, not a complete
UML specification or a guarantee of automatic layout.

## Relationship direction and meaning

| Relationship | Template style | Meaning and direction |
|--------------|----------------|-----------------------|
| Association | `uml/association` | Solid line; add navigability only when specified. |
| Dependency | `uml/dependency` | Dashed line and open barb, from client to supplier. |
| Generalization | `uml/generalization` | Solid line and hollow triangle, from child to parent. |
| Interface realization | `uml/realization` | Dashed line and hollow triangle, from implementation to interface. |
| Shared aggregation | `uml/aggregation` | Hollow diamond at the whole end; use only when that relationship is intended. |
| Composition | `uml/composition` | Filled diamond at the whole end; composition expresses stronger whole/part semantics. |
| Annotation | `uml/note-link` | Dashed connector without an arrowhead; does not create a model relationship. |

The template's aggregation and composition styles put the diamond at the start
of the path: draw from the whole toward the part. Draw generalizations and
realizations toward the parent/interface. Arrow decoration does not reverse
the model's meaning automatically.

Put a multiplicity next to the endpoint whose instances it counts. For an order
with one or more lines, put `1..*` beside OrderLine; put `1` beside Order when each
line belongs to exactly one order. Do not infer composition from a pointer field,
or shared aggregation from use of a shared-pointer type.

Sources: [OMG UML 2.5.1](https://www.omg.org/spec/UML/2.5.1/PDF) and
[TikZ arrow configuration](https://tikz.dev/tikz-arrows).

## Classes and text

Use `rectangle split` with three parts for the name, attributes, and operations.
The part names are `text`, `two`, and `three`; the first is implicit in the
template. `rectangle split ignore empty parts=false` keeps empty compartments
visible. Vertical split nodes do not honour `minimum height` as a uniform-height
control; account for the actual text and padding in each compartment.

Use `text width` to enable wrapping; `minimum width` alone does not wrap text.
Set `align=left` on the attribute/operation parts. `rectangle split part align`
positions the part boxes and is not the same as the text alignment within them.
Keep class headings centred and emphasised consistently.

Do not let TeX hyphenate a type name into a different-looking identifier.
Widen related boxes together, break before a long type, or break a signature at
argument boundaries. Escape label characters such as underscores, percent signs,
ampersands, and hashes. Preserve symbols and requested visibility notation.

Sources: [Multipart shapes](https://tikz.dev/library-shapes) and
[node text and alignment](https://tikz.dev/tikz-shapes).

## Spacing, routes, labels, and groups

With the `positioning` library, `right=16mm of A` uses the relevant node borders.
Legacy `right of=A`, explicit centre coordinates, and `on grid` can give very
different spacing. Align row tops with common coordinates when node heights differ.
Choose the next row from the tallest relevant box, not an assumed fixed height.

`-|` goes horizontally then vertically; `|-` goes vertically then horizontally.
Neither searches for obstacles. Select departure/arrival anchors that match the
path direction and add explicit waypoints or offset lanes for congested routes.
Avoid shared segments that make distinct relationships hard to follow.

Place text on an explicitly chosen straight segment. A `pos=.5` label on a
single `-|` or `|-` operation sits at the bend. Split the route into segments
for predictable label positioning, and keep endpoint labels clear of arrowheads.
Small background fills can make labels readable; do not use them to conceal a
collision. Inspect the underlying route as well as the visible stroke.

For a group, create its members first, then an empty `fit` node with padding and
a separately positioned title. Fit includes the specified nodes' cardinal
anchors; separate notes, labels, and routes need inclusion or additional space.
Put group fills on a background layer and specify their drawing styles there.
Draw outer group fills before inner ones when nested.

Sources: [Positioning and labels](https://tikz.dev/tikz-shapes),
[path bends](https://tikz.dev/tikz-paths), [fit](https://tikz.dev/library-fit),
and [background layers](https://tikz.dev/library-backgrounds).

## Components and sequences

For components, use `uml/component` with a visible component stereotype or correct
UML notation; do not invent an icon that suggests a different kind of entity.
Use the same typography, colours, padding, and relationship conventions as the
class diagrams. An informal block diagram should be identified as such.

For sequences, align participant headers and use `uml/lifeline` for vertical
lifelines. Allocate increasing event rows and space for each message label.
Use `uml/call` for synchronous calls and `uml/async` for asynchronous calls.
The template convention is `uml/reply` for dashed, open-barb replies; label
messages and keep self-calls and activation bars clear of neighbouring lifelines.

Sequence time flows downward. Preserve requested call order and distinguish
simultaneous or asynchronous behaviour from a synchronous call. For formal UML,
use its actual notation for combined fragments and activation bars rather than
implying those meanings through arbitrary boxes or colours.

Sources: [OMG UML](https://www.omg.org/spec/UML/2.5.1/PDF) and
[reply-arrow clarification](https://issues.omg.org/issues/UMLR-317).

## Portable build and visual check

For a standalone asset, keep the template's explicit border. For a figure embedded
in a document, use that document's preamble and check the figure at its final
width. Cropping to the TikZ bounding box does not prove that it fits an A4 page.

An example local workflow, using available TeX and Poppler tools:

```sh
mkdir -p build
pdflatex -interaction=nonstopmode -halt-on-error -file-line-error -output-directory=build diagram.tex
pdftoppm -png -r 150 -singlefile build/diagram.pdf build/diagram
```

An existing editor/preview or a compatible LaTeX engine can provide the same
compile-and-inspect loop. Do not enable shell escape for the supplied template.
Keep build outputs separate from source. Re-render after source changes and
inspect the actual latest image; warnings alone cannot detect hyphenated names,
incorrect arrow semantics, or overlapping annotations.

Use the whole-page view to check composition and margins, then enlarged views
to check labels, compartments, and connectors. If the canvas is crowded, reorder
nodes, reroute edges, adjust common widths/gaps, or split views when permitted by
the request. Do not solve congestion by making text unreadably small.

Plain TikZ placement is explicit geometry. The separate graphdrawing system can
calculate layouts, but requires LuaTeX and a selected layout library and still
needs visual checking. Introduce it only when the task calls for that capability.

Sources: [Standalone manual](https://tug.ctan.org/macros/latex/contrib/standalone/standalone.pdf)
and [graphdrawing prerequisites](https://tikz.dev/gd-usage-tikz).
