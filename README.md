# SciVisAgentSkills

This repository provides **agent skills** for four scientific visualization tools: **ParaView**, **napari**, **VMD** (MD Analysis), and **TTK** (Topology Analysis). Skills are Markdown files that embed tool-specific expertise — environment setup, headless rendering, API patterns, and error handling — directly into AI coding agents. The skills can be used to evaluate agents with and without skill augmentation on [SciVisAgentBench](https://scivisagentbench.github.io/).

---

## Available Skills

| Skill file | Tool |
|---|---|
| `paraview-viz/SKILL.md` | ParaView (large-scale scientific visualization) |
| `napari-viz.md` | Napari (biology image visualization) |
| `vmd-mdanalysis-viz.md` | VMD + MD Analysis (molecular dynamics) |
| `ttk-viz.md` | TTK (topological data analysis) |

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

Skills install to `~/.claude/commands/` and become available as slash commands (e.g. `/napari-viz`).

```bash
cp napari-viz.md ~/.claude/commands/napari-viz.md
cp vmd-mdanalysis-viz.md ~/.claude/commands/vmd-mdanalysis-viz.md
cp ttk-viz.md ~/.claude/commands/ttk-viz.md
cp paraview-viz/SKILL.md ~/.claude/commands/paraview-viz.md
```

To auto-trigger skills, add to the project `CLAUDE.md`:

```
For any napari visualization task, automatically invoke /napari-viz with the task description.
For any VMD or molecular dynamics task, automatically invoke /vmd-mdanalysis-viz with the task description.
For any TTK or topological data analysis task, automatically invoke /ttk-viz with the task description.
For any ParaView visualization task, automatically invoke /paraview-viz with the task description.
```

### Codex

Place skill files where the agent can read them, then reference them in `AGENTS.md`:

```bash
cp napari-viz.md <project>/skills/napari-viz.md
cp vmd-mdanalysis-viz.md <project>/skills/vmd-mdanalysis-viz.md
cp ttk-viz.md <project>/skills/ttk-viz.md
cp paraview-viz/SKILL.md <project>/skills/paraview-viz.md
```

Add to `AGENTS.md`:

```
For any napari visualization task, follow the instructions in skills/napari-viz.md.
For any VMD or molecular dynamics task, follow the instructions in skills/vmd-mdanalysis-viz.md.
For any TTK task, follow the instructions in skills/ttk-viz.md.
For any ParaView task, follow the instructions in skills/paraview-viz.md.
```
