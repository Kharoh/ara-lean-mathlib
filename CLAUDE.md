# Project conventions

## Goal

Produce math research that is **relevant, reproducible, and proved**: results that matter, experiments that re-run end-to-end, and theorems formalized in Lean.

## Layout

- `lean/` — Lean 4 + Mathlib `v4.29.1`. Package `theory`, namespace `Theory` (both placeholders — rename to your project's namespace before adding theory-specific content). Directory is `lean/` but package is `theory` because `lake new lean math` rejects `lean` as reserved.
- `notebooks/` — Jupyter (Python via `uv`).
- `.claude/skills/{compiler,research-manager,rigor-reviewer}/` — the three ARA skills, project-scoped.
- `ara/` — does **not** exist until an ARA skill bootstraps it. Don't create it manually.

## What goes in Lean

Definitions, theorems, and the proven core of the theory. Run `lake` from inside `lean/` (`cd lean && lake build`); first time use `lake exe cache get` to fetch precompiled Mathlib. Versions are pinned in `lean/lean-toolchain` and `lean/lakefile.toml` — don't bump one without the other.

The split: anything we **claim is proven** lives in Lean. Conjectures, simulations, and informal arguments live in notebooks or comments; polished outputs live in Quarto (see below).

## What goes in Quarto

Vitrin demos and papers — every final-result artifact aimed at human readers — are written in Quarto. Talks, write-ups, and showcase pages go here, not in notebooks. Notebooks are for exploration; Quarto is for what we publish.

## ARA — Agent-Native Research Artifact

ARA is a protocol that turns research into a machine-executable artifact (paper: arXiv 2604.24658). Three skills are bundled in `.claude/skills/`:

- **`ara-compiler`** — ingest a paper, repo, or notes; produces or extends `ara/`.
- **`ara-research-manager`** — invoke as a **session epilogue** (after the user's request is fully addressed). Records decisions, experiments, dead-ends, pivots, claims, heuristics into `ara/`. Never invoke during a task.
- **`ara-rigor-reviewer`** — Seal Level 2 epistemic review on an existing `ara/`, run before publication.

The four-layer structure (`logic/`, `src/` or code, `trace/`, `evidence/`, plus `staging/`) is created by the skill on first invocation. Don't pre-create directories or fight the schema.

## Shell

Prefix shell commands with `rtk` (e.g. `rtk git status`). In `&&` chains, prefix every command. Run `rtk gain` for savings. Full list: `rtk init --show`.
