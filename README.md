# Dotfiles

Shared agent instructions managed with [chezmoi](https://www.chezmoi.io/) and
three independently installable, skills-only plugins.

| Plugin | Included skills | Purpose |
|--------|----------------|---------|
| [cpp-dev](dot_agents/plugins/cpp-dev/) | [cpp-style](dot_agents/plugins/cpp-dev/skills/cpp-style/SKILL.md) | Clean Code, C++ Core Guidelines, pointer contracts and lifetimes |
| [dev-workflow](dot_agents/plugins/dev-workflow/) | [canon-tdd](dot_agents/plugins/dev-workflow/skills/canon-tdd/SKILL.md) | Scenario-driven Canon TDD |
| [doc-tools](dot_agents/plugins/doc-tools/) | [text-writing](dot_agents/plugins/doc-tools/skills/text-writing/SKILL.md), [uml-diagrams](dot_agents/plugins/doc-tools/skills/uml-diagrams/SKILL.md) | Clear prose, high-level explanatory narratives, and consistent UML diagrams |

Skill instructions remain provider-neutral. Each package has a portable
[Agent Plugins manifest](https://developers.openai.com/plugins/build/plugins),
Codex and Claude compatibility manifests, and its own `skills/` directory.
Supporting references, templates and licences stay inside the relevant package.

The old loose `writing-style` and `doc-writing` skills remain retired. Prose
guidance now lives in the `text-writing` skill inside the `doc-tools` plugin.
Vault's project-specific writing rules remain in its
[writing guide](https://github.com/expiracy/vault/blob/master/projects/vault/guides/markdown-style.md).

## Repository layout

```text
dot_agents/
  AGENTS.md
  plugins/
    cpp-dev/
    dev-workflow/
    doc-tools/
      plugin.json                 # Portable package identity
      .codex-plugin/plugin.json   # Codex compatibility
      .claude-plugin/plugin.json  # Claude compatibility
      skills/
        text-writing/SKILL.md     # Prose and explanatory narrative guidance
        uml-diagrams/            # Instructions, references and assets
.agents/plugins/marketplace.json # Codex marketplace catalog
.claude-plugin/marketplace.json   # Claude marketplace catalog
dot_codex/symlink_AGENTS.md.tmpl
dot_claude/symlink_CLAUDE.md.tmpl
```

All shared content lives under `dot_agents/`. The two catalogs list the same
three packages as `expiracy-dotfiles`. Package paths resolve from the repository
root. Plugins contain their resources directly, so an installed package does not
depend on files outside its directory.

## Set up a new computer

Install Git, chezmoi and the agent clients you use. On macOS with Homebrew already
installed, `brew install chezmoi` installs chezmoi. Other platforms can follow its
[installation guide](https://www.chezmoi.io/install/).

Clone the dotfiles and generate this machine's chezmoi configuration:

```sh
chezmoi init expiracy/dotfiles
```

Install whichever plugins you want at user scope. Use either or both clients.

### Codex

```sh
codex plugin marketplace add expiracy/dotfiles
codex plugin add cpp-dev@expiracy-dotfiles
codex plugin add dev-workflow@expiracy-dotfiles
codex plugin add doc-tools@expiracy-dotfiles
```

### Claude Code

```sh
claude plugin marketplace add expiracy/dotfiles
claude plugin install --scope user cpp-dev@expiracy-dotfiles
claude plugin install --scope user dev-workflow@expiracy-dotfiles
claude plugin install --scope user doc-tools@expiracy-dotfiles
```

After installing plugins, apply and verify the shared instructions:

```sh
chezmoi diff
chezmoi apply
chezmoi verify
```

Restart the clients to load the installed plugins. Plugin names namespace their
skills; for example, Claude exposes `/cpp-dev:cpp-style`.

For an existing checkout, start with `chezmoi init --source /path/to/dotfiles`.
For local plugin development, pass that checkout path to each client's
`plugin marketplace add` command instead of the GitHub repository name.

## Shared global instructions

Chezmoi copies `dot_agents/AGENTS.md` to `~/.agents/AGENTS.md` and creates:

| Global discovery path | Link target |
|-----------------------|-------------|
| `~/.codex/AGENTS.md` | `~/.agents/AGENTS.md` |
| `~/.claude/CLAUDE.md` | `~/.agents/AGENTS.md` |

These remain user-global defaults across projects. Codex discovers instructions
at its [documented global path](https://learn.chatgpt.com/docs/agent-configuration/agents-md);
`~/.agents/AGENTS.md` is the shared file behind the host links.

Global instructions keep the development defaults and skill-selection guidance.
Prose, narrative, and diagram-specific rules live in the `doc-tools` plugin's
skills, so they load when the task calls for them.

The plugin managers install and enable plugins globally for your user. Chezmoi
excludes the plugin source tree from home-directory copying and removes the old
loose skill installations through `.chezmoiremove`, avoiding duplicate discovery.
Install plugins before applying this migration on an existing computer.
Unrelated skills and Claude's `synced/` directory are preserved.

Codex settings in `~/.codex/config.toml` remain local. The plugin manager adds its
own marketplace and enabled-plugin entries there; this repository does not
replace the settings file. Claude's plugin manager likewise owns its local
registry and enabled-plugin settings.

## Make changes and update other computers

Edit shared defaults in `dot_agents/AGENTS.md`. Edit a skill within its plugin's
`skills/` directory. When releasing a plugin change, update its version in all
three manifests together, then commit and push.

On another computer, pull dotfile changes without applying the migration yet:

```sh
chezmoi update --apply=false
```

Refresh the marketplace and update the changed plugins using the client's plugin
manager. Codex can refresh with `codex plugin marketplace upgrade expiracy-dotfiles`
and install the desired version with `codex plugin add <name>@expiracy-dotfiles`.
Claude can refresh with `claude plugin marketplace update expiracy-dotfiles`
and update a package with `claude plugin update <name>@expiracy-dotfiles`.
Then run `chezmoi diff`, `chezmoi apply` and `chezmoi verify`, and restart the clients.

When migrating from `doc-diagrams` or `doc-writing`, install
`doc-tools@expiracy-dotfiles` first, then remove the old plugin with
`codex plugin remove <old-name>@expiracy-dotfiles` or
`claude plugin uninstall --scope user --keep-data <old-name>@expiracy-dotfiles`.
Use the command for each client you configured. The new name covers writing,
editing, reviewing, and diagrams; both skills and their resources are preserved.

Plugin packaging does not install a C++ or LaTeX toolchain. Each host controls
plugin loading and available tools; these instructions do not grant tool access.
