# Mixture-of-Experts (MoE) Scaling Optimization

## Overview
Decouples total capacity (parameters) from active computation. By routing tokens to subset experts, MoE achieves high capacity with low training compute.

## Diagram
```mermaid
flowchart TD
    A[Input Token] --> B[Gating Network]
    B --> C[Expert 1]
    B --> D[Expert 2]
    B --> E[Expert N]
    C & D & E --> F[Output Assembly]
```

[← Back to README](../README.md)
