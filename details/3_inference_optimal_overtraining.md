# The Inference-Optimal Overtraining Era (~2024–Present)

## Overview
Focuses on minimizing lifetime serving/inference costs rather than training compute. By overtraining small parameter models on massive token counts, inference costs and latency are dramatically reduced.

## Trade-off Analysis
* **Training Cost:** Higher (trained far past compute-optimal limit).
* **Inference Cost:** Lower (compact footprint, faster generation).

## Diagram
```mermaid
flowchart TD
    A[Enterprise Serving Goal] --> B[Overtrain Small Model N]
    B --> C[15T+ Tokens on 8B Parameters]
    C --> D[Dense Representation]
    D --> E[Low-latency, Low VRAM Serving]
```

[← Back to README](../README.md)
