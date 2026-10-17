# mlr-agent-lab

A small lab repo for exercising agent working rules: how an agent should read a project,
manage Python dependencies with [uv](https://docs.astral.sh/uv/), verify its own work, and
leave an honest record of what it did.

There is no product here yet. The content is the rules (`AGENTS.md`) and the trace of runs
(`RUNS.md`).

## Requirements

- [uv](https://docs.astral.sh/uv/) — Python and dependency management. No separate Python
  install step is needed; uv resolves the interpreter from `.python-version`.
- No administrator rights required for anything in this repo.

## Setup

```bash
uv sync          # creates .venv and installs from uv.lock
```

## Run things

```bash
uv run python hello.py     # the current smoke test
uv run <anything.py>       # any script, inside the project environment
uv add <pkg>               # add a dependency (updates pyproject.toml + uv.lock)
uv add --dev <pkg>         # add a dev/test dependency
```

Do **not** use bare `pip install` — see rule 2 in `AGENTS.md`.

## Layout

| File | Purpose |
| --- | --- |
| `AGENTS.md` | Working rules for every agent. **Edit this, not CLAUDE.md.** |
| `CLAUDE.md` | One job: loads `AGENTS.md` into Claude Code. |
| `PLAN.md` | Status and the next step. Update it as you go. |
| `RUNS.md` | Log of each run: model, request, how it was verified. |
| `hello.py` | The smoke test target. |
| `pyproject.toml` | Project metadata and dependencies. |
| `uv.lock` | Locked dependency resolution. |

## Checks

```bash
uv run python hello.py     # must print "hello" and exit 0
```

Run this before claiming anything is done (`AGENTS.md` rule 3).
