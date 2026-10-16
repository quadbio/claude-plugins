# quadbio Claude Code plugins

A [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugins/install) for quadbio's plugins.

| Plugin | What it does |
| --- | --- |
| [analysis-workflow](https://github.com/quadbio/analysis-workflow) | Conventions, guard hooks and a small package for analysis repos where humans (notebooks) and coding agents (scripts) work side by side. |
| [cell-type-annotation](https://github.com/quadbio/cell-type-annotation) | Evidence-driven cell-type annotation of pre-clustered single-cell and spatial data. |
| [euler-hpc](https://github.com/quadbio/euler-hpc) | Run coding agents on ETH Zurich's Euler cluster: node, allocation, storage rules and your setup at session start; a skill for Slurm jobs, software and data; jobs listed by session. |
| [research-agent-skills](https://github.com/quadbio/research-agent-skills) | How agents write research code, run and hand over research tasks, and set up a project so Claude Code and Codex read the same instructions. |
| [sci-figures](https://github.com/quadbio/sci-figures) | Nature-style research figures and their legends, with a small matplotlib package for style, layout and export. |

Install once per machine; each plugin's README says how to use it.

```bash
claude plugin marketplace add quadbio/claude-plugins
claude plugin install <plugin>@quadbio
```

Then turn on updates, which are off by default for marketplaces outside Anthropic's: in a session, `/plugin` →
Marketplaces → quadbio → Enable auto-update ([docs](https://code.claude.com/docs/en/plugins/install#keep-plugins-updated)).

Auto-update runs when Claude Code starts. To update by hand, refresh the marketplace, then the plugin; the new version
applies from the next session:

```bash
claude plugin marketplace update quadbio
claude plugin update <plugin>@quadbio
```

A plugin option's default applies only once the option is saved, and an update doesn't ask for the options it adds:
set them in `/plugin` → the plugin → Configure options.

## Conventions

Plugins here are built to work together. A new plugin, and every change to one, follows these rules; anything they
don't cover is the plugin's own choice.

**Overlap and dependencies.**
- Plugins may overlap or offer another way of working, such as an alternative to `euler-hpc` or a plugin that
  combines analysis setup with another aim. Its README names the plugins it overlaps with and how it differs, so
  users can choose.
- A plugin that builds on another defers to it instead of restating its rules, as `cell-type-annotation` does for
  `analysis-workflow`. If it needs the other to work, it lists it under `dependencies` in its `plugin.json`, so
  installing it installs the other, and its Develop section says to load both.

**Little always-on context.** Rules go in skills, which load on demand. Hooks are for what must hold in every
session, and print little at session start: every installed plugin's output lands in every session.

**One project layout**, so plugins agree on it:
- a repo's agent instructions live in one `AGENTS.md`, which Codex reads, and a `CLAUDE.md` imports it
  (`@AGENTS.md`) for Claude Code, which skips `AGENTS.md` when a `CLAUDE.local.md` or a parent folder's `CLAUDE.md`
  exists;
- worktrees live in `.claude/worktrees/`, where `claude --worktree` creates them, and `.gitignore` lists that folder.

**Repository.** Each plugin lives in its own quadbio repository; this one only lists them.
- Its README opens with what it does and its parts, then `Use`, `Install` (pointing here), `Develop`, `Release`.
- `claude plugin validate .` passes.
- Values that differ between people or labs (paths, groups, hardware) are `userConfig` options, not hard-coded.
  Hooks and skills get only saved values, never the `default`, so each works when an option is missing.
- Repositories are public: no absolute paths, usernames, hostnames, private repository names or infrastructure
  details.

**Release.** Entries follow each plugin's `main`: a plugin releases by bumping `version` in its `plugin.json`.

**Adding a plugin:** open a pull request here that adds its entry to `.claude-plugin/marketplace.json` and its row
above.
