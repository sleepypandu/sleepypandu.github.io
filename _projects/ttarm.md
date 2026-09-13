---
layout: page
title: TTARM — training-time adaptive rank modulation
description: 6.7960 Deep Learning · Fall 2025. Tracking how the effective rank of transformer activations evolves during training, and scheduling regularizers to steer it.
importance: 2
category: coursework
---

**6.7960 Deep Learning, Fall 2025.** Final project with Abrianna Zhang and Emma Li.

Transformers have no explicit regularizer on the rank of their intermediate representations, so whatever rank trajectory they follow during training emerges purely from optimization. Small pilot runs suggested a pattern — effective rank rises early as the model explores features, then falls as representations consolidate — and we asked whether deliberately encouraging that pattern is a useful inductive bias.

**What we did**

- **Measured rank dynamics** across three tasks (copy, sort, and next-token prediction on TinyStories), three model sizes (4–8 layers, 128–512 hidden dim), and every layer, using entropy-based effective rank and stable rank of activations and attention outputs.
- **Built rank regularizers** for both directions: log-determinant and effective-rank maximization to push rank up, and orthogonality and spectral-norm penalties to pull it down. Confirmed each one moves rank in the intended direction.
- **Proposed TTARM**, a schedule that applies a rank-increasing regularizer for the first 25% of training and a rank-decreasing one for the last 25%, and ran ablations: the inverted schedule (compress first, expand late), and each phase alone.
- **Tracked oversmoothing metrics** (token cosine similarity, attention-head entropy, attention-head stability) to see whether rank regularization helps with representational collapse.

**What we found**

Rank can be steered reliably, and TTARM produced the intended expand-then-compress trajectory. But it was not a universal win: it matched or beat baseline on the algorithmic tasks and underperformed on text prediction, and the generalization gap was similar across schedules. Two surprises: the _inverted_ schedule sometimes did as well as TTARM, suggesting that the presence of a regime shift matters more than its direction; and uniform rank-increasing regularization consistently reduced the oversmoothing metrics, which points to rank regularization as a practical tool against oversmoothing in deep transformers.
