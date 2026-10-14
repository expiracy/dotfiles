# Dotfiles

Shared agent instructions and reusable skills, deployed with
[chezmoi](https://www.chezmoi.io/).

Edit [dot_agents/AGENTS.md](dot_agents/AGENTS.md) for shared defaults and the
packages under [dot_agents/skills/](dot_agents/skills/) for task-specific guidance.
The instruction content remains provider-neutral. Chezmoi maps the `dot_`
directories directly to dot directories in your home.

- [C++ Style](dot_agents/skills/cpp-style/SKILL.md): C++ Core Guidelines, pointer and lifetime rules, and 48 Clean Code references.
- [Canon TDD](dot_agents/skills/canon-tdd/SKILL.md): scenario-driven test-first development.
- [Writing Style](dot_agents/skills/writing-style/SKILL.md): clear, direct prose that preserves meaning.
- [Document Writing](dot_agents/skills/doc-writing/SKILL.md): high-level explanations with a clear narrative and the detail the reader needs.
- [UML Diagrams](dot_agents/skills/uml-diagrams/SKILL.md): seven common UML views, scenario-based selection and one canonical theme, with editable TikZ sources and rendered Markdown previews.

Vault also has project-specific documentation rules in its [writing guide](https://github.com/expiracy/vault/blob/master/projects/vault/guides/markdown-style.md), required by its `AGENTS.md`.

## What chezmoi manages

| Global target | Repository source or link target |
|---------------|----------------------------------|
| `~/.agents/AGENTS.md` | File copied from `dot_agents/AGENTS.md` |
| `~/.agents/skills/<name>/` | Package copied from `dot_agents/skills/<name>/` |
| `~/.codex/AGENTS.md` | Link to `~/.agents/AGENTS.md` |
| `~/.claude/CLAUDE.md` | Link to `~/.agents/AGENTS.md` |
| `~/.claude/skills/<name>` | Link to `~/.agents/skills/<name>` |

All managed instructions and skills are installed at user-global locations and
apply across projects. Codex discovers global instructions at
[`~/.codex/AGENTS.md`](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
and global skills under
[`~/.agents/skills/`](https://learn.chatgpt.com/docs/build-skills).
Each skill has its own folder containing `SKILL.md` and any supporting files.

All shared content lives under `dot_agents/`. Codex and Claude reuse the installed
instructions through links at their required discovery paths; `~/.agents/AGENTS.md`
alone is not a Codex instruction-discovery location. The skill directories preserve
unmanaged entries, including Claude's `synced/` folder. `.chezmoiignore` excludes
this README from deployment.

Codex's settings file is `~/.codex/config.toml`; it is currently managed locally,
outside this repository.

## Repository layout

```text
.chezmoi.toml.tmpl           # Remembers this machine's checkout location
.chezmoiignore              # Excludes repository-only files
dot_agents/
  AGENTS.md                 # Shared global instructions
  skills/
    canon-tdd/
    cpp-style/
    doc-writing/
    uml-diagrams/
    writing-style/          # Each package installs under ~/.agents/skills/
dot_codex/
  symlink_AGENTS.md.tmpl     # Links to ~/.agents/AGENTS.md
dot_claude/
  symlink_CLAUDE.md.tmpl     # Links to ~/.agents/AGENTS.md
  skills/
    symlink_<name>.tmpl      # One link per installed global skill
```

Add future home-directory configuration directly at the repository root, using chezmoi's
[source attributes](https://www.chezmoi.io/reference/source-state-attributes/)
such as `dot_` for a leading dot and `symlink_` for a symbolic link.

## Set up a new computer

Install Git and [chezmoi](https://www.chezmoi.io/install/) and ensure both are on
your command path. On macOS with Homebrew already installed:

```sh
brew install chezmoi
```

Then clone and apply the public repository:

```sh
chezmoi init --apply expiracy/dotfiles
chezmoi verify
```

No GitHub login is needed to clone the public repository. By default, chezmoi
keeps the checkout at `~/.local/share/chezmoi` for future updates. The installed
shared instructions and skills are regular files; Codex's and Claude's instruction
links point to those installed files, so they do not depend on the checkout location.
Install the agent applications and any diagram tools separately.

If the computer already has instructions at one of the managed paths, run
`chezmoi init expiracy/dotfiles`, inspect `chezmoi diff`, then run `chezmoi apply`
and `chezmoi verify`.

To use an existing checkout:

```sh
chezmoi init --source /path/to/dotfiles
chezmoi diff
chezmoi apply
chezmoi verify
```

The configuration template remembers the checkout location, so later commands
can use `chezmoi diff`, `chezmoi apply`, and `chezmoi verify` directly.

## Update another computer

After committing and pushing changes to this repository, pull and apply them on
each other computer:

```sh
chezmoi update
chezmoi verify
```

## Make changes

Edit `dot_agents/AGENTS.md` or the skill files under `dot_agents/skills/`, then run
`chezmoi diff`, `chezmoi apply`, and `chezmoi verify`. Each agent controls when it
reloads instructions.

To add a global skill, create `dot_agents/skills/<name>/SKILL.md` and any supporting
files. To expose it to Claude too, add `dot_claude/skills/symlink_<name>.tmpl` with:

```text
{{ joinPath .chezmoi.destDir ".agents" "skills" "<name>" }}
```

If the checkout moves, initialise chezmoi with the new source path. Keep unrelated
local instructions and skills outside this managed set.

These Claude paths configure local Claude Code. Cowork and cloud sessions use
different skill-loading mechanisms and may skip local symlinked instructions.
See [Claude's memory rules](https://code.claude.com/docs/en/memory) and
[skill locations](https://code.claude.com/docs/en/skills).

For other hosts, supply the same instruction content through their supported
global-instruction and skill mechanisms. Automatic discovery and execution
capabilities depend on the host; these files do not grant tool access.
