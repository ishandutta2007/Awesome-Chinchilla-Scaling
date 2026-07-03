# The Learning Rate Decay Alignment Scheduler Lock

## Overview
Standard cosine learning rate schedules must decay to match the target token destination exactly. Aborting or extending runs midway leads to sub-optimal convergence.

## Diagram
```mermaid
flowchart LR
    A[Cosine LR Decay] --> B[Scheduler Lock: Must target exact total tokens]
    C[Continuous LR Scheduler] --> D[Permits flexible extensions without loss penalty]
```

[← Back to README](../README.md)
