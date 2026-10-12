# quadbio Claude Code plugins

A [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugins/install) for quadbio's plugins.

| Plugin | What it does |
| --- | --- |
| [analysis-workflow](https://github.com/quadbio/analysis-workflow) | Conventions, guard hooks and a small package for analysis repos where humans (notebooks) and coding agents (scripts) work side by side. |
| [cell-type-annotation](https://github.com/quadbio/cell-type-annotation) | Evidence-driven cell-type annotation of pre-clustered single-cell and spatial data. |
| [euler-hpc](https://github.com/quadbio/euler-hpc) | Run coding agents efficiently on ETH Zurich's Euler cluster: node, allocation, storage rules and your own setup at session start; a skill for Slurm jobs, software and data; jobs listed by the session that submitted them. |
| [sci-figures](https://github.com/quadbio/sci-figures) | Nature-style research figures and their legends, with a small matplotlib package for style, layout and export. |

Install once per machine; each plugin's README says how to use it.

```bash
claude plugin marketplace add quadbio/claude-plugins
claude plugin install <plugin>@quadbio
```

Each plugin lives in its own repository; this one only lists them. A plugin's README opens with what it does
and its parts, then `Use`, `Install` (pointing here), `Develop`, `Release`. To release a pinned plugin, bump its
`ref` here.
