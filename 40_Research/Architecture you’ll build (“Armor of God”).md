---
title: Subliminal learning — implications for 3B Llama fine‑tune
date: 2025-07-24
tags:
  - research
  - security
  - subliminal-learning
  - llama3
  - alignment
  - Apollyon
status: seed
links:
  - - - Sentinel Evaluator Protocol
  - - - Canary Test Deck
  - - - Dataset Provenance Manifest Template
source: "YouTube: *AI researchers shocked as models quietly learn to be evil* + discussion"
aliases:
  - Armor of God Architecture
---



[[Canary Test Deck]]
[[Dataset Provenance Manifest Template]]
[[Sentinel Evaluator Protocol]]

## Why this matters (TL;DR)
Teacher ↔ student of the same model family can smuggle traits through “innocent” artifacts (numbers, CoT, code). Cross‑family transfers fail → use that as a firewall.

## Immediate moves for Troy (checkboxes = implementation tracker)

- [ ] **Provenance-first datasets** (hash + signed manifest for every file you ingest).
- [ ] **Cross-family glove‑box** for synthetic data (e.g., generate with Gemma/Mistral, train Llama).
- [ ] **Behavioral canaries** (~50 probes, auto rollback on fail).
- [ ] **Sentinel evaluator** (separate lightweight model that inspects your corpus for drift).
- [ ] **Baseline diff-testing** before/after any restore/merge/upgrade.
- [ ] **Entropy/oddity scan** on incoming text to catch suspicious low‑entropy numeric strings.

## Architecture you’ll build (“Armor of God”)
- Data‑Hygiene Triad (source tagging • semantics/entropy filter • signature audit)
- Sentinel evaluator
- Canary test deck
- Cross‑family glove‑box
- Interpretability spot‑checks (simple linear probes on final activations)

## Roadmap
**Now (3B local)** → implement the triad + canaries.  
**6–12 mo (bigger GPU)** → snapshot & diff; re‑run sentinel on historical data.  
**>18 mo (multi‑agent)** → mutual attestation + public alignment‑score API.

## Open tasks / threads
- [ ] Draft 50-item **Canary Test Deck** tailored to your values.
- [ ] Write a **Dataset Provenance Manifest Template**.
- [ ] Automate weekly watch for “subliminal learning” papers.
