# 12-Month AI Research Engineer Plan: LLMs, RL, World Models

*Source of truth: [`12-month-ai-research-engineer-plan.pdf`](./12-month-ai-research-engineer-plan.pdf) (49 pages — summary + detailed week-by-week tabs for all 12 months).*

## How this plan works

Four quarters build on each other: **LLMs → RL → World Models → Robotics & Production**. Each quarter ends with one public project (repo + write-up).

- **Time:** ~12 hours/week (two 2-hour weeknight sessions, one 6-hour weekend block, 2 hours of reading).
- **Compute:** Laptop/Colab for small work; rented A100/H100 (Lambda, RunPod, Modal) for real runs (~$100–300/month).
- **Definition of done:** It runs, it is measured against a baseline, and it is written up with what failed.
- **Inference scope:** Enough to ship models (serving, quantization, latency budgets), not kernel-level optimization.

---

## Quarter 1 (Months 1–3): LLM foundations and post-training

**Goal:** Build, train, and post-train a language model yourself, and evaluate it honestly.

- **Month 1 — Transformer from scratch:** micrograd & makemore (backprop ninja), byte-level BPE tokenizer, modern decoder-only transformer (RoPE, RMSNorm, SwiGLU), AdamW + cosine schedule, train on TinyStories (CS336 A1; target val loss ≤ 1.45).
- **Month 2 — Training engineering & scaling:** A1 LR/batch/architecture ablations, profiling & bf16 mixed precision (CS336 A2 pt 1), naive DDP → bucketed overlap → ZeRO-1 → PyTorch FSDP on GPT-2 124M / FineWeb-Edu (CS336 A2 pt 2), IsoFLOP scaling laws (CS336 A3).
- **Month 3 — Post-training & evaluation:** SFT & LoRA (plain PyTorch + TRL), SEC EDGAR structured extraction dataset (500–2,000 filings) + eval harness, SFT vs DPO + `lm-eval-harness` regression check, error analysis & Hugging Face Hub publish.
- **Q1 Project:** Fine-tuned small model for structured SEC filing extraction comparing SFT vs DPO on field-level accuracy and schema validity, with a published eval suite.

## Quarter 2 (Months 4–6): Reinforcement learning

**Goal:** Implement the core algorithms yourself, then apply RL to the LLM you built in Q1.

- **Month 4 — RL foundations:** Sutton & Barto (bandits, MDPs, DP on FrozenLake, MC on Blackjack, SARSA vs Q-learning on Cliff Walking), CS285 HW2 (policy gradients, baselines, GAE), CS285 HW3 pt 1 (DQN & Double DQN).
- **Month 5 — PPO, SAC & imitation learning:** Single-file CleanRL-style PPO from scratch (discrete + continuous MuJoCo Hopper/HalfCheetah, 5 seeds), CS285 HW3 pt 2 (SAC with clipped double-Q & auto temperature), CS285 HW1 (action-chunking & flow-matching imitation on Push-T).
- **Month 6 — RL for LLMs:** CS336 A5 MATH baseline & SFT, CS285 HW4 (GR-REINFORCE & GRPO from scratch on hard MATH), GRPO on Q1 extraction model with verifiable reward, KL/group-size ablations & reward-hacking audit.
- **Q2 Project:** GRPO on the Q1 extraction task with verifiable rewards, showing reward curves vs SFT/DPO and documenting reward hacking.

## Quarter 3 (Months 7–9): World models

**Goal:** Learn models of environment dynamics and use them to plan or train policies in imagination.

- **Month 7 — Latent dynamics & model-based RL:** VAE + MDN-RNN + CMA-ES controller ("World Models" on CarRacing, real vs dream), CS285 Fall 2023 HW4 (ensembles, MPC with random shooting & CEM, MBPO).
- **Month 8 — Dreamer & TD-MPC2:** Official DreamerV3 on DMC (`walker-walk`, `cheetah-run`), minimal RSSM + imagination-trained actor-critic (`mini-Dreamer`) in PyTorch, official TD-MPC2, sample-efficiency comparison against Month 5 SAC.
- **Month 9 — Large & video world models:** V-JEPA 2 action probing vs DINOv2, landscape comparison (IRIS, DIAMOND, Genie, Cosmos), 50k simulator transitions (robosuite/LIBERO), action-conditioned latent world model + CEM/MPC planning vs true simulator, fellowship applications.
- **Q3 Project:** Action-conditioned world model on simulated robot data with MPC planning, compared against the true simulator over growing horizons.

## Quarter 4 (Months 10–12): Robotics capstone and production

**Goal:** A real (or simulated) robot running a learned policy, plus served models with production basics.

- **Month 10 — Imitation learning with LeRobot:** SO-101 arm assembly/calibration/teleop (or `gym-aloha`), 50 recorded demos on HF Hub, train & compare ACT vs Diffusion Policy (20-trial protocol).
- **Month 11 — VLA fine-tuning:** Trace & fine-tune SmolVLA on Month 10 data (+ second task for language conditioning), fine-tune a larger VLA (OpenVLA LoRA or π0), generalization tests under shifts (unseen positions, distractors, reworded instructions).
- **Month 12 — Production & capstone:** Serve extraction LLM with vLLM + 4-bit AWQ load testing, export policy to ONNX/TensorRT & measure 30 Hz loop jitter, Dockerize + CI eval gate + wire LLM command parser to robot policy, record capstone demo & year review.
- **Capstone:** Robot arm completes a task end-to-end from a natural-language command parsed by the served LLM.

---

## Habits that run all year

- **Papers:** 2/week with a one-paragraph note each in `notes/papers/`.
- **Writing:** 1 blog post or technical write-up/month in `writeups/` (negative results count).
- **Open source:** 1 merged PR/quarter to a researcher repo (TRL, CleanRL, LeRobot, `lm-eval-harness`).
- **Community:** LeRobot & EleutherAI Discords; apply to MATS / AI lab fellowships around Month 9.
- **Quarterly review:** Check what shipped, what slipped, and cut scope rather than skip the write-up.

## After Month 12 (Months 13–18): Looped transformers & frontier research

Recurrent-depth / looped transformers (Universal Transformers, Giannou et al., Geiping et al. NeurIPS 2025, Ouro, HRM, TRM, Mixture-of-Recursions, LoopFormer, LoopCoder-v2, Fan/Svete/Lee 2026, Inner-loop inference) + projects tying together Month 1 GPT, Q2 GRPO, robotics adaptive-depth policies, and serving latency/KV-cache benchmarks. Aim for a workshop paper by Month 15.
