# Part 5 — AI Harness

Configuration to build Chef's Console with AI coding agents **on-rails** — not improvising.

## Contents

| Path | Purpose |
|------|---------|
| [agent_loops/build_loop.md](agent_loops/build_loop.md) | Task execution workflow |
| [agent_loops/review_loop.md](agent_loops/review_loop.md) | Pre-merge verification |
| [skills/](skills/) | Reusable procedures |
| [.cursor/rules/](.cursor/rules/) | Project guardrails |
| [prompts/](prompts/) | System prompt templates |

## Setup (copy into main repo)

```bash
# From chefsconsole2 root
cp teardown-sample/04_AI_HARNESS/.cursor/rules/*.mdc .cursor/rules/
# Install skills to ~/.cursor/skills/ or project skills folder per your agent setup
```

## Usage with Cursor

1. Open a task from [03_WORK_BREAKDOWN/tasks/](../03_WORK_BREAKDOWN/tasks/)
2. Paste [prompts/task_executor.md](prompts/task_executor.md) with task path filled in
3. Agent follows [agent_loops/build_loop.md](agent_loops/build_loop.md)
4. Before commit, run [agent_loops/review_loop.md](agent_loops/review_loop.md)

## Non-negotiables

- Activate backend venv before Python commands
- Run commands from correct folder (`frontend/`, `backend/`, `admin/`)
- Never commit `.env` or real credentials
- Every API change scoped by `restaurant_id` with permission check

See [.cursor/rules/project-guardrails.mdc](.cursor/rules/project-guardrails.mdc).
