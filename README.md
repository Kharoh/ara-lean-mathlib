# ara-lean-mathlib

Template repo for research projects that combine **ARA**, **Lean 4 + Mathlib**, and **Python (uv)**.

- **ARA** — [Agent-Native Research Artifact](https://arxiv.org/abs/2604.24658), a machine-executable research-artifact protocol. Three Claude Code skills are bundled in [`.claude/skills/`](.claude/skills/) and auto-loaded by Claude Code:
  - `ara-compiler` — turn a paper, repo, or raw notes into a structured ARA artifact
  - `ara-research-manager` — at session end, record decisions / experiments / dead-ends / pivots into `ara/`
  - `ara-rigor-reviewer` — Seal Level 2 epistemic review across six rigor dimensions
- **Lean 4 + Mathlib** in [`lean/`](lean/), package `theory` (rename to your namespace), pinned to `v4.29.1`.
- **Python** managed by `uv`: numpy, scipy, matplotlib, torch, jupyter.

The `ara/` directory is **not** pre-created — `ara-compiler` or `ara-research-manager` bootstraps it on first run.

## Layout

```
.
├── .claude/skills/{compiler,research-manager,rigor-reviewer}/
├── lean/                # Lean+Mathlib project (Theory namespace placeholder)
├── notebooks/           # Jupyter
├── pyproject.toml       # uv project (cft → rename for your project)
├── uv.lock
└── CLAUDE.md            # repo-specific Claude Code instructions
```

## Prerequisites

- [uv](https://docs.astral.sh/uv/) — Python toolchain
- [elan](https://github.com/leanprover/elan) — Lean toolchain manager (`lake`, `lean`)
- [Claude Code](https://claude.com/claude-code) — to use the ARA skills

On Windows, `lake new <name> math` rejects reserved names (`lean`, `lake`, …) — that's why the Lean project here lives at `lean/` (directory) but with package name `theory` (namespace).

## Setup

```bash
git clone https://github.com/Kharoh/ara-lean-mathlib.git my-project
cd my-project

# Python
uv sync

# Lean (first time: ~5-10 min for Mathlib cache)
cd lean
lake exe cache get
lake build
cd ..

# Customize: rename Theory → YourNamespace in
#   lean/Theory.lean, lean/Theory/Basic.lean,
#   lean/lakefile.toml ([[lean_lib]].name, defaultTargets)
# and rename `cft` → your-project in pyproject.toml

claude   # start working
```

## References

- [The Last Human-Written Paper: Agent-Native Research Artifacts](https://arxiv.org/abs/2604.24658) (arXiv 2604.24658)
- [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs) — source of the bundled ARA skills
