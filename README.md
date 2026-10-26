# Customer Support agent · a CCA Prep Studio capstone

Build a support agent that resolves returns, billing disputes and account problems through its own tools, enforces a refund limit in code, and hands off to a person when it should. It is exam scenario 1 of the Claude Certified Architect – Foundations exam, built for real, one step at a time.

| Step | You build | Exam tasks | Tests |
|---|---|---|---|
| 1 | The agent loop | 1.1 | `tests/test_step1_loop.py` |
| 2 | Tools that say what they are for | 2.1 | `tests/test_step2_tools.py` |
| 3 | Errors the agent can act on | 2.2 | `tests/test_step3_errors.py` |
| 4 | A refund limit in code | 1.5, 1.4 | `tests/test_step4_hooks.py` |
| 5 | Handing off to a person | 5.2, 1.4 | `tests/test_step5_escalation.py` |
| 6 | Long, messy conversations | 1.6, 5.1 | `tests/test_step6_context.py` |

## Set up

1. Python 3.11 or newer, then in this folder:
   ```bash
   python -m venv .venv && source .venv/bin/activate
   pip install -e ".[dev]"
   ```
2. Copy `.env.example` to `.env` and add your Anthropic API key. Never commit `.env` (it is already in `.gitignore`).
3. In Claude Code: add the CCA Prep Studio plugin (see the capstone page in the app) and connect Claude Code from the step page, so it can read your step and report your progress.
4. Run `/cca-prep-studio:next-step` in Claude Code to begin.

## How a step counts

1. Build the step until its tests pass: `pytest tests/test_step1_loop.py`.
2. Push. GitHub Actions runs every step's tests (`.github/workflows/capstone.yml`, jobs `step-1` … `step-6`).
3. In CCA Prep Studio, answer the step's question in your own words.

When the tests pass on GitHub and your answer scores 70 or more, the step is verified and counts toward the exam tasks above. Claude Code can report a step and leave notes, but it cannot verify a step for you.

## Try your agent

After step 1 you can talk to it (it calls Claude with your key):

```bash
python -m support_agent.app
```

The tests never call Claude: they use a scripted stand-in (`tests/fakes.py`), so they are free and give the same result every time.

## What is already here

- `backend.py`: a pretend store with customers, orders and refunds. It can fail on purpose (`fail_next`).
- `policy.py`: the refund limit ($500) and the 30-day return window.
- `agent.py`, `prompts.py`, `app.py`: the wiring. You will read them, but each step's work is in the file its tests name.

Do not change the tests. If you think one is wrong, ask Archíe in CCA Prep Studio.
