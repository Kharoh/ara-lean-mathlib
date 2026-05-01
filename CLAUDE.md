# RTK (Rust Token Killer)

Prefix shell commands with `rtk` (e.g. `rtk git status`, `rtk grep ...`, `rtk ls ...`). RTK filters output if it has a matching wrapper, otherwise passes through unchanged — always safe.

In `&&` chains, prefix every command: `rtk git add . && rtk git commit -m "msg"`.

Run `rtk gain` to see savings. Full command list: `rtk init --show`.
