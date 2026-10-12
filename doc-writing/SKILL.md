---
name: doc-writing
description: Use when drafting, revising, or reviewing explanatory documents, overviews, proposals, reports, or design narratives that need a high-level account and a clear story. Detailed specifications, reference manuals, and procedures should retain their required detail.
---

# Document Writing

Explain the big picture through a clear narrative. Help the reader understand
what matters, why it matters, how the main ideas fit together, and what follows.

Build on [writing-style](../writing-style/SKILL.md): lead with the point, use plain
words and precise verbs, connect ideas, and preserve meaning. Its essential
principles are included here so this skill can also be used on its own. Follow
the requested audience, voice, format, length, and spelling conventions.

## Build the narrative

Start from the reader's purpose and the document's main point. Shape the story
around the parts that matter:

1. **Orient the reader.** State the purpose, proposed change, or central conclusion.
2. **Establish the need.** Explain the current situation, the problem, and its consequence.
3. **Explain the approach.** Describe the essential concepts and how they connect. Show how the approach addresses the need.
4. **Explain the implications.** Connect the approach to outcomes, evidence, tradeoffs, and remaining questions.
5. **Make the next step clear.** State the decision, action, or takeaway the reader needs, when one is called for.

Use this as a narrative arc, not a mandatory set of headings. Write connected
paragraphs so each idea prepares the reader for the next. Organize around the
reader's understanding rather than the order in which the work happened.

## Select the right detail

Include a detail in the main explanation when the reader needs it to understand
the approach, assess a claim or limitation, or make a decision. Otherwise omit
it from the narrative. Link supporting material or use an appendix when that
detail is useful elsewhere; do not create one automatically.

Explain mechanisms through their purpose and effect. For a high-level audience,
describe the conceptual flow and meaningful relationships; leave database
schemas, function names, API paths, configuration flags, and step-by-step
implementation mechanics to supporting material unless they serve that audience's
purpose. Define necessary technical terms in plain language.

Keep material risks, failure cases, conditions, numbers, dates, responsibilities,
and uncertainty that affect understanding or action. Distinguish a proposal from
an implemented feature and expected benefits from observed results. Preserve
attribution, quotations, and evidence; flag material ambiguity instead of
inventing facts or guarantees.

If the user requests a detailed specification, reference, or procedure, preserve
the detail needed for that task. A short overview can orient the reader without
replacing the required content.

## Keep the prose clear

Give each paragraph one main idea. Use concrete nouns and active voice when the
actor is known. Remove filler, repetition, inflated claims, and forced enthusiasm.
Use headings to guide a longer document, lists for parallel items or steps, and
tables for comparisons. Keep the main explanation in connected prose.

## Example

Implementation detail: "The offline-sync proposal stores edits in a SQLite queue
and uses a retry loop to send them after reconnection."

High-level narrative: "The proposal would let people keep editing while offline.
The app would keep their changes on the device and send them when a connection
returns."

Before delivering, check that a reader can explain the purpose, the approach,
the important implications, and any next step after one read. Remove details
that interrupt that understanding; retain the qualifications that keep it honest.
