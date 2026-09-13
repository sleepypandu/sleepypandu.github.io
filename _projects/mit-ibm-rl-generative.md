---
layout: page
title: RL for generative models
description: MIT-IBM Watson AI Lab · May 2025–May 2026. RL fine-tuning of flow models for molecules and crystals, and the diversity analysis behind Tailor (ACL 2026).
importance: 2
category: research
related_publications: true
---

**MIT-IBM Watson AI Lab, May 2025 – May 2026.** Researcher in Chuang Gan's group, working on reinforcement learning for generative models.

- **RL fine-tuning of flow models.** Investigated using RL to fine-tune flow-matching models for molecule and crystal generation, where the reward comes from downstream chemical and structural objectives rather than likelihood.
- **Tailored primitive initialization.** Co-author on {% cite yao2026tailored %}, which shows that RL fine-tuning of LLM reasoners depends heavily on the warm-start data it begins from, and proposes _Tailor_, a method for constructing a warm-start set from tailored reasoning primitives. I built the embedding-similarity pipeline used for the paper's diversity analysis — the evidence that Tailor's warm-start data is more reasoning-diverse than the Standard-CoT and 4-STaR baselines.
