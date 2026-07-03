# Aligned Compute Optimization (The Preference Optimization Shift)

## Overview
Preference optimization (RLHF, DPO) restricts output distributions. Scaling laws shift because safety alignments consume parameter capacity, requiring wider/deeper architectures earlier in the pipeline.

## Diagram
```mermaid
flowchart LR
    A[Base Model Pretraining] --> B[Alignment: RLHF / DPO]
    B --> C[Capacity Consumption / Shift in Optimal Curve]
```

[← Back to README](../README.md)
