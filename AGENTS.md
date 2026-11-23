# AGENTS.md

## Repo purpose

This repository tracks David's **12-Month AI Research Engineer Roadmap** (LLMs → RL → World Models → Robotics & Production).

- **Source of truth:** `roadmap/12-month-ai-research-engineer-plan.pdf` (49 pages: overview + detailed week-by-week specs, sources, assignments, and done criteria for Months 1–12).
- **Quick reference:** `roadmap/overview.md` (high-level summary of all 12 months, habits, and Months 13–18 frontier plan).
- **Progress tracker:** `README.md` (milestone checklist).

When starting a new month or week, read the corresponding pages of `roadmap/12-month-ai-research-engineer-plan.pdf` so targets, sources, and "Done when" criteria are exact.

## Learning-first rules (critical)

This is a **learning and research-engineering repo**, not a "ship boilerplate fast" repo.

1. **Don't solve assignments behind David's back.** Many weeks explicitly require implementing from memory or without looking at solutions (e.g., `micrograd`, makemore "backprop ninja", CS336 A1–A3, CS285 HWs, CleanRL-style PPO, SAC, GRPO, mini-Dreamer). Ask before writing core algorithm code; default to guiding, reviewing, or pairing in chunks.
2. **Teach the non-obvious choices.** Explain *why* a tensor shape, initialization, normalization, loss masking, gradient accumulation, or evaluation split is written a certain way.
3. **Hold the definition of done.** Every assignment/project is only done when:
   - it runs cleanly,
   - it is measured against a baseline (with numbers/plots), and
   - it is written up, including what failed.
4. **Sanity-check locally before spending GPU dollars.** Compute budget is ~$100–300/month on rented A100/H100s (Lambda, RunPod, Modal). Verify shapes, gradient checks, overfit-one-batch tests, and checkpointing on CPU/tiny data before launching paid runs.

## Directory conventions

- `roadmap/` — The 12-month plan PDF and `overview.md`.
- `months/month-XX-<slug>/` — Code, notebooks, configs, and experiment logs for each month (create each folder when starting that month).
- `notes/` — Reading lists and weekly paper notes (2 papers/week, one paragraph each).
- `writeups/` — Monthly technical write-ups and quarterly project posts.
- `sebastian-llms-from-scratch/` — Archived notebooks from Sebastian Raschka's *Build a Large Language Model (From Scratch)*. Treat as read-only reference unless David asks to modify it.

## Environment & git hygiene

- Python `>=3.13` managed with `uv` (`pyproject.toml`, `uv.lock`). Add dependencies via `uv add <pkg>` rather than editing `pyproject.toml` by hand.
- Never commit datasets, model checkpoints, weights, or run artifacts (`data/`, `checkpoints/`, `runs/`, `wandb/`, `*.pt`, `*.safetensors`, `*.npy`, etc. are gitignored).
- Keep scripts reproducible: fix seeds, log configs and metrics, and prefer clean `.py` modules over giant monolithic notebooks once an idea is validated.
