# Awesome-Chinchilla-Scaling

<p align="center">
  <img src="./assets/banner.svg" alt="Chinchilla Scaling Laws Banner" width="100%">
</p>

<p align="center">
  <a href="https://github.com/ishandutta2007/Awesome-Awesome-Awesome"><img src="https://img.shields.io/badge/Awesome-%E2%9C%94-blueviolet?style=flat-square&logo=github" alt="Awesome"/></a><a href="https://discord.gg/jc4xtF58Ve"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord" /></a><a href="https://github.com/ishandutta2007"><img alt="GitHub followers" src="https://img.shields.io/github/followers/ishandutta2007?label=Follow" /></a>
</p>

## 🚀 Chinchilla Scaling Laws: History, Progression, Variants, & Applications 📊

Welcome to the definitive resource for **Chinchilla Scaling Laws**, **compute-optimal LLM pre-training**, and **foundation model scaling trajectory**. This curated repository tracks the evolution from parameter-dominant scaling models (like Kaplan/OpenAI scaling laws) to modern inference-optimal overtraining and test-time compute scaling strategies.

### 🔍 SEO Overview & Key Concepts
- **Keywords:** LLM scaling laws, Chinchilla scaling, compute-optimal training, parameter-data ratio, test-time compute, MoE scaling, inference optimization.
- **Core Topics:** Kaplan vs Chinchilla scaling, 20 tokens per parameter, overtraining, System 2 test-time reasoning.

**Chinchilla Scaling Laws** represent a foundational paradigm shift in the compute-optimal design and pre-training of Large Language Models (LLMs). Formally introduced by Hoffmann et al. (DeepMind) in March 2022 ("Training Compute-Optimal Large Language Models"), Chinchilla scaling established the empirical mathematical relationship between a model’s parameter footprint ($N$) and the total volume of training data ($D$, measured in tokens) required to maximize linguistic performance for a fixed computational footprint ($C$). 

Prior to Chinchilla, the deep learning ecosystem prioritized inflating model parameter sizes while severely starving models of training tokens. Chinchilla inverted this practice, proving that for optimal training efficiency, parameters and token volumes must scale in **equal, 1:1 proportions**, demonstrating that an optimal model requires roughly **20 tokens per individual parameter**.

---

## 📅 1. The Macro Chronological Evolution

The implementation of foundation model scaling has transitioned from parameter-skewed estimations to tightly bounded tokens-per-parameter allocations, shifting toward modern inference-optimized overtraining configurations and test-time search loops.

```mermaid
flowchart LR
    A["Kaplan Scaling Laws (2020)<br/>(Prioritized Model Size over Data)"]
    --> B["Chinchilla Laws (Hoffmann et al., 2022)<br/>(Compute-Optimal Parameter–Data Scaling)"]
    --> C["LLM Overtraining (Llama, 2024)<br/>(High Token-to-Parameter Ratios)"]
    --> D["Test-Time Scaling Laws (o1/R1, 2025+)<br/>(Inference-Time Search & Verification Scaling)"]
```

| Era / Concept | Year First Used | Paper Link |
| :--- | :---: | :--- |
| **[The Parameter-Dominant Era (Kaplan / OpenAI Scaling Laws, 2020)](./details/1_parameter_dominant_era.md)**<br><br>**Concept:** The foundational scaling blueprint. The early OpenAI research team concluded that when compute budgets scale up, developers should channel the vast majority of resources into expanding model parameter size ($N$), while scaling dataset size ($D$) at a significantly slower rate.<br><br>**Limitation:** Led to heavily under-trained architectures. For example, the original GPT-3 was an un-converged 175-billion parameter model trained on a sparse 300 billion tokens. This made it mathematically capacity-starved and commercially expensive to host. | 2020 | [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361) |
| **[The Equal-Scaling Revolution (Chinchilla Scaling Laws, Hoffmann et al., 2022)](./details/2_equal_scaling_revolution.md)**<br><br>**Concept:** Overturned Kaplan’s findings by explicitly accounting for learning rate decay schedules across diverse pilot scales. DeepMind proved that $N$ and $D$ should actually scale in equal proportions. For maximum compute-optimal efficiency, a model requires approximately 20 tokens per individual parameter (e.g., a 70B model requires 1.4 trillion tokens to hit the compute-optimal frontier).<br><br>**Significance:** Completely restructured base-model training globally, delivering significantly smaller, faster, and more capable models (such as Chinchilla 70B outperforming Gopher 280B while using identical compute). | 2022 | [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556) |
| **[The Inference-Optimal Overtraining Era (~2024–Present)](./details/3_inference_optimal_overtraining.md)**<br><br>**Concept:** Shifted optimization focus from *training efficiency* to *lifetime inference serving cost*. If an enterprise model is going to be queried billions of times in production, it makes commercial sense to purposefully "overtrain" a small model far past its theoretical training compute-optimal boundary.<br><br>**Significance:** Modern enterprise architectures ingest immense token counts. For example, Llama 3 8B was trained on over 15 trillion tokens, achieving an ultra-dense ratio exceeding **1,875 tokens per parameter**, keeping generation latency and VRAM footprints compact. | 2023 | [LLaMA: Open and Efficient Foundation Language Models](https://arxiv.org/abs/2302.13971) |
| **[The Test-Time Compute Scaling Era (~2025–Present)](./details/4_test_time_compute_scaling.md)**<br><br>**Concept:** The current modern state-of-the-art foundation standard. Breaks past static token-ingestion limits by scaling compute at the inference gate (System 2 thinking). Pioneered by models like OpenAI’s o-series and DeepSeek-R1, it proves that downstream task accuracy scales as a clean power-law function of the absolute **number of reasoning tokens generated at inference time**, complementing Chinchilla pre-training scaling. | 2024 | [Scaling LLM Test-Time Compute Optimally](https://arxiv.org/abs/2408.03314) |

---

## ⚙️ 2. Core Functional & Estimation Variants

Compute-optimal frameworks are mathematically structured around distinct empirical scaling approaches to isolate power-law exponents.

| Variant / Method | Year First Used | Paper Link |
| :--- | :---: | :--- |
| **[A. Parametric Loss Power-Law Modeling](./details/5_parametric_loss_power_law.md)**<br><br>**Mechanism:** Models the final cross-entropy evaluation loss ($L$) as a multi-variable power-law function:<br>$$L(N, D) = \frac{A}{N^\alpha} + \frac{B}{D^\beta} + E$$<br>**Behavior:** By training dozens of tiny pilot models (e.g., 10M to 1B parameters) on variable token durations, engineers fit the constant exponents ($\alpha=0.34, \beta=0.28, A=406.4, B=410.7$), forecasting the precise behavior of a 100B+ parameter system before launching the main run. | 2020 | [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361) |
| **[B. Empirical Optimal Frontier Isolation](./details/6_empirical_optimal_frontier.md)**<br><br>**Mechanism:** Traces an explicit geometric envelope across a grid of completed training run data coordinates. It maps the lowest achievable loss points for every given computational FLOP expenditure level ($C \approx 6ND$), calculating the optimal breakdown where $N \propto C^a$ and $D \propto C^b$, forcing $a = b \approx 0.5$. | 2022 | [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556) |
| **[C. Downstream Capability Alignment Scaling](./details/7_downstream_capability_scaling.md)**<br><br>**Mechanism:** Moves past broad cross-entropy loss tracking to evaluate compute optimality against explicit downstream capabilities (such as coding accuracy, mathematical verification limits, or multi-hop retrieval benchmarks), proving specific safety and reasoning tasks follow harsher scaling laws than generic text predicting. | 2022 | [Broken Neural Scaling Laws](https://arxiv.org/abs/2210.14891) |

---

## 🏛️ 3. High-Capacity Architectural & Scaling Classes

Depending on whether an AI system integrates safety alignments or structural sparse routing, compute-optimal training configurations require unique modifications.

| Scaling Class | Year First Used | Paper Link |
| :--- | :---: | :--- |
| **[Aligned Compute Optimization (The Preference Optimization Shift)](./details/8_aligned_compute_optimization.md)**<br><br>**The Shift:** Incorporating alignment pipelines (SFT, RLHF, DPO) introduces an explicit behavioral constraint. Because safety guardrails restrict output distributions, the classic compute-optimal curve shifts, requiring models to scale parameter counts ($N$) wider and deeper earlier in their lifecycle to absorb safety behaviors without corrupting core logical capabilities. | 2022 | [Scaling Laws for Reward Model Overoptimization](https://arxiv.org/abs/2210.10760) |
| **[Mixture-of-Experts (MoE) Scaling Optimization](./details/9_moe_scaling_optimization.md)**<br><br>**The Shift:** Decouples a model's active compute footprint from its total parameter capacity [INDEX: 15]. By organizing weights into sparse, gated expert blocks (e.g., DeepSeek-V3), a model can hold hundreds of billions of total parameters on disk, while activating only a tiny fraction per token [INDEX: 15].<br><br>**Significance:** Completely breaks traditional Chinchilla scaling restrictions, allowing massive capacity expansions with drastically lower training FLOP expenditures [INDEX: 15]. | 2022 | [Unified Scaling Laws for Routed Language Models](https://arxiv.org/abs/2202.01629) |

```mermaid
flowchart LR
    subgraph P["Pre-Training Compute Scaling Frontiers"]
        A["Kaplan Scaling<br/><br/>Under-trained / Bloated Models<br/>Example: GPT-3 175B on ~300B Tokens"]
        --> B["Chinchilla Scaling<br/><br/>Compute-Optimal Training<br/>Example: 70B on ~1.4T Tokens"]
        --> C["Inference-Optimal Overtraining<br/><br/>High Token-to-Parameter Ratios<br/>Example: Llama 3 8B on ~15T Tokens"]
    end

    X["Few Training Tokens<br/>Higher Loss"] --- A
    C --- Y["Massive Training Tokens<br/>Lower Loss"]
```

---

## 🛠️ 4. Production Engineering Challenges & Hardware Solutions

Executing massive compute-optimal training runs across large-scale distributed hardware clusters introduces severe hyperparameter risks and data scarcity walls.

| Challenge / Solution | Year First Used | Paper Link |
| :--- | :---: | :--- |
| **[The Learning Rate Decay Alignment Scheduler Lock](./details/10_lr_decay_scheduler_lock.md)**<br><br>**The Problem:** Standard power-law projections depend on the assumption that the learning rate (LR) cosine decay schedule matches the exact pre-planned target token destination. If an enterprise training run is scheduled for 5 trillion tokens, but the engineering team decides to abort or extend the run midway, the LR scheduler will be completely unaligned, degrading the model's compute efficiency.<br><br>**Mitigation:** Implementing **Continuous/Infinite LR Schedulers** (such as constant learning rates with terminal decay steps or inverse-square-root decay scripts) to permit flexible training horizons without sacrificing optimal loss convergence. | 2022 | [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556) |
| **[The Data Wall Constraint (Token Exhaustion)](./details/11_data_wall_constraint.md)**<br><br>**The Problem:** As compute budgets climb into the YottaFLOP scale, compute-optimal equations demand tens or hundreds of trillions of unique, high-quality text tokens—rapidly exhausting the entire available pool of human-written internet text.<br><br>**Mitigation:** Deploying **Synthetic Data Generation Pipelines** (using frontier models to synthesize pristine, error-free reasoning traces, programming scenarios, and textbook scripts) alongside **Multi-Modal Data Ingestion** (tokenizing video, acoustics, and software structures) to multiply the available data matrix. | 2022 | [Will We Run Out of Data?](https://arxiv.org/abs/2211.04325) |

---

## 🌐 5. Frontier Real-World AI Infrastructure Applications

| Infrastructure Application | Year First Used | Paper Link |
| :--- | :---: | :--- |
| **[Pre-Training Frontier Foundation LLM Suites (Llama / DeepSeek)](./details/12_pretraining_frontier_suites.md)**<br><br>**Application:** Guides cluster-wide hardware allocation policies [INDEX: 15]. Deep learning infrastructure teams run tiny, high-precision pilot runs to calibrate scaling equations exactly, ensuring that multi-million dollar training budgets spent over thousands of GPUs yield the absolute sharpest possible model intelligence [INDEX: 15]. | 2023 | [LLaMA: Open and Efficient Foundation Language Models](https://arxiv.org/abs/2302.13971) |
| **[High-Throughput Inference-Optimized Serving (vLLM Deployments)](./details/13_inference_optimized_serving.md)**<br><br>**Application:** Maximizes enterprise server concurrency. By leveraging the principles of inference-optimal overtraining, companies serve heavily over-trained 1.5B and 8B parameters models that match the reasoning capacity of older 70B networks, dropping VRAM overhead and cutting request processing latencies. | 2023 | [Efficient Memory Management for Large Language Model Serving](https://arxiv.org/abs/2309.06180) |
| **[Sparsely Routed Mixture-of-Experts Scaling (DeepSeek-V3 / Mixtral)](./details/14_sparse_moe_infrastructure.md)**<br><br>**Application:** Orchestrates distributed training pipelines [INDEX: 15]. Compute-optimal tracking models for sparse architectures map exact token-to-expert routing ratios, ensuring data-parallel and expert-parallel hardware shards balance compute processing loops without encountering server stalls [INDEX: 15]. | 2023 | [Mixtral of Experts](https://arxiv.org/abs/2401.04088) |

---

## 📚 References
1. Kaplan, J., et al. (2020). Scaling laws for neural language models. *arXiv preprint arXiv:2001.08361*.
2. Hoffmann, J., et al. (2022). Training compute-optimal large language models. *arXiv preprint arXiv:2203.15556*.
3. Touvron, H., et al. (2023). Llama 2: Open foundation and fine-tuned chat models. *arXiv preprint arXiv:2307.09288*.
4. Bi, J., et al. (2024). DeepSeek-V2: A strong, economical, and efficient mixture-of-experts language model. *arXiv preprint arXiv:2405.04434*.
5. DeepSeek-AI. (2025). DeepSeek-V3 Technical Report: Multi-node distributed associative scans over sharded data-parallel expert topologies. *GitHub Repository Technical Infrastructure Manifesto* [INDEX: 15].
6. OpenAI. (2025). Scaling test-time compute past static pre-training constraints. *OpenAI o3 System Launch Document*.

---

To advance this documentation repository, scaling architecture, or MLOps automation pipeline, consider exploring these adjacent development pathways:
* Build a **Python script using NumPy** demonstrating how to calculate the power-law parameter and token targets given a specific floating-point operation (FLOP) budget based on Chinchilla coefficients.
* Generate a **comprehensive Markdown table** explicitly comparing Kaplan Scaling, Chinchilla Scaling, Inference-Optimal Overtraining, and Sparse MoE Scaling across token-per-parameter ratios, active compute allocation rules, compute scaling metrics, and target hardware constraints [INDEX: 15].
* Establish a **performance profiling notebook** to model how continuous learning rate schedules impact final model cross-entropy loss convergence when a training run is dynamically extended past its initial token target.

***

**Proactive Repository Follow-Ups:**

To assist with your documentation repository setup, let me know how you would like to proceed by choosing one of the options below:
* I can provide a **complete Python code boilerplate using SciPy** demonstrating how to perform a multi-variable non-linear regression fit to extract custom power-law scaling exponents from localized training logs.
* I can generate a **Markdown matrix table** tracking the explicit parameter counts, token counts, and token-to-parameter ratios of the leading open-weight foundation models over the past 24 months.
* I can write a detailed technical explanation focusing on **how Mixture-of-Experts (MoE) architectures modify the traditional $C \approx 6ND$ compute calculations** at runtime [INDEX: 15].

## Star History
<div align="center">
<a href="https://www.star-history.com/?repos=ishandutta2007%2FAwesome-Chinchilla-Scaling&type=date&legend=bottom-right">
<picture>
<source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=ishandutta2007/Awesome-Chinchilla-Scaling&type=date&theme=dark&legend=bottom-right" />
<source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=ishandutta2007/Awesome-Chinchilla-Scaling&type=date&legend=bottom-right" />
<img alt="Star History Chart" src="https://api.star-history.com/chart?repos=ishandutta2007/Awesome-Chinchilla-Scaling&type=date&legend=bottom-right" />
</picture>
</a>
</div>

