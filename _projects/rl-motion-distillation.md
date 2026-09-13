---
layout: page
title: RL distillation of a diffusion motion planner
description: 6.7920 Reinforcement Learning · Fall 2025. Distilling a text-to-motion diffusion planner into a lightweight autoregressive generator–selector trained with RL, and a careful post-mortem of why it's hard.
importance: 3
category: coursework
---

**6.7920 Reinforcement Learning: Foundations and Methods, Fall 2025.** Final project with Jessica Wan.

Text-to-motion diffusion models like MDM and CLoSD produce expressive human motion, but need hundreds of denoising steps per sequence, which rules them out for latency-sensitive settings like robotics simulators. We tried to distill CLoSD into a cheap, controllable **autoregressive student** trained with reinforcement learning.

**The design**

- **Generator–selector architecture.** At each timestep a _generator_ proposes a small set of candidate next frames given the motion prefix and text prompt, and a small _selector_ policy trained with PPO picks one. This is formalized as an MDP whose reward combines teacher fidelity, temporal smoothness, an acceleration penalty, and a heavily weighted terminal trajectory reward, so the selector can optimize trajectory-level properties that pure behavior cloning cannot.
- **Two modalities.** An image-space version built on SD-Turbo (generator trained with a DMD-style distillation loss plus a REINFORCE term, rewards from OpenPose keypoints and VAE/CLIP embeddings), and a keypoint-space version operating directly on 22-joint 3D skeletons from 880 CLoSD trajectories, with both models trained from scratch.
- **Curriculum.** A phased reward schedule for the generator (bone length → fidelity → smoothness/acceleration) and a two-phase selector curriculum that starts from low-noise, teacher-adjacent candidates before introducing noisier ones.

**What we learned**

Image space failed for concrete reasons: keypoint detectors trained on natural RGB humans break on stick figures, VAE/CLIP embeddings are invariant to exactly the pose differences the selector needs to discriminate (its choices were near-random), and autoregressive rollouts degenerated into noise after ~100 frames. Keypoint space was far more stable and the selector learned meaningful early-phase policies, but once noisier candidates were introduced the reward curves kept rising while visual quality dropped — a clean example of **reward hacking** plus a **reward–model capacity gap**. The write-up identifies these failure modes (representation mismatch, capacity gap, partial reward hacking) and lays out what a working RL-guided motion distillation pipeline would need: tailored encoders, more expressive selectors, and reward terms that can't be zeroed by standing still.
