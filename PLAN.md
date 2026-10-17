# PLAN

Status and the next step. Update the two top sections whenever you finish something —
don't let this file rot, it is the second thing agents read.

## Status — 2026-10-17

- Working rules written (`AGENTS.md`) and loaded via `CLAUDE.md`.
- uv project initialised: `pyproject.toml` (non-packaged, no dependencies yet),
  `.python-version` = 3.12, `uv.lock` committed, `.venv` created by `uv sync`.
- Toolchain installed per-user into `~/.local/bin` (no admin): `uv` 0.13.1, `gh` 2.102.0,
  and Python 3.12.1 fixed (a stray 0-byte `python` file was shadowing the real
  interpreter; it was moved to `%TEMP%` and a `python3.exe` shim added).
- `gh` authenticated as **Blubeeris**; git HTTPS credentials routed through
  `gh auth setup-git`.
- Pushed: repo is live and public at https://github.com/Blubeeris/mlr-agent-lab
  (commits use the `159132016+Blubeeris@users.noreply.github.com` alias, repo-local only).

## Done

- [x] Smoke test exists and passes: `uv run python hello.py` → `hello`, exit 0.
- [x] `AGENTS.md` + `CLAUDE.md` in place.
- [x] `README.md`, `PLAN.md`, `RUNS.md` created.
- [x] Public repo pushed; a clean clone + `uv sync` + `uv run python hello.py` works.

## Next step

1. Replace the `hello.py` placeholder with real content — the project name suggests ML
   regression experiments; nothing in the repo commits to that yet, so state the actual
   goal here once known.
3. Add the first real dependency with `uv add`, and a test runner (`uv add --dev pytest`)
   so rule 3 in `AGENTS.md` has something stronger than the smoke test to check.

## Open questions

- What is this lab actually for — ML regression experiments, or purely an exercise in
  agent working rules? The README says "no product yet"; that should be resolved.
- Whether tests should be required before any non-trivial change, or only suggested.
