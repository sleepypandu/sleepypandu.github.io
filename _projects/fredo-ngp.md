---
layout: page
title: Hash grid collisions in Instant-NGP
description: 6.8300 Advances in Computer Vision · Spring 2026. Where Instant-NGP's hash collisions land, a two-choice hashing scheme that spreads them out, and a router that tests whether the MLP cares.
importance: 1
category: coursework
---

**6.8300 Advances in Computer Vision, Spring 2026.** Final project with Michael Yang and Kartik Ramachandrula, on a direction suggested by Frédo Durand in lecture.

[Instant-NGP](https://nvlabs.github.io/instant-ngp/) trains NeRFs in seconds by storing multiresolution voxel features in hash tables, and at fine resolutions those tables _necessarily_ collide: unrelated points share a feature vector, and the projection MLP is left to sort it out. The original paper argues that this is fine because the collisions are pseudorandom. We asked whether that's actually true, and whether it matters.

**What we found**

- **Collisions are not uniform.** We instrumented inference to build per-pixel heatmaps of hash collisions and query pressure. Even after normalizing by query count, collision rate is strongly positively correlated with query pressure (mean pixel-wise correlation ≈ 0.60 across 50 views), so the MLP is under the most strain exactly in the regions that matter most for the render.
- **Two-choice hashing.** Inspired by balanced allocations, we gave each level two candidate hash salts, profiled per-slot load in a single preprocessing pass, froze it, and routed each point to the lower-load slot during training and inference — no per-render overhead. This made the collision-per-query profile measurably more uniform (≈6% relative reduction in CV, Gini, and a composite uniformity score; 14 of 15 held-out views improved) and weakened the coupling between collision rate and reconstruction residual, while leaving PSNR essentially unchanged.
- **Adaptive level selection.** To test whether the MLP would _use_ collision information if given it, we added a small router MLP that softmax-weights the per-level features (conditioned on position and collision/query density) instead of concatenating them. Results were comparable to baseline across fox, chair, and ship — evidence that Instant-NGP's head is already robust to collisions — with a small gain only on the real-world fox scene. Level-ablation probes showed the coarsest levels contribute disproportionately to reconstruction quality, consistent with a coarse-to-fine decoding picture.

**Takeaway:** collisions in Instant-NGP are neither benign nor destructive. They're structured, they correlate with error, and they can be redistributed for free — but the architecture tolerates them as long as coarse-scale structure survives.
