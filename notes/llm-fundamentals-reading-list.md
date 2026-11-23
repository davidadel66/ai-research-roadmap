# LLM fundamentals: an opinionated paper path

This is a reading path, not a canon. Read it alongside *Build a Large Language Model From Scratch* rather than pausing the book to finish every paper first.

**Reading rule:** understand the problem, the proposed mechanism, and the main result. Skip dense derivations and benchmark tables on the first pass.

## Core path

### 1. A Neural Probabilistic Language Model (2003) — read the idea closely

[Bengio et al., JMLR](https://www.jmlr.org/papers/v3/bengio03a.html)

- **Why:** Establishes the core idea you are implementing now: learn token representations and a next-token probability model together.
- **Focus:** Abstract and Sections 1–3; connect the paper's distributed word vectors to `nn.Embedding`.

### 2. Neural Machine Translation of Rare Words with Subword Units (2016) — skim

[Sennrich, Haddow, and Birch, ACL Anthology](https://aclanthology.org/P16-1162/)

- **Why:** Introduced byte-pair encoding to neural NLP, explaining why modern models use subword tokens instead of a word-sized vocabulary.
- **Focus:** The motivation and Section 3's BPE procedure; skim the translation experiments.

### 3. Neural Machine Translation by Jointly Learning to Align and Translate (2015) — read conceptually

[Bahdanau, Cho, and Bengio, arXiv](https://arxiv.org/abs/1409.0473)

- **Why:** Introduces learned attention as a way to select relevant parts of a sequence instead of compressing everything into one fixed vector.
- **Focus:** Abstract, Sections 2.1–2.2, and the alignment diagrams; do not get stuck on the RNN equations.

> If encoder-decoder models are unfamiliar, first skim [Sequence to Sequence Learning with Neural Networks (2014)](https://arxiv.org/abs/1409.3215).

### 4. Attention Is All You Need (2017) — read closely

[Vaswani et al., NeurIPS](https://proceedings.neurips.cc/paper/7181-attention-is-all-you-need)

- **Why:** Defines the Transformer: self-attention, scaled dot-product attention, multi-head attention, position encoding, residual connections, and feed-forward blocks.
- **Focus:** Figure 1 and Sections 3.1–3.5. Return to the equations after implementing attention yourself.

### 5. Improving Language Understanding by Generative Pre-Training (2018) — read closely

[Radford et al., OpenAI](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)

- **Why:** GPT-1 turns the Transformer decoder plus next-token pretraining into a reusable language model.
- **Focus:** Sections 2–3: the language-model objective, decoder-only architecture, and pretrain-then-fine-tune workflow.

### 6. Language Models are Unsupervised Multitask Learners (2019) — read closely

[Radford et al., OpenAI](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)

- **Why:** GPT-2 shows that scaling next-token prediction on diverse text produces useful zero-shot behavior; it also uses byte-level BPE.
- **Focus:** Sections 1–3 and the model/data description; skim the individual benchmark sections.

### 7. Language Models are Few-Shot Learners (2020) — selective read

[Brown et al., arXiv](https://arxiv.org/abs/2005.14165)

- **Why:** GPT-3 makes prompting and in-context learning central: tasks can be specified in text without gradient updates.
- **Focus:** Abstract, Sections 1–2, and the definitions of zero-, one-, and few-shot evaluation; skim the long task catalog.

### 8. RoFormer: Enhanced Transformer with Rotary Position Embedding (2021) — read after attention

[Su et al., arXiv](https://arxiv.org/abs/2104.09864)

- **Why:** Introduces RoPE, the positional mechanism used by many modern decoder-only LLMs instead of GPT-2-style learned absolute position vectors.
- **Focus:** Introduction and Section 3; revisit the rotation math once query/key attention is comfortable.

### 9. Scaling Laws for Neural Language Models (2020) — read conceptually

[Kaplan et al., arXiv](https://arxiv.org/abs/2001.08361)

- **Why:** Shows that language-model loss follows predictable power laws with model size, data, and compute.
- **Focus:** Abstract, Section 1, and the main plots; learn what a compute budget forces you to trade off.

### 10. Training Compute-Optimal Large Language Models (2022) — read after Scaling Laws

[Hoffmann et al., arXiv](https://arxiv.org/abs/2203.15556)

- **Why:** The Chinchilla result corrects the earlier scaling prescription: under a fixed budget, model parameters and training tokens should grow together.
- **Focus:** Abstract and Sections 2–3; understand why a smaller model trained on more data can beat a larger undertrained model.

## Next layer

Read these when the corresponding topic appears in your implementation or work.

1. **[Layer Normalization (2016)](https://arxiv.org/abs/1607.06450)** — why Transformer blocks normalize each example independently; read when you implement LayerNorm.
2. **[Decoupled Weight Decay Regularization (AdamW, 2019)](https://arxiv.org/abs/1711.05101)** — why weight decay must be separated from Adam's gradient update; read when you build the training loop.
3. **[FlashAttention (2022)](https://arxiv.org/abs/2205.14135)** — exact attention made faster by reducing GPU memory traffic; focus on the IO-awareness idea, not the kernel proof.
4. **[LLaMA (2023)](https://arxiv.org/abs/2302.13971)** — a compact modern pretraining recipe combining RoPE, RMSNorm, SwiGLU, and compute-efficient data scaling.
5. **[Training language models to follow instructions with human feedback (InstructGPT, 2022)](https://arxiv.org/abs/2203.02155)** — the classic SFT → reward model → PPO/RLHF post-training pipeline.
6. **[LoRA (2021)](https://arxiv.org/abs/2106.09685)** — parameter-efficient fine-tuning by learning low-rank updates while freezing the base model.
7. **[Direct Preference Optimization (2023)](https://arxiv.org/abs/2305.18290)** — preference tuning with a classification-style objective instead of an explicit reward model plus reinforcement learning.

## What to read now

At the embedding stage of the book, read only **#1 (Bengio)** and skim **#2 (BPE)**. Save **Attention Is All You Need** until you have implemented self-attention; the paper will make substantially more sense then.
