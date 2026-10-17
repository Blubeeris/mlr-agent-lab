# Working rules

These rules apply to every agent working in this repo (Claude Code and others).
`CLAUDE.md` loads this file — edit here, not there.

## 1. Read first, before touching anything

- **`README.md`** — what this project is for and how to run it.
- **`PLAN.md`** — where things stand and what the next step is.

Do not start work from a bare prompt when those two files answer it. If what you are
about to do contradicts `PLAN.md`, say so before doing it.

## 2. Python goes through uv — never global pip

```
uv run python foo.py     # run anything
uv add <pkg>             # add a runtime dependency
uv add --dev <pkg>       # add a dev/test dependency
uv sync                  # materialise the environment from uv.lock
uv run pytest            # never call pytest directly
```

- **No bare `pip install`.** Not `pip install`, not `python -m pip install`, not
  `pip install --user`. It writes into the shared system interpreter at
  `AppData\Local\Programs\Python\Python312`, which is invisible to `uv.lock` and
  unreproducible on any other machine.
- **No `python -m venv` + `pip install -r`.** `uv venv` / `uv sync` replace that whole flow.
- Every import in the code must be backed by a line in `pyproject.toml`. If it isn't,
  `uv add` it — don't rely on something being globally installed.
- `uvx <tool>` is fine for running a CLI tool without installing it.

## 3. Run checks before saying it is done

Never report work as finished on the strength of having written it. Before the final
answer, run the checks and **paste the real output** — including failures.

In this repo, the check floor is:

```
uv run python hello.py      # the current smoke test
```

Plus whatever the change itself implies: a test you added, a command the feature is
supposed to make work, `uv run pytest` once tests exist.

If a check fails, report it failing with its output. A "done" that skipped the check is
worse than an unfinished task, because it is not trustworthy.

## 4. Environment facts worth knowing

- **No admin rights.** Tools live in `C:\Users\<user>\.local\bin` (on the user PATH).
  Install per-user; never write to `Program Files`.
- `python` / `python3` / `py` / `gh` / `uv` / `uvx` all work. `pip` outside a venv is the
  shared-interpreter trap from rule 2.
- Git HTTPS auth runs through `gh` (account **Blubeeris**); don't paste tokens into files.
- Shell here is Git Bash (POSIX), not PowerShell. Locale is Slovak, so a broken Python
  shows up as „Python sa nena" with exit 49.

## 5. Log the run

After completing a task, append an entry to **`RUNS.md`**: which model ran, what was
asked, and how it was verified. Keep it factual — including when something did not work.
