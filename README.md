# 12-Month AI Research Engineer Roadmap

Self-directed 12-month engineering and research curriculum covering **LLMs → Reinforcement Learning → World Models → Robotics & Production**, built from scratch with baselines, ablations, and write-ups.

- **Full plan:** [`roadmap/12-month-ai-research-engineer-plan.pdf`](roadmap/12-month-ai-research-engineer-plan.pdf)
- **Quick overview:** [`roadmap/overview.md`](roadmap/overview.md)

## Repository layout

```text
.
├── roadmap/                        # 12-month plan PDF + Markdown overview
├── months/                         # Monthly implementations (month-01-..., month-02-..., etc.)
├── notes/                          # Reading lists & weekly paper notes (2/week habit)
├── writeups/                       # Monthly technical write-ups & experiment logs
├── sebastian-llms-from-scratch/    # Earlier notebooks from Sebastian Raschka's LLMs From Scratch
├── pyproject.toml                  # Python environment (uv)
└── AGENTS.md                       # Agent guidelines for working in this repo
```

## Milestone checklist

- [ ] **Month 1:** GPT and BPE tokenizer trained from scratch (TinyStories val loss ≤ 1.45)
- [ ] **Month 2:** Multi-GPU FSDP run plus a small scaling sweep
- [ ] **Month 3:** Extraction model with SFT vs DPO eval published *(Q1 project)*
- [ ] **Month 4:** REINFORCE and DQN solving CartPole and LunarLander
- [ ] **Month 5:** PPO and SAC from scratch on MuJoCo (+ Push-T imitation)
- [ ] **Month 6:** GRPO project published with reward-hacking notes *(Q2 project)*
- [ ] **Month 7:** World Models reproduction on CarRacing (+ model-based RL)
- [ ] **Month 8:** mini-Dreamer vs DreamerV3 / TD-MPC2 / SAC sample-efficiency comparison
- [ ] **Month 9:** World model + MPC project published; fellowship applications sent *(Q3 project)*
- [ ] **Month 10:** ACT and Diffusion Policy trained on your own demos (LeRobot)
- [ ] **Month 11:** VLA fine-tuned and compared against ACT under distribution shifts
- [ ] **Month 12:** Capstone demo with served LLM and deployed robot policy *(Q4 capstone)*

## Running habits

- **Papers:** 2/week with a one-paragraph note in `notes/`.
- **Writing:** 1 technical write-up/month in `writeups/` (negative results count).
- **Open source:** 1 merged PR/quarter to a researcher repo (TRL, CleanRL, LeRobot, `lm-eval-harness`).

## Setup

Python `>=3.13` managed with [`uv`](https://docs.astral.sh/uv/):

```bash
uv sync
```
