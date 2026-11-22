# FDE Project Starter

A production-shaped skeleton for an end-to-end Forward Deployed Engineer project.
Clone this, push changes, and you have a live service URL before you write any
real logic.

**Live demo:** _add your URL here in step 1_

## Why this exists

Most portfolio projects are repositories nobody opens. This one is built so that
the first commit is already deployable, and the deployment step is never a cliff
at the end.

## What is in the box

| Piece | Purpose |
| --- | --- |
| `src/service/` | FastAPI app with `/health`, `/version`, `/cost`, `/predict` |
| `src/config.py` | Settings from the environment, validated on startup |
| `src/observability/` | Structured JSON logging and per-call cost accounting |
| `src/governance/` | Append-only audit log and PII redaction |
| `src/models/` | Where your real model goes |
| `src/llm/` | Prompts, retrieval and agent logic |
| `app/streamlit_app.py` | The operator-facing view |
| `evals/` | Golden set and a scored eval run |
| `docs/01..04` | Discovery, architecture, evaluation, governance |
| `Dockerfile`, `render.yaml` | Deployable as a container |
| `.github/workflows/` | CI on every push, eval scorecard as an artifact |

## Quick start

```bash
git clone <your-repo> && cd fde-project-starter
cp .env.example .env          # then put your real key in .env
make install
make dev                      # http://localhost:8000/docs
make test
make eval
make cost
```

## Deploy

**Fastest (Streamlit Community Cloud)** - push to GitHub, go to
share.streamlit.io, pick this repo and `app/streamlit_app.py`, add your API key
under Settings, deploy. Public apps are free; the app sleeps after 12 hours
without traffic, and a commit no longer keeps it awake.

**Fuller (Render)** - create a web service from this repo; `render.yaml` defines
it. The free instance has 512 MB RAM and one free Postgres that expires after 30
days. It sleeps after 15 minutes idle and takes about a minute to wake, so visit
your own URL before sending it to anyone.

## Honesty rules this repo enforces

- `.env` is gitignored from the first commit. No key in history, ever.
- Every model call is cost-logged, because the cost model is one of the things
  interviewers ask about.
- The eval scorecard is committed to `outputs/scorecard.json` so the score is
  visible without running anything.
- Systems that always answer read as demos. `/predict` can abstain.

## Not compliant, by design

This is a portfolio system. It is not validated and not compliant with any
regulation. `docs/04-governance.md` states which regime a real deployment would
fall under and what additional work that would require.
