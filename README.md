# Dotfiles

Personal configuration and shared global agent instructions, deployed with
[chezmoi](https://www.chezmoi.io/).

Development and documentation plugins live in the separate public
[vibe-coding repository](https://github.com/expiracy/vibe-coding). Install and
update those plugins through its marketplace; this repository keeps the global
`AGENTS.md` defaults and their host-specific links.

## Layout

```text
.chezmoi.toml.tmpl           # Remembers this machine's checkout location
.chezmoiignore              # Excludes this README from deployment
.chezmoiremove              # Cleans up retired loose skill installations
dot_agents/AGENTS.md         # Shared global instructions
dot_codex/symlink_AGENTS.md.tmpl
dot_claude/symlink_CLAUDE.md.tmpl
```

Chezmoi copies `dot_agents/AGENTS.md` to `~/.agents/AGENTS.md` and creates:

| Global discovery path | Link target |
|-----------------------|-------------|
| `~/.codex/AGENTS.md` | `~/.agents/AGENTS.md` |
| `~/.claude/CLAUDE.md` | `~/.agents/AGENTS.md` |

These provide user-global defaults across projects. Project instructions and
explicit task requirements still apply. Prose and diagram-specific guidance is
packaged in `doc-tools` in the vibe-coding repository.

## Set up a new computer

Install Git and [chezmoi](https://www.chezmoi.io/install/). On macOS with Homebrew
already installed, use `brew install chezmoi`. Then run:

```sh
chezmoi init --apply expiracy/dotfiles
chezmoi verify
```

For an existing checkout:

```sh
chezmoi init --source /path/to/dotfiles
chezmoi diff
chezmoi apply
chezmoi verify
```

Install agent plugins separately using the
[vibe-coding setup instructions](https://github.com/expiracy/vibe-coding#install).
If migrating from an older dotfiles setup that installed loose skills, install
the replacement plugins before applying chezmoi: `.chezmoiremove` removes the
retired loose copies. Unrelated skills and Claude's `synced/` directory are
preserved.

Codex settings in `~/.codex/config.toml` and each client's plugin registry remain
local; this repository does not replace them.

## Make changes and update another computer

Edit shared defaults in `dot_agents/AGENTS.md`, then review and apply with
`chezmoi diff`, `chezmoi apply` and `chezmoi verify`. Each agent controls when it
reloads its instructions.

After committing and pushing, update another computer with:

```sh
chezmoi update
chezmoi verify
```

The plugin and skill sources have moved to vibe-coding. Their releases and
installation updates are independent of chezmoi.
