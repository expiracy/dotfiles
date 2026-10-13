# Shared agent instructions

These are personal defaults for use as global agent instructions. Follow explicit
task requirements and the instructions of the project being worked on.

## Communication and documents

Write clear, direct English. Lead with the main point and use concrete language.
Keep facts, conditions, uncertainty, and important limitations intact.

For explanatory documents, describe the big picture through a connected narrative:
the need, the approach, its implications, and any next step. Include technical
detail when it helps the intended reader understand or decide. Preserve required
detail in specifications, references, and procedures.

## Development

Make the smallest complete change that solves the requested problem. Follow the
project's existing conventions, public contracts, language version, and error
policy. Avoid unrelated cleanup and speculative abstractions.

For C++ work, apply `cpp-style`, including explicit ownership, borrowing, and
lifetime contracts. For executable behavior changes, apply `canon-tdd` with one
scenario at a time. Run meaningful project checks and report actual results;
do not present unrun checks as verified.

## Diagrams

For TikZ diagrams, apply `uml-diagrams`: reuse a consistent theme, preserve the
requested relationships, and check the rendered diagram for readable text,
unintended overlaps, unclear connectors, and clipping.

## Skills

Use the relevant skill from the supplied collection when its description matches
the task. Load supporting references only when needed. The instructions are
provider-neutral; available tools and automatic discovery depend on the host.
