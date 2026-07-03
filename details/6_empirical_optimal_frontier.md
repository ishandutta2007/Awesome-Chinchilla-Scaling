# Empirical Optimal Frontier Isolation

## Overview
Empirical frontier isolation isolates optimal parameter-token splits by tracing a geometric envelope across many runs, identifying the lowest loss path for given FLOP budgets.

## Formulation
$$C \approx 6ND$$
Determine parameters minimizing $L$ along constant $C$ contours.

## Diagram
```mermaid
flowchart LR
    A[Run Data Grid] --> B[Trace Lowest Loss Envelope]
    B --> C[Compute-Optimal Path]
```

[← Back to README](../README.md)
