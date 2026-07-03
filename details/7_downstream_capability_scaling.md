# Downstream Capability Alignment Scaling

## Overview
Evaluates scaling laws against actual downstream capabilities (e.g. coding, math tasks) instead of upstream cross-entropy loss, which often shows step-function breakthroughs.

## Diagram
```mermaid
flowchart TD
    A[Pretraining Loss: Smooth Power-Law] --> B[Downstream Task Performance]
    B --> C[Emergent Capabilities / Step-Functions]
```

[← Back to README](../README.md)
