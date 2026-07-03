# The Parameter-Dominant Era (Kaplan / OpenAI Scaling Laws, 2020)

## Overview
In early 2020, Kaplan et al. published the foundational paper "Scaling Laws for Neural Language Models," suggesting that model parameter size ($N$) should be scaled much faster than the volume of training tokens ($D$). This led to a trend of training extremely large but undertrained models.

## Mathematical Formulation
The cross-entropy loss $L$ is modeled as:
$$L(N) \approx \left(\frac{N_c}{N}\right)^{\alpha_N}$$
where model size $N$ dominates performance improvements under compute limits.

## Diagram
```mermaid
flowchart TD
    A[Compute Budget C] --> B[Prioritize Model Parameters N]
    A --> C[Slow Scaling of Data Tokens D]
    B --> D[GPT-3 175B]
    C --> D
    D --> E[Undertrained Architecture: 300B Tokens]
```

[← Back to README](../README.md)
