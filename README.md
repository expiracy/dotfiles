# Agent configuration

A portable collection of personal agent instructions and reusable skills.

Edit [AGENTS.md](AGENTS.md) to define shared defaults. Edit the packages under
[skills/](skills/) to define task-specific guidance. Each skill has a `SKILL.md`
entrypoint and only the supporting files it needs.

- [C++ Style](skills/cpp-style/SKILL.md): C++ Core Guidelines, pointer and lifetime rules, and 48 Clean Code references.
- [Canon TDD](skills/canon-tdd/SKILL.md): scenario-driven test-first development.
- [Writing Style](skills/writing-style/SKILL.md): clear, direct prose that preserves meaning.
- [Document Writing](skills/doc-writing/SKILL.md): high-level explanations with a clear narrative and the detail the reader needs.
- [TikZ Diagrams](skills/tikz-diagrams/SKILL.md): consistent UML-style diagrams with deliberate spacing, clear connectors, and render-based layout checks.

## Use the configuration

Supply `AGENTS.md` through the assistant's global-instruction mechanism, or load
its contents as instructions. Hosts differ in the filenames and settings they
recognise; keeping this file in a repository does not automatically activate it
in every application.

For hosts that support skill directories, copy the complete selected skill
folders from `skills/` into the host's configured global skill directory, or link
those folders when the host supports symbolic links. Otherwise
load the relevant `SKILL.md` as context. Keep supporting files available so relative
links resolve. No model-provider API or configuration format is required by the
instruction content.

Treat this repository as the source of truth. Linked installations read changes
from this checkout; keep it at a stable path or update links after moving it.
For copied installations, refresh the copies after editing. Preserve and reconcile
existing global instructions rather than silently replacing unrelated preferences.

Execution guidance depends on available tools. Without them, run the supplied
commands yourself and provide the actual output. These instructions do not grant
access to files, a compiler, a renderer, or a test runner.
