# CLAUDE.md

@AGENTS.md

The working rules for this repo live in **`AGENTS.md`** (loaded above) so that every agent
shares one set of rules. This file only points at it — don't duplicate rules here.

Quick recap of what AGENTS.md requires, in order:

1. Read `README.md` and `PLAN.md` before doing anything.
2. Python only via `uv` (`uv run`, `uv add`) — no global `pip install`.
3. Run the checks and show their output before claiming done.
4. Append an entry to `RUNS.md`.
