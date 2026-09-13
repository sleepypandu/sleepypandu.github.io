---
layout: page
title: Self-distillation for LLM reasoning
description: IBM Research · research intern · Jun–Aug 2026. Failure modes of self-distillation pipelines and where privileged-teacher signal lives in a rollout.
importance: 1
category: research
---

**IBM Research, Summer 2026.** Research intern working on reinforcement learning for LLM reasoning.

Self-distillation methods for reasoning train a model on its own outputs, using a "privileged" teacher (the same model given extra information, such as the reference answer) to supply a better target. I spent the summer taking these pipelines apart:

- **Ablations and reproductions.** Reproduced existing self-distillation pipelines and ran ablations on them, uncovering failure modes of OPSD and SDPO — cases where the privileged teacher's signal is unreliable or where the student learns the wrong thing from it.
- **Prefix-advantage study.** Ran a study across Qwen3-1.7B / 4B / 8B characterizing _where_ in a rollout the privileged-teacher signal localizes — i.e., how much of the advantage comes from early tokens versus the rest of the trace, and how that shifts with model scale. Submitted to the NeurIPS 2026 workshop on _Transitioning from Pre-Training to Post-Training_.
- **Follow-up question.** Whether privileged information can be used in a way that's actually helpful and not just a form of cheating — other uses of distillation beyond the standard student/teacher setup.

**Stack:** verl, vLLM, PyTorch, LoRA, FSDP, multi-node GPU training on LSF.
