---
layout: page
title: Attestation for negotiating AI agents
description: MIT Media Lab · Sep 2024–May 2025. zkSNARK proofs that an agent negotiation inside a GPU-backed TEE ran as specified, plus tool-using agents and an evaluation harness.
importance: 4
category: research
---

**MIT Media Lab, September 2024 – May 2025.** Researcher on AI security and agents.

When two AI agents negotiate on behalf of different parties, each side wants assurance that the other agent actually ran the agreed-upon protocol. I worked on making that verifiable:

- **Attestation inside TEEs.** Built attestation for AI agents negotiating inside GPU-backed trusted execution environments.
- **zkSNARK proofs of execution.** Wrote [circom](https://docs.circom.io/) circuits that produce zkSNARK proofs that the negotiation ran as specified, so a counterparty can check the proof without seeing the agent's private inputs.
- **Tool-using agents and evaluation.** Built agents that use real tools (Gmail, Google Calendar, and Shopify APIs) and an evaluation harness for multi-agent negotiation.
