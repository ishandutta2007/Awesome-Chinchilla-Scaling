# The Equal-Scaling Revolution (Chinchilla Scaling Laws, 2022)

## Overview
Hoffmann et al. (2022) demonstrated that parameters ($N$) and data tokens ($D$) should be scaled in equal proportions (1:1). For optimal performance, a model requires roughly 20 tokens per parameter.

## Mathematical Formulation
$$N \propto C^{0.5}, \quad D \propto C^{0.5}$$
With optimal coefficients:
$$G \approx 20 \text{ tokens/parameter}$$

## Diagram
```mermaid
flowchart LR
    A[Compute Budget C] --> B[Parameters N ~ 50%]
    A --> C[Data Tokens D ~ 50%]
    B & C --> D[Compute-Optimal Frontier]
    D --> E[Chinchilla 70B on 1.4T Tokens]
```

[← Back to README](../README.md)
