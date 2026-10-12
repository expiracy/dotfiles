# Portable skills

These skills contain provider-neutral instructions in plain Markdown. The YAML
frontmatter identifies each skill; the body contains its instructions. No
provider-specific tools, APIs, or configuration are required.

- [C++ Style](cpp-style/SKILL.md): C++ Core Guidelines, pointer and lifetime rules, and 48 Clean Code references.
- [Canon TDD](canon-tdd/SKILL.md): scenario-driven test-first development.
- [Writing Style](writing-style/SKILL.md): clear, direct prose that preserves meaning.
- [Document Writing](doc-writing/SKILL.md): high-level explanations with a clear narrative and only the detail the reader needs.

Load the relevant `SKILL.md` as instructions in your chosen assistant, or paste
its body into the conversation. For C++, also supply the linked references
needed for the task. In systems that support skill directories, keep the
complete folder together so relative links resolve.

Execution guidance depends on available tools. Without them, run the supplied
commands yourself and provide the actual output. Loading these instructions
does not by itself give a model access to files, a compiler, or a test runner.
