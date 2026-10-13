# Dotfiles

Agent instructions and the UML diagram skill for Vault, deployed with
[chezmoi](https://www.chezmoi.io/).

Edit [AGENTS.md](AGENTS.md) for shared defaults and the packages under
[skills/](skills/) for task-specific guidance. The instruction content remains
provider-neutral; the files under [home/](home/) adapt it to local agent paths.

- [UML Diagrams](skills/uml-diagrams/SKILL.md): seven common UML views, scenario-based selection and one canonical theme, with editable TikZ sources and rendered Markdown previews.

Writing and document-structure rules live in Vault's [writing guide](https://github.com/expiracy/vault/blob/master/projects/vault/guides/markdown-style.md), required by its `AGENTS.md`.

## What chezmoi manages

| Target | Shared source |
|--------|---------------|
| `~/.claude/CLAUDE.md` | `AGENTS.md` |
| `~/.codex/AGENTS.md` | `AGENTS.md` |
| `~/.claude/skills/<name>` | `skills/<name>` |
| `~/.agents/skills/<name>` | `skills/<name>` |

Each target is a symbolic link. Templates derive the target from chezmoi's
working-tree path, so links work from an existing checkout or a fresh clone.

The skill directories are regular containers with a link for each managed skill.
Existing entries, including Claude's `synced/` folder, are preserved. The
`.chezmoiroot` file selects `home/` as the deployment source, keeping the canonical
instructions, skill packages, and this README out of home-directory deployment.
See [source-root configuration](https://www.chezmoi.io/reference/special-files/chezmoiroot/)
and [symlink source attributes](https://www.chezmoi.io/reference/source-state-attributes/).

## Set up

On a new machine with chezmoi installed:

```sh
chezmoi init --apply expiracy/dotfiles
```

To use an existing checkout:

```sh
chezmoi init --source /path/to/dotfiles
chezmoi diff
chezmoi apply
chezmoi verify
```

The configuration template remembers the checkout location, so later commands
can use `chezmoi diff`, `chezmoi apply`, and `chezmoi verify` directly.

## Make changes

Edit the canonical `AGENTS.md` or skill files in this repository. Existing links
read those files directly; each agent controls when it reloads instructions.
When adding a skill, add its one-line symlink templates under both
`home/dot_agents/skills/` and `home/dot_claude/skills/`, then review `chezmoi diff`
and apply the new links.

If the checkout moves, initialise chezmoi with the new source path and apply again
to update the links. Keep unrelated local instructions and skills outside this
managed set.

These Claude paths configure local Claude Code. Cowork and cloud sessions use
different skill-loading mechanisms and may skip local symlinked instructions.
See [Claude's memory rules](https://code.claude.com/docs/en/memory) and
[skill locations](https://code.claude.com/docs/en/skills).

For other hosts, supply the same instruction content through their supported
global-instruction and skill mechanisms. Automatic discovery and execution
capabilities depend on the host; these files do not grant tool access.
