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

## Architecture
```
                       DATA SOURCES
        +-----------------+ +----------+ +---------+
        | The Well 15 TB  | | Biology  | | Climate |
        | 16 simulations  | | bio data | | CMIP6   |
        +--------+--------+ +----+-----+ +----+----+
                 |               |             |
                 +-------+-------+-------------+
                         v
              +-------------------------+
              | 1. Graph Constructor    |   (domain-specific)
              +-----------+-------------+
                          v
              +-------------------------+
              | 2. HGAT Encoder         |
              +-----------+-------------+
                          v  z_t
              +-------------------------+
              | 3. DBMM Belief          |
              +-----------+-------------+
                          v  b_t
   +----------+    +-------------------------+    +----------------+
   | 6. Graph |--->| 4. JEPA Latent Dynamics |<-->| 7. COCONUT LLM |
   |    RAG   |    |    z_t  ->  z_(t+k)     |    |   continuous   |
   +-----+----+    +-----------+-------------+    |   latent       |
         |                     v                  |   reasoning    |
         |         +-------------------------+    +-------+--------+
         |         | 5. EBM Plausibility     |            |
         |         +-----------+-------------+            |
         |                     v  filtered               |
         +-------------------> +-------------------------+
                               | 8. Policy + Decision    |
                               +-----------+-------------+
                                           v
                +-------------+ +--------------+ +--------------+
                | Predictions | | Hypotheses   | | Decisions    |
                |             | | + provenance | | + log        |
                +-------------+ +--------------+ +--------------+
```

## Status

Architecture submitted to ICML 2026 AI for Science workshop (April 2026).
