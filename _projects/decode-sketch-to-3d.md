---
layout: page
title: Sketch-to-3D retrieval for generative car design
description: MIT DeCoDE Lab · Jan 2025. A 2D sketch → nearest 3D car mesh retrieval pipeline inside a multi-agent engineering-design framework (ASME IDETC 2025).
importance: 3
category: research
related_publications: true
---

**MIT DeCoDE Lab, January 2025.** Researcher in Faez Ahmed's group on generative AI for engineering design.

The lab was building a multi-agent framework in which LLM-driven agents collaborate on aesthetic and aerodynamic car design {% cite elrefaie2025agents %}. My piece was the **sketch-to-3D retrieval pipeline**: given a 2D sketch of a car, retrieve the nearest 3D car mesh from a large dataset so the downstream agents can start from real geometry rather than from scratch.

- Built the retrieval pipeline end-to-end (sketch embedding → mesh-view embedding → nearest-neighbour lookup).
- Benchmarked a range of retrieval models and similarity metrics to pick the ones that best matched sketches to meshes.
