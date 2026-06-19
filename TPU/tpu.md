# TPU — Tensor Processing Unit

> **Essence:** Google's custom AI chip built around a *systolic array* — a grid of multipliers that streams data through itself to do enormous matrix math with extreme efficiency.

---

## 1. Introduction

### What is a TPU?
A **TPU (Tensor Processing Unit)** is a **custom-built ASIC** designed by **Google** specifically to accelerate **machine-learning workloads** — especially the **tensor (matrix) operations** at the heart of neural networks.

- A **GPU** is a general parallel processor adapted for AI.
- A **TPU** is **built from scratch for AI** — nothing else.

### Where did TPUs come from?
Around 2013, Google realized that if every user used voice search for a few minutes a day, they'd need to **double their data-center compute**. CPUs and GPUs were too expensive and power-hungry at that scale, so Google **designed its own chip** — the first TPU went live in **2015**, and it has powered Search, Translate, Photos, and now Gemini ever since.

### The main idea behind TPU design
> **Specialize completely around the matrix multiply.**

A TPU strips away general-purpose features and pours its silicon into one thing: a giant **systolic array** that performs matrix multiplication with minimal data movement — the single most expensive part of running a neural network.

---

## 2. Basic Functionality & Architecture

### Simple analogy: a bucket brigade
A systolic array is like a **bucket brigade** passing water hand-to-hand. Data flows **step by step** through a grid of small multiply units — each cell does a little work and passes the result along, so the chip rarely needs to fetch from memory.

### The core building block: the systolic array
The heart of a TPU is the **Matrix Multiply Unit (MXU)** — a large 2-D grid (e.g. **128 × 128 = 16,384 multipliers**) where:

- **Weights** stay loaded in the cells.
- **Inputs** stream in from one side.
- **Partial sums** accumulate as data marches across the grid.

This **keeps data on-chip**, avoiding the memory bottleneck that limits CPUs and GPUs.

### Built for tensors, not flexibility
| Element | Role |
|---------|------|
| **MXU (systolic array)** | Bulk matrix multiplication |
| **Vector / scalar units** | Activations, normalization |
| **High-Bandwidth Memory (HBM)** | Feeds the array with weights & data |
| **Interconnect (ICI)** | Links thousands of TPUs into "pods" |

### Precision
TPUs favor **BF16** (brain-float 16) and **INT8** — low-precision formats that keep accuracy high for AI while massively boosting throughput and efficiency.

### TPU vs GPU

| Feature | GPU | TPU |
|---------|-----|-----|
| Origin | Graphics, adapted for AI | **Built only for AI** |
| Core design | Thousands of general cores | **Systolic matrix array** |
| Flexibility | High (graphics, HPC, AI) | **Low (AI/tensors only)** |
| Programming | CUDA / ROCm | **TensorFlow / JAX / XLA** |
| Availability | Buy from many vendors | **Google Cloud only** |
| Efficiency on matmul | High | **Extremely high** |

---

## 3. Applications

### What TPUs are built for
- 🧠 **Training** large neural networks (LLMs, vision, recommendation)
- ⚡ **Inference** at Google scale (Search, Translate, Photos, Gemini)
- 🔬 Research via **Google Cloud TPU** and **Colab**
- 🏢 Large batch AI workloads where efficiency at scale matters

### Why scale is the point
TPUs are designed to be **linked into "pods"** — thousands of chips connected by fast interconnect, acting as one giant AI supercomputer. This makes them ideal for **training frontier models** quickly and cost-effectively.

### What TPUs are NOT good at
- General-purpose computing → **CPU**
- Graphics / rendering → **GPU**
- Branch-heavy or irregular code
- Workloads outside the ML/tensor world
- Running outside Google's ecosystem (Cloud-only)

---

## 4. Market Examples & Future

### The TPU generations
| Generation | Focus |
|------------|-------|
| **TPU v1 (2015)** | Inference only (INT8) |
| **TPU v2 / v3** | Training + inference, liquid-cooled pods |
| **TPU v4 / v5e / v5p** | Massive pods, better perf/$ and efficiency |
| **Trillium (v6)** | Latest generation — big leap in performance-per-watt |

### How you use a TPU
Unlike GPUs, you **don't buy** TPUs — you **rent** them through **Google Cloud**, or use them free in limited form via **Google Colab**. Software stack: **TensorFlow, JAX, PyTorch/XLA**.

### Trends
- **Bigger pods** — tens of thousands of chips as one machine
- **Better perf-per-watt** each generation (Trillium and beyond)
- **Powering Gemini** and Google's frontier models
- A key example of the industry move toward **custom AI silicon**

---

## 5. Summary

### TPU in one paragraph
A TPU is Google's **custom AI accelerator (ASIC)** built around a **systolic array** that performs matrix multiplication with minimal data movement. By specializing entirely on tensor math and low-precision formats like BF16, it trains and serves neural networks with exceptional efficiency at data-center scale — at the cost of being inflexible and available only through Google Cloud.

### When should you choose a TPU?
**A TPU is the right tool when:**
- You train or serve **large neural networks**
- You work within **Google Cloud / JAX / TensorFlow**
- You want **efficiency at massive scale** (pods)

**Use a GPU instead** for flexible, multi-vendor AI or graphics, and a **CPU** for general logic.

### Future trends
- Ever-larger TPU pods as unified supercomputers
- Continued perf-per-watt leaps (Trillium → beyond)
- Tight integration with Google's AI models (Gemini)
- Part of the broader shift to purpose-built AI chips

> The TPU shows what happens when a chip is designed **around the math of AI itself** — not adapted to it.
