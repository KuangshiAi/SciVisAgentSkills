# SciVisAgentSkills

This repository provides **agent skills** for four scientific visualization tools: **ParaView**, **napari**, **VMD** (MD Analysis), and **TTK** (Topology Analysis). Each skill is a self-contained package that embeds tool-specific expertise — environment setup, headless rendering, API patterns, and error handling — directly into AI coding agents. Every skill follows the same [Claude Agent Skill](https://docs.anthropic.com/en/docs/claude-code/skills) layout: a `SKILL.md` file with YAML frontmatter (`name` + a trigger `description`) followed by the procedural body, with optional `references/` files for larger API surfaces (used by the ParaView skill). The skills can be used to evaluate agents with and without skill augmentation on [SciVisAgentBench](https://scivisagentbench.github.io/).

---

## Available Skills

| Skill package | Tool |
|---|---|
| `paraview-viz/SKILL.md` | ParaView (large-scale scientific visualization) |
| `napari-viz/SKILL.md` | napari (bioimage / microscopy visualization) |
| `vmd-mdanalysis-viz/SKILL.md` | VMD + MDAnalysis + GROMACS (molecular dynamics) |
| `ttk-viz/SKILL.md` | TTK (topological data analysis) |

---

## Prerequisites

1. **Claude Code CLI** or **Codex CLI** installed and authenticated
   ```bash
   claude --version
   codex --version
   ```

2. **Python environment** with all scientific visualization packages
   ```bash
   conda create -n scivis_skills python=3.10
   conda activate scivis_skills
   conda install -c conda-forge paraview numpy scipy matplotlib
   pip install napari psutil
   conda install conda-forge::vmd-python
   conda install conda-forge::topologytoolkit
   ```

---

## Installation

### Claude Code

Each skill is a directory; install by linking (or copying) the package into the Claude Code skills directory. Claude Code then loads each skill via progressive disclosure and auto-invokes it based on the `description` in the YAML frontmatter.

```bash
# Link each skill package into the Claude Code skills directory
ln -s "$(pwd)/paraview-viz"        ~/.claude/skills/paraview-viz
ln -s "$(pwd)/napari-viz"          ~/.claude/skills/napari-viz
ln -s "$(pwd)/vmd-mdanalysis-viz"  ~/.claude/skills/vmd-mdanalysis-viz
ln -s "$(pwd)/ttk-viz"             ~/.claude/skills/ttk-viz
```

### Codex

Codex has no native skill loader, so place the `SKILL.md` files where the agent can read them and reference them from `AGENTS.md`:

```bash
mkdir -p <project>/skills
cp paraview-viz/SKILL.md       <project>/skills/paraview-viz.md
cp napari-viz/SKILL.md         <project>/skills/napari-viz.md
cp vmd-mdanalysis-viz/SKILL.md <project>/skills/vmd-mdanalysis-viz.md
cp ttk-viz/SKILL.md            <project>/skills/ttk-viz.md
```

Add to `AGENTS.md`:

```
For any ParaView visualization task, follow the instructions in skills/paraview-viz.md.
For any napari visualization task, follow the instructions in skills/napari-viz.md.
For any VMD or molecular dynamics task, follow the instructions in skills/vmd-mdanalysis-viz.md.
For any TTK or topological data analysis task, follow the instructions in skills/ttk-viz.md.
```

---

## Acknowledgements

The ParaView skill in this repository builds on and was inspired by the following projects:

- [Paraview-Skills](https://github.com/TouKaienn/Paraview-Skills) — a collection of ParaView agent skills that informed the structure and content of the ParaView skill here.
- [paraview_mcp](https://github.com/llnl/paraview_mcp) — an MCP server for ParaView developed at LLNL, which provided valuable reference for ParaView automation patterns.
