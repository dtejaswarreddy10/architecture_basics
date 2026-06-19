# IPU — Intelligence Processing Unit (Graphcore)

> **Essence:** A massively parallel AI chip built around *thousands of independent cores* and *huge on-chip memory* — designed to run many fine-grained, irregular tasks at once instead of one big block of matrix math.

---

## 1. Introduction

### What is an IPU?
An **IPU (Intelligence Processing Unit)** is an AI accelerator from **Graphcore**, designed from scratch for machine intelligence. Unlike a GPU (which excels at big, regular blocks of math), the IPU is built for **fine-grained parallelism** — thousands of cores each doing their **own** work on data held in **on-chip memory**.

- A **GPU** = thousands of cores doing the *same* operation (SIMT).
- An **IPU** = thousands of cores doing *different* operations (**MIMD**).

### Where did IPUs come from?
**Graphcore** (founded 2016, Bristol UK) argued that AI models are really **computational graphs** full of irregular, sparse, fine-grained operations — a poor fit for the GPU's lock-step model. The IPU was built to map those **graphs** directly onto hardware, giving the chip its name.

### The main idea behind IPU design
> **Keep the whole model on-chip, and let every core run independently.**

By putting **massive SRAM right next to the cores** and allowing **MIMD** execution, the IPU avoids slow trips to external memory and handles irregular, sparse workloads that stall a GPU.

---

## 2. Basic Functionality & Architecture

### Simple analogy: a huge open-plan office
A GPU is an army marching in perfect step. An IPU is a **huge office of thousands of workers**, each with their **own desk and notebook (local SRAM)**, free to work on **different tasks** — then everyone pauses to swap notes, and continues.

### The core building blocks
| Element | Role |
|---------|------|
| **Tiles** | Each = one core + its own local SRAM (e.g. GC200 has **1,472 tiles**) |
| **In-Processor Memory** | ~**900 MB SRAM** on-chip — the whole model lives on the chip |
| **Hardware multithreading** | ~6 threads per tile → **~8,800 parallel program threads** |
| **IPU-Exchange** | Ultra-high-bandwidth on-chip interconnect between tiles |
| **IPU-Links** | Connect many IPUs together into larger systems |

### Execution model: BSP (Bulk Synchronous Parallel)
The IPU runs in repeating phases:

1. **Compute** — every tile works independently on its local data
2. **Sync** — all tiles reach a barrier together
3. **Exchange** — tiles swap data over the on-chip fabric

> This clean **compute → sync → exchange** cycle makes massive parallelism predictable and easy to reason about.

### Why on-chip memory matters
GPUs constantly stream weights from external **HBM**. The IPU keeps the **model and activations in on-chip SRAM**, giving enormous memory bandwidth and low latency — a big advantage for **sparse** and **fine-grained** models.

### IPU vs GPU

| Feature | GPU | IPU |
|---------|-----|-----|
| Parallelism | SIMT (same op) | **MIMD (independent ops)** |
| Memory | External HBM | **Massive on-chip SRAM** |
| Best at | Dense, regular matrix math | **Sparse, fine-grained, graph workloads** |
| Execution | Warps / lock-step | **Bulk Synchronous Parallel** |
| Software | CUDA | **Poplar** |

---

## 3. Applications

### Where IPUs fit
- 🧠 **Models with fine-grained / sparse compute** (some NLP, GNNs)
- 🕸️ **Graph neural networks** — irregular structure suits MIMD
- 🔬 **Scientific & research AI** — exploring novel model structures
- 💹 **Finance** — low-latency, sparse models
- 🧫 **Healthcare / molecular modeling**

### Why pick an IPU?
- **Huge on-chip memory bandwidth**
- **Independent cores** for irregular work
- Strong on models that **don't map neatly to dense matmul**
- A clean, graph-oriented programming model (**Poplar**)

### What IPUs are NOT ideal for
- Plain dense matrix math at max throughput → **GPU/TPU**
- The broadest software ecosystem (CUDA dominates)
- Workloads already perfectly tuned for GPUs

---

## 4. Market Examples & Future

### Products & ecosystem
| Item | Note |
|------|------|
| **Colossus MK2 (GC200)** | 1,472 tiles, ~900 MB SRAM |
| **Bow IPU** | First processor to use **wafer-on-wafer 3D** stacking |
| **IPU-POD systems** | Racks of IPUs for data-center scale |
| **Poplar SDK** | Graph compiler & libraries (the "CUDA of IPUs") |

### Reality check
Graphcore was a high-profile NVIDIA challenger but found the **CUDA ecosystem** hard to displace commercially. In **2024 it was acquired by SoftBank**, giving it deeper backing to keep developing the architecture.

### Trends
- Backed by SoftBank's AI ambitions
- Continued focus on **sparsity** and **on-chip memory**
- 3D-stacked silicon (Bow) for more performance
- A case study in how hard it is to beat the GPU ecosystem

---

## 5. Summary

### IPU in one paragraph
The IPU is Graphcore's AI processor built around **thousands of independent (MIMD) cores** and **huge on-chip SRAM**, executing in a clean **Bulk Synchronous Parallel** cycle. By keeping entire models on-chip and letting cores run their own programs, it targets **fine-grained and sparse** AI workloads that don't map neatly onto a GPU's lock-step matrix engines. Technically distinctive, it has struggled against CUDA's dominance and is now backed by SoftBank.

### When should you choose an IPU?
**An IPU is interesting when:**
- Your model is **sparse / fine-grained / graph-like**
- You benefit from **massive on-chip memory bandwidth**
- You want **independent per-core** execution

**Use a GPU/TPU** for dense matrix math and the widest software support.

### Future trends
- SoftBank-backed development
- Deeper bets on sparsity & on-chip memory
- 3D wafer-on-wafer stacking
- Lessons for the whole AI-silicon industry

> The IPU's big idea: treat AI as a **graph of independent tasks**, and keep the whole thing **on-chip**.
