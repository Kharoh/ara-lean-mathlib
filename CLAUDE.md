# Project conventions

## Layout

- `lean/` — Lean 4 + Mathlib `v4.29.1`. Package name `theory`, namespace `Theory` (placeholders — rename to your project's namespace before adding theory-specific content).
  - Main module: `lean/Theory.lean` → `import Theory.Basic`.
  - Submodules under `lean/Theory/`.
  - The directory is `lean/` but the package is `theory` because `lake new lean math` rejects `lean` as reserved.
- `notebooks/` — Jupyter (Python).
- Python project at repo root managed by `uv` (`pyproject.toml`, `uv.lock`).
- `.claude/skills/{compiler,research-manager,rigor-reviewer}/` — bundled ARA skills (project-scoped).
- `ara/` — does **not** exist until an ARA skill bootstraps it. Don't create it manually.

## Working with Lean

- Always run `lake` commands from inside `lean/`, e.g. `cd lean && lake build`.
- First-time setup: `lake exe cache get` (precompiled Mathlib `.olean`s, ~5 min).
- Adding a Lean module: create `lean/Theory/<Name>.lean`, add `import Theory.<Name>` to the relevant file. Run `lake build` to verify.
- Lean version is pinned in `lean/lean-toolchain` (`leanprover/lean4:v4.29.1`); elan auto-installs the matching toolchain.
- Mathlib version in `lean/lakefile.toml` (`rev = "v4.29.1"`). Don't bump unless you also bump the lean-toolchain to a compatible version.

## Working with Python

- Add a dep: `uv add <pkg>` (updates `pyproject.toml` + `uv.lock`).
- Run a script: `uv run python <script.py>`. Run a notebook: `uv run jupyter lab`.
- Don't use `pip` directly; `uv` manages the venv.

## ARA (Agent-Native Research Artifact) workflow

The three bundled skills define the research lifecycle:

- **`ara-compiler`** — invoke when ingesting a paper, repo, or notes; it produces (or extends) the `ara/` artifact.
- **`ara-research-manager`** — invoke as a **session epilogue**, after the user's request is fully addressed. It scans the conversation for decisions, experiments, dead-ends, pivots, claims, heuristics and writes them into `ara/`. Never invoke during a task — it would contaminate working context.
- **`ara-rigor-reviewer`** — Seal Level 2 epistemic review on an existing `ara/`. Run before publication / release.

The artifact's four-layer structure (cognitive `logic/`, physical `src/` or code, `trace/exploration_tree.yaml`, `evidence/`, plus `staging/`) is created by the skill on first invocation. Don't pre-create directories or fight the schema.

## Shell

Prefix shell commands with `rtk` (e.g. `rtk git status`, `rtk grep ...`, `rtk ls ...`). RTK filters output if it has a matching wrapper, otherwise passes through unchanged — always safe.

In `&&` chains, prefix every command: `rtk git add . && rtk git commit -m "msg"`.

Run `rtk gain` to see savings. Full command list: `rtk init --show`.

## Platform note

This repo was scaffolded on Windows. The Lean toolchain is at `~/.elan/bin/`; if `lean`/`lake` aren't on PATH in a fresh shell, `export PATH="$USERPROFILE/.elan/bin:$PATH"` (bash) or refresh PATH from the registry (PowerShell).
