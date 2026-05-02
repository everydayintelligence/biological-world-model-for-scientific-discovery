# Biological World Model for Scientific Discovery

A multi-domain latent world model for disease prediction, drug discovery, 
and climate system simulation under partial, real-world observations.

## Architecture Overview

- **Graph State Encoder**: Universal typed-graph representation of any 
  physical or biological system
- **Latent Dynamics Module**: JEPA-style prediction in latent space 
  (no observation-space decoding)
- **Belief Inference Module**: Bayesian uncertainty over partial/noisy 
  observations
- **Plausibility Estimator**: Energy-based physical consistency filter
- **Continuous Latent Reasoning**: Bidirectional COCONUT LLM coupling 
  to simulation dynamics
- **GraphRAG Retrieval**: Structured biological knowledge graph retrieval

## Preliminary Results

Out-of-domain evaluation on behavioral dynamics datasets (absent from 
physical training distribution): within 1–4% of specialist model accuracy 
without fine-tuning.

## Pretraining Data

Multi-domain pretraining on [The Well](https://arxiv.org/abs/2412.00568) 
(15 TB, 16 PDE families) is currently in progress.

## Status

Architecture submitted to ICML 2026 AI for Science workshop (April 2026).
