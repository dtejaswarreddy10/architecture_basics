# Gaudi — AI Accelerator (Intel / Habana Labs)

> **Essence:** A deep-learning accelerator whose superpower is **networking**: it puts massive standard **Ethernet (RoCE)** right on the chip, so you can scale to thousands of accelerators using ordinary Ethernet — no proprietary fabric required.

---

## 1. Introduction

### What is Gaudi?
**Gaudi** is a family of **AI training and inference accelerators** from **Habana Labs**, a company **acquired by Intel in 2019**. Gaudi competes with GPUs for deep learning, but its standout feature is **huge amounts of integrated RoCE Ethernet** built directly into the processor for **scaling out**.

- A **GPU** typically scales using proprietary links (e.g. NVLink) + switches.
- **Gaudi** scales using **standard Ethernet (RoCE v2)** integrated on-chip.

### Where did Gaudi come from?
**Habana Labs** (Israel, 2016) set out to build purpose-built deep-learning silicon that is **cost-effective** and **easy to scale**. **Intel acquired Habana in 2019** and made Gaudi its flagship data-center training accelerator, emphasizing **price/performance** versus NVIDIA.

### The main idea behind Gaudi
> **Make scaling cheap and open by putting networking on the chip.**

Gaudi combines specialized matrix and vector engines with a large amount of **on-die Ethernet**, so clusters can be built with **standard switches** instead of expensive proprietary fabrics.

---

## 2. Basic Functionality & Architecture

### Simple analogy: workers with phones built in
Imagine a factory where every worker has a **phone built into their hands**. They don't need to walk to a central switchboard to coordinate — they just talk directly over a standard line. Gaudi bakes the **network into the chip**, so accelerators talk to each other directly using ordinary Ethernet.

### The building blocks
| Block | Role |
|-------|------|
| **MME — Matrix Math Engine** | Big matrix multiplies (the core of deep learning) |
| **TPC — Tensor Processor Cores** | Programmable **VLIW SIMD** cores for everything else |
| **HBM** | High-bandwidth memory on package |
| **Integrated RoCE Ethernet** | **Many on-chip 100GbE ports** for scale-out |

### The key differentiator: on-chip Ethernet
- **Gaudi2** integrates **24× 100 GbE RoCE v2** ports **on the chip itself**.
- This lets you connect accelerators **directly** and build large clusters with **standard Ethernet** switching.
- Result: **scale-out** without a proprietary interconnect — a cost and openness advantage.

### How a workload runs
1. **MME** handles the heavy matrix multiplications.
2. **TPCs** handle activations, normalization, custom ops.
3. **HBM** feeds data at high bandwidth.
4. **Integrated Ethernet** moves data between many Gaudis during distributed training.

### Gaudi vs GPU

| Feature | GPU | Gaudi |
|---------|-----|-------|
| Scale-out network | Proprietary links + switches | **Standard Ethernet (RoCE) on-chip** |
| Compute | CUDA cores + Tensor Cores | **MME + TPCs** |
| Memory | HBM | HBM |
| Selling point | Ecosystem &amp; performance | **Price/performance + open scaling** |
| Software | CUDA | **SynapseAI** |

---

## 3. Applications

### Where Gaudi fits
- 🧠 **Deep-learning training** at scale
- ⚡ **Inference** for large models
- ☁️ **Cloud** AI (e.g. offered on AWS &amp; Intel Developer Cloud)
- 🏢 **Cost-conscious** large clusters
- 🌐 **Ethernet-based** AI data centers

### Why pick Gaudi?
- **Cheaper scaling** with standard Ethernet
- Strong **price/performance** vs GPUs
- **No proprietary fabric** lock-in
- Purpose-built matrix + vector engines

### What Gaudi is NOT for
- General-purpose computing → **CPU**
- Graphics / rendering → **GPU**
- The largest software ecosystem (CUDA still dominates)
- Tiny edge / ultra-low-power devices → **NPU**

---

## 4. Market Examples & Future

### Products & ecosystem
| Item | Note |
|------|------|
| **Gaudi (Gaudi1)** | First generation training accelerator |
| **Gaudi2** | 24× 100GbE on-chip, HBM2e — strong MLPerf showing |
| **Gaudi3** | Newer generation, more compute &amp; memory bandwidth |
| **SynapseAI** | Software stack (PyTorch integration) |

### Business context
Intel positions Gaudi as a **price/performance** alternative to NVIDIA for AI, with **integrated Ethernet** as the architectural hook for **open, standards-based scaling**. Gaudi has been offered in the **cloud** and to enterprises building large clusters. *(Intel has also signaled a longer-term roadmap converging its GPU and Gaudi AI efforts.)*

### Trends
- **Ethernet-based** AI fabrics (open vs proprietary)
- Price/performance competition in AI silicon
- Larger HBM &amp; compute each generation
- Tighter PyTorch/framework integration

---

## 5. Summary

### Gaudi in one paragraph
Gaudi is **Intel/Habana's** deep-learning accelerator that pairs a **Matrix Math Engine** and programmable **Tensor Processor Cores** with HBM — and crucially, **integrates large amounts of standard RoCE Ethernet directly on-chip** (Gaudi2: 24× 100GbE). That on-die networking lets data centers **scale to many accelerators using ordinary Ethernet switches**, giving Gaudi a **price/performance and openness** edge versus GPUs that rely on proprietary interconnects.

### When should you choose Gaudi?
**Gaudi makes sense when:**
- You scale training/inference across **many accelerators**
- You want **standard Ethernet** scaling, not proprietary fabric
- **Price/performance** matters
- You're building **open** AI infrastructure

**Use a GPU** when you need the broadest CUDA ecosystem.

### Future trends
- Open, Ethernet-based AI networking
- Continued price/performance competition
- Bigger memory &amp; compute per generation
- Converging AI accelerator roadmaps

> Gaudi's bet: the bottleneck at scale isn't just compute — it's the **network**, so build it **into the chip** with standard Ethernet.
